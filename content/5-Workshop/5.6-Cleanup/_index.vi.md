---
title : "Dọn dẹp tài nguyên"
date : 2026-04-19
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

Sau khi hoàn thành demo hoặc kiểm thử workshop, chỉ cần xóa **SageMaker Real-time Endpoint** đã tạo cho phần demo để tránh phát sinh chi phí theo thời gian chạy.

Các tài nguyên khác như API Gateway, Lambda, Kinesis, Firehose, SNS, S3, CloudWatch Logs và IAM **không xóa trong bước này** để tránh ảnh hưởng đến các phần workshop còn lại hoặc dữ liệu cần giữ lại cho báo cáo.

{{% notice warning %}}
Không nên bỏ qua bước clean-up SageMaker Endpoint. Endpoint có thể tiếp tục phát sinh chi phí nếu để ở trạng thái `InService`.
{{% /notice %}}

## Tài nguyên cần xóa

| Dịch vụ | Tài nguyên cần xóa |
| --- | --- |
| SageMaker | Chỉ xóa SageMaker Real-time Endpoint đã dùng để demo |

{{% notice note %}}
Chỉ thao tác với endpoint SageMaker của project Fraud Detection. Không xóa S3 bucket, Lambda function, API Gateway, Kinesis, Firehose, SNS, CloudWatch Logs hoặc IAM Role trong bước này.
{{% /notice %}}

## Các bước dọn dẹp SageMaker Endpoint

1. Mở **Amazon SageMaker Console**.
2. Vào mục **Inference** → **Endpoints**.
3. Chọn endpoint đã tạo cho project Fraud Detection.
4. Chọn **Delete** để xóa endpoint.
5. Xác nhận endpoint đã không còn ở trạng thái `InService`.

![SageMaker Endpoint sau khi xóa](/images/5-Workshop/5.6-Cleanup/sagemaker_after_delete.jpg)

## Kết quả cần đạt

Sau phần clean-up, SageMaker Real-time Endpoint đã được xóa để hạn chế chi phí phát sinh. Các tài nguyên khác được giữ nguyên và không bị ảnh hưởng.
