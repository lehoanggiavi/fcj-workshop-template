---
title: "Week 3 Worklog"
date: 2026-05-03
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

**Time:** 03/05/2026 - 09/05/2026

## Week 3 Objectives

- Design the overall architecture for the fraud detection system on AWS.
- Clearly separate two processing areas: **Training Zone** and **Real-time Zone**.
- Build the initial data organization approach on Amazon S3.

## Work completed

- Designed the overall pipeline with two parts:
  - **Training Zone:** store data, train the model, evaluate the model, and deploy the endpoint.
  - **Real-time Zone:** receive transactions, process them in real time, call the model, send alerts, and store history.
- Identified the main AWS services:
  - Amazon S3 as the Data Lake.
  - Amazon SageMaker for training and deploying the model.
  - Amazon API Gateway as the system entry point.
  - AWS Lambda for request processing and feature engineering.
  - Amazon Kinesis for real-time transaction streaming.
  - Amazon SNS for sending alerts.
  - Kinesis Firehose for writing results to S3.
  - Amazon CloudWatch for monitoring logs and metrics.
- Designed the data storage structure on S3, for example:
  - `raw/` stores the original dataset.
  - `data_train/` stores training data after the data preparation step.
  - `model/` stores the model artifact and related files.
  - `model.tar.gz` is the packaged model file used to create the SageMaker Endpoint.
- Drafted an architecture diagram to use in the Proposal and Workshop sections.

## Results achieved

- Created an overall architecture for the fraud detection project on AWS.
- Defined the role of each service in the pipeline.
- Designed the data flow from training to real-time inference.
- Prepared the foundation for implementing the data and model components.
