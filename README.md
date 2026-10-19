# Titanic: Data Cleaning and Survival Analysis

**Abdelmonem | Data Analysis**

Analysis of 891 Titanic passenger records using Python, pandas, NumPy, Matplotlib and Seaborn.

![Passenger survival counts](figures/01_survival_counts.png)

## Findings

- 342 survivors and 549 non-survivors: **38.38% overall survival**.
- Female survival: **74.20%**; male survival: **18.89%**.
- First-class survival: **62.96%**; second class: **47.28%**; third class: **24.24%**.

These are descriptive associations within the supplied sample, not causal effects or predictive accuracy.

## Files

| File | Purpose |
|---|---|
| [Titanic_cleaning.ipynb](Titanic_cleaning.ipynb) | Analysis code and saved outputs |
| [train.csv](train.csv) | Raw passenger data |
| [figures/](figures/) | Eight figures from the notebook |
| [Arabic PDF](output/pdf/Titanic_Report_AR.pdf) | Methods, all eight figures, interpretations and limitations |
| [English PDF](output/pdf/Titanic_Report_EN.pdf) | English analysis report |
| [Arabic text](output/Titanic_Report_AR.md) | Editable report |
| [English text](output/Titanic_Report_EN.md) | Editable report |
| [requirements.txt](requirements.txt) | Python dependencies |

## Run

Install the dependencies:

```bash
python -m pip install -r requirements.txt
python -m jupyterlab
```

Open `Titanic_cleaning.ipynb` from the project directory containing `train.csv`, select the Python kernel and choose **Restart Kernel and Run All**. On Colab, upload the CSV to the working directory. Figures and tables are displayed inside the notebook; the final cell saves the rate chart to figures/08_survival_rates.png; it does not export a cleaned CSV.

## Workflow

1. Inspect records, column types, summary statistics, duplicates and missing values.
2. Trim column names and embarkation text, and normalize empty embarkation entries.
3. Fill the two missing embarkation values with S, the observed mode.
4. Fill 177 missing ages with median age within passenger-class and sex groups.
5. Leave Cabin unchanged with 687 missing values. The cabin-feature lines are commented out.
6. Identify 116 fares above the overall IQR upper fence of 65.6344 without removing them.
7. Derive FamilySize, IsAlone and Is Child; the executed child condition is Age < 16.
8. Display survival counts, counts by sex and class, age histograms after imputation and for observed ages only, a fare boxplot and a focused Age/Fare/FamilySize pairplot.
9. Plot survival percentages by sex, class and traveling alone, label each bar, and save the rate chart.

## Limitations

Missing cabin records remain unresolved. Age imputation can affect distribution peaks, and the code does not preserve an imputation indicator. High fares may be valid shared bookings. The sample does not cover every passenger, and no predictive model or significance tests are included. The supplied files do not independently document the dataset download source or usage terms.

## Report layout

After the executive summary, both reports begin with Ages After Imputation, Observed Ages Only, and Age, Fare and Family Size. Their explanations appear before the corresponding figures.
