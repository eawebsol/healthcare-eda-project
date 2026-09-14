# 📘 Project Guide
## Healthcare EDA Project — Patient Readmission Risk Analysis

---

## 📌 Table of Contents

1. [Project Overview](#1-project-overview)
2. [Dataset Information](#2-dataset-information)
3. [Tools & Environment](#3-tools--environment)
4. [Project Workflow](#4-project-workflow)
5. [Phase-by-Phase Tasks](#5-phase-by-phase-tasks)
6. [D-Tale Integration Points](#6-d-tale-integration-points)
7. [Deliverables Checklist](#7-deliverables-checklist)
8. [Real-World Tips](#8-real-world-tips)

---

## 1. Project Overview

### Business Context

A large hospital network wants to **reduce patient readmission rates** and **better understand the key drivers of high treatment costs**. Hospital readmissions are costly, often preventable, and serve as a key quality metric for healthcare providers.

The hospital's leadership has tasked your data analysis team with performing an **exploratory data analysis (EDA)** to uncover actionable insights from their patient records. Your findings will inform resource allocation, patient care strategies, and cost optimization initiatives.

**Your Role:** You are a data analyst on the hospital's analytics team. Your manager needs a comprehensive report with visualizations and recommendations to present to hospital leadership.

### Project Objectives

By the end of this project, you will have:

- Explored a large, realistic healthcare dataset (500,000 records)
- Cleaned and preprocessed the data with documented decisions
- Performed univariate, bivariate, and multivariate analysis
- Engineered new features for deeper insight
- Delivered a dashboard and executive summary with recommendations

### Difficulty & Duration

| Property | Value |
|----------|-------|
| **Difficulty** | Intermediate |
| **Duration** | 2-3 Weeks |
| **Mode** | Individual |
| **Prerequisites** | Basic Python, Pandas, Matplotlib, Seaborn |

---

## 2. Dataset Information

### Source

**Synthetic Healthcare Dataset** from the [Synthetic Datasets for Data Science Education](https://github.com/leventbulut/synthetic-datasets) repository.

| Property | Value |
|----------|-------|
| **Direct CSV** | [synthetic_healthcare_20250901.csv](https://raw.githubusercontent.com/leventbulut/synthetic-datasets/main/datasets/healthcare/synthetic_healthcare_20250901.csv) |
| **Records** | 500,000 |
| **Columns** | 22 |
| **Size** | 62.3 MB |
| **Classification Target** | Readmission Risk |
| **Regression Target** | Total Cost |
| **License** | Educational/Research Use |

### Data Quality Challenges

This dataset simulates **realistic data quality issues** that you would encounter in a real healthcare setting:

- **Missing Values** — Not missing at random (MNAR); follow realistic patterns
- **Outliers** — Extreme but plausible values that require investigation
- **Entry Errors** — Data-entry mistakes that must be identified and handled
- **Multiple Feature Types** — Numerical, categorical, and datetime columns

> ⚠️ **Important:** Plan your data-cleaning strategy before diving in. This is what real-world data looks like.

### Key Columns (Expected)

| Column | Type | Description |
|--------|------|-------------|
| PatientID | String | Unique patient identifier |
| Age | Integer | Patient age in years |
| Gender | Categorical | Patient gender |
| Medical Condition | Categorical | Primary diagnosis/condition |
| Admission Type | Categorical | Emergency, Urgent, Elective, etc. |
| Admission Date | Datetime | Date of admission |
| Discharge Date | Datetime | Date of discharge |
| Length of Stay | Integer | Duration of hospital stay (days) |
| Billing Amount | Float | Total treatment cost |
| Test Results | Categorical | Results from medical tests (may have missing values) |
| Readmission Risk | Categorical | Risk score/category for readmission |
| Previous Admissions | Integer | Number of prior hospitalizations |
| Insurance Type | Categorical | Patient's insurance coverage |
| Medication Count | Integer | Number of prescribed medications |

> 📌 The exact column names may vary. Always inspect the dataset first with `df.columns`.

### Data Dictionary & Suggested Tasks

The source repository includes:
- Data dictionaries at `documentation/data_dictionaries/`
- Suggested analytical questions at `documentation/suggested_tasks/`

Explore these to deepen your understanding of the dataset.

---

## 3. Tools & Environment

### Required Libraries

- **pandas** — Data manipulation
- **numpy** — Numerical operations
- **matplotlib** — Base plotting
- **seaborn** — Statistical visualization
- **dtale** — Interactive EDA (supplementary)

### D-Tale Setup

D-Tale is a **supplementary tool** for interactive exploration. It will be used at key checkpoints, but **not** as the primary analysis tool. Your main deliverables should use Pandas and Matplotlib/Seaborn.

**Example:**
```python
import dtale
d = dtale.show(df)
d.open_browser()

```

See SETUP_GUIDE.md for full environment setup.

## 4. Project Workflow

PHASE 1: Data Loading & Initial Inspection
   ↓
PHASE 2: Data Cleaning & Preprocessing
   ↓
PHASE 3: Univariate Analysis
   ↓
PHASE 4: Bivariate & Multivariate Analysis
   ↓
PHASE 5: Feature Engineering
   ↓
PHASE 6: Insights, Dashboard & Recommendations

## 5. Phase-by-Phase Tasks

PHASE 1: Data Loading & Initial Inspection
Objective: Understand the dataset structure and identify data quality issues.

Task 1.1: Load the Dataset
Import all required libraries

Load the dataset using pd.read_csv()

Display the first 5 rows

Check the shape (rows × columns)

Task 1.2: Data Overview
Generate statistical summary using .describe()

Display data types using .dtypes

Identify categorical, numerical, and datetime columns

Check memory usage

Task 1.3: Data Quality Assessment
Calculate missing values per column (count and percentage)

Display unique values in categorical columns

Identify potential data inconsistencies

Task 1.4: Launch D-Tale for Interactive Exploration
Launch D-Tale and explore the dataset

Note any patterns, outliers, or anomalies

Use D-Tale's Describe, Missing, and Correlations tabs

Task 1.5: Document Initial Findings
Write observations about data structure

Note any immediate data quality concerns

Identify columns requiring cleaning

Deliverable: A markdown section with initial observations.

PHASE 2: Data Cleaning & Preprocessing
Objective: Clean the data and prepare it for analysis.

Task 2.1: Handle Missing Values
Identify columns with missing values

For each column, decide on strategy:

Numeric: mean, median, or mode?

Categorical: mode or "Unknown"?

Date: handle based on nature

Document reasoning for each choice

Implement cleaning

Hint: Use df['column'].fillna(value) or df.dropna(subset=['column'])

Task 2.2: Handle Outliers
Use boxplots to identify outliers in numerical columns

Decide whether to:

Remove (IQR method: values beyond 1.5×IQR)

Cap (Winsorization)

Keep (if meaningful)

Implement chosen strategy and document

Hint: Use df['column'].quantile() for IQR calculations

Task 2.3: Standardize Categorical Variables
Check for inconsistent formatting (e.g., "Male" vs "male")

Standardize all categorical values

Verify consistency

Hint: Use .str.strip(), .str.title(), or .replace()

Task 2.4: Date Handling
Convert date columns to datetime format

Verify Length of Stay matches admission/discharge difference

Flag any date inconsistencies

Hint: Use pd.to_datetime() and .dt.days

Task 2.5: Check for Duplicate Records
Identify duplicate rows

Investigate duplicates based on PatientID

Remove true duplicates, keep legitimate records

Hint: Use df.duplicated() and df.drop_duplicates()

Task 2.6: Validate Cleaning with D-Tale
Reload cleaned dataset in D-Tale

Verify missing values are handled

Check distributions before and after cleaning

Document any remaining issues

Deliverable: Clean dataset with documented cleaning decisions.

PHASE 3: Univariate Analysis
Objective: Analyze each variable individually to understand distributions.

Task 3.1: Numerical Variables Analysis
Create visualizations for:

Histograms: Age, Billing Amount, Length of Stay, Previous Admissions, Medication Count

Boxplots: Billing Amount, Length of Stay, Age

Summary Table: Mean, median, mode, std, min, max, quartiles for each numerical variable

Task 3.2: Categorical Variables Analysis
Create visualizations for:

Bar Charts: Gender, Medical Condition (top 10), Admission Type, Insurance Type

Pie Charts: Admission Type (with percentages), Insurance Type

Task 3.3: Target Variable Analysis
Analyze distribution of Readmission Risk

Check if normally distributed

Create risk categories (Low/Medium/High) based on distribution

Visualize proportion in each category

Task 3.4: Observations
Write insights for each visualization

Note any surprising patterns or distributions

Deliverable: Complete univariate analysis with labeled visualizations and observations.

PHASE 4: Bivariate & Multivariate Analysis
Objective: Explore relationships between variables.

Task 4.1: Categorical vs. Categorical
Create stacked or grouped bar charts for:

Admission Type vs. Readmission Risk

Gender vs. Medical Condition

Insurance Type vs. Admission Type

Task 4.2: Categorical vs. Numerical
Create boxplots or violin plots for:

Medical Condition vs. Billing Amount

Admission Type vs. Length of Stay

Gender vs. Billing Amount

Readmission Risk Category vs. Billing Amount

Task 4.3: Numerical vs. Numerical
Create:

Scatter Plots: Age vs. Billing Amount (colored by risk), Length of Stay vs. Billing Amount, Age vs. Length of Stay

Correlation Heatmap: All numerical variables

Identify top 3 positive and negative correlations

Task 4.4: Multivariate Analysis
Pairplot: Key numerical variables colored by Readmission Risk

Facet Grids: Billing Amount by Medical Condition and Gender; Length of Stay by Admission Type and Risk

Task 4.5: D-Tale Interactive Exploration (Optional)
Use D-Tale to filter specific segments

Explore correlations interactively

Validate findings

Task 4.6: Observations
Document key relationships discovered

Note any surprising correlations

Deliverable: Comprehensive bivariate/multivariate analysis with insights.

PHASE 5: Feature Engineering
Objective: Create new features that provide additional analytical value.

Task 5.1: Create Age Groups
Create Age_Group column: 18-30 (Young Adult), 31-45 (Adult), 46-60 (Middle Age), 60+ (Senior)

Visualize readmission risk across age groups

Task 5.2: Create Cost Categories
Create Cost_Category: Low (<25th percentile), Medium (25th-75th), High (>75th)

Analyze relationship with readmission risk

Task 5.3: Create Length of Stay Categories
Create Stay_Category: Short (≤3 days), Medium (4-7 days), Long (>7 days)

Analyze if longer stays correlate with higher risk

Task 5.4: Create Comorbidity Index
Create a composite score based on:

Number of previous admissions

Medication count

Age group

Analyze relationship with readmission risk

Task 5.5: Create Treatment Complexity Score
Combine Medication Count and Length of Stay

Test correlation with billing amounts

Task 5.6: Document Feature Engineering
Explain rationale for each new feature

Show before/after visualizations

Deliverable: New features added with supporting analysis.

PHASE 6: Insights, Dashboard & Recommendations
Objective: Synthesize findings and communicate to stakeholders.

Task 6.1: Answer Key Business Questions
What are the top 3 factors most strongly correlated with readmission risk?

Which medical conditions have the highest treatment costs?

Which admission types lead to the longest hospital stays?

Is there a relationship between age, gender, and readmission risk?

What patient profile represents the highest readmission risk?

Use visualizations and summary statistics to support each answer.

Task 6.2: Create Executive Summary
Write 300-500 words covering:

Key findings

Most significant risk factors

Cost drivers

Recommended actions

Task 6.3: Create Dashboard
Using matplotlib/seaborn, create a multi-panel dashboard with:

Overview statistics (total patients, avg cost, readmission rate)

Readmission risk distribution

Top 5 conditions by cost and risk

Key correlations

Insights summary

Task 6.4: Provide Actionable Recommendations
Provide at least 5 specific recommendations:

Patient Care: Which groups need more attention?

Resource Allocation: Where to focus resources?

Preventive Measures: How to reduce readmissions?

Cost Optimization: How to manage costs?

Data Collection: What additional data would help?

Deliverable: Complete analysis with executive summary, dashboard, and recommendations.

Use the provided `presentation_template.pptx` as your starting point.
Replace all [placeholders] with your findings.

6. D-Tale Integration Points
D-Tale is used as a supplementary tool at these key milestones:

Phase	D-Tale Usage
Phase 1	Initial exploration, data quality assessment
Phase 2	Validate cleaning, check missing value patterns
Phase 4	Interactive filtering, correlation exploration
Phase 6	Optional: Quick validation of findings
Example Commands:

```
import dtale

# Launch D-Tale
d = dtale.show(df)

# Access specific features in browser:
# - Describe: Summary statistics
# - Missing: Missing value analysis
# - Correlations: Correlation matrix
# - Charts: Interactive visualizations
# - Filter: Subset data interactively
```
💡 Remember: D-Tale is for exploration. Your final deliverables should be based on Pandas, Matplotlib, and Seaborn.

7. Deliverables Checklist
Students must submit:

□ Jupyter Notebook (notebooks/healthcare_eda.ipynb)
All phases completed

Code with comments

Markdown explanations

All visualizations

□ Cleaned Dataset (outputs/cleaned_data.csv)
Exported after Phase 2 cleaning

Includes engineered features from Phase 5

□ Executive Summary (outputs/executive_summary.md or .pdf)
1-2 pages

Key findings and recommendations

□ Dashboard (outputs/figures/dashboard.png)
Multi-panel visualization

Suitable for stakeholder presentation

□ Presentation (presentation.pptx)
5-10 slides

Summary for hospital leadership

8. Real-World Tips
"What Would a Data Analyst Do?"

Phase 1: Data Loading
"In a real project, you would spend 2-3 hours just understanding the data before writing any code. D-Tale helps speed this up by showing you distributions, missing values, and correlations instantly."

Phase 2: Data Cleaning
"Real-world data is never clean. You will spend 60-70% of your time here. Document every decision — your future self (and your manager) will thank you."

Phase 3-4: Analysis
"Do not just create charts — ask questions. 'Why is this distribution skewed?' 'What does this correlation mean for the business?'"

Phase 5: Feature Engineering
"Good features tell a story. 'Age Group' is more actionable than raw 'Age' because you can target interventions to specific groups."

Phase 6: Recommendations
"A chart without a recommendation is just a picture. Always tie your findings to business actions."

End of Project Guide

