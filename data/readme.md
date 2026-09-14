# 📊 Data Folder

This folder is for storing the raw dataset locally.

---

## ⚠️ Important

The dataset is **62.3 MB** — it is **NOT committed to this repository** (see `.gitignore`). You must either load it directly from the URL or download it manually.

---

## Option A: Load Directly from URL (Recommended)

In your notebook, load the dataset with:

```python
import pandas as pd

url = "https://raw.githubusercontent.com/leventbulut/synthetic-datasets/main/datasets/healthcare/synthetic_healthcare_20250901.csv"
df = pd.read_csv(url)
```

If this works, you do not need to download anything. Continue with the notebook.

---

## Option B: Manual Download (If Option A Fails)

If the direct URL fails (common with Git LFS), follow these steps:

### Step 1: Download the CSV

1. Go to the dataset page:  
   [synthetic_healthcare_20250901.csv](https://github.com/leventbulut/synthetic-datasets/blob/main/datasets/healthcare/synthetic_healthcare_20250901.csv)
2. Click the **"Download raw file"** button (top-right of the file viewer)
3. Save the file to this folder (`data/`) with the name:
   ```
   synthetic_healthcare_20250901.csv
   ```

### Step 2: Load Locally in the Notebook

Replace the URL load with a local path:

```python
import pandas as pd

df = pd.read_csv("../data/synthetic_healthcare_20250901.csv")
```

> 📌 **Note:** The `../` is needed because the notebook is inside `notebooks/`, so it goes up one level to the repo root, then into `data/`.

---

## Dataset Details

| Property | Value |
|----------|-------|
| **Source** | [Synthetic Datasets Repository](https://github.com/leventbulut/synthetic-datasets) |
| **Records** | 500,000 |
| **Columns** | 22 |
| **Size** | 62.3 MB |
| **License** | Educational / Research Use |
| **Format** | CSV |

### Expected Columns

| Column | Type | Description |
|--------|------|-------------|
| PatientID | String | Unique patient identifier |
| Age | Integer | Patient age in years |
| Gender | Categorical | Patient gender |
| Medical Condition | Categorical | Primary diagnosis |
| Admission Type | Categorical | Emergency, Urgent, Elective, etc. |
| Admission Date | Datetime | Date of admission |
| Discharge Date | Datetime | Date of discharge |
| Length of Stay | Integer | Duration in days |
| Billing Amount | Float | Total treatment cost |
| Test Results | Categorical | Medical test outcomes |
| Readmission Risk | Categorical | Risk score/category |
| Previous Admissions | Integer | Number of prior hospitalizations |
| Insurance Type | Categorical | Patient's insurance coverage |
| Medication Count | Integer | Number of prescribed medications |

> 📌 Column names may vary slightly. Always inspect the dataset first with `df.columns`.

---

## Do NOT Commit the CSV

The `.gitignore` file at the repo root contains:

```
data/*.csv
!data/README.md
```

This means:
- ✅ CSV files in `data/` are ignored by Git
- ✅ This `README.md` is still tracked

If you accidentally commit the CSV, remove it with:
```bash
git rm --cached data/synthetic_healthcare_20250901.csv
```

Then commit the removal.

---

## ✅ Verify the Dataset Loaded Correctly

After loading, run:

```python
print("Shape:", df.shape)
print("Columns:", list(df.columns))
df.head()
```

You should see:
- Shape: `(500000, 22)`
- A list of 22 column names
- The first 5 rows of data

If you see this, you are ready to start **Phase 1** in the notebook.

---

**Happy Analyzing! 📊**
