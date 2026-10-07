# Instructor Effectiveness Modeling

A Python-based data analysis and machine learning project to analyze instructor effectiveness using learner outcomes, engagement, and feedback data.

## 📌 Project Overview

This project analyzes batch-level instructor performance data and develops an instructor-level effectiveness framework.

The analysis covers:

- Exploratory Data Analysis (EDA)
- Data preprocessing and normalization
- Statistical and correlation analysis
- Instructor-level aggregation
- Effectiveness score creation
- Effectiveness tier classification
- Machine learning model development
- Model evaluation and cross-validation
- Feature importance analysis
- Model limitations and real-world considerations

The dataset contains **2,000 course-batch records**, representing **120 instructors across 25 courses**.

---

## 🎯 Objective

The main objective is to identify patterns associated with instructor effectiveness by combining:

1. **Learner Outcomes**
2. **Learner Engagement**
3. **Learner Feedback**

A continuous effectiveness score is created and used to classify instructors into three tiers:

- Low
- Medium
- High

Machine learning models are then used to predict these effectiveness tiers.

---

## 🛠️ Technologies & Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook

---

## 📊 Dataset

The dataset contains batch-level information including:

- Completion rate
- Dropout rate
- Average score improvement
- Average quiz score
- Average watch time
- Assignment submission rate
- Forum activity rate
- Average feedback score
- Feedback response rate
- Instructor ID
- Course ID
- Batch ID

The original batch-level data is aggregated at the instructor level because individual instructors teach multiple batches.

---

## 🔍 Exploratory Data Analysis

The EDA examines:

- Dataset structure and data types
- Duplicate records
- Summary statistics
- Feature distributions
- Number of instructors, courses, and batches
- Correlations between numerical variables
- Potential outliers
- Number of batches taught by each instructor

### Key Findings

- The dataset contains **2,000 unique batches and 120 instructors**.
- Instructors teach multiple batches, making instructor-level aggregation important.
- Completion rate and dropout rate have a very strong negative correlation (**r ≈ -0.95**).
- Feedback scores are generally concentrated toward the higher end of the scale.
- Potential outliers were examined but not automatically removed because they may represent legitimate differences between batches.

---

## 🧮 Effectiveness Score

Since the variables are measured on different scales, numerical features are normalized using `MinMaxScaler`.

Instructor effectiveness is calculated using three components:

### Learner Outcome Score

Includes:

- Completion rate
- Dropout rate
- Score improvement
- Quiz score

### Engagement Score

Includes:

- Watch time
- Assignment submission rate
- Forum activity rate

### Feedback Score

Includes:

- Average feedback score
- Feedback response rate

The final effectiveness score combines these three components:

- **45% Learner Outcomes**
- **30% Engagement**
- **25% Feedback**

---

## 👨‍🏫 Instructor-Level Aggregation

Batch-level observations are aggregated by instructor using mean values.

This produces an instructor-level dataset containing **120 instructors**.

The number of batches taught by each instructor is also retained as an additional feature.

Instructors are then divided into three effectiveness tiers:

- **Low**
- **Medium**
- **High**

The tiers are created using quantile-based classification because the dataset does not contain an independently validated effectiveness label.

---

## 🤖 Machine Learning Models

Two classification algorithms were evaluated:

### 1. Random Forest

Random Forest was selected because it:

- Captures nonlinear relationships
- Handles interactions between features
- Provides feature importance estimates

### 2. Logistic Regression

Logistic Regression was used as a simpler baseline model with a linear decision boundary.

---

## 📈 Model Evaluation

The models were evaluated using:

- Accuracy
- Precision
- Recall
- Macro F1-score
- Confusion Matrix
- 5-Fold Stratified Cross-Validation

### Results

Random Forest achieved:

- **Test Accuracy:** ~91.67%
- **5-Fold Cross-Validation Macro F1:** ~0.91

Logistic Regression achieved a higher score on the single held-out test set, but Random Forest produced the stronger mean cross-validation Macro F1-score.

Therefore, **Random Forest was selected as the final model**.

---

## ⭐ Feature Importance

The most influential features in the Random Forest model were:

1. Completion Rate
2. Dropout Rate
3. Feedback Response Rate
4. Average Score Improvement
5. Average Quiz Score
6. Average Feedback Score

Completion rate and dropout rate were particularly influential.

However, these results should **not be interpreted as causal relationships**, because several of these variables were also used to construct the effectiveness score.

---

## ⚠️ Limitations

This project has several important limitations:

- The instructor-level dataset contains only 120 observations.
- The effectiveness tiers are derived from the scoring framework rather than independently validated labels.
- Completion rate and dropout rate contain highly overlapping information.
- Learner feedback may contain response bias.
- Course difficulty and learner characteristics are not fully represented.
- The model may not generalize to substantially different instructors, courses, or learner populations.
- The model should not be used as the sole basis for high-stakes instructor evaluation.

---

## 💡 Possible Improvements

Future versions could include:

- Course difficulty
- Batch size
- Instructor experience
- Learner attendance
- Pre-course assessment scores
- Learner background
- Instructor-learner interaction data
- More detailed learner feedback
- A larger instructor-level dataset
- Independent ground-truth labels for instructor effectiveness

These additions could help distinguish instructor effects from learner and course-level factors.

---

## 📁 Project Structure

```text
instructor-effectiveness-modeling/
│
├── Instructor_Effectiveness_Modeling.ipynb
├── README.md
├── requirements.txt
├── data/
│   └── dataset.xlsx
│
└── images/
    ├── correlation_matrix.png
    ├── confusion_matrix.png
    └── feature_importance.png
