
<h1 align="center">Tamweel Lite</h1>
<h3 align="center">Explainable Credit-Risk Decision Support</h3>

<p align="center">
  An end-to-end, leakage-aware machine-learning project for predicting synthetic 90-day financing default risk, balancing error costs against human-review capacity, and producing explainable, auditable decisions.
</p>

<p align="center">
  <strong>Developer:</strong> Shahad Mamdouh Abu Shaheen
  <br>
  <strong>Project type:</strong> Individual Machine Learning Capstone
  <br>
  <strong>Training:</strong> SDA-DSC-211 | Advanced Machine Learning Methods
  <br>
  <strong>Organization:</strong> SDAIA Academy
</p>

<p align="center">
  <a href="https://colab.research.google.com/drive/1Cw8_A6PngwrjMEweEB4MoIC0d07aF6wV?usp=sharing">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab">
  </a>
</p>

<p align="center">
  <a href="https://github.com/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211">GitHub Repository</a>
  |
  <a href="https://almiyead-rgb.github.io/advanced-machine-learning-methods-sda-dsc-211/#start">Training Program</a>
</p>

<hr>

<h2>Project Overview</h2>

<p>
Tamweel Lite is a machine-learning project designed to simulate a financing risk-assessment workflow. The system estimates the likelihood of a synthetic applicant experiencing a default event within 90 days of submitting a financing application.
</p>

<p>
The model produces risk scores that help prioritize applications for human review. It does not automatically approve or reject financing applications.
</p>

<p>
I developed and evaluated multiple machine-learning approaches, focusing on reliable validation, data leakage prevention, class imbalance, cost-sensitive decisions, model interpretability, probability calibration, and reproducibility.
</p>

<h2>Project Objectives</h2>

<ul>
  <li>Compare Logistic Regression, XGBoost, and LightGBM.</li>
  <li>Prevent temporal data leakage and repeated-customer overlap.</li>
  <li>Apply time-based validation and hyperparameter optimization.</li>
  <li>Address class imbalance and evaluate cost-sensitive decision policies.</li>
  <li>Optimize review thresholds under a 12% capacity constraint.</li>
  <li>Interpret predictions using SHAP and Permutation Importance.</li>
  <li>Evaluate probability calibration and temporal stability.</li>
  <li>Compare individual models with Averaging and Stacking ensembles.</li>
  <li>Select and justify a final model using quantitative evidence.</li>
  <li>Generate reproducible predictions for the final challenge.</li>
</ul>

<hr>

<h2>Key Results</h2>

<table>
  <tr>
    <th>Metric / Outcome</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>Final Selected Model</td>
    <td><strong>Logistic Regression</strong></td>
  </tr>
  <tr>
    <td>Mean Out-of-Fold Average Precision</td>
    <td><strong>0.39166</strong></td>
  </tr>
  <tr>
    <td>OOF AP Standard Deviation</td>
    <td>0.02981</td>
  </tr>
  <tr>
    <td>Mean OOF Brier Score</td>
    <td>0.06327</td>
  </tr>
  <tr>
    <td>OOF Decision Threshold</td>
    <td>0.16892</td>
  </tr>
  <tr>
    <td>Final Transported Threshold</td>
    <td>0.1222584314</td>
  </tr>
  <tr>
    <td>Maximum Review Capacity</td>
    <td>12%</td>
  </tr>
  <tr>
    <td>Challenge Applications</td>
    <td>2,500</td>
  </tr>
  <tr>
    <td>Applications Selected for Review</td>
    <td>300</td>
  </tr>
</table>

<p>
<strong>Final model decision:</strong> I selected Logistic Regression after comparing individual models and ensemble approaches across three forward validation periods. It achieved the highest mean out-of-fold Average Precision of 0.39166 among the evaluated candidates.
</p>

<p>
Although XGBoost performed best during the initial baseline comparison, the final model selection was based on a different, more extensive validation protocol. These results should not be interpreted as a direct before-and-after performance improvement.
</p>

<hr>

<h2>Technical Workflow</h2>

<p>
I organized the project into five practical labs, progressing from baseline model development to leakage-safe validation, cost-sensitive decisions, interpretability, calibration, and final model selection.
</p>

<h2>Lab 01 — Baseline Models and Boosting</h2>

<p>
  <a href="https://colab.research.google.com/github/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211/blob/main/notebooks/01_baseline_boosting.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Lab 1 in Colab">
  </a>
