# Tamweel Lite — Interpretability & Calibration Report

**Course:** Advanced Machine Learning Methods (SDA-DSC-211)  
**Project:** Tamweel Lite  
**Lab:** 04 — Explainability, Calibration, and Decision Review

## 1. Source, Model, and Data Roles

This report documents the interpretation, probability calibration, stability assessment, and review-capacity analysis performed during Lab 04.

**Explanation source:** To be confirmed from the notebook output (`LIVE` or `EDUCATIONAL_EXAMPLE`).

The prediction task is to estimate whether an applicant will experience default within 90 days after submitting a financing application.

The workflow separates the following data roles:

- **Fit:** Used to train the predictive model.
- **Calibration:** Used to fit the sigmoid probability calibrator.
- **Policy:** Used to select and evaluate the review decision threshold.
- **Evaluation:** Used to assess model behavior without refitting the model or calibrator.

Time ordering, customer separation, and the 90-day outcome maturity requirement are essential safeguards against data leakage.

The exact row counts, unique customer counts, positive cases, model hyperparameters, and date boundaries for each role must be copied from the saved Lab 04 outputs.

The evaluation conducted in this lab is an intermediate diagnostic assessment, not the final course test.

## 2. Global and Local Interpretability

### Global feature importance

The project considers three complementary explanation approaches:

**Gain importance** measures how much a feature contributes to the model's tree-based splitting improvements.

**Permutation importance** evaluates how predictive performance changes when a feature's values are shuffled.

**SHAP** estimates individual feature contributions to a model prediction relative to a reference prediction.

The reported permutation-importance results include:

| Feature | Average Precision decrease |
|---|---:|
| `bureau_score` | 0.1270 |
| `dti` | 0.0690 |

These results indicate that `bureau_score` and `dti` were important predictive features in the evaluated model.

Feature importance describes model dependence, not a causal relationship between a feature and default.

### SHAP interpretation

For a model explained in raw log-odds units, SHAP contributions are additive:

`Model raw output = Base value + Sum of SHAP values`

Positive contributions increase the model's raw predicted default risk relative to its reference value, while negative contributions decrease it.

Correlated features can share predictive information, making their individual contributions sensitive to the explanation method and background data.

The SHAP background should come from the training data, and the additivity check should be verified using the saved notebook output.

### Local explanation

A local explanation describes one selected application rather than the entire model.

The application should be selected using a documented rule that does not depend on knowing its eventual default outcome.

Up to three positive contributing factors may be reported, together with their SHAP values and whether their original inputs were imputed.

**Local case details to complete from Lab 04:**

- Application identifier: Not yet verified
- Selection rule: Not yet verified
- Positive contributing factors and values: Not yet verified
- Imputation status: Not yet verified

These SHAP explanations refer to the underlying predictive model and must not automatically be interpreted as explanations of the calibrated probability.

## 3. Calibration Evidence

Sigmoid calibration was applied to improve the relationship between predicted probabilities and observed event frequencies.

The calibrator must be fitted on calibration data separate from the evaluation data.

### Reported calibration results

| Metric | Before calibration | After calibration |
|---|---:|---:|
| Average Precision (AP) | 0.258677 | 0.258677 |
| Brier Score | 0.113027 | 0.067112 |
| Expected Calibration Error (ECE) | 0.146871 | 0.022486 |
| Log-loss | Not yet verified | Not yet verified |
| ROC-AUC | Not yet verified | Not yet verified |

The reported results show a substantial improvement in Brier Score and ECE after sigmoid calibration.

Average Precision remained unchanged, suggesting that the calibration transformation preserved the ranking behavior measured by AP in this evaluation.

However, improved Brier Score and ECE do not establish perfect calibration.

The final report must additionally record the evaluation sample size, number of positive outcomes, and the observed counts within each of the ten calibration bins.

## 4. Stability and Uncertainty

The lab considers stability through customer-level bootstrap resampling.

Customer-level sampling is important because repeated applications from the same customer may not be independent.

