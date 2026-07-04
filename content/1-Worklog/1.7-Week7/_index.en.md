---
title: "Week 7 Worklog"
date: 2026-05-31
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

**Time:** 31/05/2026 - 06/06/2026

## Week 7 Objectives

- Deploy the Machine Learning model as a **SageMaker Real-time Endpoint**.
- Test the ability to receive requests and return prediction results in real time.
- Define how the real-time components will call the endpoint in the pipeline.

## Work completed

- Studied the components involved when deploying a model on Amazon SageMaker:
  - Model artifact.
  - Inference image/container.
  - Endpoint configuration.
  - Real-time Endpoint.
- Uploaded `model.tar.gz` to Amazon S3.
- Created a SageMaker model from the packaged artifact.
- Created an endpoint configuration with an instance suitable for the demo.
- Deployed the SageMaker Real-time Endpoint.
- Sent a sample request to test the endpoint:

```json
{
  "transaction_amount": 2500000,
  "transaction_type": "transfer",
  "merchant_category": "online",
  "transaction_hour": 23,
  "device_type": "mobile"
}
```

- Checked the response returned from the endpoint and recorded errors if the input format did not match.

## Results achieved

- Deployed the model as a SageMaker Real-time Endpoint.
- Understood how the endpoint receives prediction requests and returns inference results.
- Defined the request format that Lambda needs to use in the real-time pipeline.
- Created an endpoint as the core component for fraud prediction in the system.
