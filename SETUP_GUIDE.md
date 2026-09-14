# ⚙️ Setup Guide
## Healthcare EDA Project — Environment Setup

This guide walks you through setting up your environment to run the project notebook.

---

## 📋 Prerequisites

Before you begin, make sure you have:

- **Python 3.9 or higher** — [Download Python](https://www.python.org/downloads/)
- **Git** — [Download Git](https://git-scm.com/downloads)
- **A code editor** — We recommend [VS Code](https://code.visualstudio.com/) or [JupyterLab](https://jupyter.org/install)
- **A GitHub account** — [Sign up](https://github.com/join)

To check if Python is installed:
```bash
python --version
```

🚀 Step-by-Step Setup
Step 1: Create Your Repository from the Template
Go to the template repository: healthcare-eda-project

Click the green "Use this template" button → "Create a new repository"

Fill in:

Repository name: healthcare-eda-yourname (e.g., healthcare-eda-john)

Visibility: Private (recommended) or Public

Click Create repository

You now have your own copy of the project.

Step 2: Clone Your Repository
Open a terminal (Command Prompt on Windows, Terminal on Mac/Linux) and run:

```
git clone https://github.com/<your-username>/healthcare-eda-yourname.git
cd healthcare-eda-yourname
```
### Replace <your-username> with your GitHub username.


Step 3: Create a Virtual Environment
A virtual environment keeps your project dependencies isolated.

Windows:
```
python -m venv venv
venv\Scripts\activate
```

Mac/Linux:

```
python3 -m venv venv
source venv/bin/activate
```
You should see (venv) at the beginning of your terminal prompt.

Step 4: Install Dependencies
With your virtual environment activated, install the required libraries:

```
pip install -r requirements.txt
```

This will install pandas, numpy, matplotlib, seaborn, dtale, and jupyter.

Step 5: Launch Jupyter Notebook

```
jupyter notebook
```

This will open Jupyter in your default browser.

Step 6: Open the Project Notebook
In Jupyter, navigate to the notebooks/ folder

Click on healthcare_eda.ipynb

Follow the instructions inside

📊 Dataset Download
The dataset is hosted on GitHub via Git LFS and is 62.3 MB in size.

Option A: Load Directly from URL (Try This First)
In your notebook, use:

python
```
import pandas as pd

url = "https://raw.githubusercontent.com/leventbulut/synthetic-datasets/main/datasets/healthcare/synthetic_healthcare_20250901.csv"
df = pd.read_csv(url)
```
If this works, great! Move on.

Option B: Download Manually (If Option A Fails)
If the direct load fails due to Git LFS restrictions:

Go to the dataset page: synthetic_healthcare_20250901.csv

Click the "Download raw file" button

Save it to the data/ folder in your repo as synthetic_healthcare_20250901.csv

In your notebook, load it locally:

```
df = pd.read_csv('../data/synthetic_healthcare_20250901.csv')
```

⚠️ Do NOT commit the CSV file to your repository. It is 62 MB and GitHub has file-size limits. The .gitignore file already prevents this.

🛠️ Troubleshooting
Issue: pip install fails on Windows
Solution: Try upgrading pip first:

```
python -m pip install --upgrade pip
```
Issue: D-Tale does not open in browser
Solution: Manually open the URL shown in the notebook output, or run:

python
```
d = dtale.show(df)
d.open_browser()
```
Issue: Jupyter command not found
Solution: Try:

bash
```
python -m jupyter notebook
```
Issue: Kernel dies when loading 500K rows
Solution: This is rare but possible on low-RAM machines. Options:

Close other applications

Use df = pd.read_csv(url, nrows=100000) to load a sample first

Then increase to full size once your code works

Issue: ModuleNotFoundError: No module named 'dtale'
Solution: Make sure your virtual environment is activated, then:

bash
```
pip install dtale
```
Issue: Git LFS file shows as pointer text
If the CSV opens as a small text file with "version https://git-lfs...", it means LFS did not resolve. Use Option B above (manual download).

## 📁 Project Structure

After setup, your repo should look like this:

```text
healthcare-eda-yourname/
│
├── README.md
│
├── PROJECT_GUIDE.md
│
├── SETUP_GUIDE.md          ← You are here
│
├── HINTS.md
│
├── RUBRIC.md
│
├── requirements.txt
│
├── .gitignore
│
├── notebooks/
│   └── healthcare_eda.ipynb
│
├── data/
│   └── README.md
│
└── outputs/
    ├── figures/
    ├── cleaned_data.csv
    └── executive_summary.md
```

✅ Verify Your Setup
Run this in a new Jupyter cell to confirm everything works:

python
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import dtale

print("Pandas version:", pd.__version__)
print("NumPy version:", np.__version__)
print("Matplotlib version:", plt.matplotlib.__version__)
print("Seaborn version:", sns.__version__)
print("D-Tale version:", dtale.__version__)
print("\n✅ All libraries installed successfully!")
```
If you see all the versions printed without errors, you are ready to start the project.

💡 Tips for Success
Commit often. After every meaningful change, run:

bash
```
git add .
git commit -m "Describe your change"
git push
```
Do not commit the dataset. The 62 MB CSV is ignored via .gitignore.

Do not commit your venv/ folder. Also ignored.

Save outputs (figures, CSVs) in the outputs/ folder.

Use markdown cells in the notebook to explain what you did and why.

🆘 Need Help?
Check HINTS.md for task-specific tips

Review PROJECT_GUIDE.md for detailed task descriptions

Ask your instructor for clarification





