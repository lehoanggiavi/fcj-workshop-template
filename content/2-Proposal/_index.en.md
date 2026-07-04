---
title: "Proposal"
date: 2026-04-19
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## 1. Project overview

This project proposes building a real-time transaction fraud detection system by combining **Machine Learning** with **AWS** services. The system receives transaction data from a **User or Banking System**, processes the data in a realtime stream, calls a Machine Learning model deployed on Amazon SageMaker to predict whether a transaction is **Fraud** or **Normal**, and then sends an alert when a suspicious fraudulent transaction is detected.

The project is implemented as an individual workshop, focusing on simulating a fraud detection process in financial/banking systems. In addition to prediction, the system also stores prediction history for future review, audit, and model improvement.

## 2. Background and problem statement

In electronic transaction systems, fraud can occur in many forms, such as abnormal transactions, high-value transactions that do not match user behavior, transactions from unfamiliar devices or locations, or transactions occurring at unusual times. If the checking process relies only on fixed rules or manual handling, the system will have difficulty responding quickly as transaction volume increases.

A fraud detection system needs to address the following problems:

- Receive transactions continuously in real time.
- Process transaction data with low latency.
- Predict fraud risk based on historical data and a Machine Learning model.
- Send timely alerts when suspicious transactions are detected.
- Store results for analysis, audit, and model retraining.

This project does not aim to build a real banking system. Instead, it focuses on simulating a practical use case on AWS to demonstrate the process of designing, deploying, and operating a realtime ML pipeline.

## 3. Project objectives

### 3.1. Overall objective

Build an end-to-end pipeline on AWS for transaction fraud detection, including model training, model endpoint deployment, realtime transaction ingestion, prediction, alerting, and history storage.

### 3.2. Specific objectives

- Store transaction data and training data on Amazon S3.
- Train a Machine Learning model with Amazon SageMaker.
- Use a **Random Forest** model for Fraud/Normal classification.
- Package the model as `model.tar.gz` and deploy it as a SageMaker Real-time Endpoint.
- Build an API to receive transactions from a User or Banking System using Amazon API Gateway.
- Use an input AWS Lambda function to parse JSON, validate data, normalize data, and put transactions into Kinesis.
- Use Amazon Kinesis to ingest, buffer, and scale the realtime transaction stream.
- Use Lambda Read Features to read data from Kinesis, perform feature engineering, normalize data, and map features.
- Call the SageMaker Endpoint to receive prediction results including `Fraud` or `Normal`, optionally with `fraud_probability`.
- Send alerts through Amazon SNS to the Admin Email if a transaction is predicted as fraudulent.
- Write prediction history to Amazon S3 through Kinesis Firehose.
- Add logging/monitoring with Amazon CloudWatch.
- Provide clean-up instructions to avoid incurring costs after the workshop.

## 4. Project scope

### 4.1. In scope

- Design the AWS architecture for the fraud detection system.
- Prepare sample transaction data for training and testing.
- Train a simple and explainable Machine Learning model.
- Deploy the model to a SageMaker Real-time Endpoint.
- Build a realtime pipeline using API Gateway, Lambda, Kinesis, and Lambda Read Features.
- Send email alerts to the Admin through Amazon SNS when fraud is detected.
- Store prediction history through Kinesis Firehose to Amazon S3 for audit/retraining.
- Write workshop documentation so others can follow the implementation.

### 4.2. Out of scope

- No real banking data or real sensitive information will be processed.
- No full core banking system will be built.
- No production-grade model optimization will be performed.
- No complex dashboard interface will be implemented in the initial scope.
- The system is not intended to replace specialized fraud detection systems in real enterprise environments.

## 5. Solution architecture

The architecture is divided into two main parts:

- **Training Zone:** stores data, processes data, trains the model, and deploys the model endpoint.
- **Real-time Zone:** receives transactions, processes the stream, calls the model for prediction, sends alerts, and stores history.

![Fraud Detection pipeline diagram](/images/2-Proposal/fraud_detection_pipeline.jpg)

### 5.1. Training Zone

Training Zone flow:

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

Main steps:

1. Historical transaction data is stored in Amazon S3.
2. SageMaker reads data from S3 to perform preprocessing, feature engineering, training, and evaluation.
3. After training, the Random Forest model is saved together with required files such as `model.joblib`, `scaler.joblib`, and `inference.py`.
4. The files are packaged into `model.tar.gz`.
5. SageMaker deploys the model as a Real-time Endpoint for inference.

### 5.2. Real-time Zone

Real-time Zone flow:

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

Main steps:

1. A User or simulated system sends a transaction through API Gateway.
2. The input Lambda validates data, parses JSON, and normalizes the request.
3. A valid transaction is put into Amazon Kinesis Data Stream.
4. The realtime processing Lambda reads data from Kinesis, performs feature engineering, and maps features.
5. Lambda calls the SageMaker Endpoint to receive the prediction result.
6. If the result is Fraud, the system sends an alert through Amazon SNS to the Admin email.
7. The full prediction result is written to Amazon S3 through Kinesis Firehose, including Transaction, Feature, Prediction, Timestamp, and Probability.

## 6. AWS services used and reasons for selection