</p>

<h3>What I Did</h3>

<p>
I began by exploring the synthetic financing dataset, examining the target distribution, missing values, and available predictors. I prepared a Logistic Regression baseline and compared it against XGBoost and LightGBM with early stopping.
</p>

<p>
The dataset contained 10,000 synthetic financing applications, 22 predictors, a default rate of 7.89%, and 766 missing cells.
</p>

<h3>Model Comparison</h3>

<table>
  <tr>
    <th>Model</th>
    <th>ROC-AUC</th>
    <th>Average Precision</th>
  </tr>
  <tr>
    <td>Logistic Regression</td>
    <td>0.8213</td>
    <td>0.3258</td>
  </tr>
  <tr>
    <td><strong>XGBoost</strong></td>
    <td>0.8124</td>
    <td><strong>0.3338</strong></td>
  </tr>
  <tr>
    <td>LightGBM</td>
    <td>0.8138</td>
    <td>0.3248</td>
  </tr>
</table>

<p>
<strong>Finding:</strong> XGBoost achieved the highest Average Precision in the initial comparison. However, this was a preliminary result rather than the final model decision.
</p>

<p>
The initial educational comparison was not fully customer-disjoint. I addressed this limitation through stricter validation in Lab 2.
</p>

<p align="center">
  <img src="assets/lab1_model_comparison.png" alt="Lab 1 Model Comparison" width="850">
</p>

<hr>

<h2>Lab 02 — Leakage-Safe Validation and Hyperparameter Tuning</h2>

<p>
  <a href="https://colab.research.google.com/github/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211/blob/main/notebooks/02_validation_tuning.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Lab 2 in Colab">
  </a>
</p>

<h3>What I Did</h3>

<p>
I investigated how data leakage and validation design can affect model performance. I audited feature availability, separated customers across data roles, respected the 90-day target maturation window, and constructed three forward-in-time validation folds.
</p>

<p>
I compared deliberately unsafe random and leaky validation controls against a more reliable time-based and customer-aware approach.
</p>

<p>
I also performed a bounded Optuna hyperparameter search with eight completed trials.
</p>

<h3>Validation Results</h3>

<table>
  <tr>
    <th>Validation Strategy</th>
    <th>Mean ROC-AUC</th>
    <th>Mean AP</th>
  </tr>
  <tr>
    <td>Leaky Random Control (Unsafe)</td>
    <td>0.9999</td>
    <td>0.9988</td>
  </tr>
  <tr>
    <td>Clean Random Control (Unsafe)</td>
    <td>0.8010</td>
    <td>0.3110</td>
  </tr>
  <tr>
    <td>Clean Time/Group — Fixed</td>
    <td>0.7976</td>
    <td><strong>0.3153</strong></td>
  </tr>
  <tr>
    <td>Clean Time/Group — Tuned</td>
    <td>0.7855</td>
    <td>0.3133</td>
  </tr>
</table>

<p>
The honest outer validation covered 5,039 eligible applications, while 4,961 warm-up rows did not receive outer out-of-fold predictions.
</p>

<p>
<strong>Finding:</strong> The deliberately leaky validation produced unrealistically high scores. The fixed configuration also slightly outperformed the tuned configuration on mean Average Precision, showing that tuning does not automatically improve generalization.
</p>

<p align="center">
  <img src="assets/lab2_validation_comparison.png" alt="Lab 2 Validation Results" width="850">
</p>

<hr>

<h2>Lab 03 — Cost-Sensitive Decision Making</h2>

<p>
  <a href="https://colab.research.google.com/github/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211/blob/main/notebooks/03_cost_sensitive_decision.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Lab 3 in Colab">
  </a>
</p>

<h3>What I Did</h3>

<p>
I explored class-imbalance strategies by comparing unweighted, class-weighted, and oversampled approaches using out-of-fold predictions.
</p>

<p>
I evaluated decision thresholds based on the simulated cost of false negatives and false positives, while respecting the maximum review capacity of 12% per period.
</p>

<p>
The cost assumptions were:
</p>

<ul>
  <li>False Negative (FN): 10 loss units.</li>
  <li>False Positive (FP): 1 loss unit.</li>
  <li>Maximum review capacity: 12% per period.</li>
</ul>

<h3>Selected Weighted-Model Policy</h3>

