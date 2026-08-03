# [Adult-income-prediction-ML-pipeline
> 
---

## ⚙️ Project Type Flags
> 

- [ ] Data Cleaning / Wrangling
- [ ] Exploratory Data Analysis (EDA)
- [ ]  Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning


---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Project Scope & Tools](#3-project-scope--tools)
4. [Repository Structure](#4-repository-structure)
5. [Data Workflow](#5-data-workflow)
6. [Data Model & Schema](#6-data-model--schema)
7. [Analysis & Metrics](#7-analysis--metrics)
8. [Key Insights](#8-key-insights)
9. [Recommendations](#9-recommendations)
10. [Assumptions & Limitations](#10-assumptions--limitations)
11. [Future Enhancements](#11-future-enhancements)
12. [Deliverables](#12-deliverables)
13. [Author](#13-author)

---

## 1. Project Overview

<!--

**Context:** :In workforce analytics and socioeconomic research, understanding the key drivers of individual earning potential provides valuable insights for policy formulation, talent compensation benchmarking, and targeted economic support programs. The UCI Adult Income Dataset (derived from the 1994 US Census database) offers a rich benchmark of over 32,500 individual records spanning 14 demographic, educational, and employment attributes.

**Problem Statement:** The goal of this project is to build an end-to-end binary classification machine learning pipeline to predict whether an employee earns >50K or <=50K per year based on individual demographic and employment attributes.

**Approach:** To solve this problem, an end-to-end Machine Learning pipeline was designed and executed in Python:
Data Cleaning & Preprocessing, Feature Encoding & Scaling, Model Benchmarking & Tuning, Model Evaluation & Serialization.

**Outcome:** Feature importance analysis revealed that education-num (years of education), capital-gain, age, and hours-per-week are the primary drivers predicting high earnings ($>50\text{K}$)

--->

## 2. Objectives

<!--

- **Primary Objective:** Develop, optimize, and evaluate a machine learning model that accurately predicts whether an individual earns more than $50K annually (>50K vs. <=50K)
- **Secondary Objective 1:** Perform feature importance analysis on the trained models to determine which specific attributes like education level (education-num), capital gains, age, or weekly work hours—have the strongest influence on predicting high earners.
- **Secondary Objective 2:** Design a standardized, end-to-end data preprocessing pipeline to allow for seamless deployment and inference on unseen data.



---
-->
## 3. Project Scope & Tools

### Scope

<!--

-->

| Dimension | Details |
|-----------|---------|
| **In Scope** | [https://www.kaggle.com/datasets/rdcmdev/adult-income-dataset, Segments: Individual demographic, educational, and employment attributes (e.g., age, workclass, education-num, occupation, capital-gain, hours-per-week] |
| **Time Period** | [1994 Census Database extract (Historical cross-sectional dataset).] |
| **Granularity** | [Individual-level (row-level data representing single adult survey respondents)] |

### Tools & Technologies

<!--
 
-->

| Category | Tool(s) Used |
|----------|-------------|
| Data Storage | [ CSV files] |
| Data Processing | [ Python] |
| Analysis | [ Pandas, Numpy, Sklearn] |
| Visualization | [ Matplotlib, Seaborn] |
| Version Control | [ GitHub] |
| Documentation | [ Markdown] |
| Other | [Any additional tools] |

---

## 4. Repository Structure

```
[project-root]/
│
├── LICENSE                              # Project license details (MIT)
├── README.md                               # Project documentation and guide
├── adult.data                               # Sourced training dataset
├── adult.test                                # Sourced testing dataset
├── employee_salary_prediction --.ipynb       # Main end-to-end ML notebook

```


---

## 5. Data Workflow

<!--

```

1. **Source:** tatic CSV dataset (adult.data / adult.csv) sourced from the UCI Machine Learning Repository via Kaggle, containing 32,561 rows and 15 raw attributes from the 1994 US Census database.

2. **Ingestion:** Loaded into Python using pandas.read_csv() with explicit custom column headers (COLUMN_NAMES), setting header=None, na_values=" ?", and skipinitialspace=True to handle non-standard formatting.

3. **Cleaning:** Standardized all column names to lower-case string representations.
Replaced missing "?" indicators with column modes across categorical fields (workclass, occupation, native-country).
Detected and dropped identical duplicate records.
Applied Interquartile Range (IQR) capping to treat extreme outliers in continuous attributes (capital-gain, capital-loss, hours-per-week).

4. **Transformation:** Engineerd derived financial metrics,Converted categorical attributes into numerical formats using LabelEncoder for binary variables and OneHotEncoder,Normalized continuous features using StandardScaler to maintain zero mean and unit variance.

5. **Analysis:** Conducted Exploratory Data Analysis (EDA) using summary statistics (describe), distribution plots (histplot), count plots, and correlation heatmaps.
Benchmarked five classification algorithms (Logistic Regression, Decision Tree, Random Forest, KNN, SVM).
Hyperparameter-tuned the optimal ensemble model via GridSearchCV and performed feature importance ranking.

6. **Output:** Production-ready inference pipeline test verifying predictions on new sample dat

---
-->
## 6. Data Model & Schema

<!--

-->

### Dataset / Table: `[name]`

| Field Name | Data Type | Description | Example Value |
|------------|-----------|-------------|---------------|
| `age`      |integer   | Age of the individual in years | 39 |
| `workclass`| string   | Type of employer / employment sector | Private |
| `fnlwgt`   |integer  | Final weight; sample weight assigned by Census Bureau | 77516 |

 **Row count (approx.):** 32561


---



## 7. Analysis & Metrics

<!--

### Analytical Approach

This analysis combines exploratory data analysis with supervised machine learning modeling. The approach began by exploring demographic and financial patterns within the Census Adult dataset to identify key correlations with income levels. Next, an end-to-end data preprocessing and feature engineering pipeline was built to handle missing values, cap extreme financial outliers, and scale numerical variables. Finally, five machine learning classification models were benchmarked and hyperparameter-tuned (GridSearchCV) to predict annual income brackets while mitigating class imbalance challenges.

### Key Metrics Defined

| Metric | Plain-Language Definition | Why It Matters |
|--------|--------------------------|----------------|
| `Classification Accuracy` | The percentage of total income predictions that the model got completely correct. | Provides an overall baseline measure of model correctness across the dataset.|
| `Precision (High-Income Class)` | Out of all individuals the model predicted as earning >50K, the proportion who actually earn >50K | Prevents false positives—ensuring economic interventions or target programs are not misallocated to ineligible individuals|
| `Recall / Sensitivity` | the percentage that the model successfully caught. | Measures model completeness |

### Methods Used

- Descriptive Statistics: Summary statistics (mean, median, standard deviation, IQR) for distribution analysis and continuous outlier detection across financial fields.
- Exploratory Visualizations: Univariate distributions (sns.histplot), categorical breakdown charts (sns.countplot), box plots for outlier visualization, and correlation heatmaps across continuous numerical attributes.
- Segmentation & Group Comparison: Categorical cross-tabulation and aggregation analyzing income distribution by education level (education-num), employment sector (workclass), and gender (sex)
- Feature Importance Analysis: Extracted Gini importance metrics (model.feature_importances_) from the optimal Random Forest model to rank top predictive socioeconomic drivers.
- Hyperparameter Optimization: Systematic cross-validated grid search (GridSearchCV) across model hyperparameter spaces (n_estimators, max_depth, min_samples_split).


---
-->
## 8. Key Insights

<!--
-->

**Insight 1: Education years and capital gains are the primary drivers of high earning potential.**
Years of formal education and capital-gain far outweigh attributes like age or work sector in predicting income >50K. Individuals with higher educational attainment and existing investment assets show a exponentially higher likelihood of crossing the $50K threshold. This suggests that financial literacy programs and access to higher education remain the most effective leverage points for socioeconomic mobility.

**Insight 2: Severe target class imbalance skews baseline model performance**
Roughly 76% of individuals in the dataset earn <=50K, leaving only ~24% in the >50K high-earning bracket. Relying solely on raw classification accuracy leads to deceptive performance metrics, as a naive model predicting <=50K for every record would achieve 76% accuracy while failing completely on high earners

**Insight 3 (if applicable): Earning Dynamics Depend on Compounding Demographic Factors**
The non-linear interactions between demographic variables—such as the compounding effect of high hours-per-week combined with specific occupation sectors—were far better captured by decision trees, highlighting that financial earning models require non-linear decision boundaries to capture real-world workforce dynamics.

---

## 9. Recommendations

<!--
 
-->

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | Optimize Metric Selection & Class Thresholds | Insight 2 | ML Engineering / Data Science Team |
| Medium | Prioritize High-Yield Educational & Asset Data Collection | Insight 1 | Data Strategy / Analytics Team |
| Low | Implement Non-Linear & Ensemble Modeling | Insight 3: | R&D / Advanced Analytics Team |

---

## 10. Assumptions & Limitations

<!--
 
-->

### Assumptions
- Missing values denoted by "?" in categorical attributes (workclass, occupation, native-country) were assumed to occur at random (MCAR) and were imputed using column modes without introducing significant bias.
- The $50K threshold was accepted as a static binary target representing economic status, assuming that nominal currency values across records reflect consistent buying power without adjusting for regional inflation or cost-of-living differences.


### Limitations
-  The dataset originates from the 1994 US Census extract; modern salary dynamics, remote work setups, inflation, and updated educational values are not reflected in these historical data points.
- Key financial drivers such as total net worth, regional cost of living, household debt, and industry-specific certifications,were not captured in the raw dataset, limiting the predictive ceiling of demographic attributes alone.


> 

---

## 11. Future Enhancements

<!--
  
-->

- [ ] Apply Synthetic Minority Over-sampling Technique (SMOTE) or adjust class-weight hyperparameter parameters during training to actively improve minority class recall (>50K high earners).
- [ ] Benchmark modern gradient boosted decision trees (such as XGBoost, LightGBM, or CatBoost) against the Random Forest baseline to extract higher non-linear predictive power from continuous demographic variables.

---

## 12. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| Raw Dataset | Sourced 1994 US Census Adult dataset containing 32,561 rows and 15 raw feature attributes. |./adult.csv |
| Project Documentation| Complete project guide detailing scope, methodology, data schema, metrics, key insights, and deployment instructions. | [`README.md`] |
| Analysis Notebook | Annotated Vscode covering full EDA, preprocessing, model training, hyperparameter tuning, evaluation diagnostics, and inference testing| [`[/path/to/file](https://www.google.com/search?q=./employee_salary_prediction.ipynb)`] |

---

## 13. Author

**[Onyinye Stephanie Ozor]**
[ AI & ML Specialist| Data Analyst ]

- 🔗 [https://www.linkedin.com/in/onyinyeozor/]
- 💼 [Portfolio or GitHub profile URL]


---

*Last updated: [08 2026]*

