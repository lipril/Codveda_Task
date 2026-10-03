# 🌟 Codveda Technologies Data Science Internship Portfolio

<div align="center">

![Python](https://img.shields.io/badge/Python-3.13-blue?style=for-the-badge&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-150458?style=for-the-badge&logo=pandas)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.6-F7931E?style=for-the-badge&logo=scikit-learn)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

### 🎓 A Comprehensive Data Science & Machine Learning Portfolio

*Completed during a 1-Month Intensive Internship at Codveda Technologies*

[Projects](#-project-showcase) • [Tech Stack](#-technical-stack) • [Skills Acquired](#-skills--competencies) • [Contact](#-connect-with-me)

</div>

---

## 📖 Executive Summary

This repository serves as a **comprehensive portfolio** of the data science and machine learning projects I completed during my intensive 1-month internship at **Codveda Technologies**. The internship was structured across three progressive levels—**Basic (Level 1)**, **Intermediate (Level 2)**, and **Advanced (Level 3)** —each designed to build upon foundational skills while tackling increasingly complex, real-world data challenges.

Rather than treating these as isolated academic exercises, I approached each project with a **production-first mindset**: writing robust, error-resistant code; documenting my reasoning; and critically evaluating both the strengths and limitations of every solution. The result is a collection of six end-to-end projects that demonstrate proficiency across the full data science lifecycle—from raw data acquisition to model deployment.

---

## 🎯 Internship Objectives & Philosophy

The Codveda Technologies internship program was designed to bridge the gap between theoretical knowledge and practical, industry-relevant application. The core philosophy was simple:

> **"Don't just run the code—understand why it works, when it fails, and how to make it better."**

This philosophy is reflected in every notebook and script within this repository. Each project includes:
- **Thorough documentation** explaining methodology, not just implementation.
- **Critical analysis** of results, including honest assessments of limitations.
- **Production-ready patterns** such as modular pipelines, error handling, and reusable functions.
- **Ethical considerations** regarding data usage, scraping practices, and model deployment.

---

## 📂 Project Showcase

The six projects below are organized by difficulty level, reflecting the progressive nature of the internship curriculum. Each project is fully self-contained with its own detailed README, notebook, and exported datasets.

---

### 🟢 Level 1: Foundation (Basic)

These projects established the foundational skills in web scraping, data acquisition, and preprocessing—the essential first steps of any data science pipeline.

---

#### 📈 Project 1.1: Yahoo Finance Screener Scraper

**🎯 Objective:** Build a robust web scraping pipeline to collect real-time financial data from Yahoo Finance's "Most Actives" screener.

**🔥 Technical Highlights:**
- **Advanced Anti-Bot Bypass:** Implemented `curl_cffi` with Chrome 120 TLS fingerprint impersonation to circumvent Yahoo's sophisticated bot detection—a technique that goes far beyond standard `requests` usage.
- **API Reverse-Engineering:** Successfully extracted Yahoo's dynamic `crumb` authentication token and managed session cookies to authenticate with internal JSON APIs (`query1.finance.yahoo.com`).
- **Resilient Schema Handling:** Built fallback logic to automatically detect and adapt to API schema changes (e.g., `records` → `quotes`), ensuring the scraper remains functional despite Yahoo's frequent updates.
- **Pagination Management:** Implemented offset-based pagination to extract all 382+ available records with respectful rate-limiting delays.

**🛠️ Technologies:** `curl_cffi`, `BeautifulSoup4`, `pandas`, `JSON`

**📁 Deliverables:**
| File | Description | Shape |
|:---|:---|:---|
| `yahoo_screener_full.csv` | Raw flattened output with all metadata | 400 × 168 |
| `yahoo_screener_curated.csv` | Cleaned minimal output for analysis | 400 × 3 |

**💡 Key Insight:** By targeting the underlying API instead of rendering JavaScript, this approach achieved a **10x speed improvement** over Selenium-based scrapers while being significantly more reliable.

---

#### 🧹 Project 1.2: Data Cleaning & Preprocessing Pipeline

**🎯 Objective:** Transform raw, messy financial data into a pristine, machine-learning-ready dataset using a production-grade preprocessing pipeline.

**🔥 Technical Highlights:**
- **Intelligent Dimensionality Reduction:** Systematically removed 74 redundant `.fmt` mirror columns, 15 constant-variance columns, and 28 metadata columns—reducing the feature space from 168 to 65 meaningful features.
- **Winsorization for Outlier Treatment:** Instead of blindly dropping rows (dangerous in financial data where market caps vary by orders of magnitude), applied 1st/99th percentile clipping to retain all 400 records while minimizing extreme value influence.
- **Dual Encoding Strategy:** Generated both One-Hot Encoded (for linear models) and Label Encoded (for tree-based models) versions, demonstrating understanding of algorithm-specific data requirements.
- **Scikit-Learn Pipeline Architecture:** Implemented `Pipeline` and `ColumnTransformer` to ensure reproducible, leakage-free preprocessing that can be applied to new data.

**🛠️ Technologies:** `pandas`, `scikit-learn`, `numpy`, regex

**📁 Deliverables:**
| File | Description | Shape |
|:---|:---|:---|
| `yahoo_screener_clean.csv` | Post-cleaning, pre-encoding | 400 × 65 |
| `yahoo_screener_label_encoded.csv` | Integer-encoded categoricals | 400 × 65 |
| `yahoo_screener_processed.csv` | Fully processed ML-ready matrix | 400 × 119 |

**💡 Key Insight:** Financial data requires nuanced outlier handling. Winsorization preserves the "long tail" of legitimate high-value companies while preventing extreme outliers from skewing model training.

---

### 🟡 Level 2: Intermediate (Applied Machine Learning)

These projects applied machine learning algorithms to real-world prediction and classification problems, introducing model evaluation, feature engineering, and comparative analysis.

---

#### 🏠 Project 2.1: House Price Prediction — Regression Modeling

**🎯 Objective:** Build and evaluate a regression model to predict continuous house prices based on structural and locational features.

**🔥 Technical Highlights:**
- **Complete ML Lifecycle:** Executed the full workflow from data ingestion and cleaning to feature encoding, model training, and multi-metric evaluation.
- **Categorical Encoding:** Applied One-Hot Encoding with `drop_first=True` to avoid the dummy variable trap (multicollinearity) in linear regression.
- **Comprehensive Evaluation:** Assessed model performance using R², MAE, RMSE, and MAPE—providing a holistic view of prediction accuracy.
- **Feature Scaling Experimentation:** Demonstrated that StandardScaler does not change OLS regression performance (scale-invariant), reinforcing theoretical understanding.

**🛠️ Technologies:** `scikit-learn` (LinearRegression, StandardScaler), `pandas`, `numpy`

**📊 Results:**
| Model | R² Score | MAE ($) | RMSE ($) | MAPE |
|:---|:---:|:---:|:---:|:---:|
| Linear Regression (Baseline) | 0.3741 | 30,829.93 | 41,138.55 | 18.74% |
| Linear Regression (Scaled) | 0.3741 | 30,829.93 | 41,138.55 | 18.74% |

**💡 Key Insight:** The relatively low R² (37.4%) indicates that linear models are insufficient for capturing the complex, non-linear relationships in housing data. This motivates the use of ensemble methods and tree-based models—a natural next step explored in future work.

---

#### 🌸 Project 2.2: Iris Flower Classification — Comparative ML Approach

**🎯 Objective:** Master supervised classification fundamentals by building and comparing three different classification algorithms on the classic Iris dataset.

**🔥 Technical Highlights:**
- **Multi-Model Comparative Framework:** Trained and evaluated Logistic Regression (parametric), K-Nearest Neighbors (non-parametric), and Gaussian Naive Bayes (probabilistic)—providing insights into how different algorithms make decisions.
- **Exploratory Data Analysis First:** Used `seaborn.pairplot` to visualize feature distributions and correlations *before* modeling, revealing why Setosa is easily separable while Versicolor and Virginica overlap.
- **Critical Evaluation:** Went beyond accuracy scores to analyze confusion matrices, identifying *where* models fail (Versicolor ↔ Virginica boundary) and *why*.
- **Feature Scaling Importance:** Demonstrated that StandardScaler is mandatory for distance-based algorithms like KNN, as unscaled features (Sepal Length ~5.0 vs. Petal Width ~0.2) would bias Euclidean distance calculations.

**🛠️ Technologies:** `scikit-learn`, `pandas`, `seaborn`, `matplotlib`

**📊 Model Comparison:**
| Model | Type | Strengths | Weaknesses |
|:---|:---|:---|:---|
| Logistic Regression | Parametric (Linear) | Fast, interpretable, works well for linearly separable data | Struggles with non-linear boundaries |
| KNN (k=5) | Non-Parametric | Captures local patterns, no training phase | Sensitive to feature scaling and dimensionality |
| Gaussian Naive Bayes | Probabilistic | Extremely fast, works well with small data | Assumes feature independence (often violated) |

**💡 Key Insight:** No single model is universally superior. The "best" model depends on the data's characteristics—linearity, dimensionality, and the importance of interpretability vs. raw performance.

---

### 🔴 Level 3: Advanced (Specialized Domains)

These projects tackled specialized domains—time series forecasting and natural language processing—requiring advanced statistical modeling and feature engineering techniques.

---

#### 📈 Project 3.1: Time Series Analysis & Forecasting — Apple Inc. (AAPL) Stock Prices

**🎯 Objective:** Analyze historical stock price data, decompose its components, apply smoothing techniques, and build ARIMA/SARIMA models for forecasting.

**🔥 Technical Highlights:**
- **Comprehensive Time Series Decomposition:** Used `seasonal_decompose` to break the series into trend, seasonality, and residual components—revealing that trend dominates stock price behavior.
- **Stationarity Testing:** Applied the Augmented Dickey-Fuller (ADF) test to confirm non-stationarity (p=0.7896), then achieved stationarity through first-order differencing (p=0.0000).
- **Multi-Model Forecasting:** Trained and compared five models: SES, Holt's Linear, Holt-Winters, ARIMA, and SARIMA.
- **Rigorous Evaluation:** Used MSE, RMSE, MAE, and MAPE to assess a 60-day forecasting horizon on held-out test data.

**🛠️ Technologies:** `statsmodels`, `yfinance`, `pandas`, `matplotlib`

**📊 Model Performance (60-Day Forecast):**
| Model | RMSE | MAE | MAPE |
|:---|:---:|:---:|:---:|
| **🏆 Holt's Linear Trend** | **10.79** | **9.62** | **3.55%** |
| SARIMA | 10.85 | 9.66 | 3.57% |
| Holt-Winters | 12.67 | 11.27 | 4.15% |
| ARIMA(0, 1, 0) | 14.69 | 13.24 | 4.87% |
| SES | 14.69 | 13.24 | 4.87% |

**💡 Key Insight:** Simpler models often outperform complex ones in short-term stock forecasting. Holt's Linear Trend achieved an impressive **3.55% MAPE**, proving that overfitting to noise (residuals) can hurt predictive performance.

---

#### 📩 Project 3.2: Advanced NLP — SMS Spam Classification Pipeline

**🎯 Objective:** Build a production-ready NLP pipeline to classify SMS messages as Spam or Ham, implementing text preprocessing, feature extraction, multi-model evaluation, and deployment serialization.

**🔥 Technical Highlights:**
- **Complete NLP Preprocessing:** Implemented tokenization, stopword removal, lemmatization (WordNet), and custom regex-based entity replacement (URLs, emails, numbers).
- **Advanced TF-IDF Feature Engineering:** Utilized `sublinear_tf=True` for logarithmic term frequency scaling, `ngram_range=(1, 2)` for context capture, and `max_features=10,000` for vocabulary optimization.
- **Systematic Model Comparison:** Benchmarked Naive Bayes, Logistic Regression, Linear SVC, and Random Forest using 5-fold Stratified Cross-Validation.
- **Model Interpretability:** Extracted top coefficients to reveal learned spam indicators (*"free", "claim", "urgent"*) and ham indicators (*"hey", "got", "later"*).
- **Production-Ready Deployment:** Serialized a complete `scikit-learn` Pipeline using `joblib`, enabling instant predictions on raw text without manual preprocessing.

**🛠️ Technologies:** `NLTK`, `scikit-learn`, `pandas`, `joblib`, `matplotlib`, `seaborn`

**📊 Model Performance:**
| Model | Accuracy | Precision | Recall | F1-Score | AUC |
|:---|:---:|:---:|:---:|:---:|:---:|
| **🏆 Linear SVC (Calibrated)** | **98.92%** | **96.60%** | **95.30%** | **95.95%** | **0.9944** |
| Logistic Regression | 98.83% | 97.89% | 93.29% | 95.53% | 0.9934 |
| Naive Bayes | 98.48% | 96.48% | 91.95% | 94.16% | 0.9914 |
| Random Forest | 96.68% | 100.0% | 75.17% | 85.82% | 0.9902 |

**💡 Key Insight:** Linear SVC achieved the best balance of precision and recall, while Random Forest's high precision but low recall suggests it's overly conservative—missing spam that should be caught. The choice of model depends on the cost of false positives vs. false negatives.

**🚀 Deployment Example:**

```python
import joblib
pipeline = joblib.load("nlp_spam_pipeline.joblib")
predictions = pipeline.predict(["Congratulations! You won a free iPhone!"])
# Output: ['SPAM']

🧠 Skills & Competencies
This internship provided hands-on experience across the entire data science workflow. Below is a summary of the key competencies developed:

📊 Data Acquisition & Engineering
✅ Web Scraping: Reverse-engineering APIs, bypassing anti-bot protections, handling pagination, and managing session authentication.

✅ Data Cleaning: Handling missing values, outlier detection (Winsorization), dimensionality reduction, and type coercion.

✅ Feature Engineering: Categorical encoding (One-Hot, Label), TF-IDF vectorization, n-gram extraction, and interaction term creation.

✅ Pipeline Architecture: Building reproducible, leakage-free preprocessing pipelines using scikit-learn.

🤖 Machine Learning & Modeling
✅ Regression: Linear Regression, regularization concepts (Ridge/Lasso), and evaluation (R², MAE, RMSE, MAPE).

✅ Classification: Logistic Regression, KNN, Naive Bayes, SVC, Random Forest, and ensemble methods.

✅ Time Series: Stationarity testing (ADF), decomposition, smoothing (SES, Holt, Holt-Winters), ARIMA, and SARIMA.

✅ NLP: Text preprocessing, lemmatization, TF-IDF, and model interpretability.

✅ Model Evaluation: Cross-validation, confusion matrices, ROC-AUC, and comparative model benchmarking.

📈 Data Analysis & Communication
✅ Exploratory Data Analysis: Visualizing distributions, correlations, and patterns using matplotlib and seaborn.

✅ Critical Thinking: Honestly assessing model limitations and proposing actionable next steps.

✅ Documentation: Writing clear, professional README files and inline code comments.

✅ Ethical Considerations: Respecting rate limits, understanding Terms of Service, and handling data responsibly.

### 📁 Repository Structure
📦 Codveda_Task/
│
├── 📂 Level-1-Basic/
│   ├── 📂 Task-1-Yahoo-Finance-Scraper/
│   │   ├── Data Collection Task 1 L1.ipynb
│   │   ├── yahoo_screener_full.csv
│   │   ├── yahoo_screener_curated.csv
│   │   └── README.md
│   │
│   └── 📂 Task-2-Data-Cleaning-Pipeline/
│       ├── Data Cleaning Task 2 L1.ipynb
│       ├── yahoo_screener_clean.csv
│       ├── yahoo_screener_label_encoded.csv
│       ├── yahoo_screener_processed.csv
│       └── README.md
│
├── 📂 Level-2-Intermediate/
│   ├── 📂 Task-1-House-Price-Prediction/
│   │   ├── HousePricePrediction.csv
│   │   ├── house_price_predictor.ipynb
│   │   └── README.md
│   │
│   └── 📂 Task-2-Iris-Classification/
│       ├── Iris.csv
│       ├── iris_classification.ipynb
│       └── README.md
│
├── 📂 Level-3-Advanced/
│   ├── 📂 Task-1-Time-Series-Forecasting/
│   │   ├── aapl_time_series.ipynb
│   │   ├── ts_raw.png
│   │   ├── ts_decomposition.png
│   │   ├── ts_acf_pacf.png
│   │   ├── ts_smoothing.png
│   │   ├── ts_forecast.png
│   │   ├── ts_arima_forecast.png
│   │   └── README.md
│   │
│   └── 📂 Task-2-NLP-Spam-Classification/
│       ├── nlp_spam_classifier.ipynb
│       ├── nlp_spam_pipeline.joblib
│       ├── nlp_eda.png
│       ├── nlp_roc.png
│       ├── nlp_confusion.png
│       ├── nlp_top_features.png
│       └── README.md
│
└── README.md  # This file

🏆 Key Achievements
Throughout this internship, I successfully:

✅ Completed 6 end-to-end data science projects spanning web scraping, preprocessing, regression, classification, time series, and NLP.

✅ Bypassed advanced anti-bot protections using TLS fingerprint impersonation—a technique rarely covered in standard tutorials.

✅ Built production-ready pipelines using scikit-learn's Pipeline and ColumnTransformer architecture.

✅ Achieved 98.92% accuracy on SMS spam classification, with a production-ready serialized model.

✅ Forecasted stock prices with 3.55% MAPE using Holt's Linear Trend, outperforming complex SARIMA models.

✅ Demonstrated critical thinking by honestly evaluating model limitations and proposing improvements.


🚀 Future Work
-While these projects represent a strong foundation, there are several avenues for further exploration:

-Deep Learning: Implementing neural networks (LSTMs for time series, transformers for NLP) to capture complex patterns.

-Hyperparameter Optimization: Using GridSearchCV and RandomizedSearchCV for systematic model tuning.

-Model Deployment: Containerizing models with Docker and deploying via FastAPI or Flask for real-time inference.

-Automated ML (AutoML): Exploring tools like AutoGluon or TPOT for automated model selection and tuning.

-Big Data Integration: Scaling pipelines to handle larger datasets using PySpark or Dask.

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
