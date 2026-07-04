---
title: "Week 9 Worklog"
date: 2026-06-14
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**Time:** 14/06/2026 - 20/06/2026

## Week 9 Objectives

- Integrate Amazon Kinesis to process transactions as streaming data.
- Build a Lambda function that reads data from Kinesis and performs feature engineering for real-time inference.
- Connect Lambda with the SageMaker Endpoint.

## Work completed

- Created an Amazon Kinesis Data Stream to receive transactions from the ingest Lambda.
- Updated the input Lambda to put valid transactions into Kinesis.
- Built a second Lambda function to read records from Kinesis.
- In the real-time processing Lambda, performed the following steps:
  - Decode data from Kinesis records.
  - Map transaction fields to the features required by the model.
  - Standardize features according to the format used during training.
  - Call the SageMaker Endpoint to get prediction results.
- Checked common errors:
  - Missing fields in the request.
  - Incorrect data types.
  - Incorrect feature order.
  - Lambda does not have permission to call the SageMaker Endpoint.

## Results achieved

- Built the real-time flow from API Gateway to Kinesis.
- Lambda can read transactions from the stream and prepare features for the model.
- Connected the real-time Lambda with the SageMaker Endpoint.
- Completed the main part of the real-time fraud prediction pipeline.
