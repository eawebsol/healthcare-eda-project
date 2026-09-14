# 🏥 Healthcare EDA Project
## Patient Readmission Risk Analysis

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-green)
![D-Tale](https://img.shields.io/badge/D--Tale-3.0%2B-orange)
![Status](https://img.shields.io/badge/Status-Active-success)

---

## 📖 Overview

An **end-to-end Exploratory Data Analysis (EDA)** project on a **500,000-record synthetic healthcare dataset**. Students analyze patient data to uncover factors driving **hospital readmissions** and **treatment costs**, then deliver actionable recommendations.

| Property | Value |
|----------|-------|
| **Domain** | Healthcare Analytics |
| **Level** | Intermediate |
| **Duration** | 2-3 Weeks |
| **Mode** | Individual |
| **Tools** | Python, Pandas, NumPy, Matplotlib, Seaborn, D-Tale |

---

## 🎯 Learning Objectives

By completing this project, you will be able to:

- ✅ Load and inspect large datasets (500K+ records) using Pandas
- ✅ Use D-Tale as a supplementary tool for interactive data exploration
- ✅ Identify and handle data quality issues (missing values, outliers, inconsistencies)
- ✅ Create professional visualizations using Matplotlib and Seaborn
- ✅ Perform univariate, bivariate, and multivariate analysis
- ✅ Engineer new features from existing data
- ✅ Derive business insights and provide actionable recommendations
- ✅ Create a dashboard suitable for stakeholder presentation

---

## 📊 Dataset

**Source:** [Synthetic Datasets Repository](https://github.com/leventbulut/synthetic-datasets)

| Property | Value |
|----------|-------|
| **Direct CSV** | [synthetic_healthcare_20250901.csv](https://raw.githubusercontent.com/leventbulut/synthetic-datasets/main/datasets/healthcare/synthetic_healthcare_20250901.csv) |
| **Records** | 500,000 |
| **Columns** | 22 |
| **Size** | 62.3 MB |
| **Targets** | Readmission Risk (classification), Total Cost (regression) |

> ⚠️ **Note:** The CSV is hosted via Git LFS. If `pd.read_csv()` from the raw URL fails, download the file manually and load it locally. See [`SETUP_GUIDE.md`](SETUP_GUIDE.md).

### Data Quality Challenges

As noted in the repository documentation, this dataset contains **realistic data quality challenges**:

- 🔸 **Missing Values** — Not missing at random (MNAR); follow realistic patterns
- 🔸 **Outliers** — Extreme but plausible values that require investigation
- 🔸 **Entry Errors** — Data-entry mistakes that must be identified and handled
- 🔸 **Multiple Feature Types** — Numerical, categorical, and datetime columns

---

## 📁 Repository Structure
