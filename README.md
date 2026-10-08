
<div align="center">

<h1>Advanced Machine Learning Methods-Tamweel Lite</h1>

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Machine%20Learning-6C63FF?style=flat-square" alt="Machine Learning">
  <img src="https://img.shields.io/badge/SDAIA%20Academy-008C87?style=flat-square" alt="SDAIA Academy">
</p>

<p>
  <a href="https://colab.research.google.com/drive/1Cw8_A6PngwrjMEweEB4MoIC0d07aF6wV?usp=sharing">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Google Colab">
  </a>
</p>

<p>
  <a href="https://almiyead-rgb.github.io/advanced-machine-learning-methods-sda-dsc-211/#start">Training Program</a>
  &nbsp; | &nbsp;
  <a href="https://github.com/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211">GitHub Repository</a>
</p>

<p>
  <strong>Shahad Mamdouh Abu Shaheen</strong>
  <br>
  SDA-DSC-211 | SDAIA Academy
</p>

</div>

<hr>

<h2>01. Project Overview</h2>

<p>
<strong>Tamweel Lite</strong> is an end-to-end machine learning project that investigates the prediction of financing default risk within 90 days of an application. The project uses synthetic financing data to develop, evaluate, interpret, and compare machine learning models under realistic validation and operational constraints.
</p>

<p>
The workflow extends beyond model training by addressing temporal leakage, repeated-customer overlap, class imbalance, asymmetric classification costs, probability calibration, and limited review capacity. The resulting risk scores are intended to prioritize applications for human review rather than automatically approve or reject financing requests.
</p>

<h3>Project Summary</h3>

<table>
  <tr>
    <th>Component</th>
    <th>Details</th>
  </tr>
  <tr>
    <td>Dataset</td>
    <td>10,000 synthetic financing applications</td>
  </tr>
  <tr>
    <td>Prediction Target</td>
    <td>Default within 90 days</td>
  </tr>
  <tr>
    <td>Models</td>
    <td>Logistic Regression, XGBoost, LightGBM, Averaging, Stacking</td>
  </tr>
  <tr>
    <td>Final Selected Model</td>
    <td><strong>Logistic Regression</strong></td>
  </tr>
  <tr>
    <td>Mean OOF Average Precision</td>
    <td><strong>0.39166</strong></td>
  </tr>
  <tr>
    <td>Maximum Review Capacity</td>
    <td>12% per period</td>
  </tr>
</table>

<h3>Project Objectives</h3>

<ul>
  <li>Explore and prepare synthetic financing application data.</li>
  <li>Establish baseline models and compare gradient-boosting algorithms.</li>
  <li>Implement leakage-safe temporal and customer-aware validation.</li>
  <li>Evaluate hyperparameter optimization and class-imbalance strategies.</li>
  <li>Develop cost-sensitive decision policies under review-capacity constraints.</li>
  <li>Interpret predictions using SHAP and permutation importance.</li>
  <li>Assess probability calibration and operational stability.</li>
  <li>Compare individual models with averaging and stacking ensembles.</li>
  <li>Select a final model and generate challenge predictions.</li>
</ul>

<hr>

<h2>02. Project Workflow</h2>

<table>
  <tr>
    <th>Lab</th>
    <th>Focus</th>
    <th>Techniques</th>
  </tr>
  <tr>
    <td><strong>01</strong></td>
    <td>Baseline &amp; Boosting</td>
    <td>Logistic Regression, XGBoost, LightGBM</td>
  </tr>
  <tr>
    <td><strong>02</strong></td>
    <td>Validation &amp; Tuning</td>
    <td>Forward Validation, Leakage Prevention, Optuna</td>
  </tr>
  <tr>
    <td><strong>03</strong></td>
    <td>Cost-Sensitive Decisions</td>
    <td>Class Imbalance, Error Costs, Capacity Constraints</td>
  </tr>
  <tr>
    <td><strong>04</strong></td>
    <td>Explainability &amp; Calibration</td>
    <td>SHAP, Permutation Importance, Sigmoid Calibration</td>
  </tr>
  <tr>
    <td><strong>05</strong></td>
    <td>Final Model &amp; Challenge</td>
    <td>Model Selection, Averaging, Stacking, Challenge Predictions</td>
  </tr>
