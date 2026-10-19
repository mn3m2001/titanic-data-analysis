# Titanic Passenger Survival Analysis

Prepared by Abdelmonem | 20 October 2026

## Survival patterns at a glance

### Figure 1. Comparing survival rates

![Comparing survival rates](../figures/08_survival_rates.png)

The vertical axis shows the percentage surviving within each group, with values labeled above the bars. Female survival was 74.20%, compared with 18.89% for males. Rates fell from 62.96% in first class to 24.24% in third class. Passengers with recorded relatives had 50.56% survival, versus 30.35% among those classified as alone. These are descriptive associations, not proven causes.

### What stands out?

The largest visible difference is between sex groups, alongside a clear ticket-class gradient. The report presents all eight figures and their findings first, followed by data quality, cleaning decisions, limitations and reproduction steps.


## Who survived? Sex and ticket class

### Figure 2. Survival by sex

![Survival by sex](../figures/02_sex_survival_counts.png)

Blue indicates non-survivors and orange indicates survivors. Of 314 females, 233 survived; of 577 males, 109 survived. The survival-rate gap is 55.31 percentage points. Because group sizes differ, read rates alongside counts. This comparison does not isolate class or age effects.

### Figure 3. Survival by ticket class

![Survival by ticket class](../figures/03_class_survival_counts.png)

First class: 136 survivors out of 216 (62.96%). Second class: 87 out of 184 (47.28%). Third class: 119 out of 491 (24.24%). Third class is the largest group and has the lowest survival rate in the sample. Read deaths in the context of group size; the result does not establish an independent causal effect of class.


## Age: the effect of imputation

### Figure 4. Ages after imputation

![Ages after imputation](../figures/04_age_distribution.png)

Each bar spans five years. This view includes all 891 passengers, including 177 ages filled using sex-and-class group medians. KDE lines summarize distribution shape, not survival rates. Imputation may produce peaks at median ages; compare with observed ages below.

### Figure 5. Observed ages only

![Observed ages only](../figures/05_age_observed_only.png)

This view includes 714 ages recorded in the raw data and excludes 177 estimated ages from this figure only. No rows are removed from the cleaned dataset. Differences reveal sensitivity to imputation, but do not eliminate missingness bias: known ages may differ from missing ages.


## Age, fare and family relationships

### Figure 6. Age, fare and family size

![Age, fare and family size](../figures/07_pairplot.png)

Off-diagonal panels compare two variables: column labels identify the horizontal axis and row labels the vertical axis. Diagonal panels show individual distributions, and color identifies survival. Overlapping points mean these variables do not fully separate survivors from non-survivors. Age includes imputed values, fares are skewed and family size is discrete. Visual relationships do not demonstrate causation or predictive accuracy.

### How to use this view

Use the matrix to explore patterns and overlap, then return to numerical comparisons. Passenger identifiers and binary features are excluded; the focus is age, ticket fare and family size.


## Ticket fares: differences by class

### Figure 7. Ticket fares by class

![Ticket fares by class](../figures/06_fare_boxplot.png)

The line inside each box is the median; box boundaries are the first and third quartiles. Whiskers extend to the most distant observations within 1.5 IQR of the box boundaries. Outside points are statistical outliers, not confirmed errors. First class shows higher fares and wider variation, with a maximum near 512.33. Whiskers are class-specific; the code separately applies an overall threshold of 65.6344, identifying and retaining 116 records.

### Treatment of high fares

All 116 high-fare records remain in the analysis; statistical detection does not prove error. Fare may reflect a shared booking and is not personal income. The figure uses the original, non-logarithmic scale.


## The overall survival outcome

### Figure 8. Overall survival outcomes

![Overall survival outcomes](../figures/01_survival_counts.png)

Survived = 0 means did not survive; 1 means survived. There were 342 survivors and 549 non-survivors, giving an overall survival rate of 38.38%. Labels above the bars are passenger counts, not percentages. This rate is a general reference for group comparisons, not a fixed probability for each passenger.

### Visual findings in context

Survival in this sample is associated with sex, class and recorded relatives. Age analysis demonstrates why observed and imputed values should be distinguished when interpreting distribution shapes. Outcomes overlap in the pairplot, and potentially legitimate high fares remain in the dataset.


## Data and cleaning methodology

### Data scope and initial inspection

The raw train.csv file contains 891 rows and 12 columns. The code displays head, info and describe, and counts exact duplicates; there are none. Findings apply to the supplied training sample, not every passenger on the ship.

### 1. Working copy and text cleanup

The code creates df_clean from df, strips column names and Embarked values, and converts empty embarkation text to missing values. The raw source remains unchanged.

### 2. Age and embarkation imputation

Age is missing in 177 records (19.87%) and is filled using the median within each Pclass/Sex group. Embarkation is missing in two records (0.22%); the code calculates the mode and explicitly fills them with S. No permanent age-imputation flag is added; the observed-age chart uses raw df missingness.

### 3. Cabin records and high fares

687 Cabin values remain missing (77.10%). The Has_Cabin creation and Cabin removal lines are commented out and do not execute. The code calculates the IQR and displays fares above 65.6344; it neither deletes them nor creates a permanent outlier flag.


## Variables and interpretation limits

### Core fields

Survived: 0 = did not survive, 1 = survived. Pclass: ticket class from 1 to 3. Sex and Age: sex and age in years. SibSp: siblings/spouses; Parch: parents/children aboard. Fare: recorded price; Cabin: recorded cabin identifier; Embarked: embarkation port. PassengerId, Name and Ticket are identifying fields.

### Derived features

FamilySize = SibSp + Parch + 1. IsAlone equals 1 when recorded family size is 1; it does not imply the absence of friends. Is Child uses Age < 16 and identifies 83 passengers, all with observed ages in this file. The code comment still says >16, while the actual operation uses <16. The working dataframe contains 15 columns.

### What limits the findings?

Missing Cabin information does not mean no cabin existed. Imputation does not recover true ages, and missing-age records may differ from observed-age records. Fare can reflect a shared booking. No confidence intervals, significance tests or adjusted models are included; plots do not demonstrate causation or predictive accuracy. The available files do not independently document the original download source or usage terms.


## Recommendations and handover

### Recommendations

Preserve raw data and disclose age imputation and Cabin missingness when presenting results. Read rates alongside group sizes, and review context before deleting high fares. Further analysis could examine interactions among sex, class and age; that work is outside this delivery. For future prediction, split data first and fit imputation on training data only.

### File checklist

Titanic_cleaning.ipynb: code, tables and figures.
train.csv: raw data. figures/: eight chart exports.
output/pdf/: Arabic and English PDF reports.
output/: editable report versions.
README.md and requirements.txt: instructions and dependencies.

### Run and verify

Install requirements.txt, open the notebook from the project directory containing train.csv, select Python and choose Restart Kernel and Run All. In Colab, upload the CSV to the working directory. Verify 891 passengers, 342 survivors, 687 remaining missing Cabin values and eight displayed figures. The last cell saves the percentage chart under figures/; the code does not export a cleaned CSV.
