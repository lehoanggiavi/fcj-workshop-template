---
title : "Build the realtime pipeline, alerts, and history storage"
date : 2026-04-19
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

This section builds the realtime flow to receive new transactions, call the SageMaker Endpoint to predict Fraud/Normal, send alerts when fraud is detected, and store the prediction history.

Main realtime flow:


![Realtime Zone diagram for Fraud Detection](/images/5-Workshop/5.5-Policy/realtime_zone.jpg)

## Components to deploy

| Component | Role |
| --- | --- |
| API Gateway | Receives transaction requests from the User or Banking System |
| Lambda ingest | Parses JSON, validates input, and sends transactions to Kinesis |
| Kinesis Data Streams | Buffers the realtime transaction stream |
| Lambda Read Features | Reads transactions from Kinesis, maps features, and calls the SageMaker Endpoint |
| SageMaker Endpoint | Returns the prediction `Fraud` or `Normal` |
| SNS | Sends email alerts if Fraud is detected |
| Firehose | Writes prediction results to S3 |
| Amazon S3 | Stores prediction results for later analysis |
| CloudWatch | Monitors logs and debugs errors |

## Sample transaction request

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

## Expected response

```json
{
  "prediction": 1,
  "probability": 0.9
}
```

{{% notice warning %}}
The realtime pipeline must ensure that the feature mapping in Lambda Read Features matches the feature mapping used during training. This is important to avoid incorrect model predictions caused by inconsistent input.
{{% /notice %}}

## Realtime pipeline deployment images

### API Gateway endpoint

![API Gateway endpoint sau khi deploy](/images/5-Workshop/5.5-Policy/API_Gateway_endpoint.jpg)

### Lambda ingest function

![Lambda ingest function](/images/5-Workshop/5.5-Policy/Lambda_ingest_function.jpg)

### Kinesis Data Stream

![Active Kinesis Data Stream](/images/5-Workshop/5.5-Policy/Kinesis_Data_Stream.jpg)

### Lambda Read Features / CloudWatch Logs

![Lambda Read Features or CloudWatch Logs](/images/5-Workshop/5.5-Policy/Lambda_Read_Features_or_CloudWatch_Logs.jpg)

### Email alert from Amazon SNS

![Email alert when a Fraud transaction is detected](/images/5-Workshop/5.5-Policy/EmailAlert.jpg)
