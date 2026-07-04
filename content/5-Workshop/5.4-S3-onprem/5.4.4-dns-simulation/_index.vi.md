---
title : "Kiểm tra endpoint bằng request mẫu"
date : 2026-04-19
weight : 4
chapter : false
pre : " <b> 5.4.4 </b> "
---

Sau khi SageMaker Endpoint ở trạng thái `InService`, cần gửi request mẫu để kiểm tra model có thể trả về kết quả dự đoán hay không.

## Request mẫu

Ví dụ request giao dịch:

```json
{
  "transaction_id": "txn-001",
  "user_id": "user-001",
  "transaction_amount": 2500000,
  "transaction_type": "online_payment",
  "merchant_category": "electronics",
  "location": "Ho Chi Minh City",
  "device_type": "mobile",
  "transaction_hour": 23
}
```

![Request mẫu gửi đến SageMaker Endpoint](/images/5-Workshop/5.4-S3-onprem/Request_mau.jpg)

## Response kỳ vọng

Nếu giao dịch có rủi ro cao:

```json
{
  "prediction": "Fraud",
  "fraud_probability": 0.91
}
```

Nếu giao dịch bình thường:

```json
{
  "prediction": "Normal",
  "fraud_probability": 0.08
}
```

![Kết quả dự đoán thử từ SageMaker Endpoint](/images/5-Workshop/5.4-S3-onprem/predict.jpg)

## Kết quả cần đạt

Endpoint phải trả về được nhãn dự đoán `Fraud` hoặc `Normal` cùng xác suất gian lận `fraud_probability`. Kết quả này sẽ được dùng trong realtime pipeline ở phần 5.5.
