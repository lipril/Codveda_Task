# 🏠 House Price Prediction - Regression Modeling
> **Codveda Technologies - Data Science & Machine Learning Internship (Level 2, Task 1)**

![Python](https://img.shields.io/badge/Python-3.13-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.6-orange)
![Pandas](https://img.shields.io/badge/Pandas-2.0-green)
![License](https://img.shields.io/badge/License-MIT-purple)

## 📌 Project Overview
This project was completed as part of my 1-month internship at **Codveda Technologies**. The objective of Level 2 (Intermediate) Task 1 was to build and evaluate a regression model to predict a continuous variable, specifically **house prices**, based on various structural and locational features.

The project demonstrates the full machine learning lifecycle: from data ingestion and cleaning to feature encoding, model training, and evaluation using multiple performance metrics.

## 🎯 Objectives (as per Internship Requirements)
- [x] Split the dataset into training and testing sets.
- [x] Train a linear regression model using `scikit-learn`.
- [x] Evaluate the model using MSE, RMSE, MAE, and R-squared.
- [x] Experiment with feature scaling and understand its impact.
- [ ] *Next Steps:* Experiment with multiple models (Decision Trees, Random Forest) and compare performance. *(See Future Work section)*

## 📊 Dataset Description
The dataset (`HousePricePrediction.csv`) contains **2,919 records** with **13 initial features**. 
- **Target Variable:** `SalePrice` (Continuous)
- **Features:** `MSSubClass`, `MSZoning`, `LotArea`, `LotConfig`, `BldgType`, `OverallCond`, `YearBuilt`, `YearRemodAdd`, `Exterior1st`, `BsmtFinSF2`, `TotalBsmtSF`.
- **Data Quality:** Addressed missing values in `SalePrice`, `MSZoning`, `Exterior1st`, `BsmtFinSF2`, and `TotalBsmtSF`.

## 🛠️ Technologies Used
- **Language:** Python 3.13
- **Data Manipulation:** Pandas, NumPy
- **Machine Learning:** Scikit-learn (LinearRegression, StandardScaler, train_test_split)
- **Evaluation:** Scikit-learn Metrics (r2_score, mean_absolute_error, mean_squared_error, mean_absolute_percentage_error)

## 🔄 Methodology & Workflow

### 1. Data Preprocessing & Cleaning
- **Feature Dropping:** Removed `Id` as it provides no predictive value for price.
- **Missing Values:** Imputed missing `SalePrice` with the mean and dropped remaining rows with null values to ensure model integrity (resulting in 1,460 valid records).
- **Categorical Encoding:** Applied One-Hot Encoding (`pd.get_dummies`) to categorical columns (`MSZoning`, `LotConfig`, `BldgType`, `Exterior1st`) with `drop_first=True` to avoid the dummy variable trap (multicollinearity).

### 2. Model Building & Training
- **Data Splitting:** Split the data into 80% Training and 20% Testing sets (`random_state=0`).
- **Baseline Model:** Trained a standard `LinearRegression` model.
- **Feature Scaling:** Applied `StandardScaler` to standardize features and re-trained the model to observe any performance changes.

### 3. Evaluation Metrics
Model performance was evaluated using:
- **R² Score:** Proportion of variance explained.
- **MAE (Mean Absolute Error):** Average absolute difference between predicted and actual prices.
- **RMSE (Root Mean Squared Error):** Penalizes larger errors heavily.
- **MAPE (Mean Absolute Percentage Error):** Relative error percentage.

## 📈 Results

| Model | R² Score | MAE ($) | RMSE ($) | MAPE |
| :--- | :--- | :--- | :--- | :--- |
| **Linear Regression (Baseline)** | 0.3741 | 30,829.93 | 41,138.55 | 18.74% |
| **Linear Regression (Scaled)** | 0.3741 | 30,829.93 | 41,138.55 | 18.74% |

### 💡 Key Insights
1. **Model Performance:** The baseline Linear Regression model explains approximately **37.4%** of the variance in house prices. The average prediction error (MAE) is roughly $30,829.
2. **Feature Scaling Impact:** Applying `StandardScaler` did not change the performance of the Linear Regression model. This is expected behavior because ordinary least squares (OLS) regression is scale-invariant; it calculates coefficients based on the scale of the data.
3. **Limitations:** The relatively low R² score indicates that a linear model is insufficient to capture the complex, non-linear relationships present in housing data.

## 🚀 Future Work (Level 2 Continued)
To improve upon this baseline and fulfill the remaining internship objectives, the following steps are planned:
1. **Ensemble Methods:** Implement **Decision Trees**, **Random Forests**, and **Gradient Boosting (XGBoost/LightGBM)** to capture non-linear interactions.
2. **Hyperparameter Tuning:** Use `GridSearchCV` or `RandomizedSearchCV` to optimize tree depth, learning rate, and estimators.
3. **Advanced Feature Engineering:** Create polynomial features and interaction terms (e.g., `YearBuilt` * `OverallCond`).
4. **Regularization:** Implement Ridge and Lasso regression to handle potential multicollinearity better.
---
## 🤝 Contributing

Contributions, issues, and feature requests are welcome!  
Feel free to check 

---

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---

## 👥 Author

**Your Name**  
- GitHub: [@lipril](https://github.com/lipril)  
- LinkedIn: [LinkedIn](https://www.linkedin.com/in/liprilomar/)

---

**⭐ If you find this project useful, please consider giving it a star!**
## 📂 Repository Structure
```text
├── HousePricePrediction.csv      # Raw dataset
├── house_price_predictor.ipynb   # Jupyter Notebook with full analysis
├── README.md                     # Project documentation
└── requirements.txt              # Dependencies (optional)