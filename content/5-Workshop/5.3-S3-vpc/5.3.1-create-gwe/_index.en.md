---
title : "Create the S3 bucket and Data Lake structure"
date : 2026-04-19
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

The first step is to create an S3 bucket to store all data and artifacts for the Fraud Detection system.

## 1. Open the Amazon S3 Console

Access the AWS Console, search for the **S3** service, and open the bucket management page.

![Amazon S3 Console](/images/5-Workshop/5.3-S3-vpc/S3.jpg)

## 2. Create a bucket for the project

Choose **Create bucket** and name the bucket using an easy-to-recognize convention, for example:

```text
fraud-detection-<your-name>-<date>
```

The bucket name must be globally unique across AWS, so you can add your personal name or the creation date at the end of the bucket name.

Recommended configuration:

| Configuration | Recommended value |
| --- | --- |
| Region | `us-east-1` |
| Object Ownership | ACLs disabled |
| Block Public Access | Enable all settings |
| Bucket Versioning | Can be disabled for the demo |
| Default encryption | Keep the default or enable SSE-S3 |

{{% notice warning %}}
Do not make the bucket public because transaction data and model artifacts should not be publicly accessible.
{{% /notice %}}

![Create an S3 bucket for Fraud Detection](/images/5-Workshop/5.3-S3-vpc/create_bucket.jpg)

## 3. Create the folder structure in the bucket

After the bucket is created, create the following prefixes to make data management easier:

```text
raw/
data_train/
model/
model.tar.gz
```

Meaning:

- `raw/`: contains the original `creditcard.csv` dataset file.
- `data_train/`: contains training data after the data preparation step.
- `model/`: contains model artifacts and related files.
- `model.tar.gz`: packaged model file used to create the SageMaker Endpoint.

![S3 bucket structure after creation](/images/5-Workshop/5.3-S3-vpc/bucket.jpg)

## Expected result

After this step, the S3 bucket is ready for uploading the dataset directly using the Amazon S3 Console and for storing artifacts from the Machine Learning pipeline.
