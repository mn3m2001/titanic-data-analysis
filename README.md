# Titanic: Data Cleaning & Survival Analysis

Final delivery documentation for the Titanic passenger-data cleaning and descriptive survival analysis.

**Prepared by:** Abdelmonem | **Report date:** 19 October 2026

![Survival comparisons](figures/08_survival_rates.png)

## Delivery scope

The analysis examines missing values, ticket fares, family relationships and survival patterns in the provided Titanic training data. The delivery contains an executed notebook, cleaned data, nine chart exports, a computed metrics summary and a detailed Arabic report. Processing decisions, validation results and analytical limitations are documented for review and reuse.

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

## Delivery files

| File or folder | Purpose |
|---|---|
| [Titanic_analysis_updated.ipynb](Titanic_analysis_updated.ipynb) | Complete analysis code and executed results |
| [Titanic_cleaning.ipynb](Titanic_cleaning.ipynb) | Historical source notebook retained for traceability |
| `train.csv` | Original supplied passenger dataset |
| [figures/](figures/) | Nine final PNG chart exports |
| [figures/original/](figures/original/) | Historical source figures retained for traceability |
| [output/titanic_cleaned.csv](output/titanic_cleaned.csv) | Cleaned data with engineered features |
| [output/analysis_summary.json](output/analysis_summary.json) | Computed analysis metrics |
| [Detailed Arabic PDF](output/pdf/Titanic_Client_Delivery_Report_AR.pdf) | Executive summary, scope, methods, chart interpretations, recommendations and handover checks |
| [English delivery PDF](output/pdf/Titanic_Client_Delivery_Report_EN.pdf) | English counterpart with the same findings, figures and delivery scope |
| [Editable Arabic report](output/Client_Delivery_Report_AR.md) | Editable counterpart of the final PDF |
| [Editable English report](output/Client_Delivery_Report_EN.md) | Editable counterpart of the English PDF |
| [CHANGELOG.md](CHANGELOG.md) | Changes compared with the original notebook |
| [requirements.txt](requirements.txt) | Notebook dependencies |

## Validation checks

The delivered notebook was executed from top to bottom: **15 code cells completed without errors**. Checks confirmed preservation of 891 rows and the survival labels, unique passenger IDs, documented remaining Cabin missingness and existence of all nine final chart exports. The cleaned CSV contains 19 columns.

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

## Analytical limitations and source documentation

The local `train.csv` was supplied with the project and uses the familiar Titanic training-data schema. Its original download location and redistribution terms were not independently documented in the supplied files. No new license is asserted for the dataset.

The training sample does not cover every person on the ship. Missing ages and cabin information may introduce bias. Median imputation can change distribution shapes. Ticket fares may reflect shared bookings. Survival comparisons are not adjusted causal effects, and no machine-learning model is trained or evaluated.

If extending this work to prediction, split the data first and fit imputation only on the training fold to avoid leakage.

## Tools

Python · pandas · NumPy · Matplotlib · Seaborn · Jupyter Notebook
