---
title: "Week 2 Worklog"
date: 2026-04-26
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Time:** 26/04/2026 - 02/05/2026

## Week 2 Objectives

- Analyze the transaction fraud detection problem in the context of financial/banking systems.
- Define the system input, output, and success evaluation criteria.
- Choose a Machine Learning approach suitable for the scope of the internship project.

## Work completed

- Studied the characteristics of the fraud detection problem:
  - Transaction data contains many attributes such as amount, time, transaction type, location, device, and behavior history.
  - Fraud data is usually imbalanced compared with normal transactions.
  - The system needs to respond quickly to support real-time alerts.
- Defined the project objectives:
  - Receive transactions from a User or Banking System through API Gateway.
  - Predict whether a transaction is `Fraud` or `Normal`.
  - Return the fraud probability `fraud_probability` when available.
  - Send alerts through SNS to the Admin Email when a suspicious transaction is detected.
  - Store the full prediction history through Kinesis Firehose to Amazon S3 for audit and retraining.
- Reviewed several Machine Learning algorithms that could be used:
  - Logistic Regression
  - Decision Tree
  - Random Forest
  - Gradient Boosting
- Selected **Random Forest** as the main model because it is easy to deploy, easy to explain, and suitable for tabular data.

## Results achieved

- Clearly defined the problem, scope, and expected system outputs.
- Selected a suitable Machine Learning approach for the project.
- Identified the main components of the real-time fraud detection system.
- Established a basis for designing the AWS architecture in the following weeks.
