# Network Intrusion Detection System

A binary classification system that distinguishes benign network traffic from DoS attacks using the [CIC-IDS2017 dataset](https://www.unb.ca/cic/datasets/ids-2017.html).

**Authors:** Denise Godinez, Jack Mulvihill, Fareen Samad

---

## Overview

This project implements a full ETL pipeline and trains five machine learning classifiers to detect Denial-of-Service (DoS) attacks in network traffic data. The dataset spans 12 files across CSV, JSON, and Parquet formats with 79 network flow features per record.

**Attack types classified:** DoS Hulk, DoS GoldenEye, DoS Slowhttptest vs. BENIGN

---

## Pipeline

**Extract** — Ingests all CSV, JSON, and Parquet source files into a single Pandas DataFrame using Glob.

**Transform** — Standardizes column names, removes duplicates, coerces all features to numeric types, and drops NaN rows and columns.

**Load** — Persists the cleaned dataset to `transformed_data.csv` for downstream modeling.

---

## Classifiers

| Model | Notes |
|---|---|
| Perceptron | Linear baseline |
| Logistic Regression | Linear probabilistic classifier |
| XGBoost | Gradient boosting, 150 estimators |
| Decision Tree | Max depth 10 to prevent overfitting |
| Random Forest | 100 trees, max depth 10 |

Each model is evaluated on accuracy, precision, recall, and F1-score. Recall is prioritized given the cost of missed attack detection (false negatives).

---

## Results

XGBoost and Random Forest achieved the highest performance across all metrics, confirming that ensemble methods are well-suited for this task. Logistic Regression performed competitively despite its linear nature. The Perceptron achieved the lowest performance, likely due to sensitivity to class imbalance in the dataset.
