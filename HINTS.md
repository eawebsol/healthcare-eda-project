# 💡 Hints
## Healthcare EDA Project — Task Hints

This file contains optional hints for each phase. **Try to solve problems yourself before reading these.** The hints are meant to unblock you, not to give you the answer.

> 🎯 **Rule of Thumb:** Struggle for 15-20 minutes, then check the hint.

---

## 📘 Table of Contents

1. [Phase 1: Data Loading & Inspection](#phase-1-data-loading--inspection)
2. [Phase 2: Data Cleaning](#phase-2-data-cleaning)
3. [Phase 3: Univariate Analysis](#phase-3-univariate-analysis)
4. [Phase 4: Bivariate & Multivariate](#phase-4-bivariate--multivariate)
5. [Phase 5: Feature Engineering](#phase-5-feature-engineering)
6. [Phase 6: Insights & Reporting](#phase-6-insights--reporting)
7. [D-Tale Quick Reference](#d-tale-quick-reference)

---

## Phase 1: Data Loading & Inspection

### Hint 1.1 — Load the dataset

```python
import pandas as pd

url = "https://raw.githubusercontent.com/leventbulut/synthetic-datasets/main/datasets/healthcare/synthetic_healthcare_20250901.csv"
df = pd.read_csv(url)
```

If the download fails, see [SETUP_GUIDE.md](SETUP_GUIDE.md) → Option B.

### Hint 1.2 — Quick overview

- `df.head()` — First 5 rows
- `df.shape` — Rows and columns
- `df.info()` — Types and memory usage
- `df.describe()` — Summary statistics

### Hint 1.3 — Missing values

```python
# Count of missing values
df.isnull().sum()

# Percentage
(df.isnull().sum() / len(df)) * 100
```

### Hint 1.4 — Unique values in categorical columns

```python
# Identify categorical columns
cat_cols = df.select_dtypes(include='object').columns

# Loop and print unique values
for col in cat_cols:
    print(f"{col}: {df[col].nunique()} unique values")
    print(df[col].unique()[:10])  # First 10
    print("---")
```

### Hint 1.5 — Launch D-Tale

```python
import dtale
d = dtale.show(df)
d.open_browser()
```

---

## Phase 2: Data Cleaning

### Hint 2.1 — Handle missing values

Decide strategy based on column type:

```python
# Numeric column — fill with median
df['column'].fillna(df['column'].median(), inplace=True)

# Categorical column — fill with mode
df['column'].fillna(df['column'].mode()[0], inplace=True)

# Create "Unknown" category
df['column'].fillna('Unknown', inplace=True)
```

### Hint 2.2 — Detect outliers with IQR

```python
Q1 = df['column'].quantile(0.25)
Q3 = df['column'].quantile(0.75)
IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[(df['column'] < lower) | (df['column'] > upper)]
print(f"Outliers: {len(outliers)}")
```

### Hint 2.3 — Standardize categorical values

```python
# Strip whitespace and title-case
df['Gender'] = df['Gender'].str.strip().str.title()

# Replace values
df['Gender'] = df['Gender'].replace({'M': 'Male', 'F': 'Female'})
```

### Hint 2.4 — Convert to datetime

```python
df['Admission Date'] = pd.to_datetime(df['Admission Date'], errors='coerce')
df['Discharge Date'] = pd.to_datetime(df['Discharge Date'], errors='coerce')

# Calculate length of stay
df['Calculated_LOS'] = (df['Discharge Date'] - df['Admission Date']).dt.days
```

### Hint 2.5 — Duplicates

```python
# Count duplicates
df.duplicated().sum()

# Remove duplicates
df = df.drop_duplicates()
```

---

## Phase 3: Univariate Analysis

### Hint 3.1 — Histogram

```python
fig, ax = plt.subplots(figsize=(10, 5))
sns.histplot(df['Age'], bins=30, kde=True, ax=ax)
ax.set_title('Age Distribution')
ax.set_xlabel('Age')
plt.show()
```

### Hint 3.2 — Boxplot

```python
sns.boxplot(x=df['Billing Amount'])
plt.title('Billing Amount Distribution')
plt.show()
```

### Hint 3.3 — Bar chart for categorical

```python
df['Medical Condition'].value_counts().head(10).plot(kind='barh')
plt.title('Top 10 Medical Conditions')
plt.xlabel('Count')
plt.show()
```

### Hint 3.4 — Pie chart

```python
df['Admission Type'].value_counts().plot(
    kind='pie',
    autopct='%1.1f%%',
    figsize=(8, 8)
)
plt.title('Admission Type Distribution')
plt.ylabel('')
plt.show()
```

### Hint 3.5 — Summary statistics table

```python
num_cols = df.select_dtypes(include=['int64', 'float64']).columns

summary = df[num_cols].describe().T
summary['median'] = df[num_cols].median()
summary['mode'] = df[num_cols].mode().iloc[0]

print(summary)
```

---

## Phase 4: Bivariate & Multivariate

### Hint 4.1 — Grouped bar chart

```python
pd.crosstab(df['Admission Type'], df['Readmission Risk']).plot(
    kind='bar',
    stacked=True,
    figsize=(10, 6)
)
plt.title('Readmission Risk by Admission Type')
plt.ylabel('Count')
plt.xticks(rotation=0)
plt.show()
```

### Hint 4.2 — Boxplot for group comparison

```python
sns.boxplot(
    data=df,
    x='Medical Condition',
    y='Billing Amount'
)
plt.xticks(rotation=45, ha='right')
plt.title('Billing Amount by Medical Condition')
plt.tight_layout()
plt.show()
```

### Hint 4.3 — Scatter plot

```python
sns.scatterplot(
    data=df,
    x='Age',
    y='Billing Amount',
    hue='Readmission Risk',
    alpha=0.5
)
plt.title('Age vs Billing Amount')
plt.show()
```

### Hint 4.4 — Correlation heatmap

```python
plt.figure(figsize=(12, 8))
corr = df.corr(numeric_only=True)
sns.heatmap(corr, annot=True, cmap='coolwarm', fmt='.2f')
plt.title('Correlation Matrix')
plt.show()
```

### Hint 4.5 — Pairplot

```python
sns.pairplot(
    df[['Age', 'Billing Amount', 'Length of Stay', 'Readmission Risk']],
    hue='Readmission Risk',
    corner=True
)
plt.show()
```

> ⚠️ **Performance Tip:** For 500K rows, use `df.sample(5000)` before running pairplot or scatter plots. They will render much faster.

---

## Phase 5: Feature Engineering

### Hint 5.1 — Age groups

```python
bins = [0, 30, 45, 60, 100]
labels = ['Young Adult', 'Adult', 'Middle Age', 'Senior']
df['Age_Group'] = pd.cut(df['Age'], bins=bins, labels=labels)
```

### Hint 5.2 — Cost categories

```python
low = df['Billing Amount'].quantile(0.25)
high = df['Billing Amount'].quantile(0.75)

def cost_cat(x):
    if x < low:
        return 'Low'
    elif x > high:
        return 'High'
    else:
        return 'Medium'

df['Cost_Category'] = df['Billing Amount'].apply(cost_cat)
```

Or vectorized version (faster):

```python
df['Cost_Category'] = pd.cut(
    df['Billing Amount'],
    bins=[-float('inf'), low, high, float('inf')],
    labels=['Low', 'Medium', 'High']
)
```

### Hint 5.3 — Stay categories

```python
df['Stay_Category'] = pd.cut(
    df['Length of Stay'],
    bins=[-1, 3, 7, float('inf')],
    labels=['Short', 'Medium', 'Long']
)
```

### Hint 5.4 — Comorbidity index

```python
# Normalize each component
df['Prev_Adm_Norm'] = df['Previous Admissions'] / df['Previous Admissions'].max()
df['Med_Count_Norm'] = df['Medication Count'] / df['Medication Count'].max()

# Create score
df['Comorbidity_Index'] = (
    df['Prev_Adm_Norm'] + df['Med_Count_Norm']
) / 2
```

### Hint 5.5 — Treatment complexity

```python
df['Treatment_Complexity'] = (
    df['Medication Count'] * df['Length of Stay']
)
```

---

## Phase 6: Insights & Reporting

### Hint 6.1 — Top correlations with Readmission Risk

```python
# If Readmission Risk is categorical, encode it
df['Risk_Encoded'] = df['Readmission Risk'].astype('category').cat.codes

# Correlate with numerics
corr = df.corr(numeric_only=True)['Risk_Encoded'].sort_values(ascending=False)
print(corr.head(10))
```

### Hint 6.2 — Executive summary structure

```
# Executive Summary

## Overview
[1-2 sentences about the analysis]

## Key Findings
1. [Finding 1 with supporting number]
2. [Finding 2 with supporting number]
3. [Finding 3 with supporting number]

## Recommendations
1. [Action 1]
2. [Action 2]
3. [Action 3]

## Conclusion
[Final takeaway]
```

### Hint 6.3 — Multi-panel dashboard

```python
fig, axes = plt.subplots(2, 2, figsize=(16, 10))

# Panel 1: Readmission Risk distribution
df['Readmission Risk'].value_counts().plot(kind='bar', ax=axes[0, 0])
axes[0, 0].set_title('Readmission Risk Distribution')

# Panel 2: Top conditions
df['Medical Condition'].value_counts().head(5).plot(kind='barh', ax=axes[0, 1])
axes[0, 1].set_title('Top 5 Medical Conditions')

# Panel 3: Billing distribution
sns.histplot(df['Billing Amount'], bins=30, ax=axes[1, 0])
axes[1, 0].set_title('Billing Amount Distribution')

# Panel 4: Age vs Cost
axes[1, 1].scatter(df['Age'], df['Billing Amount'], alpha=0.3, s=5)
axes[1, 1].set_title('Age vs Billing Amount')

plt.tight_layout()
plt.savefig('../outputs/figures/dashboard.png', dpi=150, bbox_inches='tight')
plt.show()
```

---

## D-Tale Quick Reference

### Launch
```python
import dtale
d = dtale.show(df)
d.open_browser()
```

### Useful D-Tale Features

| Tab | What It Does |
|-----|--------------|
| **Describe** | Summary stats for all columns |
| **Missing** | Visualize missing value patterns |
| **Correlations** | Correlation heatmap + scatter matrix |
| **Charts** | Interactive histograms, bar charts, box plots |
| **Filter** | Subset data interactively |
| **Outliers** | Detect outliers with configurable thresholds |
| **Duplicates** | Find duplicate rows |

### Stop D-Tale
```python
d.kill()
```

Or from the browser UI: click the **X** on the D-Tale tab.

### Kill All D-Tale Instances
```python
dtale.instances()
# Returns dict of all running instances
# Kill each one:
for instance_id in dtale.instances():
    dtale.get_instance(instance_id).kill()
```

---

## 🧠 General Debugging Tips

### Issue: Kernel crashes on large operations
**Fix:** Sample the data first:
```python
df_sample = df.sample(10000, random_state=42)
```

### Issue: Slow plotting
**Fix:** Reduce data points:
```python
df.sample(5000).plot(...)
```

### Issue: Memory warning
**Fix:** Downcast dtypes:
```python
df['Age'] = df['Age'].astype('int8')
df['Billing Amount'] = df['Billing Amount'].astype('float32')
```

### Issue: Column names with spaces cause errors
**Fix:** Use bracket notation:
```python
df['Billing Amount']  # ✅ Works
df.Billing Amount     # ❌ Fails
```

---

## 📚 Additional Resources

- [Pandas Cheat Sheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [Seaborn Gallery](https://seaborn.pydata.org/examples/index.html)
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/index.html)
- [D-Tale Documentation](https://github.com/man-group/dtale)

---

**Remember:** These hints are a safety net, not a shortcut. Try first, then check. 💪
