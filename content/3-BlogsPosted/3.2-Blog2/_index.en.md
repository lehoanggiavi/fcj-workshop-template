---
title: "Blog 2 - How Does Amazon Automate Workforce Planning with Serverless?"
date: 2026-04-19
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# How Does Amazon Automate Workforce Planning with Serverless?

Hello everyone in the AWS Study Group VN community.

I recently read an interesting article from the AWS Architecture Blog about **ALAP (Automated Labor Assumptions Platform)**, a system Amazon built to automate workforce planning for more than 100 sort centers across North America.

## The problem

Previously, every week, **Labor Planning Analysts (LPAs)** had to consolidate data from multiple sources, edit many Excel files, meet with different teams, and create input data for the workforce planning system.

This process took about **10+ hours per week for each planner**, was prone to errors, difficult to scale, and had almost no audit trail.

## Solution architecture

Amazon built a fully Serverless platform on AWS with the following components:

- **Amazon S3** stores data and guidance documents.
- **AWS Glue** handles ETL and aggregates data from multiple systems.
- **Amazon Aurora PostgreSQL** acts as a Data Mart for analytical queries.
- **Amazon EventBridge** schedules the weekly workflow.
- **Amazon SQS** distributes more than 3,000 parallel tasks for each site and metric.
- **AWS Lambda** handles calculations, backend APIs, and orchestration.
- **Amazon DynamoDB** stores metadata, job status, and override history.
- **Amazon Cognito + CloudFront + S3** build the user-facing web interface.

## How the process works

Every week, **EventBridge** automatically triggers the pipeline.

**Lambda** creates thousands of parallel tasks to read historical data, apply business rules and results from the Machine Learning model, then generate planning datasets for the **next 13 weeks**.

Managers can access the web interface to view data, make edits (**override**), submit approvals, and finally export the data to the workforce optimization system.

## Results achieved

After deploying ALAP, Amazon recorded:

- About **70% reduction in planning time**, from more than 10 hours to around 3–4 hours per week for each planner.
- Standardized processes for more than 100 sort centers.
- Almost complete elimination of manual data entry errors.
- Full change and approval history (**Audit Trail**).
- Completion of more than **3,000 processing tasks** in only about 3 hours.

## What I learned

The most impressive point to me is how Amazon combines multiple Serverless services to build a system that is both scalable and cost-optimized:

- **Lambda** processes compute tasks on demand.
- **SQS** enables fan-out for thousands of parallel tasks.
- **Aurora PostgreSQL** supports complex analytical queries.
- **DynamoDB** stores metadata and workflow status.
- **EventBridge** automates the entire process on a schedule.

This is a very typical example of how **Event-Driven** and **Serverless** architecture can replace manual processes, increasing operational efficiency while still reducing infrastructure management costs.

If you are building batch processing systems, automated workflows, or internal enterprise platforms, the ALAP architecture is a case study worth referencing.
