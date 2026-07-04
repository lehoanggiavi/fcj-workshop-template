---
title: "Bản đề xuất"
date: 2026-04-19
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## 1. Tổng quan dự án

Dự án đề xuất xây dựng một hệ thống phát hiện gian lận giao dịch theo thời gian thực bằng cách kết hợp **Machine Learning** và các dịch vụ **AWS**. Hệ thống nhận dữ liệu giao dịch từ **User hoặc Banking System**, xử lý dữ liệu theo luồng realtime, gọi mô hình Machine Learning đã triển khai trên Amazon SageMaker để dự đoán giao dịch là **Fraud** hoặc **Normal**, sau đó gửi cảnh báo nếu phát hiện giao dịch nghi ngờ gian lận.

Project được triển khai như một workshop cá nhân, tập trung vào việc mô phỏng quy trình phát hiện gian lận trong các hệ thống tài chính/ngân hàng. Bên cạnh chức năng dự đoán, hệ thống còn lưu lại lịch sử prediction để phục vụ kiểm tra, audit và cải thiện mô hình trong tương lai.

## 2. Bối cảnh và vấn đề cần giải quyết

Trong các hệ thống giao dịch điện tử, gian lận có thể xảy ra dưới nhiều hình thức như giao dịch bất thường, giao dịch có giá trị lớn không phù hợp với hành vi người dùng, giao dịch từ thiết bị hoặc vị trí lạ, hoặc giao dịch diễn ra vào thời điểm bất thường. Nếu quy trình kiểm tra chỉ dựa vào rule cố định hoặc xử lý thủ công, hệ thống sẽ khó phản ứng nhanh khi số lượng giao dịch tăng lên.

Một hệ thống phát hiện gian lận cần giải quyết các vấn đề sau:

- Tiếp nhận giao dịch liên tục theo thời gian thực.
- Xử lý dữ liệu giao dịch với độ trễ thấp.
- Dự đoán khả năng gian lận dựa trên dữ liệu lịch sử và mô hình Machine Learning.
- Gửi cảnh báo kịp thời khi phát hiện giao dịch nghi ngờ.
- Lưu lại kết quả để phục vụ phân tích, kiểm toán và tái huấn luyện mô hình.

Dự án này không nhằm xây dựng một hệ thống ngân hàng thật, mà tập trung vào việc mô phỏng một use-case thực tế trên AWS để thể hiện quy trình thiết kế, triển khai và vận hành một pipeline ML realtime.

## 3. Mục tiêu dự án

### 3.1. Mục tiêu tổng quát

Xây dựng một pipeline end-to-end trên AWS cho bài toán phát hiện gian lận giao dịch, bao gồm quá trình huấn luyện mô hình, triển khai model endpoint, nhận giao dịch realtime, dự đoán kết quả, gửi cảnh báo và lưu lịch sử.

### 3.2. Mục tiêu cụ thể

- Lưu trữ dữ liệu giao dịch và dữ liệu huấn luyện trên Amazon S3.
- Huấn luyện mô hình Machine Learning bằng Amazon SageMaker.
- Sử dụng mô hình **Random Forest** cho bài toán phân loại Fraud/Normal.
- Đóng gói mô hình thành `model.tar.gz` và triển khai thành SageMaker Real-time Endpoint.
- Xây dựng API nhận giao dịch từ User hoặc Banking System bằng Amazon API Gateway.
- Sử dụng AWS Lambda đầu vào để parse JSON, validate dữ liệu, chuẩn hóa dữ liệu và đưa transaction vào Kinesis.
- Sử dụng Amazon Kinesis để tiếp nhận, buffer và mở rộng luồng giao dịch realtime.
- Sử dụng Lambda Read Features để đọc dữ liệu từ Kinesis, thực hiện feature engineering, chuẩn hóa dữ liệu và mapping feature.
- Gọi SageMaker Endpoint để nhận kết quả prediction gồm `Fraud` hoặc `Normal`, có thể kèm `fraud_probability`.
- Gửi cảnh báo qua Amazon SNS đến Email Admin nếu giao dịch được dự đoán là gian lận.
- Ghi lịch sử prediction xuống Amazon S3 thông qua Kinesis Firehose.
- Bổ sung logging/monitoring bằng Amazon CloudWatch.
- Có hướng dẫn clean-up để tránh phát sinh chi phí sau khi thực hành.

