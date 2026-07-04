---
title : "Huấn luyện mô hình và triển khai SageMaker Endpoint"
date : 2026-04-19
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

Phần này tập trung vào quá trình xây dựng mô hình Machine Learning cho bài toán phát hiện gian lận thẻ tín dụng và triển khai model thành **SageMaker Real-time Endpoint**.

Dữ liệu đầu vào được lấy từ Amazon S3 Data Lake ở phần 5.3. Sau khi xử lý dữ liệu và huấn luyện mô hình, các artifact cần thiết sẽ được đóng gói để SageMaker có thể phục vụ realtime inference.

![Sơ đồ Training Zone cho Fraud Detection](/images/5-Workshop/5.4-S3-onprem/training_zone.jpg)

## Mục tiêu của phần này

Sau khi hoàn thành phần 5.4, cần đạt được các kết quả sau:

- Đọc dataset từ Amazon S3.
- Thực hiện preprocessing và feature engineering.
- Huấn luyện mô hình Random Forest cho bài toán Fraud/Normal.
- Lưu model thành `model.joblib` và scaler thành `scaler.joblib`.
- Chuẩn bị file `inference.py` để SageMaker Endpoint xử lý request realtime.
- Đóng gói model thành `model.tar.gz`.
- Deploy model thành SageMaker Real-time Endpoint.

## Nội dung thực hiện

1. [Chuẩn bị môi trường train model](5.4.1-prepare/)
2. [Train model và lưu artifact](5.4.2-create-interface-enpoint/)
3. [Đóng gói model và tạo SageMaker Endpoint](5.4.3-test-endpoint/)
4. [Kiểm tra endpoint bằng request mẫu](5.4.4-dns-simulation/)

{{% notice warning %}}
SageMaker Real-time Endpoint có thể phát sinh chi phí khi endpoint còn chạy. Sau khi demo xong cần xóa endpoint trong phần clean-up.
{{% /notice %}}
