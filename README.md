# 🚗 Used Car Price Prediction

A machine learning project that explores the used car market and predicts a car's **selling price** from details such as brand, age, kilometres driven, fuel type, engine capacity and power. It covers the full workflow: data cleaning, exploratory analysis, feature engineering, and training and comparing four regression models.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Workflow](#-project-workflow)
- [Data Preprocessing](#-data-preprocessing)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Models](#-models)
- [Model Evaluation](#-model-evaluation)
- [Insights & Findings](#-insights--findings)
- [Tech Stack](#️-tech-stack)
- [Getting Started](#-getting-started)
- [Repository Structure](#-repository-structure)
- [Limitations & Future Work](#-limitations--future-work)
- [Author](#-author)

---

## 📖 Overview

Buying or selling a used car is hard because prices depend on many factors at once. This project:

1. Cleans and prepares a used car listings dataset.
2. Explores the trends that drive price (age, mileage, brand, seller type, fuel type).
3. Trains and compares **Linear Regression, Decision Tree, Random Forest and a TensorFlow neural network** to predict `selling_price`.

---

## 📂 Dataset

| Column | Description |
|---|---|
| `car_name` | Full name of the car |
| `brand` | Manufacturer |
| `model` | Specific model |
| `vehicle_age` | Age of the car (years) |
| `km_driven` | Total distance driven (km) |
| `seller_type` | Dealer or Individual |
| `fuel_type` | Petrol, Diesel or CNG |
| `transmission_type` | Manual or Automatic |
| `mileage` | Fuel efficiency (km/l) |
| `engine` | Engine capacity (cc) |
| `max_power` | Maximum power output |
| `selling_price` | **Target variable**: price at which the car was sold |

---

## 🔄 Project Workflow

```
Raw data → Cleaning → EDA → Encoding & scaling → Train/test split → Model training → Evaluation → Insights
```

---

## 🧹 Data Preprocessing

| Step | What was done |
|---|---|
| **Duplicates** | Identified and removed duplicate rows |
| **Missing values** | Filled missing `mileage` values with the column mean |
| **Outliers** | Inspected the price distribution with boxplots |
| **Encoding** | Converted categorical features (brand, seller type, fuel type, transmission) to numeric form |
| **Scaling** | Standardised numerical features with `StandardScaler()` |

> **Tip:** fit the scaler (and any imputer) on the **training set only**, then apply it to the test set, to avoid data leakage. Scaling matters for Linear Regression and the neural network; tree-based models don't need it.

---

## 📊 Exploratory Data Analysis

- **Histogram:** distribution of selling prices.
- **Boxplot:** spread and outliers in price.
- **Scatter plot:** mileage vs. selling price.
- **Bar chart:** average selling price by brand.
- **Heatmap:** correlation between numerical features.

---

## 🤖 Models

| Model | Why it was used |
|---|---|
| **Linear Regression** | Simple, interpretable baseline for numerical relationships |
| **Decision Tree Regressor** | Captures non-linear relationships and feature interactions |
| **Random Forest Regressor** | Ensemble of trees; usually more accurate and less prone to overfitting |
| **Neural Network (TensorFlow/Keras)** | Learns complex patterns through multiple dense layers |

---

## 🏆 Model Evaluation

Regression models are evaluated with:

- **R² Score:** how much of the variance in price the model explains.
- **MAE** (Mean Absolute Error): average error in price units.
- **RMSE** (Root Mean Squared Error): error that penalises large misses more heavily.

> Classification "accuracy" doesn't apply to a continuous target like price, so R², MAE and RMSE are used instead.

**Results** *(fill in from your notebook)*

| Model | R² (Train) | R² (Test) | MAE | RMSE |
|---|---|---|---|---|
| Linear Regression | – | – | – | – |
| Decision Tree | – | – | – | – |
| Random Forest | – | – | – | – |
| Neural Network | – | – | – | – |

---

## 💡 Insights & Findings

- **Vehicle age and kilometres driven** have a strong effect on price: older, higher-mileage cars sell for less.
- **Dealer-listed cars** tend to be priced higher than those sold by individuals.
- **Luxury brands** such as BMW and Mercedes command noticeably higher prices.
- **Diesel cars** often hold their resale value better than petrol cars.

---

## 🛠️ Tech Stack

- **Python**
- **Pandas & NumPy:** data manipulation
- **Matplotlib & Seaborn:** visualisation
- **Scikit-learn:** preprocessing and ML models
- **TensorFlow / Keras:** neural network

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/Sanika881/used-car-price-prediction.git
cd used-car-price-prediction

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow jupyter

# 3. Launch the notebook
jupyter notebook Used_Car_Price_Prediction.ipynb
```

---

## 📁 Repository Structure

```
used-car-price-prediction/
├── data/
│   └── used_cars.csv
├── notebooks/
│   └── Used_Car_Price_Prediction.ipynb
├── images/                  # EDA and results charts
├── requirements.txt
└── README.md
```

> Adjust repository name, file names and paths to match your project.

---

## 🔮 Limitations & Future Work

- Compare models with **cross-validation** and tune hyperparameters (`GridSearchCV` / `RandomizedSearchCV`).
- Try **log-transforming** `selling_price` to handle its skew.
- Add **feature importance** (Random Forest) or SHAP plots to explain predictions.
- Try gradient boosting models such as **XGBoost** or **LightGBM**.
- Deploy the best model as a small **Streamlit** or **Flask** app.

---

## 👩‍💻 Author

**Sanika**
GitHub: [@Sanika881](https://github.com/Sanika881)
