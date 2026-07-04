---
title: "Week 4 Worklog"
date: 2026-05-10
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Time:** 10/05/2026 - 16/05/2026

## Week 4 Objectives

- Prepare data for the Machine Learning problem.
- Perform data preprocessing and build features for training.
- Ensure the input data format is consistent between training and inference.

## Work completed

- Reviewed data fields that can be used for the fraud detection model, for example:
  - `transaction_amount`
  - `transaction_type`
  - `merchant_category`
  - `location`
  - `device_type`
  - `transaction_hour`
  - `user_history_count`
  - `label`
- Performed preprocessing steps:
  - Checked missing values.
  - Standardized data types.
  - Encoded categorical variables if needed.
  - Normalized or scaled numerical fields.
  - Split the data into train/test sets.
- Built meaningful features for the fraud detection problem:
  - Transaction time.
  - Unusual transaction value.
  - Transaction type group.
  - Device or location characteristics.
- Stored the processed data on Amazon S3 so SageMaker can read it during training.

## Results achieved

- Created a standardized dataset for model training.
- Gained a clearer understanding of the role of feature engineering in the fraud detection problem.
- Identified the list of features that must remain consistent between training data and the **Lambda Read Features** step when calling the model in the real-time pipeline.
- Prepared the data for the training step on Amazon SageMaker.
