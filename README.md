# [Adult-income-prediction-ML-pipeline
> *One sentence. What did you analyze, build, or solve - and why does it matter?*

---

## ⚙️ Project Type Flags
> *Check what applies. This helps reviewers and collaborators understand the nature of the work at a glance. Delete this block before publishing.*

- [ ] Exploratory Data Analysis (EDA)
- [ ] SQL Analysis / Querying
- [ ] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [ ] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: ___________

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
11. [Future Enhancements](#12-future-enhancements)
12. [Deliverables](#13-deliverables)
13. [Author](#14-author)

---

## 1. Project Overview

<!--
  Write 3–5 sentences in plain language.
  Cover: context → problem → approach → outcome.
  Read it out loud. If it sounds like a form - rewrite it.

  WHAT GOOD LOOKS LIKE:
  "A mid-size retail business was seeing inconsistent revenue across
  its regional stores but couldn't identify the root cause. This project
  explored 18 months of transaction data across five regions to determine
  whether underperformance was driven by sales volume, pricing, or return
  rates. The analysis revealed that one region's gap was almost entirely
  explained by an unusually high return rate on a single product category -
  a finding invisible in the company's top-level reporting."

  WHAT TO AVOID:
  "This project analyzes sales data to find trends and insights."
  (Too vague. Could describe 10,000 projects. Describes none of them.)
-->

**Context:** :In workforce analytics and socioeconomic research, understanding the key drivers of individual earning potential provides valuable insights for policy formulation, talent compensation benchmarking, and targeted economic support programs. The UCI Adult Income Dataset (derived from the 1994 US Census database) offers a rich benchmark of over 32,500 individual records spanning 14 demographic, educational, and employment attributes.

**Problem Statement:** The goal of this project is to build an end-to-end binary classification machine learning pipeline to predict whether an employee earns >50K or <=50K per year based on individual demographic and employment attributes.

**Approach:** To solve this problem, an end-to-end Machine Learning pipeline was designed and executed in Python:
Data Cleaning & Preprocessing, Feature Encoding & Scaling, Model Benchmarking & Tuning, Model Evaluation & Serialization.

**Outcome:** Feature importance analysis revealed that education-num (years of education), capital-gain, age, and hours-per-week are the primary drivers predicting high earnings ($>50\text{K}$)

---

## 2. Objectives

<!--

- **Primary Objective:** Develop, optimize, and evaluate a machine learning model that accurately predicts whether an individual earns more than $50K annually (>50K vs. <=50K)
- **Secondary Objective 1:** Perform feature importance analysis on the trained models to determine which specific attributes like education level (education-num), capital gains, age, or weekly work hours—have the strongest influence on predicting high earners.
- **Secondary Objective 2:** Design a standardized, end-to-end data preprocessing pipeline to allow for seamless deployment and inference on unseen data.



---

## 3. Project Scope & Tools

### Scope

<!--
  WHAT GOOD LOOKS LIKE:
  In Scope: "Transaction-level data for Regions A–E, Jan 2023–Jun 2024.
             Analysis covers revenue, return rates, and product category performance."
  Out of Scope: "Customer demographics and marketing spend data were excluded -
                 demographic data was incomplete for two regions, and marketing
                 data sits in a separate system outside this engagement."

  WHAT TO AVOID:
  ❌ Leaving Out of Scope blank. This is the section that protects your credibility.
     If you don't define the fence, reviewers assume you missed things.
-->

| Dimension | Details |
|-----------|---------|
| **In Scope** | [https://www.kaggle.com/datasets/rdcmdev/adult-income-dataset, Segments: Individual demographic, educational, and employment attributes (e.g., age, workclass, education-num, occupation, capital-gain, hours-per-week] |
| **Time Period** | [1994 Census Database extract (Historical cross-sectional dataset).] |
| **Granularity** | [Individual-level (row-level data representing single adult survey respondents)] |

### Tools & Technologies

<!--
  List only what you actually used on this project.
  This is not your skills section - it's the project's technical context.
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
├── data/
│   ├── raw/                  # Original, unmodified source data - never edited
│   ├── processed/            # Cleaned and transformed data
│   └── external/             # Reference data, lookup tables, third-party files
│
├── notebooks/                # Jupyter, R Markdown, or Colab notebooks
│
├── scripts/                  # Reusable .py, .R, or .sh processing files
│
├── queries/                  # SQL files (retain this folder for SQL-heavy projects)
│   ├── exploratory/          # Ad-hoc or investigative queries
│   ├── transformations/      # Cleaning and reshaping logic
│   └── final/                # Production-ready or presentation queries
│
├── reports/                  # Final outputs: PDFs, slide decks, Word docs
│
├── visuals/                  # Exported charts, dashboard screenshots, ERD diagrams
│
├── docs/                     # Data dictionaries, schema notes, reference material
│
├── project_metadata.yml      # Machine-readable metadata (optional)
└── README.md                 # You are here
```

> ⚠️ *Delete folders you didn't use. An empty folder is worse than no folder.*
> SQL-heavy projects: keep `queries/`. Analysis-only projects: keep `notebooks/`. Both? Keep both.

---

## 5. Data Workflow

<!--
  Show how data moved through your project - from source to output.
  Every transformation decision should be traceable here.

  WHAT GOOD LOOKS LIKE:
  1. Source: "Monthly CSV exports pulled from the internal POS system.
              Five files, one per region, covering Jan 2023–Jun 2024."
  2. Ingestion: "Loaded into Python using pandas. Files concatenated into
                 a single dataframe (approx. 340,000 rows)."
  3. Cleaning: "Removed 1.2% of rows with null transaction IDs.
                Standardised date formats across regional files.
                Resolved product category naming inconsistencies (3 variants → 1)."
  4. Transformation: "Created a returns_rate field at product-category level.
                      Aggregated to weekly and regional grain for trend analysis."
  5. Analysis: "Descriptive statistics, regional comparison, return rate
                segmentation by product category."
  6. Output: "Summary report (PDF), annotated notebook, processed CSV."

  
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

## 6. Data Model & Schema

<!--
  Define your fields so that someone reading your analysis can follow along
  without digging through your code.

  WHAT GOOD LOOKS LIKE (one row example):
  | transaction_id | string | Unique identifier per sales transaction | TXN-00482 |
  | return_flag    | boolean | Whether the transaction included a return | TRUE |
  | region_code    | string | Two-letter identifier for store region | "NE" |


-->

### Dataset / Table: `[name]`

| Field Name | Data Type | Description | Example Value |
|------------|-----------|-------------|---------------|
| `age`      |integer   | Age of the individual in years | 39 |
| `workclass`| string   | Type of employer / employment sector | Private |
| `fnlwgt`   |integer  | Final weight; sample weight assigned by Census Bureau | 77516 |

> **Row count (approx.):** [32561]


---



## 7. Analysis & Metrics

<!--
  Explain what you measured and how - before you share what you found.

  WHAT GOOD LOOKS LIKE:
  Metric: "Customer Return Rate"
  Definition: "Number of transactions flagged as returns divided by total
               transactions, calculated at product-category and regional grain."
  Why It Matters: "Return rate - not sales volume - was hypothesised to
                  explain regional revenue gaps. This metric tests that hypothesis."

  WHAT TO AVOID:
  ❌ Defining a metric only in code: SUM(returns) / COUNT(transaction_id)
     That's an implementation. Write the plain-language definition here.
     Both belong in your project - the definition in the README,
     the implementation in the code.
-->

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

## 9. Key Insights

<!--
  Findings + implications. Not just what happened - what it means.

  WHAT GOOD LOOKS LIKE:
  ✅ "Return rates, not sales volume, explain Region A's underperformance.
      Region A's return rate on home goods was 34% - more than double the
      company average. Revenue was not lost at the point of sale; it was
      lost post-sale through refunds. This points to a fulfilment or
      product quality issue specific to that region, not a demand problem."

  WHAT TO AVOID:
  ❌ "Region A had lower revenue than other regions in Q4."
     (That's an observation. It describes what happened.
      An insight says what it means and where to look next.)

  Aim for 3–6 insights. Quality over quantity.
-->

**Insight 1: [Short descriptive headline]**
[What you found + what it suggests. One short paragraph.]

**Insight 2: [Short descriptive headline]**
[What you found + what it suggests.]

**Insight 3: [Short descriptive headline]**
[What you found + what it suggests.]

**Insight 4 (if applicable): [Short descriptive headline]**
[What you found + what it suggests.]

---

## 10. Recommendations

<!--
  Action-oriented. Addressed to a real audience.
  Tied explicitly to the insight that supports each one.

  WHAT GOOD LOOKS LIKE:
  Priority: High
  Recommendation: "Conduct a fulfilment audit for home goods deliveries
                   in Region A - specifically investigating whether returns
                   correlate with a particular warehouse, carrier, or SKU batch."
  Based On: Insight 1 - return rate anomaly in Region A
  Owner: Operations / Supply Chain team

  WHAT TO AVOID:
  ❌ "Improve the return rate."
     (Not actionable. Doesn't say who, how, or where to start.)
  ❌ "Further analysis is needed."
     (This is a placeholder, not a recommendation.)
-->

| Priority | Recommendation | Based On | Suggested Owner |
|----------|---------------|----------|-----------------|
| High | [Specific, actionable step] | [Insight it comes from] | [Who should act] |
| Medium | [Specific, actionable step] | [Insight it comes from] | [Who should act] |
| Low | [Exploratory or longer-term suggestion] | [Insight it comes from] | [Who should act] |

---

## 11. Assumptions & Limitations

<!--
  WHAT GOOD LOOKS LIKE:
  Assumption: "Transaction records were assumed to be complete for all five regions.
               No validation was performed against source system record counts."
  Limitation: "The analysis cannot distinguish between returns initiated by
               the customer vs. returns initiated by the business (e.g., recalls).
               If business-initiated returns are concentrated in Region A, the
               return rate finding may reflect a policy decision, not a quality issue."

  WHAT TO AVOID:
  ❌ Leaving this section blank or writing "None known."
     Every project has limitations. Documenting them is a sign of
     analytical maturity - not a confession of failure.
-->

### Assumptions
- [What did you treat as true without being able to verify?]
- [What simplifications did you make for scope or feasibility?]
- [What domain rules or definitions did you accept as given?]

### Limitations
- [What gaps exist in the data?]
- [What analysis was out of scope but could affect interpretation?]
- [What would a more rigorous version of this project include?]
- [Are there known biases in the data source or collection method?]

> *The goal here is pre-emptive Q&A. What would a thoughtful skeptic push back on? Document the answer here, before they ask.*

---

## 12. Future Enhancements

<!--
  WHAT GOOD LOOKS LIKE:
  ✅ "Automate the monthly data pull from the POS export folder using
      a scheduled Python script, replacing the current manual process."
  ✅ "Expand the return rate analysis to include carrier-level data,
      which was unavailable in this dataset but exists in the logistics system."

  WHAT TO AVOID:
  ❌ "Add a machine learning model."
     (Vague, and disconnected from the actual findings of this project.)
  ❌ Listing aspirational features that don't follow logically from the work.
-->

- [ ] [Enhancement 1 - specific and traceable to a real gap in this project]
- [ ] [Enhancement 2]
- [ ] [Enhancement 3]
- [ ] [Enhancement 4]

---

## 13. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| [Name] | [What it contains] | [`/path/to/file`] |
| [Name] | [What it contains] | [`/path/to/file`] |
| [Name] | [What it contains] | [`/path/to/file`] |

---

## 14. Author

**[Onyinye Stephanie Ozor]**
[ AI & ML Specialist| Data Analyst ]

- 🔗 [https://www.linkedin.com/in/onyinyeozor/]
- 💼 [Portfolio or GitHub profile URL]
- 📧 

---

*Last updated: [Month YYYY]*
*If this template helped you, consider starring the repository.*
