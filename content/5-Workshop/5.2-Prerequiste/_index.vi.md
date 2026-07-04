---
title : "Các bước chuẩn bị"
date : 2026-04-19
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

Trước khi triển khai workshop phát hiện gian lận thẻ tín dụng bằng Machine Learning trên AWS, cần chuẩn bị tài khoản AWS, region, quyền IAM, dataset mẫu, email nhận cảnh báo và một số công cụ hỗ trợ.

## 1. Tài khoản AWS sử dụng

Trong workshop này, tài khoản AWS sử dụng là:

```text
ViLamAI2108
```

![Tài khoản AWS ViLamAI2108](/images/5-Workshop/5.2-Prerequisite/account.jpg)

## 2. Region triển khai

Region sử dụng trong workshop:

```text
us-east-1 - N. Virginia
```

Lý do chọn `us-east-1`:

- Đây là region phổ biến, hỗ trợ đầy đủ các dịch vụ cần dùng trong workshop.
- Dễ kiểm tra các dịch vụ như Amazon S3, SageMaker, API Gateway, Lambda, Kinesis, SNS, Firehose và CloudWatch.
- Phù hợp với nhiều tài liệu AWS và ví dụ triển khai.

![Region us-east-1 trên AWS Console](/images/5-Workshop/5.2-Prerequisite/region.png)

## 3. Dịch vụ AWS cần sử dụng

Workshop này sử dụng các dịch vụ chính sau:

| Dịch vụ | Mục đích sử dụng |
| --- | --- |
| Amazon S3 | Lưu dataset, model artifact và prediction history |
| Amazon SageMaker | Train model, đóng gói model và deploy endpoint |
| SageMaker Real-time Endpoint | Nhận request prediction realtime |
| Amazon API Gateway | Nhận transaction request từ User hoặc Banking System |
| AWS Lambda | Validate dữ liệu, xử lý feature, gọi endpoint và gửi kết quả |
| Amazon Kinesis Data Streams | Tiếp nhận và buffer transaction stream |
| Kinesis Firehose | Ghi prediction history xuống S3 |
| Amazon SNS | Gửi email cảnh báo khi phát hiện Fraud |
| Amazon CloudWatch | Theo dõi log, metric và hỗ trợ debug |
| IAM Role | Phân quyền giữa các dịch vụ |

![Các dịch vụ AWS sử dụng trong workshop](/images/5-Workshop/5.2-Prerequisite/service.jpg)

## 4. IAM Role và quyền truy cập

Trong quá trình thực hiện workshop, tài khoản AWS hiện có một số IAM Role liên quan đến SageMaker và các dịch vụ tích hợp. Một số role đã ghi nhận gồm:

```text
AmazonSageMaker-ExecutionRole-20260526T124392
AmazonSageMaker-ExecutionRole-20260604T161463
AmazonSageMakerAdminIAMExecutionRole
AmazonSagemakerCanvasBedrockRole-20260526T124391
AmazonSageMakerCanvasEMRSExecutionAccess-20260526T124391
AmazonSageMakerServiceCatalogProductsApiGatewayRole
AmazonSageMakerServiceCatalogProductsCloudformationRole
AmazonSageMakerServiceCatalogProductsCodeBuildRole
AmazonSageMakerServiceCatalogProductsCodePipelineRole
AmazonSageMakerServiceCatalogProductsEventsRole
AmazonSageMakerServiceCatalogProductsExecutionRole
AmazonSageMakerServiceCatalogProductsFirehoseRole
AmazonSageMakerServiceCatalogProductsGlueRole
AmazonSageMakerServiceCatalogProductsLambdaRole
AmazonSageMakerServiceCatalogProductsLaunchRole
AmazonSageMakerServiceCatalogProductsUseRole
AWSServiceRoleForAmazonAthena
AWSServiceRoleForAmazonEMRServerless
AWSServiceRoleForAmazonSageMakerNotebooks
AWSServiceRoleForResourceExplorer
```

{{% notice note %}}
Danh sách IAM Role trên được dùng để đối chiếu các quyền liên quan đến SageMaker và các dịch vụ AWS trong workshop. Khi triển khai thực tế, chỉ chọn role phù hợp với từng bước và tránh cấp quyền rộng hơn nhu cầu.
{{% /notice %}}

### Quyền IAM cần thiết theo chức năng

Thay vì cấp quyền quá rộng, workshop nên định hướng theo nguyên tắc **least privilege**. Các nhóm quyền cần có gồm:

