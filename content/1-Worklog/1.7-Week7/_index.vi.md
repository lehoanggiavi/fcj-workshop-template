---
title: "Worklog Tuần 7"
date: 2026-05-31
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

**Thời gian:** 31/05/2026 - 06/06/2026

## Mục tiêu tuần 7

- Triển khai mô hình Machine Learning thành **SageMaker Real-time Endpoint**.
- Kiểm tra khả năng nhận request và trả kết quả prediction theo thời gian thực.
- Xác định cách các thành phần realtime sẽ gọi endpoint trong pipeline.

## Công việc đã thực hiện

- Tìm hiểu các thành phần khi deploy model trên Amazon SageMaker:
  - Model artifact.
  - Inference image/container.
  - Endpoint configuration.
  - Real-time Endpoint.
- Upload `model.tar.gz` lên Amazon S3.
- Tạo SageMaker model từ artifact đã đóng gói.
- Tạo endpoint configuration với instance phù hợp cho demo.
- Deploy SageMaker Real-time Endpoint.
- Gửi thử request mẫu để kiểm tra endpoint:

```json
{
  "transaction_amount": 2500000,
  "transaction_type": "transfer",
  "merchant_category": "online",
  "transaction_hour": 23,
  "device_type": "mobile"
}
```

- Kiểm tra response trả về từ endpoint và ghi nhận lỗi nếu format input chưa khớp.

## Kết quả đạt được

- Triển khai được model thành SageMaker Real-time Endpoint.
- Hiểu cách endpoint nhận request prediction và trả kết quả inference.
- Xác định được format request cần dùng cho Lambda ở realtime pipeline.
- Có endpoint làm trung tâm cho phần dự đoán gian lận trong hệ thống.
