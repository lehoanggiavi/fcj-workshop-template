---
title: "Week 11 Worklog"
date: 2026-06-28
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

**Time:** 28/06/2026 - 04/07/2026

## Week 11 Objectives

- Add monitoring, logs, and operational alerts for the system.
- Review basic security according to the principle of least privilege.
- Identify possible cost optimization points during demo and operation.

## Work completed

- Checked CloudWatch Logs of the Lambda functions.
- Monitored logs as requests passed through the components:
  - API Gateway
  - Lambda ingest
  - Kinesis
  - Lambda feature processing
  - SageMaker Endpoint
  - SNS
  - Firehose
- Identified several metrics to observe:
  - Number of API requests.
  - Lambda errors.
  - Lambda processing time.
  - Errors when calling the SageMaker Endpoint.
  - Number of records passing through Kinesis/Firehose.
- Reviewed IAM Roles for each component:
  - Lambda only has permission to write to Kinesis when needed.
  - The real-time Lambda only has permission to call the SageMaker Endpoint, publish to SNS, and write to Firehose within the required scope.
  - Do not hard-code access keys or secret keys in source code.
- Recorded cost optimization directions:
  - Only enable the SageMaker Endpoint when needed for demo.
  - Clean up the endpoint after practice.
  - Use a sufficient amount of demo data.
  - Monitor resources that may incur costs.

## Results achieved

- Created a system monitoring plan using CloudWatch Logs and metrics.
- Understood the points that need to be checked when the real-time system encounters errors.
- Reviewed basic IAM permissions to avoid granting overly broad access.
- Identified cost optimization actions and ways to reduce the risk of unexpected AWS costs.
