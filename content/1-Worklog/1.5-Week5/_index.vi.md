---
title: "Worklog Tuần 5"
date: 2026-05-17
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Thời gian:** 17/05/2026 - 23/05/2026

## Mục tiêu tuần 5

- Huấn luyện mô hình Machine Learning cho bài toán phát hiện gian lận.
- Đánh giá mô hình bằng các chỉ số phù hợp.
- Chọn phiên bản model có thể đóng gói và triển khai lên SageMaker Endpoint.

## Công việc đã thực hiện

- Sử dụng dữ liệu đã xử lý từ Amazon S3 để huấn luyện mô hình.
- Xây dựng mô hình **Random Forest** cho bài toán phân loại giao dịch:
  - `Fraud`
  - `Normal`
- Thực hiện chia dữ liệu train/test để đánh giá mô hình.
- Theo dõi các chỉ số đánh giá:
  - Accuracy
  - Precision
  - Recall
  - F1-score
  - Confusion Matrix
- Chú ý đến vấn đề mất cân bằng dữ liệu giữa giao dịch gian lận và giao dịch bình thường.
- So sánh kết quả ban đầu và điều chỉnh một số tham số cơ bản của Random Forest.

## Kết quả đạt được

- Huấn luyện được mô hình Random Forest đầu tiên cho fraud detection.
- Có kết quả đánh giá ban đầu để xác định mô hình có thể sử dụng cho demo workshop.
- Hiểu rõ hơn trade-off giữa Precision và Recall trong bài toán phát hiện gian lận.
- Chọn được phiên bản model phù hợp để tiếp tục đóng gói và triển khai.
