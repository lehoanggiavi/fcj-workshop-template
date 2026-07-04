---
title : "Clean up resources"
date : 2026-04-19
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

After completing the workshop demo or testing, you only need to delete the **SageMaker Real-time Endpoint** created for the demo to avoid ongoing runtime costs.

Other resources such as API Gateway, Lambda, Kinesis, Firehose, SNS, S3, CloudWatch Logs, and IAM are **not deleted in this step** to avoid affecting the remaining workshop sections or data that must be retained for the report.

{{% notice warning %}}
Do not skip the SageMaker Endpoint clean-up step. The endpoint may continue to incur costs if it remains in the `InService` state.
{{% /notice %}}

## Resource to delete

| Service | Resource to delete |
| --- | --- |
| SageMaker | Delete only the SageMaker Real-time Endpoint used for the demo |

{{% notice note %}}
Only work with the SageMaker endpoint for the Fraud Detection project. Do not delete the S3 bucket, Lambda function, API Gateway, Kinesis, Firehose, SNS, CloudWatch Logs, or IAM Role in this step.
{{% /notice %}}

## SageMaker Endpoint clean-up steps

1. Open the **Amazon SageMaker Console**.
2. Go to **Inference** → **Endpoints**.
3. Select the endpoint created for the Fraud Detection project.
4. Choose **Delete** to delete the endpoint.
5. Confirm that the endpoint is no longer in the `InService` state.

![SageMaker Endpoint after deletion](/images/5-Workshop/5.6-Cleanup/sagemaker_after_delete.jpg)

## Expected result

After the clean-up section, the SageMaker Real-time Endpoint has been deleted to limit ongoing costs. Other resources are retained and not affected.