</table>

<hr>

<h2>03. Experimental Development</h2>

<h3>Lab 01 — Baseline Models &amp; Boosting</h3>

<p>
<strong>Objective:</strong> Establish a baseline for financing default prediction and evaluate whether gradient-boosting methods improve predictive performance.
</p>

<h4>Implementation</h4>

<p>
I began by examining the synthetic dataset, reviewing the distribution of the target variable, identifying missing values, and preparing the predictors for machine learning. I trained a Logistic Regression baseline and compared it against XGBoost and LightGBM.
</p>

<p>
The dataset contained 10,000 applications, 22 predictor variables, a default rate of 7.89%, and 766 missing cells.
</p>

<h4>Model Comparison</h4>

<table>
  <tr>
    <th>Model</th>
    <th>ROC-AUC</th>
    <th>Average Precision</th>
  </tr>
  <tr>
    <td>Logistic Regression</td>
    <td><strong>0.8213</strong></td>
    <td>0.3258</td>
  </tr>
  <tr>
    <td>XGBoost</td>
    <td>0.8124</td>
    <td><strong>0.3338</strong></td>
  </tr>
  <tr>
    <td>LightGBM</td>
    <td>0.8138</td>
    <td>0.3248</td>
  </tr>
</table>

<h4>Results &amp; Interpretation</h4>

<p>
XGBoost achieved the highest Average Precision of 0.3338 in the initial experiment, while Logistic Regression achieved the highest ROC-AUC of 0.8213.
</p>

<p>
These findings showed that model rankings can differ depending on the evaluation metric. Because the initial educational comparison was not fully customer-disjoint, its results were treated as preliminary rather than as the final model-selection evidence.
</p>

<p align="center">
  <img src="assets/lab1_model_comparison.png" alt="Lab 1 model comparison" width="780">
</p>

<hr>

<h3>Lab 02 — Leakage-Safe Validation &amp; Tuning</h3>

<p>
<strong>Objective:</strong> Design a reliable evaluation framework that respects application chronology, prevents target leakage, and controls repeated-customer overlap.
</p>

<h4>Implementation</h4>

<p>
I audited feature availability, incorporated the 90-day target-maturation requirement, separated customers across data roles, and constructed three forward-in-time validation folds.
</p>

<p>
I compared deliberately unsafe random and leaky validation controls with clean time-based and customer-aware validation. I also evaluated hyperparameter optimization using eight completed Optuna trials.
</p>

<h4>Validation Comparison</h4>

<table>
  <tr>
    <th>Validation Strategy</th>
    <th>ROC-AUC</th>
    <th>Average Precision</th>
  </tr>
  <tr>
    <td>Leaky Random Control — Unsafe</td>
    <td>0.9999</td>
    <td>0.9988</td>
  </tr>
  <tr>
    <td>Clean Random Control — Unsafe for Intended Use</td>
    <td>0.8010</td>
    <td>0.3110</td>
  </tr>
  <tr>
    <td>Clean Time/Group — Fixed</td>
    <td><strong>0.7976</strong></td>
    <td><strong>0.3153</strong></td>
  </tr>
  <tr>
    <td>Clean Time/Group — Tuned</td>
    <td>0.7855</td>
    <td>0.3133</td>
  </tr>
</table>

<h4>Results &amp; Interpretation</h4>

<p>
The deliberately leaky control produced unrealistically high scores, demonstrating how invalid validation procedures can exaggerate performance.
</p>

<p>
The clean fixed configuration slightly outperformed the tuned configuration in Average Precision. This indicated that hyperparameter tuning did not improve generalization in this experiment.
</p>

<p>
The honest outer validation generated predictions for 5,039 eligible applications, while 4,961 warm-up rows did not receive outer out-of-fold predictions.
</p>

