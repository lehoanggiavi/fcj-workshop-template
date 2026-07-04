---
title: "Workshop"
date: 2026-04-19
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

## Tổng quan

Trong workshop này, chúng ta sẽ xây dựng một hệ thống **phát hiện gian lận thẻ tín dụng theo thời gian thực** bằng cách kết hợp Machine Learning và các dịch vụ AWS.

Hệ thống được thiết kế theo hai phần chính:

- **Training Zone:** chuẩn bị dữ liệu, huấn luyện mô hình Machine Learning, đóng gói model và triển khai SageMaker Real-time Endpoint.
- **Real-time Zone:** nhận giao dịch từ User hoặc Banking System, xử lý dữ liệu theo luồng realtime, gọi model để dự đoán Fraud/Normal, gửi cảnh báo nếu phát hiện giao dịch nghi ngờ và lưu lịch sử prediction.

Sau khi hoàn thành workshop, người thực hiện sẽ hiểu cách xây dựng một pipeline ML end-to-end trên AWS, từ dữ liệu huấn luyện đến realtime inference.

## Mục tiêu workshop

Sau khi hoàn thành workshop, bạn có thể:

- Tạo Amazon S3 Data Lake để lưu dữ liệu giao dịch, feature, dataset train/test, model artifact và prediction history.
- Huấn luyện mô hình **Random Forest** bằng Amazon SageMaker.
- Đóng gói các file `model.joblib`, `scaler.joblib`, `inference.py` thành `model.tar.gz`.
- Triển khai model thành **SageMaker Real-time Endpoint**.
- Xây dựng API nhận giao dịch bằng Amazon API Gateway.
- Sử dụng AWS Lambda để parse JSON, validate dữ liệu, chuẩn hóa dữ liệu và đưa transaction vào Kinesis.
- Sử dụng Amazon Kinesis để tiếp nhận stream giao dịch realtime.
- Sử dụng Lambda Read Features để feature engineering, mapping feature và gọi SageMaker Endpoint.
- Gửi cảnh báo qua Amazon SNS đến Email Admin khi phát hiện Fraud.
- Lưu prediction result xuống Amazon S3 thông qua Kinesis Firehose.
- Theo dõi log/metric bằng Amazon CloudWatch.
- Clean-up tài nguyên để tránh phát sinh chi phí.

## Kiến trúc tổng thể

```text
Training Zone

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

```text
Real-time Zone

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

![Sơ đồ pipeline Fraud Detection](/images/2-Proposal/fraud_detection_pipeline.jpg)

{{% notice note %}}
**Hình cần chuẩn bị sau:** Ảnh sơ đồ kiến trúc cuối cùng của hệ thống Fraud Detection trên AWS. Có thể dùng sơ đồ hiện tại hoặc vẽ lại bằng draw.io/Excalidraw để rõ hơn các thành phần Training Zone và Real-time Zone.
{{% /notice %}}

## Dịch vụ AWS sử dụng

| Dịch vụ | Vai trò |
| --- | --- |
| Amazon S3 | Data Lake, lưu dataset, model artifact và prediction history |
| Amazon SageMaker | Train, evaluate, deploy và inference model |
| SageMaker Real-time Endpoint | Dự đoán giao dịch Fraud/Normal theo thời gian thực |
| Amazon API Gateway | API nhận giao dịch từ User hoặc Banking System |
| AWS Lambda | Validate dữ liệu, chuẩn hóa dữ liệu, feature engineering và gọi endpoint |
| Amazon Kinesis Data Streams | Tiếp nhận và buffer stream giao dịch realtime |
| Kinesis Firehose | Ghi prediction result xuống Amazon S3 |
| Amazon SNS | Gửi email cảnh báo cho Admin khi phát hiện Fraud |
| Amazon CloudWatch | Theo dõi log, metric và hỗ trợ debug |
| IAM Role | Phân quyền giữa các dịch vụ theo nguyên tắc least privilege |

## Nội dung workshop

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Chuẩn bị dữ liệu và S3 Data Lake](5.3-S3-vpc/)
4. [Huấn luyện mô hình và triển khai SageMaker Endpoint](5.4-S3-onprem/)
5. [Xây dựng realtime pipeline, alert và lưu lịch sử](5.5-Policy/)
6. [Dọn dẹp tài nguyên](5.6-Cleanup/)

{{% notice warning %}}
SageMaker Real-time Endpoint, Kinesis Data Streams và một số dịch vụ AWS khác có thể phát sinh chi phí nếu để chạy lâu. Luôn thực hiện phần clean-up sau khi hoàn thành workshop.
{{% /notice %}}