## 4. Phạm vi dự án

### 4.1. Trong phạm vi

- Thiết kế kiến trúc AWS cho hệ thống fraud detection.
- Chuẩn bị dữ liệu giao dịch mẫu phục vụ huấn luyện và kiểm thử.
- Train mô hình Machine Learning đơn giản, dễ giải thích.
- Deploy model lên SageMaker Real-time Endpoint.
- Xây dựng realtime pipeline bằng API Gateway, Lambda, Kinesis và Lambda Read Features.
- Gửi cảnh báo email cho Admin thông qua Amazon SNS khi phát hiện fraud.
- Lưu lịch sử dự đoán thông qua Kinesis Firehose xuống Amazon S3 để phục vụ audit/retraining.
- Viết tài liệu workshop để người khác có thể làm theo.

### 4.2. Ngoài phạm vi

- Không xử lý dữ liệu ngân hàng thật hoặc thông tin nhạy cảm thật.
- Không xây dựng đầy đủ hệ thống core banking.
- Không tối ưu mô hình ở mức production-grade.
- Không triển khai giao diện dashboard phức tạp trong phạm vi ban đầu.
- Không thay thế các hệ thống fraud detection chuyên dụng trong môi trường doanh nghiệp thật.

## 5. Kiến trúc giải pháp

Kiến trúc được chia thành hai phần chính:

- **Training Zone:** lưu trữ dữ liệu, xử lý dữ liệu, huấn luyện mô hình và triển khai model endpoint.
- **Real-time Zone:** nhận giao dịch, xử lý stream, gọi model để dự đoán, gửi cảnh báo và lưu lịch sử.

![Sơ đồ pipeline Fraud Detection](/images/2-Proposal/fraud_detection_pipeline.jpg)

### 5.1. Training Zone

Luồng Training Zone:

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

Các bước chính:

1. Dữ liệu giao dịch lịch sử được lưu trong Amazon S3.
2. SageMaker đọc dữ liệu từ S3 để thực hiện preprocessing, feature engineering, training và evaluation.
3. Mô hình Random Forest sau khi train được lưu cùng các file cần thiết như `model.joblib`, `scaler.joblib` và `inference.py`.
4. Các file được đóng gói thành `model.tar.gz`.
5. SageMaker deploy model thành Real-time Endpoint để phục vụ inference.

### 5.2. Real-time Zone

Luồng Real-time Zone:

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

Các bước chính:

1. User hoặc hệ thống giả lập gửi giao dịch thông qua API Gateway.
2. Lambda đầu vào validate dữ liệu, parse JSON và chuẩn hóa request.
3. Transaction hợp lệ được đưa vào Amazon Kinesis Data Stream.
4. Lambda xử lý realtime đọc dữ liệu từ Kinesis, thực hiện feature engineering và mapping feature.
5. Lambda gọi SageMaker Endpoint để nhận kết quả prediction.
6. Nếu kết quả là Fraud, hệ thống gửi cảnh báo qua Amazon SNS đến email Admin.
7. Toàn bộ prediction result được ghi xuống Amazon S3 thông qua Kinesis Firehose, gồm Transaction, Feature, Prediction, Timestamp và Probability.

## 6. Dịch vụ AWS sử dụng và lý do lựa chọn

