# Titanic: Final Analysis & Delivery Report

Prepared by: Abdelmonem | 19 October 2026


## Final Delivery Report

### Executive summary

A dataset containing 891 passengers and 12 original fields was inspected, cleaned and analyzed. The objective is to provide usable data and explain survival patterns, with documented processing decisions and limitations that affect interpretation.

### Key findings

342 passengers survived (38.38%); 549 did not survive.
Female survival was 74.20%, compared with 18.89% for males.
Survival rates were 62.96% in first class, 47.28% in second class and 24.24% in third class.
Passengers with recorded relatives had a 50.56% survival rate, compared with 30.35% for passengers classified as traveling alone.

### Delivery status

The descriptive analysis, notebook execution and export of processed data and figures are complete. Execution and data-integrity checks passed, as detailed in the validation section. The delivery includes the files needed to review and reproduce the findings.

### Interpretation note

Findings apply to the dataset examined. Observed differences are descriptive associations that may involve several overlapping factors; they should not be treated as proven causes or individual predictions.


## 1. Scope and Deliverables

### Purpose of the analysis

Assess passenger-record quality, address missing values using a documented approach, and compare survival by sex, ticket class, age, family relationships and availability of cabin information. This report explains each figure and provides results that can be recalculated.

### Work completed

1. Inspected the data structure, types, duplicates and missing values.
2. Trimmed whitespace and standardized empty-text handling.
3. Imputed age and embarkation while recording which values were estimated.
4. Documented missing Cabin values and added an availability indicator.
5. Reviewed high fares and derived family and child indicators.
6. Produced nine figures and calculated survival counts and rates.
7. Exported processed data and a metrics summary, and validated execution.

### Scope boundaries

The delivery covers data cleaning, exploratory analysis, documentation and reproducibility. It does not include predictive-model training, causal-inference testing or reconciliation with an external historical database. Documentation of the original file download source and its terms was not available.

### How to use the delivery

Start with the executive summary and figures, then consult the cleaning methodology when evaluating data suitability. Use the CSV for further analysis and the notebook to review the code and reproduce results. Missingness indicators distinguish estimated values from recorded values.


## 2. Data Quality and Field Definitions

### Input quality overview

The input contains 891 rows and 12 columns. There are no exact duplicate rows, and every passenger identifier is unique. Age is missing in 177 records (19.87%), Cabin in 687 (77.10%) and Embarked in two (0.22%). All 891 passengers were retained after processing.

### Core fields

PassengerId: passenger identifier. Survived: 0 = did not survive; 1 = survived.
Pclass: ticket class, where 1 = first, 2 = second and 3 = third.
Sex and Age: sex and age in years. Name: passenger name.
SibSp and Parch: recorded relatives aboard, covering siblings/spouses and parents/children.
Ticket and Fare: ticket identifier and recorded fare.
Cabin: recorded cabin identifier, if available. Embarked: embarkation port.

### Checks applied

Checks covered required-column availability, uniqueness of PassengerId, Survived values restricted to 0 or 1, and Pclass values restricted to 1, 2 or 3. Fares were checked for non-negative values, and ages for an expected range. These are internal-consistency checks, not independent verification of every historical detail.

### Implications for analysis

Missing ages affect age-based analysis. Extensive missing cabin information means that a missing entry cannot be interpreted as the absence of a cabin. Fare may reflect a shared booking; it is not a measure of passenger income.


## 3. Cleaning and Processing Methodology

### Preserving the source

The raw file was preserved unchanged, and processing was performed on a separate dataframe. Surrounding whitespace was trimmed from text fields and column names, and empty text was converted to missing values.

### Age and embarkation imputation

177 missing ages were filled with the median within the combined sex and passenger-class group, with an overall median as a fallback. The median reduces sensitivity to extreme values but does not recover each passenger's true age. The two missing embarkation values were filled with the mode, S. AgeWasMissing and EmbarkedWasMissing identify estimated records.

### Cabin information

687 missing Cabin values were retained, and HasCabin was added to indicate whether a cabin was recorded. Cabin identifiers were not invented, and passengers were not removed because of missing cabin information. This remaining missingness is intentional and documented; the dataset is not completely free of missing values.

### High fares

The interquartile range (IQR) was calculated from the first and third quartiles. The upper fence, Q3 + 1.5 x IQR, is 65.6344; 116 records exceed it. These records were retained and flagged with FareHighOutlier. A statistically high value alone does not establish that a fare is erroneous.

### Derived features

FamilySize = SibSp + Parch + 1. IsAlone equals 1 when FamilySize equals 1. IsChild identifies passengers younger than 16; the count is 83 in this file, all with observed ages. These fields support comparisons without changing the survival outcome.


