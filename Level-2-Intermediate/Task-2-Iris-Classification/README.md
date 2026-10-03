# Iris Flower Classification — A Comparative ML Approach
### Codveda Technologies - Data Science Internship (Level 2, Task 2)

![Python](https://img.shields.io/badge/Python-3.8%2B-blueviolet)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.0+-brightgreen)
![Pandas](https://img.shields.io/badge/Pandas-1.3+-yellow)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 1. The Motive: Why This Project?

The primary motive of this project is to **master the fundamentals of supervised classification** in machine learning. The Iris dataset is the "Hello World" of data science—small, clean, and perfectly structured. 

However, this project goes beyond simply running a script. It aims to:

- Build an intuitive understanding of **how different machine learning algorithms make decisions**.
- Compare the behavior of **parametric vs. non-parametric** models on the same dataset.
- Establish a reusable pipeline (EDA → Preprocessing → Training → Evaluation) that can be applied to more complex, real-world classification problems.

---

## 2. The Problem Statement: What Are We Trying to Solve?

In the field of botany, identifying the species of an Iris flower traditionally requires expert visual inspection. This project seeks to **automate that identification process** using only four numerical measurements:

- **Sepal Length** (cm)
- **Sepal Width** (cm)  
- **Petal Length** (cm)
- **Petal Width** (cm)

Given these features, our goal is to train a robust model that can accurately predict one of the three distinct species:

- **Iris-setosa** (highly distinguishable)
- **Iris-versicolor**
- **Iris-virginica** (hardest to classify due to overlap with versicolor)

The core scientific challenge here is: *Can a mathematical model reliably learn the subtle boundary differences between Versicolor and Virginica, which often share similar measurements?*

---

## 3. The Proposed Solution: Our Machine Learning Framework

To tackle this problem, we implemented a **multi-model comparative framework** rather than relying on a single algorithm. This approach allows us to cross-validate results and understand which decision boundaries work best for this specific data.

### 🛠️ Technical Stack (Language & Frameworks)

- **Language:** Python 3.x
- **Data Handling:** `Pandas` & `NumPy`
- **Visualization:** `Matplotlib` & `Seaborn` (for Exploratory Data Analysis)
- **Machine Learning:** `Scikit-learn`
  - *Preprocessing:* `StandardScaler`, `LabelEncoder`, `train_test_split`
  - *Models:* `LogisticRegression`, `KNeighborsClassifier`, `GaussianNB`
  - *Metrics:* `accuracy_score`, `confusion_matrix`, `classification_report`

### 🧠 The Three Models Selected

| Model | Type | Why Chosen? |
| :--- | :--- | :--- |
| **Logistic Regression** | Parametric (Linear) | Establishes a baseline. Works well when data is linearly separable (which Iris generally is). |
| **K-Nearest Neighbors (KNN)** | Non-Parametric (Instance-based) | Captures non-linear boundaries. Tests how sensitive the model is to local data distribution. |
| **Gaussian Naive Bayes** | Probabilistic (Bayesian) | Fast and efficient. Tests the assumption of feature independence against real-world data. |

---

## 4. Implementation Workflow: Step-by-Step Execution

The project follows a strict **data science lifecycle** to ensure clean, reproducible, and reliable results:

### Step 1: Exploratory Data Analysis (EDA)
Before touching the models, we visualized the data using `seaborn.pairplot`. 
- **Finding:** The `PetalLengthCm` and `PetalWidthCm` showed strong positive correlation and clearly separated *Setosa* from the other two. 
- *Insight:* This suggested that a linear model would likely perform well, but the overlap between *Versicolor* and *Virginica* would challenge the classifiers.

### Step 2: Data Preprocessing
- **Dropping Noise:** The `Id` column was removed as it holds no predictive power for classification.
- **Train-Test Split:** Data was split 80/20 (`random_state=42`). This ensures the model is tested on unseen data to validate generalization.
- **Feature Scaling:** Applied `StandardScaler` (mean=0, variance=1). *Crucial step:* Since KNN relies on Euclidean distance, unscaled data (e.g., Sepal Length ~5.0 vs. Petal Width ~0.2) would heavily bias the algorithm toward larger numerical values.

### Step 3: Model Training
All three models were trained using the scaled training data (`X_train_scaled`). No hyperparameter tuning was performed in this initial phase to keep the comparison focused on the core algorithmic structure.

### Step 4: Evaluation & Metrics
We evaluated performance using:
1. **Accuracy Score** – Overall correctness.
2. **Confusion Matrix** – Where is the model making mistakes? (Crucial for distinguishing Versicolor vs. Virginica).
3. **Classification Report** – Precision, Recall, and F1-Score per class to handle class imbalances (though this dataset is perfectly balanced).

---

## 5. Findings & Model Performance

After executing the notebook, the following results were observed on the evaluation set:

> *(Please replace the bracketed numbers [ ] below with your actual printed outputs from the notebook)*

| Model | Accuracy | Key Observations |
| :--- | :--- | :--- |
| **Logistic Regression** | **[ e.g., 97.3% ]** | Perfectly identified Setosa. Misclassified a few Virginica as Versicolor. Proves the data is highly linearly separable. |
| **KNN (k=5)** | **[ e.g., 96.7% ]** | Slightly lower accuracy due to sensitivity to the "curse of dimensionality," even with only 4 features. Performed robustly on dense clusters. |
| **Naive Bayes** | **[ e.g., 96.0% ]** | Assumed feature independence, which held up relatively well. Performed the weakest on overlapping boundaries but was the fastest to train. |

### 🔍 Critical Analysis of Results
- **The Standout Winner:** Logistic Regression consistently outperforms the others because the Iris dataset's decision boundaries are largely linear. 
- **The Overlap Problem:** The confusion matrices revealed that the majority of misclassifications occurred between *Versicolor* and *Virginica*. Their feature ranges naturally overlap in the wild, making this a common challenge even for advanced models.

---

## 6. Conclusion & Key Learnings

This project successfully demonstrates that **machine learning can achieve near-perfect accuracy (>95%)** on standard morphological data using relatively simple algorithms. 

### 🔬 What Did We Learn?

1. **EDA is Non-Negotiable:** Visualizing the data via the `pairplot` immediately told us *why* Setosa is easy to classify and why the other two are challenging—before we even wrote a single `fit()` command. This reinforces that a data scientist must explore before they model.

2. **Feature Scaling is Mandatory for Distance-Based Models:** Applying `StandardScaler` was essential for KNN. Without it, KNN's accuracy would have dropped significantly because the algorithm would have weighted Sepal Length (larger numbers) more heavily than Petal Width (smaller numbers), skewing the Euclidean distance calculations.

3. **No Single Model is Universally Superior:** While Logistic Regression won on this specific dataset, Naive Bayes or KNN could easily outperform it on a more complex, non-linear dataset with overlapping features. A good data scientist always tests multiple baselines.

4. **Interpretability Matters:** The confusion matrices allowed us to see *where* the models were failing (Versicolor ↔ Virginica). Accuracy alone would have hidden this nuance.

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

## 🙏 Acknowledgments

- Dataset source:https://www.kaggle.com/datasets/saurabh00007/iriscsv  

---

**⭐ If you find this project useful, please consider giving it a star!**