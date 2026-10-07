# 🚗 Used Car Price Prediction

A machine learning project that predicts a used car's **selling price** from its brand, age, kilometres driven, fuel type, engine capacity and power. It covers data checks, exploratory analysis, preprocessing, and a comparison of four regression models plus one classification baseline.

**Best result so far:** a feedforward neural network reaches **R² = 0.944** on the held-out test set, with Random Forest close behind at **0.932**.

---

## 📌 Table of Contents

- [Dataset](#-dataset)
- [Workflow](#-workflow)
- [Preprocessing](#-preprocessing)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Models](#-models)
- [Results](#-results)
- [Known Issues](#️-known-issues)
- [Tech Stack](#️-tech-stack)
- [Getting Started](#-getting-started)
- [Repository Structure](#-repository-structure)
- [Future Work](#-future-work)
- [Author](#-author)

---

## 📂 Dataset

**15,411 used car listings**, 14 columns. The target is `selling_price`.

| Column              | Description                                    |
| ------------------- | ---------------------------------------------- |
| `car_name`          | Full name of the car                           |
| `brand`             | Manufacturer                                   |
| `model`             | Specific model                                 |
| `vehicle_age`       | Age of the car (years)                         |
| `km_driven`         | Total distance driven (km)                     |
| `seller_type`       | Dealer or Individual                           |
| `fuel_type`         | Petrol, Diesel or CNG                          |
| `transmission_type` | Manual or Automatic                            |
| `mileage`           | Fuel efficiency (km/l)                         |
| `engine`            | Engine capacity (cc)                           |
| `max_power`         | Maximum power output                           |
| `seats`             | Number of seats                                |
| `selling_price`     | **Target:** price at which the car was sold    |

---

## 🔄 Workflow

```
Load data → Duplicate & missing-value checks → EDA → Scaling → Encoding → 80/20 split → Train models → Compare R²
```

---

## 🧹 Preprocessing

| Step               | What was done                                                                 |
| ------------------ | ----------------------------------------------------------------------------- |
| **Duplicates**     | Checked: none found                                                           |
| **Missing values** | Checked: none found                                                           |
| **Outliers**       | Inspected the price distribution with a boxplot                               |
| **Scaling**        | `StandardScaler` on numeric columns                                           |
| **Encoding**       | One-hot encoding with `pd.get_dummies(drop_first=True)`                       |
| **Split**          | 80% train / 20% test, `random_state=42`                                       |

---

## 📊 Exploratory Data Analysis

- **Histogram:** distribution of selling prices.
- **Boxplot:** spread and outliers in price.
- **Scatter plot:** price against a numeric feature, coloured by fuel type.
- **Bar chart:** average selling price by brand.
- **Heatmap:** correlation between numeric features.

---

## 🤖 Models

| Model                              | Setup                                                                    |
| ---------------------------------- | ------------------------------------------------------------------------ |
| **Linear Regression**              | Baseline                                                                 |
| **Decision Tree Regressor**        | Default parameters                                                       |
| **Random Forest Regressor**        | Default parameters                                                       |
| **Feedforward Neural Network**     | Dense 64 → 32 → 1 (ReLU), Adam (lr 0.01), 50 epochs, batch size 32, 20% validation split |
| **Logistic Regression** (classification) | Predicts whether a car's price is above the median                 |

---

## 🏆 Results

Regression models are scored with **R²** on the test set.

| Model                                   | Test score                                 |
| --------------------------------------- | ------------------------------------------ |
| Feedforward Neural Network              | **R² = 0.944**                             |
| Random Forest                           | R² = 0.932                                 |
| Decision Tree                           | R² = 0.871                                 |
| Linear Regression                       | R² ≈ −1.6 × 10¹⁷ (failed, see Known Issues) |
| Logistic Regression (above/below median) | Accuracy = 0.918 (a classification task, not comparable to R²) |

**Takeaways**

- Tree-based models and the neural network all clear R² = 0.87, so the features carry strong signal for price.
- The neural network and Random Forest are within 0.012 R² of each other. With a single run and no cross-validation, this is too small a gap to call a winner.
- Random Forest is the more stable choice: the network's validation loss was noisy across epochs.

---

## ⚠️ Known Issues

These are being fixed in the notebook, and the results above will be updated afterwards:

- **Linear Regression fails** (R² of about −10¹⁷). The likely cause is collinear one-hot features, since `car_name` duplicates `brand` + `model`.
- **The `mileage` column is overwritten** by `max_power` values in the missing-value step, so the "mileage" used in the charts and models is actually max power.
- **Scaling is applied before the train/test split** and to every numeric column, including the target and the leftover index column `Unnamed: 0`. This leaks test-set statistics into training, and error metrics would not be in rupees.
- **One extreme `km_driven` value (3,800,000 km)** is not handled.
- Only R² is reported; MAE and RMSE are not yet calculated.

---

## 🛠️ Tech Stack

- **Python**
- **Pandas & NumPy:** data manipulation
- **Matplotlib & Seaborn:** visualisation
- **Scikit-learn:** preprocessing and models
- **TensorFlow / Keras:** neural network

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/Sanika881/Data-Science-and-Machine-Learning.git
cd Data-Science-and-Machine-Learning

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn tensorflow jupyter

# 3. Add the dataset (not stored in this repo) and update the file path in the
#    first cells. The notebook currently reads from a Google Colab path (/content/...).

# 4. Launch the notebook
jupyter notebook used_car_dataset.ipynb
```

---

## 📁 Repository Structure

```
Data-Science-and-Machine-Learning/
├── used_car_dataset.ipynb    # Checks, EDA, preprocessing, models, comparison
└── README.md
```

---

## 🔮 Future Work

- Fit the scaler on the training set only; leave the target unscaled.
- Report **MAE** and **RMSE** in rupees alongside R².
- Use **cross-validation** and hyperparameter tuning (`GridSearchCV`).
- Try a **log-transform** of the price, and gradient boosting (XGBoost / LightGBM).
- Add **feature importance** or SHAP plots.
- Deploy the best model as a small **Streamlit** app.

---

## 👩‍💻 Author

**Sanika Kadam**
[GitHub: @Sanika881](https://github.com/Sanika881) · [LinkedIn](https://www.linkedin.com/in/sanika-kadam007/)
