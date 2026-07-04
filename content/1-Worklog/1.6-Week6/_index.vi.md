---
title: "Worklog Tuần 6"
date: 2026-05-24
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Thời gian:** 24/05/2026 - 30/05/2026

## Mục tiêu tuần 6

- Đóng gói mô hình đã huấn luyện để chuẩn bị triển khai trên Amazon SageMaker.
- Xây dựng inference script để endpoint có thể nhận input và trả kết quả prediction.
- Đảm bảo quá trình xử lý input lúc inference tương thích với dữ liệu lúc training.

## Công việc đã thực hiện

- Lưu các thành phần cần thiết của mô hình:
  - `model.joblib`
  - `scaler.joblib` nếu có sử dụng bước chuẩn hóa dữ liệu.
  - `inference.py` để định nghĩa logic inference.
- Xây dựng luồng xử lý trong `inference.py`:
  - Load model.
  - Nhận request dạng JSON.
  - Parse dữ liệu giao dịch.
  - Mapping đúng thứ tự feature.
  - Thực hiện prediction.
  - Trả về kết quả `Fraud` hoặc `Normal` cùng xác suất nếu có.
- Đóng gói các file thành artifact:

```text
model.tar.gz
```

- Chuẩn bị artifact để upload lên Amazon S3 và dùng cho SageMaker model deployment.

## Kết quả đạt được

- Hoàn thành bước đóng gói mô hình phục vụ triển khai.
- Có inference script mô tả rõ cách endpoint xử lý request.
- Xác định được format input/output cho SageMaker Endpoint.
- Sẵn sàng triển khai model thành endpoint realtime ở tuần tiếp theo.
