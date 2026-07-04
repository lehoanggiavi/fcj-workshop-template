---
title : "Package the model and create the SageMaker Endpoint"
date : 2026-04-19
weight : 3
chapter : false
pre : " <b> 5.4.3 </b> "
---

For SageMaker to serve the model as a realtime endpoint, the model artifacts must be packaged together with the inference file.

## Required files

```text
model.joblib
scaler.joblib
inference.py
```

Where:

- `model.joblib`: the trained model.
- `scaler.joblib`: the scaler used to standardize input data.
- `inference.py`: the file that defines how to load the model, process input requests, and return predictions.

## Package as model.tar.gz

The files above will be packaged into:

```text
model.tar.gz
```

Then upload the `model.tar.gz` file to S3 using the Amazon S3 Console interface, for example:

```text
s3://<bucket-name>/model.tar.gz
```

![model.tar.gz file after packaging the model](/images/5-Workshop/5.4-S3-onprem/pakage_model.jpg)

## Create the SageMaker Endpoint

After `model.tar.gz` is available, create a SageMaker model, endpoint configuration, and realtime endpoint.

The expected result is an endpoint with the status:

```text
InService
```

![SageMaker Endpoint in InService status](/images/5-Workshop/5.4-S3-onprem/sage_maker_endpoint.jpg)

{{% notice warning %}}
An endpoint in the `InService` state can incur costs. Keep the endpoint only for the time needed for the demo/test and delete it after completion.
{{% /notice %}}
