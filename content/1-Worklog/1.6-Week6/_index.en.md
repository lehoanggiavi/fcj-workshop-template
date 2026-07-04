---
title: "Week 6 Worklog"
date: 2026-05-24
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Time:** 24/05/2026 - 30/05/2026

## Week 6 Objectives

- Package the trained model to prepare for deployment on Amazon SageMaker.
- Build an inference script so the endpoint can receive input and return prediction results.
- Ensure input processing during inference is compatible with the data used during training.

## Work completed

- Saved the required model components:
  - `model.joblib`
  - `scaler.joblib` if a data normalization step is used.
  - `inference.py` to define the inference logic.
- Built the processing flow in `inference.py`:
  - Load model.
  - Receive requests in JSON format.
  - Parse transaction data.
  - Map features in the correct order.
  - Perform prediction.
  - Return the `Fraud` or `Normal` result together with the probability if available.
- Packaged the files into an artifact:

```text
model.tar.gz
```

- Prepared the artifact to upload to Amazon S3 and use for SageMaker model deployment.

## Results achieved

- Completed the model packaging step for deployment.
- Created an inference script that clearly describes how the endpoint processes requests.
- Defined the input/output format for the SageMaker Endpoint.
- Became ready to deploy the model as a real-time endpoint in the following week.