| Service | Role in the system | Reason for selection |
| --- | --- | --- |
| Amazon S3 | Data Lake; stores historical data, feature engineering outputs, train/test dataset, model artifact, and prediction history | Low cost, easy to integrate, suitable as a Data Lake |
| Amazon SageMaker | Data preprocessing, feature engineering, training, evaluation, deployment, and inference | Managed service for Machine Learning, reducing infrastructure configuration effort |
| SageMaker Real-time Endpoint | Receives prediction requests from the realtime system and returns Fraud/Normal | Suitable for use cases that require immediate prediction when a transaction occurs |
| Amazon API Gateway | Entry point for receiving transaction requests from a User or Banking System | Easy to create REST APIs and integrates well with Lambda |
| AWS Lambda | Parses JSON, validates data, normalizes data, puts data into Kinesis, reads features, and calls the endpoint | Serverless and runs only when there is a request/event |
| Amazon Kinesis Data Streams | Ingests transaction streams, supports streaming, large-scale processing, and data buffering | Suitable for streaming data processing and scalable workloads |
| Kinesis Firehose | Writes prediction results to S3 | Simplifies moving streaming data into storage |
| Amazon SNS | Sends fraud alert emails to the Admin | Easy notification configuration and suitable for demo alerts |
| Amazon CloudWatch | Monitors Lambda, Kinesis, and SageMaker Endpoint | Added as an improvement to observe operations and debug the pipeline |
| IAM Role | Manages permissions between services | Helps apply least privilege and avoid hard-coded credentials |

## 7. Data and Machine Learning model

### 7.1. Input data

Sample transaction data may include the following fields:

```json
{
  "transaction_id": "txn-001",
  "user_id": "user-001",
  "transaction_amount": 2500000,
  "transaction_type": "transfer",
  "merchant_category": "online",
  "location": "Ho Chi Minh City",
  "device_type": "mobile",
  "transaction_hour": 23
}
```

### 7.2. Feature engineering

Some possible features include:

- Transaction amount.
- Transaction type.
- Merchant group.
- Transaction time.
- Device used.
- Transaction location.
- Number of previous transactions by the user if historical data is available.

These features must be mapped consistently between the training stage and Lambda Read Features in the realtime pipeline to avoid input mismatches when calling the SageMaker Endpoint.

### 7.3. Model used

The proposed main model is **Random Forest**.

Reasons for selection:

- Suitable for tabular data.
- Easy to deploy in a demo project.
- Able to handle nonlinear relationships between features.
- Easy to compare results using metrics such as Precision, Recall, and F1-score.
- More suitable for explanation in an internship report than overly complex models.

## 8. Implementation roadmap

| Phase | Estimated time | Main activities |
| --- | --- | --- |
| Phase 1 | Week 1 - Week 2 | Learn AWS, analyze the fraud detection problem, define system requirements |
| Phase 2 | Week 3 - Week 4 | Design architecture, prepare data, preprocess data, and perform feature engineering |
| Phase 3 | Week 5 - Week 6 | Train Random Forest, evaluate the model, package the model and inference script |
| Phase 4 | Week 7 - Week 9 | Deploy SageMaker Endpoint, build API Gateway, Lambda, Kinesis, and realtime inference |
| Phase 5 | Week 10 - Week 11 | Integrate SNS, Firehose, S3, CloudWatch, review IAM, and optimize costs |
| Phase 6 | Week 12 | Test end-to-end, finalize workshop documentation, and clean up |

## 9. Budget estimation

Costs depend on service uptime, data volume, and number of requests. Within the scope of an individual workshop, the system is designed to run with demo data and short usage time to limit costs.

Main cost sources:

- **Amazon S3:** cost for storing dataset, model artifact, and prediction history.
- **Amazon SageMaker:** cost for training job and Real-time Endpoint. This is the most important part to monitor because the endpoint can incur costs while running.
- **API Gateway:** cost based on the number of requests.
- **AWS Lambda:** cost based on invocation count and runtime.
- **Kinesis Data Streams:** cost based on shard/hour and streaming data volume.
- **Kinesis Firehose:** cost based on ingested data volume.
- **SNS:** notification cost, usually low at demo scale.
- **CloudWatch:** cost for log storage and metrics if used heavily.

Cost optimization direction:

- Turn on the SageMaker Endpoint only when needed for demo or testing.
- Delete endpoints, streams, and unnecessary logs after the workshop.
- Use a small sample dataset.
- Configure appropriate CloudWatch log retention.
- Check the AWS Billing Dashboard after the practice session.

## 10. Risks and mitigation plans

| Risk | Impact | Mitigation plan |
| --- | --- | --- |
| SageMaker Endpoint incurs costs if it is not deleted | High | Add clear clean-up steps and check the endpoint after the demo |
| Input format between training and inference does not match | High | Standardize the feature list and test sample requests before realtime integration |
| Lambda lacks permission to call SageMaker/SNS/Firehose | Medium | Create IAM Roles by function and check CloudWatch Logs |
| Imbalanced data causes poor model predictions | Medium | Monitor Precision, Recall, and F1-score; consider imbalance handling if needed |
| Kinesis or Firehose has an incorrect destination configuration | Medium | Test each step before running end-to-end |
| API request is missing fields or has incorrect data types | Low | Validate data in the input Lambda and return clear errors |

## 11. Expected results

After completion, the project is expected to achieve the following results:

- A complete AWS architecture for a realtime fraud detection use case.
- A Random Forest model trained and deployed on SageMaker Endpoint.
- An API for receiving transactions and processing them in realtime with Lambda + Kinesis.
- An email alert mechanism when a suspicious fraudulent transaction is detected.
- Prediction history stored on Amazon S3 for audit and retraining.
- CloudWatch Logs to support system observation and debugging.
- Step-by-step workshop documentation so others can redeploy the system.

## 12. Future development directions

- Add a dashboard showing Fraud/Normal transaction counts over time.
- Use Amazon SageMaker Feature Store to ensure feature consistency between training and inference.
- Automate the retraining pipeline with SageMaker Pipelines or AWS Step Functions.
- Add EventBridge to trigger retraining on a schedule.
- Improve the model with other algorithms such as XGBoost or LightGBM.
- Add a manual review mechanism for transactions with high fraud probability but not high enough for automatic blocking.
- Extend the system to handle batch prediction in parallel with realtime prediction.
