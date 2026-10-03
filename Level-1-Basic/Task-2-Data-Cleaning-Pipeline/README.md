# Data Cleaning & Preprocessing Pipeline: Yahoo Screener Dataset
### Codveda Technologies - Data Science Internship (Level 1, Task 2)

![Python](https://img.shields.io/badge/Python-3.13-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458.svg)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-F7931E.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)

## 📌 Project Overview
During my 1-month Data Science Internship at **Codveda Technologies**, I was tasked with completing **Level 1 (Basic) - Task 2: Data Cleaning and Preprocessing**. 

The objective was to take a raw, messy financial dataset (Yahoo Screener) and transform it into a pristine, machine-learning-ready dataset. Raw financial data often contains high dimensionality, redundant metadata, missing values, and extreme outliers. This project demonstrates a robust, production-ready preprocessing pipeline built to handle these real-world data challenges.

## 🎯 Objectives & Requirements
As outlined by the internship requirements, this project focuses on:
- **Handling missing data** via intelligent imputation and column/row removal.
- **Detecting and removing outliers** using statistical methods.
- **Converting categorical variables** into numerical formats (One-Hot Encoding and Label Encoding).
- **Normalizing and standardizing** numerical data for ML algorithms.
- **Tools:** Python, pandas, scikit-learn.

## 📊 Dataset
- **Source:** Yahoo Screener API (Financial data)
- **Initial Shape:** 400 rows × 168 columns
- **Key Features:** Market Cap, PE Ratios, EPS, Dividend Yields, Analyst Ratings, Pre-market data, and technical averages.

## ⚙️ Methodology & Pipeline

### 1. Data Cleaning & Dimensionality Reduction
- **Removed Redundant Columns:** Dropped 74 formatted (`.fmt`) and `.longFmt` mirror columns to retain only the numerical `.raw` equivalents, significantly reducing dimensionality.
- **Removed Constant Columns:** Identified and dropped 15 columns with zero variance (constant values).
- **Removed Metadata:** Dropped 28 metadata columns (e.g., `quoteSourceName`, `language`, `exchangeTimezoneName`, `marketState`) that provide no analytical value for predictive modeling.
- **Missing Data Handling:** 
  - Dropped rows missing the essential identifier (`symbol`).
  - Dropped columns with >60% missing values.
  - Imputed remaining missing numerical values using the **median** strategy.
  - Imputed categorical missing values with an "unknown" constant.

### 2. Feature Engineering
- **Analyst Rating Extraction:** The raw `averageAnalystRating` column (e.g., "1.6 - Buy") was parsed into two distinct features: `analyst_score` (float) and `analyst_label` (categorical). 
- **Type Coercion:** Automatically detected and converted boolean-like strings ("true"/"false") to actual boolean types. Forced all `.raw` columns to numeric dtypes, coercing errors to `NaN`.

### 3. Outlier Detection & Treatment
Instead of blindly dropping rows with extreme values (which is dangerous with financial data where market caps can vary wildly), I applied **Winsorization**. 
- Key numeric columns (`marketCap`, `regularMarketPrice`, `regularMarketVolume`, `regularMarketChangePercent`) were clipped at the **1st and 99th percentiles**. 
- This retained all 400 rows while minimizing the influence of extreme outliers.

### 4. Categorical Encoding (Dual Strategy)
To support different types of downstream machine learning models, two versions of the dataset were generated:
- **One-Hot Encoding (OHE):** Used for nominal categorical features (`financialCurrency`, `analyst_label`, etc.) to prevent ordinality assumptions, producing the primary processed matrix.
- **Label Encoding:** Created a separate dataset where categorical variables are mapped to integers (useful for tree-based models like XGBoost or Random Forest).

### 5. Feature Scaling
- Applied `StandardScaler` to all 59 numerical features. 
- This ensures a mean of 0 and a standard deviation of 1, which is crucial for distance-based algorithms (e.g., KNN, SVM) and gradient descent optimization.

## 📁 Repository Structure & Outputs
The notebook exports three distinct datasets to preserve the different stages of processing:

| File Name | Description | Shape |
| :--- | :--- | :--- |
| `yahoo_screener_clean.csv` | The dataset after dropping columns and parsing dates/analyst ratings, but *before* scaling and encoding. | 400 x 65 |
| `yahoo_screener_label_encoded.csv` | Clean dataset with categorical variables converted to integer labels. Great for tree-based models. | 400 x 65 |
| `yahoo_screener_processed.csv` | The fully processed matrix. Numeric features standardized, categorical features One-Hot Encoded. **Ready for ML.** | 400 x 119 |

## 🚀 Why This Project Stands Out
- **Production-Ready Code:** The use of Scikit-Learn `Pipeline` and `ColumnTransformer` ensures that the exact same preprocessing steps can be applied to new incoming data without data leakage.
- **Thoughtful Outlier Handling:** Opting for Winsorization over simple row-dropping shows an understanding of data preservation in niche financial datasets.
- **Dual-Encoding Approach:** Providing both Label Encoded and One-Hot Encoded outputs demonstrates an understanding of how different machine learning algorithms require different data formats.
- **Robust Error Handling:** Utilized regex extraction, type coercion, and dynamic missing-value thresholds to ensure the pipeline doesn't break on unseen data.

## 💻 How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/Codveda-Level1-Task2.git


----
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

## 🙏 Acknowledgments

- Dataset source:https://www.kaggle.com/datasets/saurabh00007/iriscsv  

---

**⭐ If you find this project useful, please consider giving it a star!**