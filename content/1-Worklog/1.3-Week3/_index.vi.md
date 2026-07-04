---
title: "Worklog Tuần 3"
date: 2026-05-03
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

**Thời gian:** 03/05/2026 - 09/05/2026

## Mục tiêu tuần 3

- Thiết kế kiến trúc tổng thể cho hệ thống phát hiện gian lận trên AWS.
- Tách rõ hai vùng xử lý: **Training Zone** và **Real-time Zone**.
- Xây dựng cách tổ chức dữ liệu ban đầu trên Amazon S3.

## Công việc đã thực hiện

- Thiết kế pipeline tổng thể gồm hai phần:
  - **Training Zone:** lưu dữ liệu, train model, evaluate model và deploy endpoint.
  - **Real-time Zone:** nhận giao dịch, xử lý realtime, gọi model, cảnh báo và lưu lịch sử.
- Xác định các dịch vụ AWS chính:
  - Amazon S3 làm Data Lake.
  - Amazon SageMaker để huấn luyện và triển khai mô hình.
  - Amazon API Gateway làm điểm vào của hệ thống.
  - AWS Lambda để xử lý request và feature engineering.
  - Amazon Kinesis để stream giao dịch realtime.
  - Amazon SNS để gửi cảnh báo.
  - Kinesis Firehose để ghi kết quả xuống S3.
  - Amazon CloudWatch để theo dõi log và metric.
- Thiết kế cấu trúc lưu trữ dữ liệu trên S3, ví dụ:
  - `raw/` lưu dataset gốc.
  - `data_train/` lưu dữ liệu train sau bước chuẩn bị dữ liệu.
  - `model/` lưu model artifact và các file liên quan.
  - `model.tar.gz` là file model đã đóng gói để tạo SageMaker Endpoint.
- Phác thảo sơ đồ kiến trúc để dùng trong phần Proposal và Workshop.

## Kết quả đạt được

- Có kiến trúc tổng thể cho project fraud detection trên AWS.
- Xác định được vai trò của từng dịch vụ trong pipeline.
- Thiết kế được luồng dữ liệu từ training đến realtime inference.
- Chuẩn bị được nền tảng để triển khai phần dữ liệu và mô hình.
