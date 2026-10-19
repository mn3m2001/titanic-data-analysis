# Changes from the original notebook

The original `Titanic_cleaning.ipynb` is preserved byte-for-byte.
The complete revised code is in `Titanic_analysis_updated.ipynb`.

1. Replaced the fixed Google Drive path with a working-directory-relative CSV path.
2. Added schema, value, unique passenger and missing-value checks.
3. Kept grouped age-median imputation; added a fallback and missingness indicators.
4. Retained Cabin as recorded and added HasCabin; explicitly documented remaining missing values.
5. Retained high fares, added an IQR flag and documented the threshold.
6. Renamed Is Child to IsChild, corrected the age comment, separated observed and imputed child counts.
7. Added readable labels and automatic PNG exports; original seven embedded images are also archived.
8. Replaced the duplicate age histogram with an observed-age sensitivity comparison.
9. Focused the pairplot on Age, Fare and FamilySize; excluded passenger identifiers.
10. Added survival-rate comparisons and cabin-record analysis with sample sizes and caveats.
11. Added Arabic explanations below every revised chart and computed conclusions.
12. Added cleaned CSV/JSON exports and end-of-run integrity checks.

These changes extend a descriptive analysis. No predictive model or causal claim is introduced.

## Final delivery reporting - 19 October 2026

Reframed the PDF and README as client-facing delivery documentation. Added scope, an executive summary, validation criteria, recommendations and a handover guide. Removed the historical-chart appendix from the final report; source figures remain available for traceability. Added an editable Arabic report. Analytical code, data and computed findings are unchanged.
