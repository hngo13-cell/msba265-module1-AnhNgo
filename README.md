# MSBA 265 - Module 1 Homework

## Project Overview

This repository contains my MSBA 265 Module 1 homework project using the French Motor Third Party Liability Claims dataset from OpenML.

The purpose of this project is to perform exploratory data analysis, data quality verification, business data documentation, correlation analysis, distribution analysis, and production outlier filtering.

The project includes:

- Programmatic data download from OpenML
- Structural and data quality audits
- Raw boundary verification
- Business Data Dictionary
- Univariate skewness diagnostics
- Pearson correlation analysis
- Pearson correlation heatmap
- Distribution box plots and KDE histograms
- Written interpretation of distribution charts
- Tukey 1.5 × IQR outlier filtering
- Production outlier filtering script
- Final homework report

---

## Repository Structure

```text
msba265-module1-AnhNgo/
│
├── .gitignore
├── README.md
├── requirements.txt
├── Module1 Homework Report.pdf
│
├── data/
│   ├── download_data.py
│   ├── raw_business_data.csv
│   └── cleaned_business_data.csv
│
├── notebooks/
│   └── 01_eda_and_data_dictionary.ipynb
│
├── src/
│   └── clean_outliers.py
│
└── reports/
    ├── data_dictionary.csv
    └── figures/
        ├── correlation_heatmap.png
        └── feature_distributions.png
```
## Requirements

The project was developed using Python and Jupyter Notebook in Visual Studio Code.

Required Python packages are listed in:

`requirements.txt`

---

## Setup Instructions

### 1. Clone and Open the Repository

Open a terminal in Visual Studio Code.

Use `cd` to navigate to the folder where you want to save the project. For example:

```bash
cd C:\Users\YourName\Documents
```

Clone the GitHub repository:

```bash
git clone https://github.com/hngo13-cell/msba265-module1-AnhNgo.git
```

Move into the cloned project folder:

```bash
cd msba265-module1-AnhNgo
```

Open the project folder in Visual Studio Code:

1. Open Visual Studio Code.
2. Click **File > Open Folder...**
3. Select the `msba265-module1-AnhNgo` folder.
4. Click **Select Folder**.

The `msba265-module1-AnhNgo` project should now open in Visual Studio Code.

---

### 2. Create a Virtual Environment

In `msba265-module1-AnhNgo` project, open a new terminal in Visual Studio Code and run:

#### Windows

```powershell
python -m venv venv
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
.\venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

After activation, the terminal should indicate that the virtual environment is active.

---
### 3. Install Required Packages and Register the Jupyter Kernel

With the virtual environment activated, install the required packages:

```bash
python -m pip install --upgrade pip
```

Install all required packages:

```bash
pip install -r requirements.txt
```

---

## Execution Instructions

All commands below should be executed from the root project directory:

`msba265-module1-AnhNgo/`

---

### Step 1: Download the Raw Dataset

Run:

```bash
python data/download_data.py
```

This script downloads the French Motor Third Party Liability Claims dataset from OpenML and saves it as:

`data/raw_business_data.csv`

Expected dataset size:

`678,013 rows x 12 columns`

Expected terminal output should include:

```text
[+] Saved locally to: data/raw_business_data.csv
[+] Record Count: 678013 rows x 12 columns
```

---

### Step 2: Run the Jupyter Notebook

Open:

`notebooks/01_eda_and_data_dictionary.ipynb`

Before running the notebook, make sure it is using the Python interpreter from the project's virtual environment.

To select the correct kernel:

1. In the **top-right corner** of the notebook, click the current kernel name or **Select Kernel**.
2. Select **Python Environments...**.
3. Choose the Python environment named `venv`.

The correct environment should show a path similar to:

```text
venv\Scripts\python.exe
```

Visual Studio Code may also label this environment as **Recommended**.

After selecting it, confirm that `venv` appears in the top-right corner of the notebook.

Then click **Run All** to run all notebook cells from top to bottom.

The notebook performs the following analysis:

- Loads the French Motor Claims dataset
- Runs `df.info()` and `df.describe().T`
- Reviews data types and missing values
- Audits raw minimum and maximum values
- Creates a Business Data Dictionary
- Calculates univariate skewness
- Evaluates automated transformation recommendations
- Creates a Pearson correlation heatmap
- Creates distribution box plots and KDE histograms
- Provides written interpretation of the visual results

The notebook generates the following files:

```text
reports/data_dictionary.csv
reports/figures/correlation_heatmap.png
reports/figures/feature_distributions.png
```

---

## Data Quality Audit Results

The raw boundary audit produced the following results:

```text
DrivAge:
Minimum = 18
Maximum = 100

Exposure:
Minimum ≈ 0.0027
Maximum = 2.01

BonusMalus:
Minimum = 50
Maximum = 230
```

These checks were used to identify possible negative values, sentinel values, or other obvious data quality problems.

---

## Business Data Dictionary

The notebook creates a Business Data Dictionary containing:

- Feature Name
- Business Label
- Data Type
- Unit
- Null Count
- Unique Values
- Business Definition

The resulting file is saved as:

`reports/data_dictionary.csv`

---

## Correlation Heatmap

The Pearson correlation heatmap is created in the notebook and saved as:

`reports/figures/correlation_heatmap.png`

The heatmap is used to examine the strength and direction of linear relationships between numerical features.

---

## Distribution Analysis

The notebook creates four distribution charts:

1. Population Density Box Plot
2. Driver Age Histogram and KDE
3. BonusMalus Risk Index Box Plot
4. Vehicle Age Histogram and KDE

The combined figure is saved as:

`reports/figures/feature_distributions.png`

---

## Step 3: Run the Production Outlier Filtering Script

In terminal, run:

```bash
python src/clean_outliers.py
```

The script applies Tukey 1.5 × IQR filtering to the `Density` feature.

The script calculates:

```text
IQR = Q3 - Q1

Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
```

Expected output:

```text
============================================================
 PRODUCTION OUTLIER FILTERING REPORT
============================================================
Target Feature Filtered: Density
Initial Dataset Records: 678,013
Tukey IQR Valid Range: [-2,257.00, 4,007.00]
Outlier Records Removed: 77,566 (11.44%)
Final Cleaned Records: 600,447
```

The cleaned dataset is saved as:

`data/cleaned_business_data.csv`

---

## Expected Output Files

After successfully running the project, the following files should exist:

```text
data/raw_business_data.csv
data/cleaned_business_data.csv
reports/data_dictionary.csv
reports/figures/correlation_heatmap.png
reports/figures/feature_distributions.png
```

The raw dataset should contain:

`678,013 records`

The cleaned dataset should contain:

`600,447 records`

---

## Final Homework Report

The final written answers and required figures are compiled into:

`Module1 Homework Report.pdf`

The report includes:

- Raw boundary audit findings
- Exposure and Density/Area explanation
- ClaimNb skewness override explanation
- Pearson correlation heatmap
- Heatmap interpretation
- Distribution plots
- Three interpretation statements for each distribution chart
- Production outlier filtering results
