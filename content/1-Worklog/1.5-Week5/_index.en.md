---
title: "Week 5 Worklog"
date: 2026-05-17
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Time:** 17/05/2026 - 23/05/2026

## Week 5 Objectives

- Train a Machine Learning model for the fraud detection problem.
- Evaluate the model using suitable metrics.
- Select a model version that can be packaged and deployed to a SageMaker Endpoint.

## Work completed

- Used the processed data from Amazon S3 to train the model.
- Built a **Random Forest** model for transaction classification:
  - `Fraud`
  - `Normal`
- Split the data into train/test sets to evaluate the model.
- Monitored evaluation metrics:
  - Accuracy
  - Precision
  - Recall
  - F1-score
  - Confusion Matrix
- Paid attention to the data imbalance issue between fraudulent transactions and normal transactions.
- Compared the initial results and adjusted several basic Random Forest parameters.

## Results achieved

- Trained the first Random Forest model for fraud detection.
- Obtained initial evaluation results to determine whether the model can be used for the workshop demo.
- Better understood the trade-off between Precision and Recall in the fraud detection problem.
- Selected a suitable model version to continue packaging and deployment.
