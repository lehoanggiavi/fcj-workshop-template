---
title : "Đóng gói model và tạo SageMaker Endpoint"
date : 2026-04-19
weight : 3
chapter : false
pre : " <b> 5.4.3 </b> "
---

Để SageMaker có thể phục vụ model dưới dạng realtime endpoint, cần đóng gói model artifact cùng file inference.

## Các file cần có

```text
model.joblib
scaler.joblib
inference.py
```

Trong đó:

- `model.joblib`: model đã train.
- `scaler.joblib`: scaler dùng để chuẩn hóa dữ liệu đầu vào.
- `inference.py`: file định nghĩa cách load model, xử lý input request và trả về prediction.

## Đóng gói thành model.tar.gz

Các file trên sẽ được đóng gói thành:

```text
model.tar.gz
```

Sau đó tải file `model.tar.gz` lên S3 bằng giao diện Amazon S3 Console, ví dụ:

```text
s3://<bucket-name>/model.tar.gz
```

![File model.tar.gz sau khi đóng gói model](/images/5-Workshop/5.4-S3-onprem/pakage_model.jpg)

## Tạo SageMaker Endpoint

Sau khi có `model.tar.gz`, tạo SageMaker model, endpoint configuration và realtime endpoint.

Kết quả cần có là một endpoint có trạng thái:

```text
InService
```

![SageMaker Endpoint ở trạng thái InService](/images/5-Workshop/5.4-S3-onprem/sage_maker_endpoint.jpg)

{{% notice warning %}}
Endpoint ở trạng thái `InService` có thể phát sinh chi phí. Chỉ giữ endpoint trong thời gian cần demo/test và xóa sau khi hoàn thành.
{{% /notice %}}
