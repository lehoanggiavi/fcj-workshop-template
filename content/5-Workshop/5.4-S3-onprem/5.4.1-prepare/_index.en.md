---
title : "Prepare the model training environment"
date : 2026-04-19
weight : 1
chapter : false
pre : " <b> 5.4.1 </b> "
---

This section prepares the environment for data processing and Machine Learning model training.

You can do this in one of two ways:

1. Use **Amazon SageMaker Notebook / Studio**.
2. Prepare the code on a local machine and then upload the required files to SageMaker/S3 through the AWS Console interface if needed.

In this workshop, the preferred approach is to use SageMaker Notebook/Studio so that data, models, and AWS access permissions are managed more conveniently.

## Required libraries

```text
pandas
numpy
scikit-learn
joblib
boto3
```

## Check the Python environment

You can use the following code snippet to check the main libraries:

```python
import pandas as pd
import numpy as np
import sklearn
import joblib
import boto3

print("Environment is ready")
```

## Required input

The dataset was uploaded to S3 using the Amazon S3 Console in section 5.3, for example:

```text
s3://<bucket-name>/raw/creditcard.csv
```

This path will be used as the input for the preprocessing and training step.
