---
title: "Worklog Tuần 4"
date: 2026-05-10
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Thời gian:** 10/05/2026 - 16/05/2026

## Mục tiêu tuần 4

- Chuẩn bị dữ liệu cho bài toán Machine Learning.
- Thực hiện tiền xử lý dữ liệu và xây dựng feature phục vụ huấn luyện.
- Đảm bảo dữ liệu đầu vào có định dạng nhất quán giữa training và inference.

## Công việc đã thực hiện

- Khảo sát các trường dữ liệu có thể dùng cho mô hình fraud detection, ví dụ:
  - `transaction_amount`
  - `transaction_type`
  - `merchant_category`
  - `location`
  - `device_type`
  - `transaction_hour`
  - `user_history_count`
  - `label`
- Thực hiện các bước tiền xử lý:
  - Kiểm tra missing values.
  - Chuẩn hóa kiểu dữ liệu.
  - Mã hóa biến phân loại nếu cần.
  - Chuẩn hóa hoặc scale các trường số.
  - Tách dữ liệu train/test.
- Xây dựng các feature có ý nghĩa cho bài toán gian lận:
  - Thời điểm giao dịch.
  - Giá trị giao dịch bất thường.
  - Nhóm loại giao dịch.
  - Đặc điểm thiết bị hoặc vị trí.
- Lưu dữ liệu đã xử lý vào Amazon S3 để SageMaker có thể đọc trong quá trình training.

## Kết quả đạt được

- Có bộ dữ liệu đã được chuẩn hóa để huấn luyện mô hình.
- Hiểu rõ hơn vai trò của feature engineering trong bài toán fraud detection.
- Xác định được danh sách feature cần giữ nhất quán giữa dữ liệu huấn luyện và bước **Lambda Read Features** khi gọi model ở realtime pipeline.
- Chuẩn bị dữ liệu sẵn sàng cho bước huấn luyện trên Amazon SageMaker.