<table>
  <tr>
    <th>Metric</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>Eligible OOF Applications</td>
    <td>5,039</td>
  </tr>
  <tr>
    <td>Selected Threshold</td>
    <td><strong>0.658347</strong></td>
  </tr>
  <tr>
    <td>Flagged Applications</td>
    <td>526</td>
  </tr>
  <tr>
    <td>Simulated Loss</td>
    <td>2,639 units</td>
  </tr>
  <tr>
    <td>Recall</td>
    <td>0.4089</td>
  </tr>
  <tr>
    <td>Precision</td>
    <td>0.2985</td>
  </tr>
</table>

<p>
I also evaluated alternative error-cost assumptions and examined descriptive regional false-positive-rate differences.
</p>

<p>
<strong>Finding:</strong> Threshold selection must consider both classification errors and the available review capacity. The selected Lab 3 threshold belongs to this weighted-model experiment and is not the final Lab 5 threshold.
</p>

<p align="center">
  <img src="assets/lab3_cost_threshold.png" alt="Lab 3 Cost-Sensitive Threshold Analysis" width="850">
</p>

<hr>

<h2>Lab 04 — Model Interpretability, Calibration and Stability</h2>

<p>
  <a href="https://colab.research.google.com/github/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211/blob/main/notebooks/04_explain_calibrate.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Lab 4 in Colab">
  </a>
</p>

<h3>What I Did</h3>

<p>
I analyzed model behavior using TreeSHAP and held-out permutation importance. I examined global feature contributions and local explanations, while distinguishing model associations from causal relationships.
</p>

<p>
I interpreted SHAP contributions in log-odds rather than treating them as additive changes in probability.
</p>

<h3>Permutation Importance</h3>

<p>
The largest decreases in held-out Average Precision were associated with:
</p>

<table>
  <tr>
    <th>Feature</th>
    <th>AP Decrease</th>
  </tr>
  <tr>
    <td>bureau_score</td>
    <td>0.1270</td>
  </tr>
  <tr>
    <td>dti</td>
    <td>0.0690</td>
  </tr>
</table>

<p align="center">
  <img src="assets/lab4_shap.png" alt="Lab 4 SHAP Interpretability Analysis" width="850">
</p>

<h3>Probability Calibration</h3>

<p>
I applied sigmoid calibration to the frozen weighted model and compared its probability quality against the raw model on 1,733 evaluation applications.
</p>

<table>
  <tr>
    <th>Metric</th>
    <th>Raw Model</th>
    <th>Calibrated Model</th>
  </tr>
  <tr>
    <td>Average Precision</td>
    <td>0.258677</td>
    <td>0.258677</td>
  </tr>
  <tr>
    <td>Brier Score</td>
    <td>0.113027</td>
    <td><strong>0.067112</strong></td>
  </tr>
  <tr>
    <td>Expected Calibration Error</td>
    <td>0.146871</td>
    <td><strong>0.022486</strong></td>
  </tr>
</table>

<p>
<strong>Finding:</strong> Sigmoid calibration improved probability quality without changing Average Precision in this evaluation.
</p>

<p>
The notebook also reported <code>CAPACITY_REVIEW_REQUIRED</code> because the evaluation review-band scenario exceeded the available capacity. I retained this operational limitation instead of using the evaluation data to retune the policy.
</p>

<p align="center">
  <img src="assets/lab4_calibration.png" alt="Lab 4 Calibration Reliability Analysis" width="850">
</p>

<hr>

<h2>Lab 05 — Final Model Selection, Ensembles and Challenge Predictions</h2>

<p>
  <a href="https://colab.research.google.com/github/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211/blob/main/notebooks/05_final_model.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Lab 5 in Colab">
  </a>
</p>

<h3>What I Did</h3>

<p>
I performed the final model comparison using three forward validation periods and 2,155 live out-of-fold predictions.
</p>

<p>
I compared Logistic Regression, XGBoost, and LightGBM against three ensemble approaches:
</p>

<ul>
  <li>Equal-weight Averaging.</li>
  <li>Weighted Averaging.</li>
  <li>Stacking.</li>
</ul>

<p>
I evaluated whether ensemble methods provided sufficient improvement to justify replacing a simpler individual model.
</p>

<h3>Final Model Comparison</h3>

