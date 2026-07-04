---
title : "Prepare Data and S3 Data Lake"
date : 2026-04-19
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

In this section, we prepare the credit card transaction dataset and create the storage structure on Amazon S3 for the entire Fraud Detection pipeline.

Amazon S3 serves as the workshop's **Data Lake**, used to store:

- The original `creditcard.csv` dataset.
- Training data after the data preparation step.
- The directory for model artifacts after training.
- The packaged `model.tar.gz` file used for the SageMaker Endpoint.

![S3 Data Lake overview for Fraud Detection](/images/5-Workshop/5.3-S3-vpc/S3.jpg)

## Objectives of this section

After completing section 5.3, you should achieve the following results:

- Create an S3 bucket for the Fraud Detection project.
- Organize the bucket with a clear structure.
- Upload the `creditcard.csv` dataset to S3 using the Amazon S3 Console.
- Verify that the dataset is in the correct location in the bucket.
- Prepare the S3 paths for the model training step in section 5.4.

## Proposed S3 structure

```text
s3://<bucket-name>/raw/
s3://<bucket-name>/data_train/
s3://<bucket-name>/model/
s3://<bucket-name>/model.tar.gz
```

| Prefix/Object | Purpose |
| --- | --- |
| `raw/` | Stores the original `creditcard.csv` dataset |
| `data_train/` | Stores training data after the data preparation step |
| `model/` | Stores model artifacts and related files |
| `model.tar.gz` | Packaged model file used to create the SageMaker Endpoint |

{{% notice warning %}}
The dataset used in this workshop is for learning and demo purposes only. Do not upload real credit card data or real sensitive data to S3.
{{% /notice %}}

## Implementation steps

1. [Create the S3 bucket and Data Lake structure](5.3.1-create-gwe/)
2. [Upload the dataset to S3 using the AWS Console and verify the data](5.3.2-test-gwe/)
