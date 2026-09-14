 Healthcare EDA Project
Patient Readmission Risk Analysis

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-green)
![D-Tale](https://img.shields.io/badge/D--Tale-3.0%2B-orange)
![Status](https://img.shields.io/badge/Status-Active-success)

📖 Overview
An end-to-end Exploratory Data Analysis (EDA) project on a 500,000-record synthetic healthcare dataset. Students analyze patient data to uncover factors driving hospital readmissions and treatment costs, then deliver actionable recommendations.

Property	Value
Domain	Healthcare Analytics
Level	Intermediate
Duration	2-3 Weeks
Mode	Individual
Tools	Python, Pandas, NumPy, Matplotlib, Seaborn, D-Tale
🎯 Learning Objectives
By completing this project, you will be able to:

✅ Load and inspect large datasets (500K+ records) using Pandas

✅ Use D-Tale as a supplementary tool for interactive data exploration

✅ Identify and handle data quality issues (missing values, outliers, inconsistencies)

✅ Create professional visualizations using Matplotlib and Seaborn

✅ Perform univariate, bivariate, and multivariate analysis

✅ Engineer new features from existing data

✅ Derive business insights and provide actionable recommendations

✅ Create a dashboard suitable for stakeholder presentation


📊 Dataset
Source: Synthetic Datasets Repository

Property	Value
Direct CSV	synthetic_healthcare_20250901.csv
Records	500,000
Columns	22
Size	62.3 MB
Targets	Readmission Risk (classification), Total Cost (regression)

⚠️ Note: The CSV is hosted via Git LFS. If pd.read_csv() from the raw URL fails, download the file manually and load it locally. See SETUP_GUIDE.md.

Data Quality Challenges
As noted in the repository documentation, this dataset contains realistic data quality challenges:

🔸 Missing Values — Not missing at random (MNAR); follow realistic patterns

🔸 Outliers — Extreme but plausible values that require investigation

🔸 Entry Errors — Data-entry mistakes that must be identified and handled

🔸 Multiple Feature Types — Numerical, categorical, and datetime columns

## 📁 Repository Structure

```text
healthcare-eda-project/
│
├── README.md                      # This file
│
├── PROJECT_GUIDE.md               # Complete task documentation
│
├── SETUP_GUIDE.md                 # Environment setup instructions
│
├── HINTS.md                       # Optional hints per phase
│
├── RUBRIC.md                      # Evaluation criteria
│
├── requirements.txt               # Python dependencies
│
├── .gitignore                     # Git ignore rules
│
├── notebooks/
│   └── healthcare_eda.ipynb       # Student notebook (TEMPLATE)
│
├── data/
│   └── README.md                  # Data download instructions
│
└── outputs/                       # Student deliverable folder
    ├── figures/                   # Saved visualizations
    ├── cleaned_data.csv           # Exported clean dataset
    └── executive_summary.md       # Final report

```

🚀 Quick Start
1. Create Your Copy
Click the green "Use this template" button at the top of this repo → "Create a new repository".

Name it something like healthcare-eda-yourname

Set it to Private (recommended) or Public

Click Create repository

2. Clone Your Copy
bash
```
git clone https://github.com/<your-username>/healthcare-eda-yourname.git
cd healthcare-eda-yourname
```
4. Set Up Environment
bash
```
# Create virtual environment
python -m venv venv
```
# Activate on Windows:
```
venv\Scripts\activate
```
# Mac/Linux:
```
source venv/bin/activate
```

# Install dependencies
```
pip install -r requirements.txt
```
4. Launch Jupyter
bash
```
jupyter notebook
```

5. Open the Notebook
Open notebooks/healthcare_eda.ipynb and follow the instructions inside.

📋 Project Phases
Phase	Focus	Key Output
1	Data Loading & Inspection	Initial observations + D-Tale exploration

2	Data Cleaning	Clean dataset with documented decisions

3	Univariate Analysis	Distribution visualizations

4	Bivariate & Multivariate	Relationship insights

5	Feature Engineering	New business-relevant features

6	Insights & Reporting	Dashboard + Recommendations

See PROJECT_GUIDE.md for full task details.

📦 Deliverables

□ Completed Jupyter Notebook (notebooks/healthcare_eda.ipynb)

□ Cleaned dataset (outputs/cleaned_data.csv)

□ Executive Summary (outputs/executive_summary.md or .pdf)

□ Dashboard image (outputs/figures/dashboard.png)

□ Presentation (`presentation_template.pptx`) — Use this template

🎓 Submission
Submit your work as a single ZIP file containing:

Your notebook (with all cells executed)

Cleaned dataset

Executive summary

Dashboard image

Presentation (if completed)

Naming convention: FirstName_LastName_HealthcareEDA.zip

Submit via: (https://drive.google.com/drive/folders/1Blo6xGIF9rf6s88bF9T3QIAZYTlWSHHw?usp=sharing)

📚 Resources
Pandas Docs

Seaborn Docs

D-Tale Docs

Kaggle EDA Course

Full Project Guide

Setup Guide

Hints

⚙️ Requirements
See requirements.txt for the full list. Core libraries:

text
pandas>=2.0.0

numpy>=1.24.0

matplotlib>=3.7.0

seaborn>=0.12.0

dtale>=3.0.0

jupyter>=1.0.0

🏫 For Instructors

Full task list: PROJECT_GUIDE.md

Grading rubric: RUBRIC.md

Student hints: HINTS.md

Setup instructions: SETUP_GUIDE.md

📝 License

Educational use only. Dataset is synthetic and safe for classroom use.

Happy Analyzing! 📊
