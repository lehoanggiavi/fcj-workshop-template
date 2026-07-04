---
title: "Worklog Tuần 10"
date: 2026-06-21
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Thời gian:** 21/06/2026 - 27/06/2026

## Mục tiêu tuần 10

- Xử lý kết quả dự đoán từ SageMaker Endpoint.
- Gửi cảnh báo khi phát hiện giao dịch gian lận.
- Lưu lịch sử prediction để phục vụ audit và phân tích sau này.

## Công việc đã thực hiện

- Chuẩn hóa response trả về từ SageMaker Endpoint, gồm:
  - `prediction`
  - `fraud_probability`
  - `timestamp`
  - thông tin transaction gốc.
- Xây dựng logic xử lý kết quả:
  - Nếu prediction là `Fraud`, gửi cảnh báo.
  - Nếu prediction là `Normal`, ghi nhận kết quả và không gửi cảnh báo.
- Tạo Amazon SNS Topic để gửi email cảnh báo cho Admin.
- Cấu hình email subscription và xác nhận subscription.
- Tích hợp Lambda realtime với SNS.
- Tạo Kinesis Firehose để ghi kết quả prediction xuống Amazon S3.
- Thiết kế dữ liệu lưu lịch sử gồm:
  - Transaction
  - Feature
  - Prediction
  - Probability
  - Timestamp

## Kết quả đạt được

- Hệ thống có thể gửi cảnh báo khi phát hiện giao dịch nghi ngờ gian lận.
- Toàn bộ kết quả prediction được lưu xuống Amazon S3 thông qua Kinesis Firehose, gồm Transaction, Feature, Prediction, Timestamp và Probability.
- Có dữ liệu lịch sử phục vụ audit, monitoring và retraining trong tương lai.
- Pipeline realtime trở nên hoàn chỉnh hơn từ input, prediction, alert đến lưu trữ.