## 4.1 Survival Outcomes

![4.1 Survival Outcomes](../figures/01_survival_counts.png)

### How to read the figure

The horizontal axis divides passengers into non-survivors and survivors; the vertical axis shows passenger counts. Labels above the bars give the actual counts. This establishes the outcome imbalance: two outcome categories do not imply equal survival chances. Rates apply to the supplied training file only.

### Finding and interpretation

342 passengers survived and 549 did not; the overall survival rate is 38.38%. Non-survivors form the larger group.

This rate is a general reference for subsequent comparisons, not a fixed survival probability for every passenger.


## 4.2 Survival by Sex

![4.2 Survival by Sex](../figures/02_sex_survival_counts.png)

### How to read the figure

Within each sex category, compare the survivor and non-survivor bars. The larger number of male passengers affects absolute counts, so survival rates should be read alongside the figure. Observed associations may overlap with class and age; sex alone is not a causal explanation.

### Finding and interpretation

233 of 314 female passengers survived, compared with 109 of 577 male passengers. The rates are 74.20% and 18.89%, a difference of 55.31 percentage points.

Because group sizes differ, interpret rates together with counts. This comparison does not isolate overlapping effects of class and age.


## 4.3 Survival by Ticket Class

![4.3 Survival by Ticket Class](../figures/03_class_survival_counts.png)

### How to read the figure

The horizontal axis shows first, second and third class. Compare survivors and non-survivors within each class, then use survival rates to compare groups of different sizes. The higher number of deaths in third class must be considered alongside its larger passenger count. The figure does not isolate sex, age or passenger-location effects.

### Finding and interpretation

First class: 136 survivors out of 216; second class: 87 out of 184; third class: 119 out of 491. Survival rates are 62.96%, 47.28% and 24.24%, respectively.

Third class is the largest group and has the lowest survival rate in the sample. This descriptive comparison does not establish an independent causal effect of class.


## 4.4 Ages After Imputation

![4.4 Ages After Imputation](../figures/04_age_distribution.png)

### How to read the figure

Each bar covers a five-year age interval, with color distinguishing survival outcomes. KDE lines summarize distribution shape; they do not directly represent survival probabilities. Peaks around certain ages are affected by group-median imputation. More passengers at an age does not establish higher or lower survival chances.

### Finding and interpretation

Ages are concentrated among young people and adults. The figure includes 177 ages estimated using the median of the sex and class group.

Imputation affects distribution peaks. KDE lines do not represent survival rates or statistical confidence.


## 4.5 Observed Ages Only

![4.5 Observed Ages Only](../figures/05_age_observed_only.png)

### How to read the figure

This figure uses the same age intervals but excludes passengers whose ages were originally missing. Comparison with the preceding figure shows how imputation affects distribution shape. This sensitivity check does not eliminate missingness bias: passengers with known ages may differ from those with missing ages.

### Finding and interpretation

The figure includes 714 observed ages and excludes 177 estimated values. Differences from the previous figure show sensitivity to the imputation decision.

Exclusion is for this visual comparison only. The final dataset still retains every passenger; known ages may not represent the missing ages.


## 4.6 Ticket Fares by Class

![4.6 Ticket Fares by Class](../figures/06_fare_boxplot.png)

### How to read the figure

The line inside each box is the median; the box boundaries are the first and third quartiles. Whiskers extend to the most distant observations within 1.5 IQR of the quartiles. Points beyond them are statistical outliers, not confirmed errors. The left panel uses the original scale; the right changes the scale to make smaller values visible while retaining zero. Distances are not directly comparable across the two scales, and high fares are not automatically removed.

### Finding and interpretation

First class shows higher fares and a wider spread. All 116 values above the overall upper fence of 65.6344 were retained.

The right panel uses a symlog scale, which compresses large fares while retaining zero. Boxplot whiskers are calculated within each class; FareHighOutlier uses one overall threshold for the file.


## 4.7 Age, Fare and Family Size

![4.7 Age, Fare and Family Size](../figures/07_pairplot.png)

### How to read the figure

Each off-diagonal panel shows two variables, while diagonal panels show one-variable distributions. Color indicates survival; overlapping points show that the variables do not completely separate the outcomes. The matrix contains selected analytical variables; passenger identifiers are not meaningful for this comparison. Fare is strongly skewed, FamilySize is discrete and Age contains imputed values, so the figure alone cannot establish a linear or causal relationship.

### Finding and interpretation

Survivors and non-survivors overlap across age, fare and family size. There is no complete visual separation of the two outcomes.

