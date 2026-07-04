---
title : "Preparation steps"
date : 2026-04-19
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

Before deploying the credit card fraud detection workshop with Machine Learning on AWS, you need to prepare an AWS account, region, IAM permissions, sample dataset, alert email addresses, and several supporting tools.

## 1. AWS account used

In this workshop, the AWS account used is:

```text
ViLamAI2108
```

![AWS account ViLamAI2108](/images/5-Workshop/5.2-Prerequisite/account.jpg)

## 2. Deployment Region

Region used in the workshop:

```text
us-east-1 - N. Virginia
```

Reasons for choosing `us-east-1`:

- This is a common region that fully supports the services needed in the workshop.
- It is easy to check services such as Amazon S3, SageMaker, API Gateway, Lambda, Kinesis, SNS, Firehose, and CloudWatch.
- It is suitable for many AWS documents and deployment examples.

![us-east-1 Region on AWS Console](/images/5-Workshop/5.2-Prerequisite/region.png)

## 3. AWS services required

This workshop uses the following main services:

| Service | Purpose |
| --- | --- |
| Amazon S3 | Stores dataset, model artifact, and prediction history |
| Amazon SageMaker | Trains the model, packages the model, and deploys the endpoint |
| SageMaker Real-time Endpoint | Receives realtime prediction requests |
| Amazon API Gateway | Receives transaction requests from a User or Banking System |
| AWS Lambda | Validates data, processes features, calls the endpoint, and sends results |
| Amazon Kinesis Data Streams | Ingests and buffers the transaction stream |
| Kinesis Firehose | Writes prediction history to S3 |
| Amazon SNS | Sends email alerts when Fraud is detected |
| Amazon CloudWatch | Monitors logs and metrics and supports debugging |
| IAM Role | Manages permissions between services |

![AWS services used in the workshop](/images/5-Workshop/5.2-Prerequisite/service.jpg)

## 4. IAM Roles and access permissions

During the workshop, the current AWS account has several IAM Roles related to SageMaker and integrated services. Some recorded roles include:

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
The IAM Role list above is used to cross-check permissions related to SageMaker and AWS services in the workshop. In a real deployment, choose only the role appropriate for each step and avoid granting permissions broader than necessary.
{{% /notice %}}

### Required IAM permissions by function

Instead of granting overly broad permissions, the workshop should follow the **least privilege** principle. The required permission groups include:

| Permission group | Used for |
| --- | --- |
| S3 permissions | Creating buckets, uploading datasets with the Amazon S3 Console, reading model artifacts, and storing prediction history |
| SageMaker permissions | Creating training jobs, models, endpoint configurations, and endpoints |
| Lambda permissions | Creating functions, invoking functions, and writing logs |
| API Gateway permissions | Creating a REST API or HTTP API to receive transaction requests |
| Kinesis permissions | Creating streams, putting records, and reading records |
| Firehose permissions | Creating delivery streams and writing data to S3 |
| SNS permissions | Creating topics, subscribing emails, and publishing messages |
| CloudWatch Logs permissions | Writing and viewing logs |
| IAM PassRole | Allowing services to use the appropriate roles |

![IAM Roles and access permissions on AWS Console](/images/5-Workshop/5.2-Prerequisite/role.jpg)

## 5. Sample dataset

The sample dataset used in the workshop is located on the local machine at:

```text
E:\aws\dataset\creditcard.csv
```

This dataset is used to simulate credit card transaction data for the fraud detection problem.

During deployment, the dataset will be uploaded directly to Amazon S3 using the S3 Console, for example with the following structure:

```text
s3://<bucket-name>/raw/
s3://<bucket-name>/data_train/
s3://<bucket-name>/model/
s3://<bucket-name>/model.tar.gz
```

{{% notice warning %}}
Do not use real credit card data or real sensitive information in the workshop. The dataset should only be used for learning, demo, and reporting purposes.
{{% /notice %}}

![Sample dataset creditcard.csv](/images/5-Workshop/5.2-Prerequisite/data.jpg)

## 6. SNS alert email addresses

When the system predicts that a transaction is `Fraud`, Amazon SNS will send an alert email to the Admin.

Emails used to receive alerts:

```text
lehoanggiavi21082004@gmail.com
thanpham2k4@gmail.com
```

When creating an SNS subscription, each email needs to confirm the subscription through the email sent by AWS.

![SNS alert email addresses](/images/5-Workshop/5.2-Prerequisite/EmailAlter.jpg)

## 7. What needs to be prepared for Python?

Python is used for the Machine Learning part, specifically data processing, model training, and model packaging.

In this workshop, Python can be used in two ways:

1. Run directly in **Amazon SageMaker Notebook / Studio**.
2. Run on the local machine to prepare code, then upload required files to SageMaker/S3 through the AWS Console if needed.

Required libraries include:

```text
pandas
numpy
scikit-learn
joblib
boto3
```

Role of each library:

| Library | Role |
| --- | --- |
| pandas | Reads and processes the dataset |
| numpy | Processes numeric data |
| scikit-learn | Trains the Random Forest model and evaluates the model |
| joblib | Saves the model as `model.joblib` and the scaler as `scaler.joblib` |
| boto3 | Communicates with AWS services using Python if needed |

Example for checking libraries:

```python
import pandas as pd
import numpy as np
import sklearn
import joblib
import boto3

print("Environment is ready")
```

## 8. Cost warning

Before starting the workshop, you need to clearly identify resources that may incur costs to avoid leaving them running after the demo or testing. Resources that require special attention include:

- **SageMaker Real-time Endpoint:** may continue to incur costs when the endpoint is in the `InService` state.
- **Kinesis Data Streams:** may incur costs based on shard/hour while the stream is active.
- **Kinesis Firehose:** incurs costs based on the amount of data ingested and written to S3.
- **CloudWatch Logs:** may incur costs if many logs are stored or retention is too long.
- **Amazon S3:** has storage costs for the dataset, model artifact, and prediction history, although these are usually low for demo data.
- **API Gateway and Lambda:** costs are usually low in the workshop, but should still be monitored if testing with many requests.

{{% notice warning %}}
After the demo or workshop is complete, perform the clean-up section to delete the SageMaker Endpoint, Kinesis Stream, Firehose, Lambda, API Gateway, SNS, and other resources that are no longer used.
{{% /notice %}}

![AWS cost warning](/images/5-Workshop/5.2-Prerequisite/cost.jpg)
