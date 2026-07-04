---
title : "Train the model and save artifacts"
date : 2026-04-19
weight : 2
chapter : false
pre : " <b> 5.4.2 </b> "
---

After the Python environment is ready, the next step is to read the dataset from S3, process the data, and train the Random Forest model.

## Main processing flow

1. Read the `creditcard.csv` file from S3.
2. Check the input data.
3. Separate features and labels.
4. Split the data into train/test sets.
5. Standardize the data if needed.
6. Train the Random Forest model.
7. Evaluate the model results.
8. Save the model and scaler using `joblib`.

## Artifacts to create

After the training step, the following files must be created:

```text
model.joblib
scaler.joblib
```

Where:

- `model.joblib`: the trained Random Forest model.
- `scaler.joblib`: the scaler used to ensure realtime data is standardized in the same way as during training.

![Random Forest training and evaluation results](/images/5-Workshop/5.4-S3-onprem/evaluate.jpg)

{{% notice warning %}}
Ensure that the feature mapping used during training is consistent with the feature mapping in the realtime Lambda. If the order or meaning of features differs, the model may make incorrect predictions.
{{% /notice %}}
