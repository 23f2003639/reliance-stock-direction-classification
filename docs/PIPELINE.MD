# RELIANCE Stock Direction Classification — ML Pipeline

## 1. Pipeline Objective

The objective of this project is to build a supervised machine learning pipeline that predicts the **direction of RELIANCE Industries' next trading-day closing price**.

The prediction problem is formulated as binary classification:

```text
UP   → 1
DOWN → 0
```

The pipeline then compares multiple classification algorithms using the same prepared dataset and evaluation approach.

---

# 2. End-to-End Pipeline

```text
┌──────────────────────────────┐
│ Historical RELIANCE Data     │
│ Open, High, Low, Close, Vol. │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Data Collection              │
│ yfinance                     │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Data Cleaning / Preparation   │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Feature Preparation           │
│ Market / OHLCV features       │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Target Construction           │
│ Next-Day Direction             │
│ 1 = UP, 0 = DOWN              │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Train / Test Split            │
└──────────────┬───────────────┘
               ↓
       ┌───────┴────────┐
       ↓                ↓
┌──────────────┐  ┌──────────────┐
│ Model Train  │  │ Model Train  │
│ 7 Algorithms │  │ + Prediction │
└──────┬───────┘  └──────┬───────┘
       └────────┬─────────┘
                ↓
┌──────────────────────────────┐
│ Accuracy Evaluation           │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ Model Comparison              │
└──────────────────────────────┘
```

---

# 3. Stage 1 — Data Collection

Historical RELIANCE stock data is obtained using the `yfinance` library.

The dataset contains standard market variables:

- Open
- High
- Low
- Close
- Volume

These variables describe the daily trading activity of the stock.

---

# 4. Stage 2 — Data Preparation

The collected data is inspected and prepared for machine learning.

Typical preparation includes:

- Handling missing values
- Ensuring chronological ordering
- Selecting relevant columns
- Preparing the feature matrix
- Preparing the target variable

Because the data represents a time series, maintaining chronological order is important.

---

# 5. Stage 3 — Feature Preparation

The initial model setup uses historical market information available in the dataset.

The feature matrix is represented as:

```text
X = input features
```

and the target is represented as:

```text
y = next-day price direction
```

The important principle is that features should represent information available at prediction time.

---

# 6. Stage 4 — Target Construction

The target is created from the relationship between the current closing price and the next trading day's closing price.

Conceptually:

```text
If Next Day Close > Current Close:
        Target = 1  (UP)
else:
        Target = 0  (DOWN)
```

This converts the original stock-price time series into a binary classification problem.

For example:

| Current Close | Next Close | Target |
|---:|---:|---|
| 1400 | 1420 | 1 |
| 1420 | 1410 | 0 |
| 1410 | 1435 | 1 |

The final observation cannot be used for target construction because there is no following trading day available.

---

# 7. Stage 5 — Train/Test Split

The prepared dataset is divided into training and testing portions.

```text
Historical Data
       ↓
┌───────────────────┬──────────────────┐
│ Training Data     │ Testing Data     │
│ Model learns from │ Final evaluation │
└───────────────────┴──────────────────┘
```

For financial time-series problems, chronological splitting is generally preferable to randomly shuffling observations because future observations should not influence training on past observations.

---

# 8. Stage 6 — Model Training

Seven classification algorithms are trained.

### Logistic Regression

A linear probabilistic classifier used as a simple baseline.

### K-Nearest Neighbors

Classifies observations based on the labels of nearby training observations.

### Decision Tree

Learns a sequence of decision rules from the input features.

### Random Forest

Combines multiple decision trees to create an ensemble classifier.

### Support Vector Machine

Attempts to find a decision boundary that separates the classes with a large margin.

### Naive Bayes

Uses probabilistic assumptions about the relationship between features and classes.

### XGBoost

A gradient-boosting ensemble method that builds trees sequentially to improve predictions.

---

# 9. Stage 7 — Prediction

After training, each model predicts the class of unseen test observations.

The output is:

```text
1 → Predicted UP
0 → Predicted DOWN
```

These predictions are compared with the actual test-set labels.

---

# 10. Stage 8 — Evaluation

The primary evaluation metric used in this project is **classification accuracy**.

```text
Accuracy =
Correct Predictions / Total Predictions
```

Accuracy is expressed as a percentage.

The same evaluation approach is applied to all seven models to make the comparison consistent.

---

# 11. Stage 9 — Model Comparison

The observed results are:

| Model | Accuracy |
|---|---:|
| Naive Bayes | **53.21%** |
| KNN | 50.15% |
| Logistic Regression | 49.54% |
| XGBoost | 49.54% |
| SVM | 49.54% |
| Random Forest | 48.93% |
| Decision Tree | 46.48% |

The results are visualized using a model accuracy comparison chart.

---

# 12. Interpretation

Naive Bayes achieved the highest observed accuracy at:

```text
53.21%
```

However, this does **not** mean that Naive Bayes is a reliable trading strategy.

The results are relatively close to 50%, which indicates that the selected features and models have limited predictive power for next-day direction in this experiment.

This is an important machine learning finding rather than a failure of the project.

Financial markets are affected by many factors that are not captured by basic historical price and volume information.

---

# 13. Important ML Considerations

## Data Leakage

Features used to predict a particular trading day must not contain information that would only become available after that prediction point.

## Time-Series Ordering

Financial observations are ordered in time. Randomly mixing past and future observations can produce overly optimistic evaluation results.

## Non-Stationarity

Relationships in financial markets can change over time. A model that performs well during one period may not perform similarly in another period.

## Accuracy Limitations

Accuracy alone does not determine whether a model would produce a profitable trading strategy.

Transaction costs, slippage, risk, position sizing, and drawdowns would need to be considered in a real trading system.

---

# 14. Current Project Scope

The current project focuses on:

```text
Historical Market Data
        ↓
Binary Direction Classification
        ↓
Multiple ML Models
        ↓
Accuracy Comparison
```

It does **not** attempt to build a live trading system or provide investment recommendations.

---

# 15. Future Pipeline

A future version could extend the pipeline to:

```text
Historical Data
      ↓
Feature Engineering
      ↓
Technical Indicators
      ↓
Lagged Returns
      ↓
Volatility Features
      ↓
Time-Series Validation
      ↓
Hyperparameter Tuning
      ↓
Model Comparison
      ↓
Walk-Forward Evaluation
      ↓
Trading Strategy Backtest
      ↓
Risk / Return Analysis
```

Possible additional evaluation metrics:

- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion Matrix
- Sharpe Ratio
- Maximum Drawdown
- Cumulative Return

---

## Final Note

The purpose of this pipeline is to demonstrate a complete machine learning workflow on a real financial dataset:

**data → preprocessing → target construction → training → prediction → evaluation → comparison.**