<p align="center">
  <img src="assets/lab2_validation_comparison.png" alt="Lab 2 validation comparison" width="780">
</p>

<hr>

<h3>Lab 03 — Cost-Sensitive Decision Making</h3>

<p>
<strong>Objective:</strong> Convert predictive risk scores into review decisions while balancing classification errors, asymmetric costs, and operational capacity.
</p>

<h4>Implementation</h4>

<p>
I evaluated unweighted, class-weighted, and oversampled modeling approaches using out-of-fold predictions. I then examined decision thresholds under different simulated error-cost assumptions.
</p>

<p>
The main policy experiment assigned a cost of 10 units to a false negative and 1 unit to a false positive, while limiting review selections to 12% of applications per period.
</p>

<h4>Selected Policy Results</h4>

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
    <td>Recall</td>
    <td>0.4089</td>
  </tr>
  <tr>
    <td>Precision</td>
    <td>0.2985</td>
  </tr>
  <tr>
    <td>Simulated Cost</td>
    <td>2,639 units</td>
  </tr>
</table>

<h4>Results &amp; Interpretation</h4>

<p>
The experiment demonstrated that the threshold with the strongest classification metrics is not necessarily the most practical decision threshold. Error costs and available review capacity must also be considered.
</p>

<p>
I additionally examined alternative false-negative costs and descriptive regional false-positive-rate differences. The selected threshold of 0.658347 belongs to the Lab 03 weighted-model experiment and is separate from the final threshold selected in Lab 05.
</p>

<p align="center">
  <img src="assets/lab3_cost_threshold.png" alt="Lab 3 cost-sensitive threshold analysis" width="780">
</p>

<hr>

<h3>Lab 04 — Explainability &amp; Calibration</h3>

<p>
<strong>Objective:</strong> Understand model predictions, identify influential features, and evaluate the reliability of predicted probabilities.
</p>

<h4>Implementation</h4>

<p>
I applied TreeSHAP to examine global and local model explanations and used held-out permutation importance to measure the influence of predictors on Average Precision.
</p>

<p>
SHAP contributions were interpreted in log-odds for the weighted tree model. These explanations describe statistical model behavior rather than causal relationships.
</p>

<h4>Feature Importance</h4>

<table>
  <tr>
    <th>Feature</th>
    <th>Decrease in Average Precision</th>
  </tr>
  <tr>
    <td><code>bureau_score</code></td>
    <td><strong>0.1270</strong></td>
  </tr>
  <tr>
    <td><code>dti</code></td>
    <td>0.0690</td>
  </tr>
</table>

<p>
Bureau score and debt-to-income ratio showed the largest held-out permutation effects among the reported features.
</p>

<p align="center">
  <img src="assets/lab4_shap.png" alt="Lab 4 SHAP analysis" width="780">
</p>

<h4>Probability Calibration</h4>

<p>
I applied sigmoid calibration to the frozen weighted model and evaluated probability quality on 1,733 applications.
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

<h4>Results &amp; Interpretation</h4>

<p>
Sigmoid calibration improved the quality of predicted probabilities, reducing both the Brier Score and Expected Calibration Error while preserving Average Precision in this evaluation.
</p>

<p>
The review-band analysis reported <code>CAPACITY_REVIEW_REQUIRED</code>, indicating that the evaluated operational scenario exceeded the available review capacity. This limitation was documented rather than resolved by retuning against evaluation outcomes.
</p>

<p align="center">
  <img src="assets/lab4_calibration.png" alt="Lab 4 calibration analysis" width="780">
</p>

<hr>

<h3>Lab 05 — Final Model Selection &amp; Challenge</h3>

<p>
<strong>Objective:</strong> Select the strongest justified model using forward-validation evidence, evaluate ensemble alternatives, and produce capacity-constrained challenge predictions.
</p>

<h4>Implementation</h4>

<p>
I compared Logistic Regression, XGBoost, and LightGBM against three ensemble approaches: equal-weight averaging, weighted averaging, and stacking.
</p>

