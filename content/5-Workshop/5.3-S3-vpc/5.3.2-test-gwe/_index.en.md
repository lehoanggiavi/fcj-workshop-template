---
title : "Upload the dataset to S3 using the AWS Console and verify the data"
date : 2026-04-19
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

The dataset used in the workshop is located on the local machine:

```text
E:\aws\dataset\creditcard.csv
```

This file will be uploaded directly through the Amazon S3 Console interface to the `raw/` folder in the S3 bucket to support the model training step in section 5.4.

## 1. Upload the dataset using the Amazon S3 Console

In the S3 bucket created in the previous step:

1. Open the `raw/` folder.
2. Choose **Upload** in the Amazon S3 interface.
3. Select the `creditcard.csv` file from the local machine.
4. Choose **Upload** to upload the file directly to S3.
5. Wait until the upload status is complete.

![creditcard.csv dataset in the raw folder on Amazon S3](/images/5-Workshop/5.3-S3-vpc/data_in_raw.jpg)

## 2. Verify the dataset after upload

After uploading, verify that the S3 bucket contains the object:

```text
raw/creditcard.csv
```

After the data preparation step, the training data will be stored in `data_train/`, and the model artifact will be stored in `model/` or `model.tar.gz` according to the S3 structure that was created.

{{% notice warning %}}
You do not need to open or capture the entire dataset content if it contains many rows of data. If an illustration is needed, only capture the file name, file size, and storage location in S3.
{{% /notice %}}

## Expected result

After this step, the dataset is stored on Amazon S3 and ready for preprocessing, feature engineering, and model training with SageMaker.
