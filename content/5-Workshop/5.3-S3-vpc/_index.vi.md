---
title : "Chuẩn bị dữ liệu và S3 Data Lake"
date : 2026-04-19
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

Trong phần này, chúng ta chuẩn bị dataset giao dịch thẻ tín dụng và tạo cấu trúc lưu trữ trên Amazon S3 để phục vụ cho toàn bộ pipeline Fraud Detection.

Amazon S3 đóng vai trò là **Data Lake** của workshop, dùng để lưu:

- Dataset gốc `creditcard.csv`.
- Dữ liệu train sau bước chuẩn bị dữ liệu.
- Thư mục lưu model artifact sau khi train.
- File đóng gói `model.tar.gz` dùng cho SageMaker Endpoint.

![Tổng quan S3 Data Lake cho Fraud Detection](/images/5-Workshop/5.3-S3-vpc/S3.jpg)

## Mục tiêu của phần này

Sau khi hoàn thành phần 5.3, cần đạt được các kết quả sau:

- Tạo được S3 bucket cho project Fraud Detection.
- Tổ chức bucket theo cấu trúc rõ ràng.
- Tải dataset `creditcard.csv` lên S3 bằng Amazon S3 Console.
- Kiểm tra dataset đã nằm đúng vị trí trong bucket.
- Chuẩn bị sẵn đường dẫn S3 để dùng cho bước huấn luyện model ở phần 5.4.

## Cấu trúc S3 đề xuất

```text
s3://<bucket-name>/raw/
s3://<bucket-name>/data_train/
s3://<bucket-name>/model/
s3://<bucket-name>/model.tar.gz
```

| Prefix/Object | Mục đích |
| --- | --- |
| `raw/` | Lưu dataset gốc `creditcard.csv` |
| `data_train/` | Lưu dữ liệu train sau bước chuẩn bị dữ liệu |
| `model/` | Lưu model artifact và các file liên quan |
| `model.tar.gz` | File model đã đóng gói để tạo SageMaker Endpoint |

{{% notice warning %}}
Dataset sử dụng trong workshop chỉ phục vụ mục đích học tập và demo. Không tải dữ liệu thẻ tín dụng thật hoặc dữ liệu nhạy cảm thật lên S3.
{{% /notice %}}

## Nội dung thực hiện

1. [Tạo S3 bucket và cấu trúc Data Lake](5.3.1-create-gwe/)
2. [Tải dataset lên S3 bằng AWS Console và kiểm tra dữ liệu](5.3.2-test-gwe/)
