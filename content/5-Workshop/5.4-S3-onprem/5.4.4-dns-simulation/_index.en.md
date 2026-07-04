---
title : "Test the endpoint with a sample request"
date : 2026-04-19
weight : 4
chapter : false
pre : " <b> 5.4.4 </b> "
---

After the SageMaker Endpoint is in the `InService` state, send a sample request to verify that the model can return a prediction result.

## Sample request

Example transaction request:

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

![Sample request sent to SageMaker Endpoint](/images/5-Workshop/5.4-S3-onprem/Request_mau.jpg)

## Expected response

If the transaction is high-risk:

```json
{
  "prediction": "Fraud",
  "fraud_probability": 0.91
}
```

If the transaction is normal:

```json
{
  "prediction": "Normal",
  "fraud_probability": 0.08
}
```

![Sample prediction result from SageMaker Endpoint](/images/5-Workshop/5.4-S3-onprem/predict.jpg)

## Expected result

The endpoint must return the prediction label `Fraud` or `Normal` along with the fraud probability `fraud_probability`. This result will be used in the realtime pipeline in section 5.5.
