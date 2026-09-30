# Day 18: Build a Basic ML Pipeline

## Goals
- Understand the estimator-transformer pipeline pattern in Spark ML.
- Prepare features and evaluate a model without leaking target information.

## Learn
Read the [MLlib guide](https://spark.apache.org/docs/latest/ml-guide.html) and [pipeline guide](https://spark.apache.org/docs/latest/ml-pipeline.html).

## Practice
1. Choose a small labeled dataset with numeric or categorical features.
2. Split it into training and test sets before fitting transformations.
3. Build a pipeline with feature preparation, an estimator, and an evaluator.
4. Report a metric on the held-out test set and note one limitation.

## Deliverable
A reproducible ML pipeline that fits, predicts, and reports a held-out evaluation metric.
