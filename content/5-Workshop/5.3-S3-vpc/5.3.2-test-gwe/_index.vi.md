---
title : "Tải dataset lên S3 bằng AWS Console và kiểm tra dữ liệu"
date : 2026-04-19
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

Dataset sử dụng trong workshop nằm tại máy local:

```text
E:\aws\dataset\creditcard.csv
```

File này sẽ được tải trực tiếp bằng giao diện Amazon S3 Console lên thư mục `raw/` trong S3 bucket để phục vụ bước train model ở phần 5.4.

## 1. Tải dataset bằng Amazon S3 Console

Trong S3 bucket đã tạo ở bước trước:

1. Mở folder `raw/`.
2. Chọn **Upload** trên giao diện Amazon S3.
3. Chọn file `creditcard.csv` từ máy local.
4. Chọn **Upload** để tải file trực tiếp lên S3.
5. Chờ trạng thái upload hoàn tất.

![Dataset creditcard.csv trong thư mục raw trên Amazon S3](/images/5-Workshop/5.3-S3-vpc/data_in_raw.jpg)

## 2. Kiểm tra dataset sau khi upload

Sau khi upload, kiểm tra trong S3 bucket có object:

```text
raw/creditcard.csv
```

Sau bước chuẩn bị dữ liệu, dữ liệu train sẽ được lưu trong `data_train/` và model artifact sẽ được lưu ở `model/` hoặc `model.tar.gz` theo cấu trúc S3 đã tạo.

{{% notice warning %}}
Không cần mở hoặc chụp toàn bộ nội dung dataset nếu có nhiều dòng dữ liệu. Nếu cần minh họa, chỉ chụp tên file, kích thước file và vị trí lưu trong S3.
{{% /notice %}}

## Kết quả cần đạt

Sau bước này, dataset đã được lưu trên Amazon S3 và sẵn sàng cho quá trình preprocessing, feature engineering và training model bằng SageMaker.
