---
title: "Blog 1 - Credit Card Fraud Detection with Machine Learning on AWS"
date: 2026-04-19
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Building a Real-Time Credit Card Fraud Detection System on AWS

## 1. Problem statement

In the digital era, credit card fraud causes significant losses for the financial industry. The challenge is not only detecting fraudulent transactions, but also responding quickly: the system needs to identify abnormal signals almost immediately, before a transaction is completed or causes greater damage.

In this article, our team shares the process of designing a pipeline on AWS to automatically receive transactions, process data in real time, call a Machine Learning model to predict fraud risk, and send alerts to administrators when suspicious transactions are detected.

## 2. System architecture analysis

The system is divided into two main areas: **Training Zone** and **Real-time Zone**. These two areas operate independently at different stages, but are connected through the model trained and deployed on Amazon SageMaker.

### A. Training Zone

**Amazon S3 Data Lake** serves as the storage location for historical transaction data. This data may include raw data, processed data, train/test datasets, and artifacts generated during training.

**Amazon SageMaker** is the central component of the training area. Data from S3 is loaded into SageMaker for preprocessing, feature engineering, model training, and evaluation. After the model achieves the expected results, artifacts such as `model.joblib`, `scaler.joblib`, and `inference.py` are packaged into `model.tar.gz`, then deployed as a SageMaker Real-time Endpoint to be ready for prediction.

### B. Real-time Zone

**Amazon API Gateway** and **AWS Lambda** are the entry points of the real-time system. When a user or transaction system sends a request, API Gateway receives the request and triggers Lambda to parse JSON, validate the data, and standardize the input format.

**Amazon Kinesis Data Streams** acts as a high-speed buffer for the transaction stream. Instead of having the input Lambda call the model directly, transactions are sent to Kinesis to decouple the data ingestion step from the prediction processing step. This design helps the pipeline handle load better when traffic spikes.

During inference, another Lambda reads data from Kinesis, performs feature mapping, and calls the SageMaker Endpoint to receive prediction results. If a transaction is classified as `Fraud`, the system sends an alert through **Amazon SNS** to the administrator's email.

In parallel with the alerting process, transaction data and prediction results are written back to **Amazon S3** through **Kinesis Data Firehose**. This data can be used for auditing, post-deployment analysis, or model retraining in the future.

## 3. Lessons and insights from the team

During the architecture design process, the team drew several practical lessons about choosing and combining AWS services for the fraud detection problem.

### Use services that match each specific role

Initially, the team considered using a single Lambda to receive requests, process data, and call the model. This approach is simpler, but it can make the system tightly coupled between transaction ingestion and prediction.

Placing Amazon Kinesis in the middle helps separate these two parts. The input Lambda only needs to focus on receiving and validating data, while the downstream processing Lambda can read from the stream and call the SageMaker Endpoint. This design makes the system easier to scale and reduces the risk of losing transactions when traffic spikes.

### Automate the alerting flow

Instead of building an email server or integrating a third-party email API, the team uses **Amazon SNS** to send alerts. When the model predicts a transaction as fraudulent, SNS can send an email to the administrator almost immediately. Within the workshop scope, SNS is a suitable choice because it is simple to configure, easy to test, and integrates well with other AWS services.

### Take advantage of SageMaker Real-time Endpoint

One advantage of using SageMaker is that the process of moving a model from the training stage to the inference serving stage is simplified. After the model is packaged with the correct structure, SageMaker can deploy it as an endpoint that other components can call through an API. This helps the team focus more on the data flow and fraud detection logic instead of managing a model-serving server manually.

### Reduce operational code with Kinesis Data Firehose

If the team wrote custom code to collect streaming data and store it in S3, the system would need additional logic for batching, retries, and write failures. With **Kinesis Data Firehose**, prediction data can be automatically delivered to S3 without managing a separate server. This fits the goal of building a serverless pipeline that is easy to operate and scale.

## 4. Cost optimization strategy

Cloud cost is a factor that needs to be considered from the design stage. For this problem, the team focuses on cost optimization in three main directions.

### Prioritize serverless architecture

Components such as API Gateway, Lambda, SNS, and Kinesis reduce the need to maintain continuously running EC2 servers. The system only incurs costs based on actual usage, making it suitable for demo environments, workshops, or early experimentation stages.

### Optimize training cost with SageMaker

Model training can consume significant CPU/GPU resources. With SageMaker, the team can consider using **Managed Spot Training** to take advantage of AWS spare instances, thereby reducing training costs compared with always using On-Demand Instances.

### Manage the data lifecycle on S3

Transaction data and prediction history may grow over time. Therefore, the team proposes using **S3 Lifecycle Policies** to automatically move older data to lower-cost storage classes such as S3 Standard-IA or S3 Glacier after a certain period. This approach helps retain data for long-term analysis while still controlling storage costs.

## 5. Future development directions

Within the workshop scope, the system focuses on simulating an end-to-end pipeline and using a traditional Machine Learning model such as Random Forest to classify transactions as `Fraud` or `Normal`.

In the next development stages, the team can improve the AI core in SageMaker. Because financial fraud data is often highly imbalanced, data balancing techniques such as SMOTE-ENN can be tested to improve fraud-class detection. In addition, deep learning models for time-series data such as Bi-LSTM can also be explored if the system needs to capture sequential transaction behavior.

Overall, this architecture demonstrates how AWS services such as S3, SageMaker, API Gateway, Lambda, Kinesis, Firehose, and SNS can be combined to build a real-time fraud detection pipeline. It provides a solid foundation for expanding into a more complete transaction monitoring system in the future.
