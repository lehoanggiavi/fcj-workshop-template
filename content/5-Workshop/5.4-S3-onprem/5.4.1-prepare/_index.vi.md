---
title : "Chuẩn bị môi trường train model"
date : 2026-04-19
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

Phần này chuẩn bị môi trường để xử lý dữ liệu và huấn luyện mô hình Machine Learning.

Có thể thực hiện bằng một trong hai cách:

1. Sử dụng **Amazon SageMaker Notebook / Studio**.
2. Chuẩn bị code trên máy local rồi đưa file cần thiết lên SageMaker/S3 qua giao diện AWS Console nếu cần.

Trong workshop này, hướng ưu tiên là dùng SageMaker Notebook/Studio để dữ liệu, model và quyền truy cập AWS được quản lý thuận tiện hơn.

## Thư viện cần dùng

```text
pandas
numpy
scikit-learn
joblib
boto3
```

## Kiểm tra môi trường Python

Có thể dùng đoạn code sau để kiểm tra các thư viện chính:

```python
import pandas as pd
import numpy as np
import sklearn
import joblib
import boto3

print("Environment is ready")
```


## Input cần chuẩn bị

Dataset đã được tải lên S3 bằng Amazon S3 Console ở phần 5.3, ví dụ:

```text
s3://<bucket-name>/raw/creditcard.csv
```

Đường dẫn này sẽ được dùng làm input cho bước preprocessing và training.
