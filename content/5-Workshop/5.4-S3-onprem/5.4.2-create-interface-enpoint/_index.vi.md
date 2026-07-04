---
title : "Train model và lưu artifact"
date : 2026-04-19
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

Sau khi môi trường Python đã sẵn sàng, bước tiếp theo là đọc dataset từ S3, xử lý dữ liệu và huấn luyện mô hình Random Forest.

## Luồng xử lý chính

1. Đọc file `creditcard.csv` từ S3.
2. Kiểm tra dữ liệu đầu vào.
3. Tách feature và label.
4. Chia dữ liệu train/test.
5. Chuẩn hóa dữ liệu nếu cần.
6. Train mô hình Random Forest.
7. Đánh giá kết quả model.
8. Lưu model và scaler bằng `joblib`.

## Artifact cần tạo

Sau bước train, cần tạo được các file:

```text
model.joblib
scaler.joblib
```

Trong đó:

- `model.joblib`: mô hình Random Forest đã train.
- `scaler.joblib`: scaler dùng để đảm bảo dữ liệu realtime được chuẩn hóa giống lúc training.

![Kết quả train và đánh giá model Random Forest](/images/5-Workshop/5.4-S3-onprem/evaluate.jpg)

{{% notice warning %}}
Cần đảm bảo feature mapping khi training và feature mapping trong realtime Lambda là nhất quán. Nếu thứ tự hoặc ý nghĩa feature khác nhau, model có thể dự đoán sai.
{{% /notice %}}