Estimated ages, skewed fares and discrete family sizes limit interpretation. These patterns alone should not be turned into prediction rules or causal claims.


## 4.8 Comparing Survival Rates

![4.8 Comparing Survival Rates](../figures/08_survival_rates.png)

### How to read the figure

The vertical axis shows the percentage surviving within each group, not the total passenger count. The n label gives group size, making comparisons clearer than counts alone. IsAlone = 1 means no relatives are recorded in SibSp and Parch. Rate differences do not prove that traveling with family caused survival. No confidence intervals or significance tests are shown.

### Finding and interpretation

Passengers with recorded relatives had a survival rate of 50.56%, compared with 30.35% for those classified as alone, a gap of 20.21 percentage points. The other panels show survival rates by sex and class.

n is the group size. IsAlone concerns recorded relatives, not the absence of friends or acquaintances. These comparisons do not include confidence intervals.


## 4.9 Cabin Records and Survival

![4.9 Cabin Records and Survival](../figures/09_cabin_information.png)

### How to read the figure

The first panel shows survivor and non-survivor counts by availability of a cabin record; the second shows survival rates within those groups. HasCabin measures recording completeness, not cabin ownership or occupancy. The class cross-tabulation in the notebook helps identify overlap between ticket class and record availability; an independent causal effect should not be inferred.

### Finding and interpretation

Cabin information is available for 204 passengers, of whom 136 survived (66.67%). It is missing for 687 passengers, of whom 206 survived (29.99%).

HasCabin measures record completeness. The rate difference may be associated with class and recording practices; it does not prove that a recorded cabin identifier caused survival.


## 5. Conclusions and Recommendations

### Main conclusions

Survival rates differ clearly by sex and ticket class, and are higher among passengers with recorded relatives than among those classified as alone. Age-distribution interpretation is affected by imputation, and cabin information remains extensively incomplete. Counts alone cannot fairly compare differently sized groups; rates and sample sizes are essential.

### Recommendations for using the data

1. Use the cleaned CSV for analysis and preserve the raw source.
2. Retain missingness indicators when analyzing age or embarkation.
3. Disclose incomplete Cabin records when presenting related findings.
4. Review booking context or source records before removing high fares.
5. Report group sizes and survival rates together.

### Suggested additional analysis

If decisions require adjusted estimates, examine interactions among sex, class and age, and add confidence intervals or a suitable statistical model. This requires additional scope; no such results are included in the current delivery.

### If a predictive model is developed later

Split the data first, learn imputation medians and the mode from training data only, and evaluate performance on unseen data. This analysis does not demonstrate the accuracy of a model that has not been built or tested.


## 6. Validation and Delivery Checklist

### Validation results

All 15 code cells executed sequentially without errors. All 891 passengers were retained; PassengerId remained unique and Survived values were unchanged. Every field is complete after processing except Cabin, in line with the documented decision. Checks confirmed that HasCabin matches Cabin availability, that all nine figures exist and that the processed data and metrics summary were exported.

### Main deliverables

This report: executive summary, methodology, figures and conclusions.
Notebook: complete code and executed results for review and reproduction.
Cleaned CSV: 891 rows and 19 columns, including the original fields and seven derived fields.
Figures: nine high-resolution PNG exports, one for each analysis presented.
Metrics summary: calculated indicators in JSON format.
README: usage instructions and requirements.

### Delivery controls

Successful checks demonstrate execution within the stated scope; they do not remove data limitations. The raw file is preserved, and indicators document estimates and missing information. Reproduction instructions are provided, and results can be recalculated from the same source.


## 7. File Guide and Reproduction

### File locations

The notebook is Titanic_analysis_updated.ipynb in the project directory. The raw data is train.csv. Figures are in figures/, processed data is in output/ and reports are in output/pdf/. Historical versions and the change log are technical references and do not form part of the reported conclusions.

### Reproducing the analysis

Install the libraries in requirements.txt in a suitable Python environment. Open the notebook with the project directory as its working directory, select the Python kernel and choose Restart Kernel and Run All. A Validation passed message should appear and data and figure exports should be regenerated. On Colab, upload train.csv and the notebook to the same working directory, and download outputs before the session ends.

### Checks on receipt

The cleaned CSV should contain 891 rows and 19 columns, and there should be nine final figures. Confirm the 38.38% survival rate and 342 survivors against analysis_summary.json. The 687 remaining missing Cabin values are expected and do not indicate an execution failure.

### Version documentation

Report date: 19 October 2026. This report was prepared from the executed notebook outputs and the accompanying raw file. analysis_summary.json is the numerical reference; requirements.txt documents the runtime requirements. This is the English counterpart of the Arabic final delivery report.