| Dịch vụ | Vai trò trong hệ thống | Lý do lựa chọn |
| --- | --- | --- |
| Amazon S3 | Data Lake, lưu dữ liệu lịch sử, feature engineering, dataset train/test, model artifact và prediction history | Chi phí thấp, dễ tích hợp, phù hợp làm Data Lake |
| Amazon SageMaker | Data preprocessing, feature engineering, train, evaluate, deploy và inference | Managed service cho Machine Learning, giảm công sức cấu hình hạ tầng |
| SageMaker Real-time Endpoint | Nhận request prediction từ hệ thống realtime và trả về Fraud/Normal | Phù hợp cho use-case cần dự đoán ngay khi có giao dịch |
| Amazon API Gateway | Điểm vào nhận transaction request từ User hoặc Banking System | Dễ tạo REST API, tích hợp tốt với Lambda |
| AWS Lambda | Parse JSON, validate dữ liệu, chuẩn hóa dữ liệu, đưa dữ liệu vào Kinesis, đọc feature và gọi endpoint | Serverless, chỉ chạy khi có request/event |
| Amazon Kinesis Data Streams | Tiếp nhận stream giao dịch, hỗ trợ streaming, scale lớn và buffer dữ liệu | Phù hợp xử lý dữ liệu streaming và có khả năng mở rộng |
| Kinesis Firehose | Ghi prediction result xuống S3 | Đơn giản hóa việc đưa dữ liệu stream vào storage |
| Amazon SNS | Gửi email cảnh báo fraud cho Admin | Dễ cấu hình notification, phù hợp demo alert |
| Amazon CloudWatch | Giám sát Lambda, Kinesis và SageMaker Endpoint | Bổ sung theo đề xuất cải tiến để theo dõi vận hành và debug pipeline |
| IAM Role | Phân quyền giữa các dịch vụ | Giúp áp dụng least privilege và tránh hard-code credential |

## 7. Dữ liệu và mô hình Machine Learning

### 7.1. Dữ liệu đầu vào

Dữ liệu giao dịch mẫu có thể bao gồm các trường:

```json
{
  "transaction_id": "txn-001",
  "user_id": "user-001",
  "transaction_amount": 2500000,
  "transaction_type": "transfer",
  "merchant_category": "online",
  "location": "Ho Chi Minh City",
  "device_type": "mobile",
  "transaction_hour": 23
}
```

### 7.2. Feature engineering

Một số feature có thể sử dụng:

- Giá trị giao dịch.
- Loại giao dịch.
- Nhóm merchant.
- Thời điểm giao dịch.
- Thiết bị sử dụng.
- Vị trí giao dịch.
- Số lượng giao dịch trước đó của người dùng nếu có dữ liệu lịch sử.

Các feature này cần được mapping nhất quán giữa giai đoạn training và Lambda Read Features trong realtime pipeline để tránh sai lệch input khi gọi SageMaker Endpoint.

### 7.3. Mô hình sử dụng

Mô hình chính được đề xuất là **Random Forest**.

Lý do lựa chọn:

- Phù hợp với dữ liệu dạng bảng.
- Dễ triển khai trong project demo.
- Có khả năng xử lý quan hệ phi tuyến giữa các feature.
- Dễ so sánh kết quả bằng các chỉ số như Precision, Recall và F1-score.
- Phù hợp để giải thích trong báo cáo thực tập hơn so với các mô hình quá phức tạp.

## 8. Lộ trình triển khai

| Giai đoạn | Thời gian dự kiến | Nội dung chính |
| --- | --- | --- |
| Giai đoạn 1 | Tuần 1 - Tuần 2 | Tìm hiểu AWS, phân tích bài toán fraud detection, xác định yêu cầu hệ thống |
| Giai đoạn 2 | Tuần 3 - Tuần 4 | Thiết kế kiến trúc, chuẩn bị dữ liệu, tiền xử lý và feature engineering |
| Giai đoạn 3 | Tuần 5 - Tuần 6 | Train Random Forest, đánh giá mô hình, đóng gói model và inference script |
| Giai đoạn 4 | Tuần 7 - Tuần 9 | Deploy SageMaker Endpoint, xây API Gateway, Lambda, Kinesis và realtime inference |
| Giai đoạn 5 | Tuần 10 - Tuần 11 | Tích hợp SNS, Firehose, S3, CloudWatch, rà soát IAM và tối ưu chi phí |
| Giai đoạn 6 | Tuần 12 | Test end-to-end, hoàn thiện tài liệu workshop và clean-up |

## 9. Ước tính ngân sách

