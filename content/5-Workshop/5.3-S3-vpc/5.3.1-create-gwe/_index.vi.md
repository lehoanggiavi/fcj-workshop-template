---
title : "Tạo S3 bucket và cấu trúc Data Lake"
date : 2026-04-19
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

Bước đầu tiên là tạo một S3 bucket để lưu toàn bộ dữ liệu và artifact của hệ thống Fraud Detection.

## 1. Mở Amazon S3 Console

Truy cập AWS Console, tìm dịch vụ **S3** và mở trang quản lý bucket.

![Amazon S3 Console](/images/5-Workshop/5.3-S3-vpc/S3.jpg)

## 2. Tạo bucket cho project

Chọn **Create bucket** và đặt tên bucket theo quy tắc dễ nhận biết, ví dụ:

```text
fraud-detection-<your-name>-<date>
```

Tên bucket cần là duy nhất trên toàn AWS, vì vậy có thể thêm tên cá nhân hoặc ngày tạo vào cuối tên bucket.

Cấu hình đề xuất:

| Cấu hình | Giá trị đề xuất |
| --- | --- |
| Region | `us-east-1` |
| Object Ownership | ACLs disabled |
| Block Public Access | Bật toàn bộ |
| Bucket Versioning | Có thể tắt trong demo |
| Default encryption | Giữ mặc định hoặc bật SSE-S3 |

{{% notice warning %}}
Không public bucket vì dữ liệu giao dịch và model artifact không nên được truy cập công khai.
{{% /notice %}}

![Tạo S3 bucket cho Fraud Detection](/images/5-Workshop/5.3-S3-vpc/create_bucket.jpg)

## 3. Tạo cấu trúc thư mục trong bucket

Sau khi bucket được tạo, tạo các prefix sau để dễ quản lý dữ liệu:

```text
raw/
data_train/
model/
model.tar.gz
```

Ý nghĩa:

- `raw/`: chứa file dataset gốc `creditcard.csv`.
- `data_train/`: chứa dữ liệu train sau bước chuẩn bị dữ liệu.
- `model/`: chứa model artifact và các file liên quan.
- `model.tar.gz`: file model đã đóng gói để tạo SageMaker Endpoint.

![Cấu trúc S3 bucket sau khi tạo](/images/5-Workshop/5.3-S3-vpc/bucket.jpg)

## Kết quả cần đạt

Sau bước này, S3 bucket đã sẵn sàng để tải dataset trực tiếp bằng Amazon S3 Console và lưu các artifact của pipeline Machine Learning.
