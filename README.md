# Titanic: Data Cleaning & Survival Analysis

A reproducible Python portfolio project that turns passenger records into a documented cleaning workflow and interpretable survival comparisons.

**Author:** Abdelmonem — Data Analyst & Aspiring Data Scientist

![Survival comparisons](figures/08_survival_rates.png)

## Project overview

The analysis examines missing values, ticket fares, family relationships and survival patterns in the provided Titanic training data. The revised notebook includes complete code, Arabic explanations below every chart, a change map and automatically exported results. The original notebook is preserved.

### Questions explored

- How complete are the passenger records, and how should missing values be handled?
- How do survival counts and rates vary by sex and passenger class?
- How does age imputation affect the age distribution?
- How do family size and recorded cabin information relate to survival?
- Are high fares necessarily data errors?

## Key findings

- **891 passengers**, **342 survivors**, **38.38% overall survival**.
- Female survival was **74.20%**, compared with **18.89%** for males.
- Survival rates were **62.96%** in first class, **47.28%** in second class and **24.24%** in third class.
- **177 missing ages** were filled using median age within passenger-class and sex groups, with missingness preserved in an indicator.
- **2 missing embarkation values** were filled with the most frequent port.
- **687 missing cabin records** remain explicitly documented. `HasCabin` measures whether a cabin was recorded, not whether a passenger had one.
- High ticket fares are flagged with the IQR rule and retained for analysis.

These are descriptive associations within the supplied training sample. They do not establish causation or predictive performance.

## Repository contents

| File or folder | Purpose |
|---|---|
| [Titanic_analysis_updated.ipynb](Titanic_analysis_updated.ipynb) | Complete revised notebook with executed results and marked changes |
| [Titanic_cleaning.ipynb](Titanic_cleaning.ipynb) | Preserved original work |
| `train.csv` | Original supplied passenger dataset |
| [figures/](figures/) | Nine revised PNG chart exports |
| [figures/original/](figures/original/) | Seven figures extracted from the original notebook |
| [output/titanic_cleaned.csv](output/titanic_cleaned.csv) | Cleaned data with engineered features |
| [output/analysis_summary.json](output/analysis_summary.json) | Computed analysis metrics |
| [Detailed Arabic PDF](output/pdf/Titanic_Analysis_Report_AR.pdf) | Cleaning steps, charts, interpretation and original-chart appendix |
| [CHANGELOG.md](CHANGELOG.md) | Changes compared with the original notebook |
| [requirements.txt](requirements.txt) | Notebook dependencies |

## Run locally

Use Python 3.12 or a compatible Python environment:

```bash
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m jupyterlab
```

Open `Titanic_analysis_updated.ipynb` with this repository as the working directory, select the Python kernel and choose **Restart Kernel and Run All**. `train.csv` must be in that working directory. Outputs are saved under `figures/` and `output/`.

On Google Colab, upload the revised notebook and `train.csv` to the same working directory. Download generated outputs before the temporary session ends.

## Cleaning decisions

1. Keep the raw dataframe and source CSV unchanged.
2. Validate column availability, passenger identifiers and expected value ranges.
3. Trim surrounding whitespace and normalize empty text values.
4. Fill embarkation with the observed mode and age with grouped medians, tracking both imputations.
5. Retain missing cabin information and derive `HasCabin`.
6. Flag high fares without automatically removing legitimate expensive tickets.
7. Derive `FamilySize`, `IsAlone` and `IsChild`; distinguish observed and imputed ages.
8. Compare both counts and rates, annotate charts and export reproducible results.

## Limits and data provenance

The local `train.csv` was supplied with the project and uses the familiar Titanic training-data schema. Its original download location and redistribution terms were not independently documented in the supplied files. No new license is asserted for the dataset.

The training sample does not cover every person on the ship. Missing ages and cabin information may introduce bias. Median imputation can change distribution shapes. Ticket fares may reflect shared bookings. Survival comparisons are not adjusted causal effects, and no machine-learning model is trained or evaluated.

If extending this work to prediction, split the data first and fit imputation only on the training fold to avoid leakage.

## Tools

Python · pandas · NumPy · Matplotlib · Seaborn · Jupyter Notebook
