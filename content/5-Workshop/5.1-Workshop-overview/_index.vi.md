---
title : "Tổng quan về workshop"
date : 2026-04-19
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

## 1. Bối cảnh

Gian lận thẻ tín dụng là một bài toán quan trọng trong các hệ thống thanh toán điện tử. Một giao dịch gian lận nếu không được phát hiện kịp thời có thể gây thiệt hại tài chính, ảnh hưởng đến uy tín của tổ chức và làm giảm mức độ tin cậy của người dùng đối với hệ thống.

Trong thực tế, các hệ thống phát hiện gian lận thường cần xử lý giao dịch gần như theo thời gian thực. Khi một giao dịch mới xuất hiện, hệ thống cần nhanh chóng đánh giá mức độ rủi ro, xác định giao dịch là bình thường hay nghi ngờ gian lận, sau đó gửi cảnh báo cho người quản trị nếu cần.

Workshop này mô phỏng một hệ thống như vậy bằng cách sử dụng Machine Learning và các dịch vụ AWS.

## 2. Mục tiêu của workshop

Trong workshop này, chúng ta sẽ xây dựng một hệ thống **phát hiện gian lận thẻ tín dụng theo thời gian thực bằng Machine Learning trên AWS**.

Hệ thống cần đạt được các mục tiêu sau:

- Lưu trữ dữ liệu giao dịch lịch sử trên Amazon S3.
- Huấn luyện mô hình Machine Learning bằng Amazon SageMaker.
- Sử dụng mô hình Random Forest để phân loại giao dịch thành `Fraud` hoặc `Normal`.
- Đóng gói model và triển khai thành SageMaker Real-time Endpoint.
- Nhận giao dịch mới thông qua Amazon API Gateway.
- Xử lý giao dịch realtime bằng AWS Lambda và Amazon Kinesis.
- Gọi SageMaker Endpoint để dự đoán kết quả.
- Gửi cảnh báo qua Amazon SNS nếu phát hiện giao dịch gian lận.
- Lưu lịch sử prediction xuống Amazon S3 thông qua Kinesis Firehose.
- Theo dõi log và metric bằng Amazon CloudWatch.

## 3. Kết quả sau khi hoàn thành

Sau khi hoàn thành workshop, bạn sẽ có một pipeline gồm:

- Một S3 Data Lake để lưu dữ liệu huấn luyện, model artifact và lịch sử dự đoán.
- Một mô hình Machine Learning đã được huấn luyện bằng SageMaker.
- Một SageMaker Real-time Endpoint để phục vụ realtime inference.
- Một API endpoint để gửi giao dịch mẫu.
- Một Kinesis Data Stream để tiếp nhận transaction realtime.
- Một Lambda Read Features để xử lý feature và gọi model.
- Một SNS Topic để gửi email cảnh báo khi phát hiện Fraud.
- Một Firehose Delivery Stream để ghi prediction history xuống S3.
- CloudWatch Logs để kiểm tra quá trình xử lý và debug lỗi.

## 4. Kiến trúc workshop

Kiến trúc được chia thành hai vùng xử lý.

### 4.1. Training Zone

Training Zone chịu trách nhiệm chuẩn bị dữ liệu, huấn luyện mô hình và triển khai model endpoint.

```text
Amazon S3
  │
  ▼
Amazon SageMaker Training
  │
  ▼
model.tar.gz
  │
  ▼
SageMaker Real-time Endpoint
```

Trong vùng này:

1. Dữ liệu giao dịch lịch sử được lưu trên Amazon S3.
2. SageMaker đọc dữ liệu từ S3 để preprocessing, feature engineering, train và evaluate model.
3. Model Random Forest sau khi train được lưu thành `model.joblib`.
4. Nếu có bước chuẩn hóa dữ liệu, scaler được lưu thành `scaler.joblib`.
5. File `inference.py` định nghĩa cách model nhận input và trả prediction.
6. Các file được đóng gói thành `model.tar.gz`.
7. SageMaker deploy model thành Real-time Endpoint.

### 4.2. Real-time Zone

Real-time Zone chịu trách nhiệm nhận giao dịch mới, gọi model để dự đoán, gửi cảnh báo và lưu lịch sử.

```text
User / Banking System
  │
  ▼
Amazon API Gateway
  │
  ▼
AWS Lambda
  │
  ▼
Amazon Kinesis
  │
  ▼
Lambda Read Features
  │
  ▼
SageMaker Endpoint
  ├── Fraud  ─► Amazon SNS ─► Email Admin
  └── Prediction Result
          │
          ▼
Kinesis Firehose
          │
          ▼
Amazon S3
```

Trong vùng này:

1. User hoặc Banking System gửi transaction request qua API Gateway.
2. Lambda đầu vào parse JSON, validate dữ liệu và chuẩn hóa request.
3. Transaction hợp lệ được đưa vào Amazon Kinesis.
4. Lambda Read Features đọc record từ Kinesis, thực hiện feature engineering và mapping feature.
5. Lambda gọi SageMaker Endpoint để dự đoán `Fraud` hoặc `Normal`.
6. Nếu kết quả là `Fraud`, hệ thống gửi cảnh báo qua SNS đến Email Admin.
7. Toàn bộ prediction result được ghi xuống S3 thông qua Kinesis Firehose.

![Sơ đồ pipeline Fraud Detection](/images/2-Proposal/fraud_detection_pipeline.jpg)

{{% notice note %}}
**Hình cần chụp/chèn sau:** Ảnh sơ đồ kiến trúc hệ thống Fraud Detection. Nếu bạn vẽ lại sơ đồ, nên thể hiện rõ hai vùng Training Zone và Real-time Zone, kèm các dịch vụ: S3, SageMaker, API Gateway, Lambda, Kinesis, SNS, Firehose và CloudWatch.
{{% /notice %}}

## 5. Dữ liệu đầu vào và đầu ra mong đợi

Một giao dịch đầu vào có thể có dạng:

```json
{
  "transaction_id": "txn-001",
  "user_id": "user-001",
  "transaction_amount": 2500000,
  "transaction_type": "online_payment",
  "merchant_category": "electronics",
  "location": "Ho Chi Minh City",
  "device_type": "mobile",
  "transaction_hour": 23
}
```

Kết quả trả về từ model có thể là:

```json
{
  "prediction": "Fraud",
  "fraud_probability": 0.91
}
```

Hoặc:

```json
{
  "prediction": "Normal",
  "fraud_probability": 0.08
}
```

## 6. Lưu ý quan trọng

- Không sử dụng dữ liệu thẻ tín dụng thật trong workshop.
- Chỉ sử dụng dữ liệu mẫu hoặc dữ liệu đã được ẩn danh phục vụ mục đích học tập.
- Không hard-code AWS Access Key hoặc Secret Key trong source code.
- Nên dùng IAM Role theo nguyên tắc least privilege.
- SageMaker Endpoint có thể phát sinh chi phí khi đang chạy, vì vậy cần clean-up sau khi demo.
- Mỗi bước triển khai nên được kiểm thử riêng trước khi chạy end-to-end.