For a paired comparison, the same bootstrap samples should be used to compare the original and calibrated predictions, while keeping the predictive model and calibrator fixed.

The following details must be verified from the notebook:

- Number of valid bootstrap draws
- Bootstrap interval bounds
- Metrics compared
- Differences between evaluation periods
- Whether the `bureau_score ±1` sensitivity test was performed

Bootstrap intervals describe uncertainty in an estimated evaluation metric under the resampling procedure.

They are not guarantees of future model performance and should not be interpreted as confidence intervals for an individual applicant's probability of default.

## 5. Threshold and Review-Capacity Analysis

The review decision is based on the rule:

`Flag for review if score >= threshold`

The review-capacity constraint is **12% per evaluation period**.

The near-threshold diagnostic region uses a score margin of **±0.02** around the decision threshold.

This region identifies applications whose scores are close to the operational decision boundary. It is a diagnostic region, not a statistical confidence interval.

### Reported review-capacity findings

The previously observed Lab 04 output included:

| Item | Result |
|---|---:|
| Reported threshold | 0.588195 |
| Flagged applications | 68 |
| Overall capacity | 70 |
| 2024 Q3 near-threshold review candidates | 109 |
| 2024 Q3 review capacity | 100 |
| 2024 Q4 near-threshold review candidates | 122 |
| 2024 Q4 review capacity | 107 |

Although the reported flagged count remained within the overall capacity in that output, the near-threshold review workload exceeded the available capacity in two periods.

The diagnostic therefore indicated:

**`CAPACITY_REVIEW_REQUIRED`**

This status highlights an operational limitation. It should not be treated as a software execution error or silently changed into a passing result.

A revised review policy would need to be developed and evaluated separately before claiming that the additional workload is operationally feasible.

The raw threshold, transported threshold, per-period flagged counts, near-threshold counts, and deduplicated union totals should be verified from the notebook before final submission.

## 6. Interpretation and Decision Rationale

**Global versus local explanations:** Global explanations identify features that influence model performance across the dataset, whereas local explanations describe contributions to one particular prediction.

**SHAP units:** When SHAP is calculated on the raw model output, contributions are measured in log-odds rather than calibrated probabilities.

**Limits of explanations:** Feature contributions reflect model behavior and associations. They do not prove causation or justify automatic financing decisions.

**Calibration evidence:** Brier Score improved from 0.113027 to 0.067112, and ECE decreased from 0.146871 to 0.022486. AP remained at 0.258677.

**Stability limitations:** Bootstrap analysis can assess sensitivity to the observed customer sample, but it cannot guarantee future performance or eliminate dataset shift.

**Capacity impact:** Near-threshold review candidates may create additional workload beyond the standard flagged-application count. The reported capacity exceedances require explicit documentation and further policy evaluation.

## 7. Limitations and Required Evidence

The project uses synthetic financing data for educational purposes only.

The following evidence must be retained with the report:

- Executed Lab 04 notebook
- Explanation source and model configuration
- Data-role counts and validation boundaries
- Global and local explanation outputs
- Calibration metrics and ten-bin reliability results
- Bootstrap results and valid draw counts
- Threshold and per-period capacity diagnostics

Values marked as not yet verified must be completed from the actual notebook outputs rather than replaced with illustrative numbers.

## 8. Conclusion

Lab 04 demonstrates how predictive performance, interpretability, calibration, and operational constraints contribute to responsible model evaluation.

The observed sigmoid calibration results improved probability-quality metrics without changing the reported Average Precision.

Permutation importance highlighted `bureau_score` and `dti` as influential predictors.

The review-capacity diagnostics also identified periods where additional near-threshold review workload exceeded capacity, emphasizing the need to distinguish predictive quality from operational feasibility.

**Review status:** The reflection form previously returned `READY_FOR_REVIEW`, indicating that its required response fields were completed. This does not independently certify that all operational constraints or final submission requirements have been satisfied.
