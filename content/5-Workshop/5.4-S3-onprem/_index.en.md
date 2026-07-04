---
title : "Train the Model and Deploy a SageMaker Endpoint"
date : 2026-04-19
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

This section focuses on building a Machine Learning model for the credit card fraud detection problem and deploying the model as a **SageMaker Real-time Endpoint**.

The input data is taken from the Amazon S3 Data Lake in section 5.3. After data processing and model training, the required artifacts are packaged so that SageMaker can serve realtime inference.

![Training Zone diagram for Fraud Detection](/images/5-Workshop/5.4-S3-onprem/training_zone.jpg)

## Objectives of this section

After completing section 5.4, you should achieve the following results:

- Read the dataset from Amazon S3.
- Perform preprocessing and feature engineering.
- Train a Random Forest model for the Fraud/Normal classification problem.
- Save the model as `model.joblib` and the scaler as `scaler.joblib`.
- Prepare the `inference.py` file so that the SageMaker Endpoint can process realtime requests.
- Package the model as `model.tar.gz`.
- Deploy the model as a SageMaker Real-time Endpoint.

## Implementation steps

1. [Prepare the model training environment](5.4.1-prepare/)
2. [Train the model and save artifacts](5.4.2-create-interface-enpoint/)
3. [Package the model and create the SageMaker Endpoint](5.4.3-test-endpoint/)
4. [Test the endpoint with a sample request](5.4.4-dns-simulation/)

{{% notice warning %}}
A SageMaker Real-time Endpoint can incur costs while the endpoint is running. After finishing the demo, delete the endpoint in the clean-up section.
{{% /notice %}}
