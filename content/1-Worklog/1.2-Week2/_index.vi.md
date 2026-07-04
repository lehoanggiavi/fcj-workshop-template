---
title: "Worklog Tuần 2"
date: 2026-04-26
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Thời gian:** 26/04/2026 - 02/05/2026

## Mục tiêu tuần 2

- Phân tích bài toán phát hiện gian lận giao dịch trong bối cảnh hệ thống tài chính/ngân hàng.
- Xác định input, output và tiêu chí đánh giá thành công của hệ thống.
- Lựa chọn hướng tiếp cận Machine Learning phù hợp với quy mô project thực tập.

## Công việc đã thực hiện

- Tìm hiểu đặc điểm của bài toán fraud detection:
  - Dữ liệu giao dịch có nhiều thuộc tính như số tiền, thời gian, loại giao dịch, vị trí, thiết bị và lịch sử hành vi.
  - Dữ liệu gian lận thường mất cân bằng so với giao dịch bình thường.
  - Hệ thống cần phản hồi nhanh để hỗ trợ cảnh báo realtime.
- Xác định mục tiêu của project:
  - Nhận giao dịch từ User hoặc Banking System thông qua API Gateway.
  - Dự đoán giao dịch là `Fraud` hoặc `Normal`.
  - Trả về xác suất gian lận `fraud_probability` nếu có.
  - Gửi cảnh báo qua SNS đến Email Admin khi phát hiện giao dịch nghi ngờ.
  - Lưu toàn bộ lịch sử dự đoán thông qua Kinesis Firehose xuống Amazon S3 để phục vụ audit và retraining.
- Khảo sát một số thuật toán Machine Learning có thể dùng:
  - Logistic Regression
  - Decision Tree
  - Random Forest
  - Gradient Boosting
- Chọn **Random Forest** làm mô hình chính vì dễ triển khai, dễ giải thích và phù hợp với dữ liệu dạng bảng.

## Kết quả đạt được

- Xác định rõ bài toán, phạm vi và đầu ra mong muốn của hệ thống.
- Chọn được hướng tiếp cận Machine Learning phù hợp cho project.
- Xác định các thành phần chính của hệ thống realtime fraud detection.
- Có cơ sở để thiết kế kiến trúc AWS ở các tuần tiếp theo.
