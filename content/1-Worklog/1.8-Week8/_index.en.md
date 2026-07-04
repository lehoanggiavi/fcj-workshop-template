---
title: "Week 8 Worklog"
date: 2026-06-07
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Time:** 07/06/2026 - 13/06/2026

## Week 8 Objectives

- Build an API to receive transactions from users or a simulated system.
- Use Amazon API Gateway as the entry point of the real-time pipeline.
- Write the first Lambda function to validate and standardize transaction requests.

## Work completed

- Designed the transaction request structure in JSON format.
- Created an Amazon API Gateway endpoint to receive `POST` requests.
- Built an AWS Lambda function to process requests from API Gateway:
  - Parse JSON body.
  - Check required fields.
  - Validate data types.
  - Standardize input data.
  - Return clear errors if the request is missing information.
- Prepared the logic to push valid transactions to Amazon Kinesis in the next step.
- Tested the API with sample requests and observed logs in CloudWatch Logs.

## Results achieved

- Created the input API for the fraud detection system.
- Lambda can receive and validate transaction data.
- Defined a stable request format for the entire real-time pipeline.
- Established the foundation for integrating API Gateway, Lambda, and Kinesis.
