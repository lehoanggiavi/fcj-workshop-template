---
title: "Worklog Tuần 12"
date: 2026-04-19
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

**Thời gian:** 05/07/2026 - 19/07/2026

## Mục tiêu tuần 12

- Hoàn thiện kịch bản kiểm thử end-to-end cho hệ thống fraud detection.
- Hoàn thiện nội dung báo cáo workshop bằng tiếng Việt.
- Chuẩn bị phần clean-up để tránh phát sinh chi phí sau khi demo.

## Công việc đã thực hiện

- Xây dựng kịch bản kiểm thử luồng end-to-end:
  - Gửi transaction mẫu vào API Gateway.
  - Lambda nhận và validate request.
  - Transaction được đưa vào Kinesis.
  - Lambda realtime đọc record và tạo feature.
  - Lambda gọi SageMaker Endpoint để dự đoán.
  - Nếu kết quả là Fraud, SNS gửi email cảnh báo.
  - Kết quả prediction được ghi xuống S3 thông qua Kinesis Firehose.
- Chuẩn bị các test case cần chạy khi triển khai thực tế:
  - Giao dịch bình thường.
  - Giao dịch có dấu hiệu bất thường.
  - Request thiếu field bắt buộc.
  - Request sai kiểu dữ liệu.
- Rà soát nội dung báo cáo theo các phần bắt buộc:
  - Worklog.
  - Proposal.
  - Workshop.
  - Self-evaluation.
  - Feedback.
- Lập danh sách tài nguyên cần dọn dẹp:
  - SageMaker Endpoint.
  - Endpoint configuration.
  - SageMaker model.
  - Lambda functions.
  - API Gateway.
  - Kinesis Data Stream.
  - Kinesis Firehose.
  - SNS Topic.
  - S3 bucket hoặc object demo nếu không cần giữ lại.
  - CloudWatch Log Groups nếu cần xóa.

## Kết quả đạt được

- Có kịch bản kiểm thử end-to-end cho hệ thống phát hiện gian lận realtime.
- Có nội dung worklog phản ánh quá trình xây dựng project trong 12 tuần.
- Xác định được các tài nguyên cần clean-up để tránh phát sinh chi phí.
- Sẵn sàng tiếp tục bổ sung minh chứng triển khai, hình ảnh kiểm thử và kết quả thực tế vào Workshop.
