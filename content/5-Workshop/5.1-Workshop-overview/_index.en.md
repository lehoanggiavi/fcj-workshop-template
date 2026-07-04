---
title : "Workshop overview"
date : 2026-04-19
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

## 1. Background

Credit card fraud is an important problem in electronic payment systems. If a fraudulent transaction is not detected in time, it can cause financial loss, affect an organization's reputation, and reduce user trust in the system.

In practice, fraud detection systems often need to process transactions almost in real time. When a new transaction appears, the system must quickly assess the risk level, determine whether the transaction is normal or suspicious, and then send an alert to the administrator if needed.

This workshop simulates such a system using Machine Learning and AWS services.

## 2. Workshop objectives

In this workshop, we will build a **real-time credit card fraud detection system using Machine Learning on AWS**.

The system needs to achieve the following objectives:

- Store historical transaction data on Amazon S3.
- Train a Machine Learning model with Amazon SageMaker.
- Use a Random Forest model to classify transactions as `Fraud` or `Normal`.
- Package the model and deploy it as a SageMaker Real-time Endpoint.
- Receive new transactions through Amazon API Gateway.
- Process realtime transactions with AWS Lambda and Amazon Kinesis.
- Call the SageMaker Endpoint to predict results.
- Send alerts through Amazon SNS if a fraudulent transaction is detected.
- Store prediction history to Amazon S3 through Kinesis Firehose.
- Monitor logs and metrics with Amazon CloudWatch.

## 3. Results after completion

After completing the workshop, you will have a pipeline that includes:

- An S3 Data Lake to store training data, model artifact, and prediction history.
- A Machine Learning model trained with SageMaker.
- A SageMaker Real-time Endpoint for realtime inference.
- An API endpoint for sending sample transactions.
- A Kinesis Data Stream to ingest realtime transactions.
- A Lambda Read Features function to process features and call the model.
- An SNS Topic to send email alerts when Fraud is detected.
- A Firehose Delivery Stream to write prediction history to S3.
- CloudWatch Logs to inspect the processing flow and debug errors.

## 4. Workshop architecture

The architecture is divided into two processing zones.

### 4.1. Training Zone

The Training Zone is responsible for preparing data, training the model, and deploying the model endpoint.

```text
Amazon S3
  │
  ▼
Amazon SageMaker Training
  │
  ▼
model.tar.gz
  │
  ▼
SageMaker Real-time Endpoint
```

In this zone:

1. Historical transaction data is stored on Amazon S3.
2. SageMaker reads data from S3 to perform preprocessing, feature engineering, training, and model evaluation.
3. After training, the Random Forest model is saved as `model.joblib`.
4. If there is a data normalization step, the scaler is saved as `scaler.joblib`.
5. The `inference.py` file defines how the model receives input and returns predictions.
6. The files are packaged into `model.tar.gz`.
7. SageMaker deploys the model as a Real-time Endpoint.

### 4.2. Real-time Zone

The Real-time Zone is responsible for receiving new transactions, calling the model for prediction, sending alerts, and storing history.

```text
User / Banking System
  │
  ▼
Amazon API Gateway
  │
  ▼
AWS Lambda
  │
  ▼
Amazon Kinesis
  │
  ▼
Lambda Read Features
  │
  ▼
SageMaker Endpoint
  ├── Fraud  ─► Amazon SNS ─► Email Admin
  └── Prediction Result
          │
          ▼
Kinesis Firehose
          │
          ▼
Amazon S3
```

In this zone:

1. A User or Banking System sends a transaction request through API Gateway.
2. The input Lambda parses JSON, validates data, and normalizes the request.
3. A valid transaction is put into Amazon Kinesis.
4. Lambda Read Features reads records from Kinesis, performs feature engineering, and maps features.
5. Lambda calls the SageMaker Endpoint to predict `Fraud` or `Normal`.
6. If the result is `Fraud`, the system sends an alert through SNS to the Admin Email.
7. The full prediction result is written to S3 through Kinesis Firehose.

![Fraud Detection pipeline diagram](/images/2-Proposal/fraud_detection_pipeline.jpg)

{{% notice note %}}
**Image to capture/insert later:** The architecture diagram of the Fraud Detection system. If you redraw the diagram, it should clearly show the two zones, Training Zone and Real-time Zone, with these services: S3, SageMaker, API Gateway, Lambda, Kinesis, SNS, Firehose, and CloudWatch.
{{% /notice %}}

## 5. Expected input and output data

An input transaction may look like this:

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

The result returned by the model may be:

```json
{
  "prediction": "Fraud",
  "fraud_probability": 0.91
}
```

Or:

```json
{
  "prediction": "Normal",
  "fraud_probability": 0.08
}
```

## 6. Important notes

- Do not use real credit card data in the workshop.
- Use only sample data or anonymized data for learning purposes.
- Do not hard-code AWS Access Key or Secret Key in source code.
- Use IAM Roles according to the least privilege principle.
- SageMaker Endpoint can incur costs while running, so it must be cleaned up after the demo.
- Each deployment step should be tested separately before running end-to-end.
