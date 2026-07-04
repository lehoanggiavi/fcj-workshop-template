---
title : "Xây dựng realtime pipeline, alert và lưu lịch sử"
date : 2026-04-19
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

Phần này xây dựng luồng realtime để nhận giao dịch mới, gọi SageMaker Endpoint để dự đoán Fraud/Normal, gửi cảnh báo khi phát hiện gian lận và lưu lịch sử kết quả dự đoán.

Luồng realtime chính:


![Sơ đồ Realtime Zone cho Fraud Detection](/images/5-Workshop/5.5-Policy/realtime_zone.jpg)

## Các thành phần cần triển khai

| Thành phần | Vai trò |
| --- | --- |
| API Gateway | Nhận request giao dịch từ User hoặc Banking System |
| Lambda ingest | Parse JSON, validate input và đưa transaction vào Kinesis |
| Kinesis Data Streams | Buffer luồng giao dịch realtime |
| Lambda Read Features | Đọc transaction từ Kinesis, mapping feature và gọi SageMaker Endpoint |
| SageMaker Endpoint | Trả về prediction `Fraud` hoặc `Normal` |
| SNS | Gửi email cảnh báo nếu phát hiện Fraud |
| Firehose | Ghi prediction result xuống S3 |
| Amazon S3 | Lưu kết quả prediction để phân tích sau |
| CloudWatch | Theo dõi log và debug lỗi |

## Request giao dịch mẫu

```json
{
  "transaction": {
    "Time": 134766.0,
    "V1": -0.0796525365521887,
    "V2": 3.22201046223725,
    "V3": -3.7242013893074,
    "V4": 6.03734512826846,
    "V5": 0.583394746331946,
    "V6": -0.691346179707007,
    "V7": -1.79988483348006,
    "V8": -2.62778128431688,
    "V9": -4.00133786259094,
    "V10": -2.27152578398956,
    "V11": 1.51389817939856,
    "V12": -3.68294346446482,
    "V13": 0.185830426148668,
    "V14": -4.69278763834241,
    "V15": 0.247495674947084,
    "V16": -2.68188105082889,
    "V17": -2.28614467887841,
    "V18": -1.04884490280911,
    "V19": 0.994829500437418,
    "V20": 1.1985372847387,
    "V21": -0.664694294683722,
    "V22": 1.13855644649209,
    "V23": -0.350753364122197,
    "V24": -0.287467300585566,
    "V25": 0.808889022979463,
    "V26": 0.823961705381379,
    "V27": 0.668496565754242,
    "V28": 0.595609828713858,
    "Amount": 1.0
}
```

## Response kỳ vọng

```json
{
  "prediction": 1,
  "probability": 0.9
}
```

{{% notice warning %}}
Phần realtime pipeline cần đảm bảo feature mapping trong Lambda Read Features giống với feature mapping đã dùng khi training. Đây là điểm quan trọng để tránh model dự đoán sai do input không nhất quán.
{{% /notice %}}

## Hình ảnh triển khai realtime pipeline

### API Gateway endpoint

![API Gateway endpoint sau khi deploy](/images/5-Workshop/5.5-Policy/API_Gateway_endpoint.jpg)

### Lambda ingest function

![Lambda ingest function](/images/5-Workshop/5.5-Policy/Lambda_ingest_function.jpg)

### Kinesis Data Stream

![Kinesis Data Stream đang hoạt động](/images/5-Workshop/5.5-Policy/Kinesis_Data_Stream.jpg)

### Lambda Read Features / CloudWatch Logs

![Lambda Read Features hoặc CloudWatch Logs](/images/5-Workshop/5.5-Policy/Lambda_Read_Features_or_CloudWatch_Logs.jpg)

### Email alert từ Amazon SNS

![Email alert khi phát hiện giao dịch Fraud](/images/5-Workshop/5.5-Policy/EmailAlert.jpg)