<p>
The final evaluation used three forward validation periods and 2,155 out-of-fold predictions. Model selection considered Average Precision, performance stability, and whether the added complexity of ensembles provided sufficient benefit.
</p>

<h4>Final Model Comparison</h4>

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

<h4>Final Model Selection</h4>

<p>
<strong>Logistic Regression was selected as the final model.</strong>
</p>

<p>
It achieved the highest mean out-of-fold Average Precision of <strong>0.39166</strong>, with a fold standard deviation of 0.02981 and mean Brier Score of 0.06327.
</p>

<p>
The ensemble approaches did not satisfy the acceptance criteria needed to replace the simpler individual model.
</p>

<p>
Although XGBoost performed best in the preliminary Lab 01 Average Precision comparison, the final decision used a separate, more extensive validation protocol. The scores from these experiments should not be treated as directly comparable.
</p>

<p align="center">
  <img src="assets/lab5_model_selection.png" alt="Lab 5 final model comparison" width="780">
</p>

<h4>Decision Threshold</h4>

<table>
  <tr>
    <th>Metric</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>OOF Decision Threshold</td>
    <td><strong>0.16892</strong></td>
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
    <td>Maximum Per-Period Flagged Fraction</td>
    <td>11.749%</td>
  </tr>
  <tr>
    <td>Transported Final Threshold</td>
    <td>0.1222584314</td>
  </tr>
</table>

<p>
The out-of-fold policy remained within the maximum review-capacity constraint of 12% per period.
</p>

<h4>Challenge Results</h4>

<p>
After final fitting and calibration, the transported threshold was applied to a synthetic challenge batch containing 2,500 applications.
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
    <td>Applications Above Threshold</td>
    <td>330</td>
  </tr>
  <tr>
    <td>Maximum Review Capacity</td>
    <td>300</td>
  </tr>
  <tr>
    <td>Selected for Review</td>
    <td><strong>300</strong></td>
  </tr>
  <tr>
    <td>Excluded Above-Threshold Applications</td>
    <td>30</td>
  </tr>
</table>

<p>
To respect the 12% review-capacity limit, the 300 highest-priority applications were selected. Thirty additional above-threshold applications were excluded because the available capacity had been reached.
</p>

<p align="center">
  <img src="assets/lab5_challenge_capacity.png" alt="Lab 5 challenge capacity analysis" width="780">
</p>

<p>
<strong>Submission note:</strong> The final notebook reported <code>PROJECT_WORK_REQUIRED</code> because some required supporting reports and presentation materials were unavailable during execution. The model-selection results do not certify the entire submission package as complete.
</p>

<hr>

<h2>04. Final Results</h2>

<table>
  <tr>
    <th>Metric</th>
    <th>Outcome</th>
  </tr>
  <tr>
    <td>Final Selected Model</td>
    <td><strong>Logistic Regression</strong></td>
  </tr>
  <tr>
    <td>Mean OOF Average Precision</td>
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
    <td>OOF Policy Threshold</td>
    <td>0.16892</td>
  </tr>
  <tr>
    <td>Transported Threshold</td>
    <td>0.1222584314</td>
  </tr>
  <tr>
    <td>Maximum Review Capacity</td>
    <td>12%</td>
  </tr>
  <tr>
    <td>Challenge Review Selections</td>
    <td>300 / 2,500</td>
  </tr>
</table>

<p>
The final model was selected based on forward-validation evidence and operational decision constraints rather than model complexity alone.
</p>

<hr>

<h2>05. Decision Policy &amp; Human Oversight</h2>

<p>
Tamweel Lite is a risk-based decision-support project. It does not perform automatic financing approval or rejection.
</p>

<ul>
  <li>Predicted risk scores prioritize applications for human review.</li>
  <li>False negatives and false positives are evaluated using simulated costs.</li>
  <li>Review selections must respect the 12% per-period capacity limit.</li>
  <li>Decision thresholds are selected using designated policy or out-of-fold evidence.</li>
  <li>Above-threshold applications may be excluded when capacity is exhausted.</li>
  <li>Human oversight remains necessary for interpreting and acting on predictions.</li>
