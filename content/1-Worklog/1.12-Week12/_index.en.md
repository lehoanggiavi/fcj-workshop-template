---
title: "Week 12 Worklog"
date: 2026-04-19
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

**Time:** 05/07/2026 - 19/07/2026

## Week 12 Objectives

- Complete the end-to-end testing scenario for the fraud detection system.
- Finalize the workshop report content in Vietnamese.
- Prepare the clean-up section to avoid costs after the demo.

## Work completed

- Built the end-to-end testing scenario:
  - Send a sample transaction to API Gateway.
  - Lambda receives and validates the request.
  - The transaction is sent to Kinesis.
  - The real-time Lambda reads the record and creates features.
  - Lambda calls the SageMaker Endpoint for prediction.
  - If the result is Fraud, SNS sends an alert email.
  - The prediction result is written to S3 through Kinesis Firehose.
- Prepared test cases to run during the actual deployment:
  - Normal transaction.
  - Transaction with abnormal signs.
  - Request missing required fields.
  - Request with incorrect data types.
- Reviewed the report content according to the required sections:
  - Worklog.
  - Proposal.
  - Workshop.
  - Self-evaluation.
  - Feedback.
- Created a list of resources to clean up:
  - SageMaker Endpoint.
  - Endpoint configuration.
  - SageMaker model.
  - Lambda functions.
  - API Gateway.
  - Kinesis Data Stream.
  - Kinesis Firehose.
  - SNS Topic.
  - S3 bucket or demo objects if they do not need to be kept.
  - CloudWatch Log Groups if they need to be deleted.

## Results achieved

- Created an end-to-end testing scenario for the real-time fraud detection system.
- Prepared worklog content that reflects the 12-week project development process.
- Identified the resources that need to be cleaned up to avoid costs.
- Ready to continue adding deployment evidence, testing screenshots, and actual results to the Workshop.