Chi phí phụ thuộc vào thời gian bật dịch vụ, lượng dữ liệu và số request. Trong phạm vi workshop cá nhân, hệ thống được thiết kế để chạy với dữ liệu demo và thời gian sử dụng ngắn nhằm hạn chế chi phí.

Các nguồn chi phí chính:

- **Amazon S3:** chi phí lưu dataset, model artifact và prediction history.
- **Amazon SageMaker:** chi phí training job và Real-time Endpoint. Đây là phần cần chú ý nhất vì endpoint có thể phát sinh chi phí khi đang chạy.
- **API Gateway:** chi phí theo số lượng request.
- **AWS Lambda:** chi phí theo số lần gọi và thời gian chạy.
- **Kinesis Data Streams:** chi phí theo shard/hour và lượng dữ liệu stream.
- **Kinesis Firehose:** chi phí theo lượng dữ liệu ingest.
- **SNS:** chi phí notification, thường thấp với quy mô demo.
- **CloudWatch:** chi phí log lưu trữ và metric nếu dùng nhiều.

Định hướng tối ưu chi phí:

- Chỉ bật SageMaker Endpoint khi cần demo hoặc kiểm thử.
- Xóa endpoint, stream và log không cần thiết sau workshop.
- Dùng dữ liệu mẫu nhỏ.
- Cấu hình CloudWatch log retention phù hợp.
- Kiểm tra AWS Billing Dashboard sau khi thực hành.

## 10. Rủi ro và phương án giảm thiểu

| Rủi ro | Ảnh hưởng | Phương án giảm thiểu |
| --- | --- | --- |
| SageMaker Endpoint phát sinh chi phí nếu quên xóa | Cao | Thêm bước clean-up rõ ràng, kiểm tra endpoint sau demo |
| Format input giữa training và inference không khớp | Cao | Chuẩn hóa feature list, kiểm thử request mẫu trước khi tích hợp realtime |
| Lambda thiếu quyền gọi SageMaker/SNS/Firehose | Trung bình | Tạo IAM Role theo từng chức năng và kiểm tra CloudWatch Logs |
| Dữ liệu mất cân bằng làm mô hình dự đoán kém | Trung bình | Theo dõi Precision, Recall, F1-score; cân nhắc xử lý imbalance nếu cần |
| Kinesis hoặc Firehose cấu hình sai destination | Trung bình | Test từng bước trước khi chạy end-to-end |
| Request API thiếu field hoặc sai kiểu dữ liệu | Thấp | Validate dữ liệu tại Lambda đầu vào và trả lỗi rõ ràng |

## 11. Kết quả kỳ vọng

Sau khi hoàn thành, project kỳ vọng đạt được các kết quả sau:

- Có một kiến trúc AWS hoàn chỉnh cho use-case fraud detection realtime.
- Có mô hình Random Forest được train và deploy trên SageMaker Endpoint.
- Có API nhận giao dịch và xử lý realtime bằng Lambda + Kinesis.
- Có cơ chế cảnh báo email khi phát hiện giao dịch nghi ngờ gian lận.
- Có lịch sử prediction được lưu trên Amazon S3 phục vụ audit và retraining.
- Có CloudWatch Logs hỗ trợ quan sát và debug hệ thống.
- Có tài liệu workshop từng bước để người khác có thể triển khai lại.

## 12. Hướng phát triển trong tương lai

- Thêm dashboard hiển thị số lượng giao dịch Fraud/Normal theo thời gian.
- Sử dụng Amazon SageMaker Feature Store để đảm bảo feature nhất quán giữa training và inference.
- Tự động hóa pipeline retraining bằng SageMaker Pipelines hoặc AWS Step Functions.
- Thêm EventBridge để kích hoạt retraining theo lịch.
- Cải thiện mô hình bằng các thuật toán khác như XGBoost hoặc LightGBM.
- Thêm cơ chế review thủ công cho các giao dịch có xác suất gian lận cao nhưng chưa đủ ngưỡng chặn tự động.
- Mở rộng hệ thống để xử lý batch prediction song song với realtime prediction.
