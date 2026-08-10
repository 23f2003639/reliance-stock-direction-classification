# RELIANCE Stock Direction Classification

A machine learning classification project that predicts the **next-day direction of RELIANCE Industries stock** using historical market data and compares multiple classification algorithms.

> **Project type:** Supervised Machine Learning — Binary Classification  
> **Asset:** RELIANCE Industries (NSE)  
> **Primary task:** Predict whether the next trading day's closing price will move **UP or DOWN**

---

## 📌 Project Overview

Stock-price direction prediction is a challenging machine learning problem because financial markets contain substantial noise, non-stationarity, and uncertainty.

This project builds a reproducible classification pipeline using historical RELIANCE stock data and evaluates seven machine learning models:

- Logistic Regression
- K-Nearest Neighbors (KNN)
- Decision Tree
- Random Forest
- Support Vector Machine (SVM)
- Naive Bayes
- XGBoost

The goal is not to claim reliable investment predictions, but to **compare the behavior and performance of different classification algorithms on a financial time-series problem**.

---

## 🔄 Machine Learning Pipeline

```text
Historical RELIANCE Stock Data
            ↓
      Data Collection
            ↓
       Data Cleaning
            ↓
   Feature Preparation
            ↓
   Target Construction
     (Next-Day Direction)
            ↓
     Train/Test Split
            ↓
     Model Training
            ↓
    Model Prediction
            ↓
      Model Evaluation
            ↓
 Model Accuracy Comparison
```

For a detailed explanation of each stage, see [`docs/PIPELINE.md`](docs/PIPELINE.md).

---

## 📊 Dataset

Historical market data is collected using `yfinance`.

The dataset contains standard OHLCV variables:

| Feature | Description |
|---|---|
| Open | Opening price |
| High | Highest price during the session |
| Low | Lowest price during the session |
| Close | Closing price |
| Volume | Trading volume |

The notebook performs the required preprocessing and feature/target preparation before model training.

---

## 🎯 Target Variable

The problem is formulated as binary classification.

The target represents the direction of the **next trading day's closing price**:

```text
1 → UP
0 → DOWN
```

Conceptually:

```text
Next Day Close > Current Day Close → UP
Next Day Close ≤ Current Day Close → DOWN
```

This makes the task a directional prediction problem rather than an exact price prediction problem.

---

## 🤖 Models Compared

| Model | Type |
|---|---|
| Logistic Regression | Linear classifier |
| KNN | Distance-based classifier |
| Decision Tree | Tree-based classifier |
| Random Forest | Ensemble tree model |
| SVM | Margin-based classifier |
| Naive Bayes | Probabilistic classifier |
| XGBoost | Gradient boosting ensemble |

---

## 📈 Results

| Model | Accuracy |
|---|---:|
| Naive Bayes | **53.21%** |
| KNN | 50.15% |
| Logistic Regression | 49.54% |
| XGBoost | 49.54% |
| SVM | 49.54% |
| Random Forest | 48.93% |
| Decision Tree | 46.48% |

### Best Performing Model

**Naive Bayes — 53.21% accuracy**

The results show that the models perform relatively close to the 50% level. This highlights how difficult short-term stock-direction prediction can be when using relatively basic market features.

The project intentionally reports the observed results rather than optimizing the workflow solely to maximize accuracy.

---

## 📉 Model Comparison

The notebook includes a visualization comparing the classification accuracy of all seven models.

This makes it easier to identify the strongest and weakest performers on the selected dataset and feature set.

---

## 🛠️ Tech Stack

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- XGBoost
- yfinance
- Google Colab
- Jupyter Notebook

---

## 📁 Repository Structure

```text
reliance-stock-direction-classification/
│
├── docs/
│   └── PIPELINE.md
│
├── reliance_stock_direction_classification.ipynb
│
└── README.md
```

---

## 🚀 How to Run

#### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/reliance-stock-direction-classification.git
cd reliance-stock-direction-classification
```

#### 2. Install dependencies

```bash
pip install pandas numpy matplotlib scikit-learn xgboost yfinance
```

#### 3. Open the notebook

Open:

```text
reliance_stock_direction_classification.ipynb
```

The notebook can be run using Jupyter Notebook, JupyterLab, or Google Colab.

---

## Author

<div align="center">

[![Sridevi S](https://img.shields.io/badge/Sridevi%20S-111111?style=for-the-badge&logo=github&logoColor=white)](https://github.com/23f2003639)

</div>