</ul>

<hr>

<h2>06. Repository Structure</h2>

<p>
The following represents the intended submission structure. The actual repository contents should be verified before treating the project as fully submitted.
</p>

<pre>
Advanced-Machine-Learning-Methods-Tamweel-Lite/
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
|-- final_presentation.pdf
</pre>

<hr>

<h2>07. How to Run</h2>

<h3>Google Colab</h3>

<ol>
  <li>Open the project notebook using the Google Colab badge at the beginning of this README.</li>
  <li>Start a fresh Python runtime.</li>
  <li>Install or verify the dependencies required by the notebook.</li>
  <li>Run the cells in their intended order.</li>
  <li>Review the generated metrics, plots, and decision-policy results.</li>
  <li>Export executed notebooks and required deliverables.</li>
</ol>

<p>
<strong>Important:</strong> Preserve the intended temporal and customer-aware validation design. Do not replace it with random splitting or bypass integrity checks.
</p>

<hr>

<h2>08. Limitations &amp; Responsible Use</h2>

<ul>
  <li><strong>Synthetic dataset:</strong> The project uses simulated financing applications for educational purposes.</li>
  <li><strong>Real-world validity:</strong> The models have not been validated for real lending decisions.</li>
  <li><strong>Data leakage:</strong> Validation must respect chronological and customer-level separation.</li>
  <li><strong>Interpretability:</strong> SHAP and permutation importance do not establish causal relationships or guarantee fairness.</li>
  <li><strong>Calibration:</strong> Better probability calibration does not necessarily improve ranking performance or satisfy review capacity.</li>
  <li><strong>Evaluation limitations:</strong> Some evaluation data appeared earlier in the course and should not be described as a completely untouched final test.</li>
  <li><strong>Operational capacity:</strong> Capacity constraints may exclude some above-threshold applications.</li>
  <li><strong>Fairness assessment:</strong> Descriptive regional error-rate comparisons do not constitute formal fairness certification.</li>
</ul>

<hr>

<h2>09. Submission Deliverables</h2>

<p>
The complete course submission requires:
</p>

<ul>
  <li><code>README.md</code></li>
  <li><code>00_readiness_check.ipynb</code></li>
  <li><code>01_baseline_boosting.ipynb</code></li>
  <li><code>02_validation_tuning.ipynb</code></li>
  <li><code>03_cost_sensitive_decision.ipynb</code></li>
  <li><code>04_explain_calibrate.ipynb</code></li>
  <li><code>05_final_model.ipynb</code></li>
  <li><code>99_final_submission_check.ipynb</code></li>
  <li>Decision Card</li>
  <li>Interpretability Report</li>
  <li>Model Card</li>
  <li><code>submission.csv</code></li>
  <li><code>final_presentation.pdf</code></li>
</ul>

<p>
This README documents the experimental work and reported results. It does not replace the required notebooks, reports, prediction file, or presentation.
</p>

<hr>

<h2>10. Training &amp; Acknowledgments</h2>

<p>
This project was developed as part of <strong>SDA-DSC-211 — Advanced Machine Learning Methods</strong>, associated with <strong>SDAIA Academy</strong>.
</p>

<p>
<strong>Training Organization:</strong>
<a href="https://sdaia.gov.sa/">Saudi Data &amp; Artificial Intelligence Authority (SDAIA)</a>
</p>

<p>
<strong>Course Website:</strong>
<a href="https://almiyead-rgb.github.io/advanced-machine-learning-methods-sda-dsc-211/#start">Advanced Machine Learning Methods — SDA-DSC-211</a>
</p>

<p>
<strong>Course Materials:</strong>
<a href="https://github.com/almiyead-rgb">Training Materials on GitHub</a>
</p>

<hr>

<div align="center">

<p>
  <strong>Developed by Shahad Mamdouh Abu Shaheen</strong>
</p>

<p>
  SDAIA Academy | Advanced Machine Learning Methods
</p>

<p>
  <a href="https://github.com/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211">View GitHub Repository</a>
</p>

</div>
