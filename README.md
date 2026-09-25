# Store Sales Prediction

## Overview

This project develops a machine learning model to predict daily retail store sales using historical sales data, store characteristics, promotions, holidays, calendar features, and competition-related information.

The project follows a forecasting-oriented workflow from exploratory analysis and feature engineering to chronological validation and final test prediction.

## Business Problem

Retail sales forecasting can support decisions related to inventory planning, staffing, promotions, and store operations.

The objective of this project is to predict daily sales for stores using information available before the sales outcome.

## Dataset

The project uses three datasets:

* `train.csv` — historical store sales and related information
* `test.csv` — observations for which sales must be predicted
* `store.csv` — store-level characteristics

The training data contains approximately 1 million observations across 1,115 stores.

## Exploratory Data Analysis

The analysis examined:

* Sales trends over time
* Day-of-week and monthly patterns
* Promotional effects
* State and school holidays
* Store types and assortment
* Competition distance
* Customer-sales relationship
* Sales outliers

The analysis found several strong historical associations, including higher average sales during promotional periods and a strong positive relationship between customer count and sales.

These relationships are interpreted as associations rather than causal effects.

## Feature Engineering

The final dataset includes engineered features such as:

* Year
* Month
* Day
* Week of Year
* Promo2 active status
* Competition age in months
* Competition missing-value indicators
* Competition distance missing-value indicator
* Encoded categorical store and promotion variables

## Validation Strategy

Because this is a forecasting problem, a chronological train-validation split was used.

* Training period: January 2013 – May 2015
* Validation period: June 2015 – July 2015

This prevents future observations from being used to train the model.

## Model

The final model is a:

**HistGradientBoostingRegressor**

with:

* `max_iter = 500`
* `learning_rate = 0.05`
* `max_leaf_nodes = 31`
* `l2_regularization = 1.0`
* `random_state = 42`

## Results

| Metric | Validation Result |
| ------ | ----------------: |
| MAE    |           1043.46 |
| RMSE   |           1466.13 |

The final model was trained using only features available in the test dataset.

Customer count was excluded from the final model because it is not available in the test data.

## Final Predictions

Predictions were generated for all **41,088** test observations.

Final prediction checks:

* Missing predictions: 0
* Minimum predicted sales: 0
* Maximum predicted sales: approximately 25,073.80
* Closed-store predicted sales: 0

The final predictions were saved as `submission.csv`.

## Project Structure

```text
store-sales-prediction/
│
├── store_sales_prediction.ipynb
├── README.md
├── submission.csv
└── .gitignore
```

## Key Learning

One important modeling lesson from this project was the importance of checking feature availability between training and test datasets.

A highly predictive training feature is not useful for final forecasting if the same feature is unavailable when making predictions.

## Limitations

* The validation period covers only June–July 2015.
* Historical associations should not be interpreted as causal relationships.
* Customer count was unavailable in the test dataset and therefore excluded from the final model.
* Performance on future unseen periods may differ from the historical validation results.
