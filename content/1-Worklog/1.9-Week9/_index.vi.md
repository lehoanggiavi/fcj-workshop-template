---
title: "Worklog Tuần 9"
date: 2026-06-14
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**Thời gian:** 14/06/2026 - 20/06/2026

## Mục tiêu tuần 9

- Tích hợp Amazon Kinesis để xử lý giao dịch theo dạng streaming.
- Xây dựng Lambda đọc dữ liệu từ Kinesis và thực hiện feature engineering cho realtime inference.
- Kết nối Lambda với SageMaker Endpoint.

## Công việc đã thực hiện

- Tạo Amazon Kinesis Data Stream để tiếp nhận transaction từ Lambda ingest.
- Cập nhật Lambda đầu vào để đưa giao dịch hợp lệ vào Kinesis.
- Xây dựng Lambda thứ hai để đọc record từ Kinesis.
- Trong Lambda xử lý realtime, thực hiện:
  - Decode dữ liệu từ Kinesis record.
  - Mapping các trường transaction sang feature model cần.
  - Chuẩn hóa feature theo format đã dùng khi training.
  - Gọi SageMaker Endpoint để lấy kết quả dự đoán.
- Kiểm tra lỗi thường gặp:
  - Thiếu field trong request.
  - Sai kiểu dữ liệu.
  - Sai thứ tự feature.
  - Lambda chưa có quyền gọi SageMaker Endpoint.

## Kết quả đạt được

- Xây dựng được luồng realtime từ API Gateway đến Kinesis.
- Lambda có thể đọc transaction từ stream và chuẩn bị feature cho model.
- Kết nối được Lambda realtime với SageMaker Endpoint.
- Hoàn thiện phần chính của pipeline dự đoán gian lận theo thời gian thực.
