---
title: "Worklog Tuần 8"
date: 2026-06-07
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Thời gian:** 07/06/2026 - 13/06/2026

## Mục tiêu tuần 8

- Xây dựng API để nhận giao dịch từ người dùng hoặc hệ thống giả lập.
- Sử dụng Amazon API Gateway làm điểm vào của realtime pipeline.
- Viết Lambda đầu tiên để validate và chuẩn hóa request giao dịch.

## Công việc đã thực hiện

- Thiết kế cấu trúc request giao dịch dạng JSON.
- Tạo Amazon API Gateway với endpoint nhận request `POST`.
- Xây dựng AWS Lambda để xử lý request từ API Gateway:
  - Parse JSON body.
  - Kiểm tra các trường bắt buộc.
  - Validate kiểu dữ liệu.
  - Chuẩn hóa dữ liệu đầu vào.
  - Trả lỗi rõ ràng nếu request thiếu thông tin.
- Chuẩn bị logic để đẩy transaction hợp lệ vào Amazon Kinesis ở bước tiếp theo.
- Kiểm thử API bằng request mẫu và quan sát log trong CloudWatch Logs.

## Kết quả đạt được

- Có API đầu vào cho hệ thống fraud detection.
- Lambda có thể tiếp nhận và validate dữ liệu giao dịch.
- Xác định được format request ổn định cho toàn bộ realtime pipeline.
- Có nền tảng để tích hợp API Gateway, Lambda và Kinesis.