<table>
  <tr>
    <th>Model</th>
    <th>Mean OOF AP</th>
    <th>Fold SD</th>
  </tr>
  <tr>
    <td>LightGBM</td>
    <td>0.34549</td>
    <td>0.04348</td>
  </tr>
  <tr>
    <td>XGBoost</td>
    <td>0.35263</td>
    <td>0.02904</td>
  </tr>
  <tr>
    <td><strong>Logistic Regression</strong></td>
    <td><strong>0.39166</strong></td>
    <td>0.02981</td>
  </tr>
  <tr>
    <td>Equal Averaging</td>
    <td>0.37170</td>
    <td>0.03258</td>
  </tr>
  <tr>
    <td>Weighted Averaging</td>
    <td>0.38942</td>
    <td>0.02906</td>
  </tr>
  <tr>
    <td>Stacking</td>
    <td>0.38314</td>
    <td>0.02949</td>
  </tr>
</table>

<p>
<strong>Final Selection: Logistic Regression</strong>
</p>

<p>
I retained Logistic Regression as the final model because it achieved the highest mean out-of-fold Average Precision of 0.39166 among the evaluated candidates. The ensemble approaches did not satisfy the acceptance criteria needed to replace the individual model.
</p>

<p align="center">
  <img src="assets/lab5_model_selection.png" alt="Lab 5 Final Model Comparison" width="850">
</p>

<h3>Final Decision Threshold</h3>

<p>
I selected an out-of-fold policy threshold of <strong>0.16892</strong>, flagging 245 out of 2,155 applications. The maximum per-period flagged fraction was 11.749%, within the 12% capacity constraint.
</p>

<table>
  <tr>
    <th>Metric</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>OOF Threshold</td>
    <td>0.16892</td>
  </tr>
  <tr>
    <td>Flagged OOF Applications</td>
    <td>245 / 2,155</td>
  </tr>
  <tr>
    <td>Recall</td>
    <td>0.46927</td>
  </tr>
  <tr>
    <td>Precision</td>
    <td>0.34286</td>
  </tr>
  <tr>
    <td>Transported Final Threshold</td>
    <td>0.1222584314</td>
  </tr>
</table>

<h3>Challenge Predictions</h3>

<p>
After final fitting and calibration, I applied the transported decision threshold to the synthetic challenge batch containing 2,500 applications.
</p>

<p>
A total of 330 applications exceeded the transported threshold. To comply with the 12% review-capacity limit, I retained the 300 highest-priority applications and excluded 30 otherwise above-threshold cases.
</p>

<table>
  <tr>
    <th>Challenge Metric</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>Total Applications</td>
    <td>2,500</td>
  </tr>
  <tr>
    <td>Maximum Review Capacity</td>
    <td>300</td>
  </tr>
  <tr>
    <td>Above-Threshold Applications</td>
    <td>330</td>
  </tr>
  <tr>
    <td>Final Flagged Applications</td>
    <td><strong>300</strong></td>
  </tr>
  <tr>
    <td>Excluded Above-Threshold Cases</td>
    <td>30</td>
  </tr>
</table>

<p align="center">
  <img src="assets/lab5_challenge_capacity.png" alt="Lab 5 Challenge Capacity Analysis" width="850">
</p>

<p>
<strong>Submission note:</strong> The final notebook reported <code>PROJECT_WORK_REQUIRED</code> because earlier evidence bundles and the presentation were not available in that execution environment. Final model selection was completed, but this status did not certify the full submission package as complete.
</p>

<hr>

<h2>Decision Policy and Human Oversight</h2>

<p>
The project uses a risk-based review policy rather than an automated financing decision system.
</p>

<p>
I evaluated false negatives at a simulated cost of 10 units and false positives at 1 unit, while applying review-capacity constraints.
</p>

<p>
Decision thresholds were selected using designated policy or out-of-fold evidence rather than retrospectively optimizing against evaluation outcomes.
</p>

<p>
A flagged application indicates a need for human review, not a confirmed default or an automatic financing rejection.
</p>

<hr>

<h2>Repository Structure</h2>

<pre>
Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211/
|
|-- README.md
|
|-- assets/
|   |-- lab1_model_comparison.png
|   |-- lab2_validation_comparison.png
|   |-- lab3_cost_threshold.png
|   |-- lab4_shap.png
|   |-- lab4_calibration.png
|   |-- lab5_model_selection.png
|   |-- lab5_challenge_capacity.png
|
|-- notebooks/
|   |-- 00_readiness_check.ipynb
|   |-- 01_baseline_boosting.ipynb
|   |-- 02_validation_tuning.ipynb
|   |-- 03_cost_sensitive_decision.ipynb
|   |-- 04_explain_calibrate.ipynb
|   |-- 05_final_model.ipynb
|   |-- 99_final_submission_check.ipynb
|
|-- reports/
|   |-- Decision Card
|   |-- Interpretability Report
|   |-- Model Card
|
|-- submission.csv
|
|-- final_presentation.pdf
</pre>

