---
title: "Workshop"
date: 2026-04-19
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

## Overview

In this workshop, we will build a **real-time credit card fraud detection system** by combining Machine Learning and AWS services.

The system is designed with two main parts:

- **Training Zone:** prepares data, trains the Machine Learning model, packages the model, and deploys a SageMaker Real-time Endpoint.
- **Real-time Zone:** receives transactions from a User or Banking System, processes data in a realtime stream, calls the model to predict Fraud/Normal, sends alerts when suspicious transactions are detected, and stores prediction history.

After completing the workshop, participants will understand how to build an end-to-end ML pipeline on AWS, from training data to realtime inference.

## Workshop objectives

After completing the workshop, you can:

- Create an Amazon S3 Data Lake to store transaction data, features, train/test dataset, model artifact, and prediction history.
- Train a **Random Forest** model with Amazon SageMaker.
- Package `model.joblib`, `scaler.joblib`, and `inference.py` into `model.tar.gz`.
- Deploy the model as a **SageMaker Real-time Endpoint**.
- Build an API to receive transactions with Amazon API Gateway.
- Use AWS Lambda to parse JSON, validate data, normalize data, and put transactions into Kinesis.
- Use Amazon Kinesis to ingest realtime transaction streams.
- Use Lambda Read Features to perform feature engineering, map features, and call the SageMaker Endpoint.
- Send alerts through Amazon SNS to the Admin Email when Fraud is detected.
- Store prediction results to Amazon S3 through Kinesis Firehose.
- Monitor logs/metrics with Amazon CloudWatch.
- Clean up resources to avoid incurring costs.

## Overall architecture

```text
Training Zone

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

```text
Real-time Zone

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

![Fraud Detection pipeline diagram](/images/2-Proposal/fraud_detection_pipeline.jpg)


## AWS services used

| Service | Role |
| --- | --- |
| Amazon S3 | Data Lake; stores dataset, model artifact, and prediction history |
| Amazon SageMaker | Trains, evaluates, deploys, and runs inference for the model |
| SageMaker Real-time Endpoint | Predicts Fraud/Normal transactions in real time |
| Amazon API Gateway | API that receives transactions from a User or Banking System |
| AWS Lambda | Validates data, normalizes data, performs feature engineering, and calls the endpoint |
| Amazon Kinesis Data Streams | Ingests and buffers realtime transaction streams |
| Kinesis Firehose | Writes prediction results to Amazon S3 |
| Amazon SNS | Sends email alerts to the Admin when Fraud is detected |
| Amazon CloudWatch | Monitors logs and metrics and supports debugging |
| IAM Role | Manages permissions between services according to the least privilege principle |

## Workshop content

1. [Workshop overview](5.1-Workshop-overview/)
2. [Preparation](5.2-Prerequiste/)
3. [Prepare data and S3 Data Lake](5.3-S3-vpc/)
4. [Train the model and deploy the SageMaker Endpoint](5.4-S3-onprem/)
5. [Build the realtime pipeline, alerts, and history storage](5.5-Policy/)
6. [Clean up resources](5.6-Cleanup/)

{{% notice warning %}}
SageMaker Real-time Endpoint, Kinesis Data Streams, and some other AWS services may incur costs if left running for a long time. Always complete the clean-up section after finishing the workshop.
{{% /notice %}}
