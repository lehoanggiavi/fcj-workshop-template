---
title: "Week 10 Worklog"
date: 2026-06-21
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Time:** 21/06/2026 - 27/06/2026

## Week 10 Objectives

- Process prediction results from the SageMaker Endpoint.
- Send alerts when fraudulent transactions are detected.
- Store prediction history for audit and later analysis.

## Work completed

- Standardized the response returned from the SageMaker Endpoint, including:
  - `prediction`
  - `fraud_probability`
  - `timestamp`
  - original transaction information.
- Built result processing logic:
  - If the prediction is `Fraud`, send an alert.
  - If the prediction is `Normal`, record the result and do not send an alert.
- Created an Amazon SNS Topic to send alert emails to the Admin.
- Configured the email subscription and confirmed the subscription.
- Integrated the real-time Lambda with SNS.
- Created Kinesis Firehose to write prediction results to Amazon S3.
- Designed the stored history data, including:
  - Transaction
  - Feature
  - Prediction
  - Probability
  - Timestamp

## Results achieved

- The system can send alerts when a suspicious fraudulent transaction is detected.
- All prediction results are stored in Amazon S3 through Kinesis Firehose, including Transaction, Feature, Prediction, Timestamp, and Probability.
- Historical data is available for audit, monitoring, and future retraining.
- The real-time pipeline became more complete, from input and prediction to alerting and storage.