| Nhóm quyền | Dùng cho |
| --- | --- |
| S3 permissions | Tạo bucket, tải dataset bằng Amazon S3 Console, đọc model artifact, lưu prediction history |
| SageMaker permissions | Tạo training job, model, endpoint configuration và endpoint |
| Lambda permissions | Tạo function, invoke function, ghi log |
| API Gateway permissions | Tạo REST API hoặc HTTP API để nhận transaction request |
| Kinesis permissions | Tạo stream, put record, read record |
| Firehose permissions | Tạo delivery stream và ghi dữ liệu xuống S3 |
| SNS permissions | Tạo topic, subscribe email, publish message |
| CloudWatch Logs permissions | Ghi và xem log |
| IAM PassRole | Cho phép các dịch vụ sử dụng role phù hợp |

![IAM Role và quyền truy cập trên AWS Console](/images/5-Workshop/5.2-Prerequisite/role.jpg)

## 5. Dataset mẫu

Dataset mẫu sử dụng trong workshop nằm trên máy local tại:

```text
E:\aws\dataset\creditcard.csv
```

Dataset này được dùng để mô phỏng dữ liệu giao dịch thẻ tín dụng phục vụ bài toán phát hiện gian lận.

Trong quá trình triển khai, dataset sẽ được tải trực tiếp lên Amazon S3 bằng giao diện S3 Console, ví dụ theo cấu trúc:

```text
s3://<bucket-name>/raw/
s3://<bucket-name>/data_train/
s3://<bucket-name>/model/
s3://<bucket-name>/model.tar.gz
```

{{% notice warning %}}
Không sử dụng dữ liệu thẻ tín dụng thật hoặc thông tin nhạy cảm thật trong workshop. Dataset chỉ nên dùng cho mục đích học tập, demo và báo cáo.
{{% /notice %}}

![Dataset mẫu creditcard.csv](/images/5-Workshop/5.2-Prerequisite/data.jpg)

## 6. Email nhận cảnh báo SNS

Khi hệ thống dự đoán một giao dịch là `Fraud`, Amazon SNS sẽ gửi email cảnh báo đến Admin.

Email dùng để nhận alert:

```text
lehoanggiavi21082004@gmail.com
thanpham2k4@gmail.com
```

Khi tạo SNS subscription, mỗi email cần xác nhận subscription thông qua email AWS gửi về.

![Email nhận cảnh báo SNS](/images/5-Workshop/5.2-Prerequisite/EmailAlter.jpg)

## 7. Python cần chuẩn bị gì?

Python được dùng cho phần Machine Learning, cụ thể là xử lý dữ liệu, huấn luyện mô hình và đóng gói model.

Trong workshop này, Python có thể được sử dụng theo hai cách:

1. Chạy trực tiếp trong **Amazon SageMaker Notebook / Studio**.
2. Chạy trên máy local để chuẩn bị code, sau đó đưa file cần thiết lên SageMaker/S3 qua giao diện AWS Console nếu cần.

Các thư viện cần dùng gồm:

```text
pandas
numpy
scikit-learn
joblib
boto3
```

Vai trò của từng thư viện:

| Thư viện | Vai trò |
| --- | --- |
| pandas | Đọc và xử lý dataset |
| numpy | Xử lý dữ liệu dạng số |
| scikit-learn | Train mô hình Random Forest và đánh giá model |
| joblib | Lưu model thành `model.joblib` và scaler thành `scaler.joblib` |
| boto3 | Giao tiếp với AWS services bằng Python nếu cần |

Ví dụ kiểm tra thư viện:

```python
import pandas as pd
import numpy as np
import sklearn
import joblib
import boto3

print("Environment is ready")
```

## 8. Cảnh báo chi phí

Trước khi bắt đầu workshop, cần xác định rõ các tài nguyên có thể phát sinh chi phí để tránh để quên sau khi demo hoặc kiểm thử. Các tài nguyên cần đặc biệt chú ý gồm:

- **SageMaker Real-time Endpoint:** có thể tiếp tục phát sinh chi phí khi endpoint ở trạng thái `InService`.
- **Kinesis Data Streams:** có thể phát sinh chi phí theo shard/hour trong thời gian stream hoạt động.
- **Kinesis Firehose:** phát sinh chi phí theo lượng dữ liệu ingest và ghi xuống S3.
- **CloudWatch Logs:** có thể phát sinh chi phí nếu lưu log nhiều hoặc retention quá dài.
- **Amazon S3:** có chi phí lưu trữ dataset, model artifact và prediction history, tuy thường thấp với dữ liệu demo.
- **API Gateway và Lambda:** chi phí thường thấp trong workshop, nhưng vẫn nên theo dõi nếu test với nhiều request.

{{% notice warning %}}
Sau khi demo hoặc hoàn thành workshop, cần thực hiện phần clean-up để xóa SageMaker Endpoint, Kinesis Stream, Firehose, Lambda, API Gateway, SNS và các tài nguyên không còn sử dụng.
{{% /notice %}}

![Cảnh báo chi phí AWS](/images/5-Workshop/5.2-Prerequisite/cost.jpg)