<p>
<strong>Note:</strong> This structure represents the intended submission layout. The final Model Card, submission.csv, and final presentation must be uploaded and verified before the repository can be considered complete.
</p>

<hr>

<h2>How to Run</h2>

<h3>1. Open the Notebooks</h3>

<p>
Open the required notebook through GitHub or Google Colab using the links provided in each lab section.
</p>

<h3>2. Prepare the Environment</h3>

<p>
Start a fresh Google Colab CPU runtime and select:
</p>

<pre>Runtime &gt; Run all</pre>

<h3>3. Verify Dependencies and Data</h3>

<p>
Follow the notebook's pinned dependency versions, checksum verification, and support-asset requirements. Do not bypass failed integrity checks.
</p>

<h3>4. Preserve the Validation Design</h3>

<p>
Maintain the intended time-based and customer-aware separation. Do not replace it with a random split.
</p>

<h3>5. Export the Results</h3>

<p>
Inspect the executed outputs, export the required reports and predictions, and download each completed notebook as an <code>.ipynb</code> file before uploading it to GitHub.
</p>

<p>
The standard workflow is designed for free CPU execution without requiring a paid GPU, Google Drive mount, or GitHub authorization from Colab.
</p>

<hr>

<h2>Interpretation and Limitations</h2>

<ul>
  <li>The financing dataset is synthetic and intended for educational use.</li>
  <li>Results have not been validated for real-world lending decisions.</li>
  <li>SHAP and permutation importance explain model behavior but do not establish causality or fairness.</li>
  <li>Some evaluation data appeared earlier in the course and should not be described as a completely untouched final test.</li>
  <li>Improved calibration does not necessarily improve ranking performance or satisfy review-capacity requirements.</li>
  <li>Lab 4 reported CAPACITY_REVIEW_REQUIRED, indicating that additional operational capacity review was needed.</li>
  <li>Regional false-positive-rate comparisons are descriptive audits of synthetic groups, not formal fairness certification.</li>
  <li>Capacity constraints may prevent some above-threshold applications from being selected for review.</li>
  <li>All risk predictions require appropriate human oversight.</li>
</ul>

<hr>

<h2>Final Deliverables</h2>

<p>
The course submission requires:
</p>

<ul>
  <li>README.md</li>
  <li>00_readiness_check.ipynb</li>
  <li>01_baseline_boosting.ipynb</li>
  <li>02_validation_tuning.ipynb</li>
  <li>03_cost_sensitive_decision.ipynb</li>
  <li>04_explain_calibrate.ipynb</li>
  <li>05_final_model.ipynb</li>
  <li>99_final_submission_check.ipynb</li>
  <li>Decision Card</li>
  <li>Interpretability Report</li>
  <li>Model Card</li>
  <li>submission.csv</li>
  <li>final_presentation.pdf</li>
</ul>

<p>
This README documents the five executed project labs. It does not replace the required reports, executed submission checks, prediction file, or final presentation.
</p>

<hr>

<h2>Training Program and Acknowledgment</h2>

<p>
This project was developed as part of <strong>SDA-DSC-211 — Advanced Machine Learning Methods</strong>, associated with <strong>SDAIA Academy</strong>.
</p>

<p>
<strong>Training Organization:</strong>
<a href="https://sdaia.gov.sa/">Saudi Data & Artificial Intelligence Authority (SDAIA)</a>
</p>

<p>
<strong>Course Materials:</strong>
<a href="https://github.com/almiyead-rgb">SDAIA Academy Course Materials on GitHub</a>
</p>

<p>
<strong>Course Website:</strong>
<a href="https://almiyead-rgb.github.io/advanced-machine-learning-methods-sda-dsc-211/#start">Advanced Machine Learning Methods — SDA-DSC-211</a>
</p>

<hr>

<p align="center">
  <strong>Developed by Shahad Mamdouh Abu Shaheen</strong>
  <br>
  SDAIA Academy | Advanced Machine Learning Methods
  <br>
  <a href="https://github.com/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211">View Project on GitHub</a>
</p>
