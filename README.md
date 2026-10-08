
<div align="center">

<h1>Advanced Machine Learning Methods-Tamweel Lite</h1>

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Machine%20Learning-6C63FF?style=flat-square" alt="Machine Learning">
  <img src="https://img.shields.io/badge/SDAIA%20Academy-008C87?style=flat-square" alt="SDAIA Academy">
</p>

<p>
  <strong>Developer:</strong> Shahad Mamdouh Abu Shaheen
  <br>
  <strong>Project Type:</strong> Individual Capstone Project
  <br>
  <strong>Training Program:</strong> SDA-DSC-211
</p>

<p>
  <a href="https://colab.research.google.com/drive/1Cw8_A6PngwrjMEweEB4MoIC0d07aF6wV?usp=sharing">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab">
  </a>
</p>

<p>
  <a href="https://github.com/nfsh46655-jpg/Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211">GitHub Repository</a>
  &nbsp; | &nbsp;
  <a href="https://almiyead-rgb.github.io/advanced-machine-learning-methods-sda-dsc-211/#start">Training Program</a>
</p>

</div>

<hr>

<h2>Project Overview</h2>

<p>
<strong>Tamweel Lite</strong> is an end-to-end machine learning capstone project focused on predicting the risk of financing default within 90 days of an application. Using synthetic financing data, the project investigates how predictive models can be developed, evaluated, explained, and translated into operational decisions.
</p>

<p>
The complete workflow covers exploratory data analysis, baseline modeling, gradient boosting, leakage-safe validation, hyperparameter tuning, cost-sensitive classification, SHAP explanations, permutation importance, probability calibration, ensemble learning, and final challenge predictions.
</p>

<p>
The project emphasizes reliable evaluation and practical decision support. Predictions are used to prioritize applications for human review, not to automatically approve or reject financing applications.
</p>

<h3>Dataset and Prediction Task</h3>

<table>
  <tr><th>Property</th><th>Description</th></tr>
  <tr><td>Dataset Type</td><td>Synthetic financing applications</td></tr>
  <tr><td>Applications</td><td>10,000</td></tr>
  <tr><td>Predictor Variables</td><td>22</td></tr>
  <tr><td>Prediction Target</td><td>Default within 90 days</td></tr>
  <tr><td>Observed Default Rate</td><td>7.89%</td></tr>
  <tr><td>Missing Data Cells</td><td>766</td></tr>
  <tr><td>Operational Review Capacity</td><td>12% per period</td></tr>
</table>

<h3>Project Objectives</h3>

<ul>
  <li>Develop a reproducible machine learning workflow for financing risk prediction.</li>
  <li>Compare Logistic Regression, XGBoost, and LightGBM.</li>
  <li>Prevent temporal leakage and repeated-customer overlap.</li>
  <li>Evaluate reliable forward-in-time validation strategies.</li>
  <li>Investigate Optuna hyperparameter optimization.</li>
  <li>Analyze class imbalance and asymmetric error costs.</li>
  <li>Optimize review decisions under operational capacity constraints.</li>
  <li>Explain predictions using SHAP and permutation importance.</li>
  <li>Evaluate probability calibration and model stability.</li>
  <li>Compare individual models against averaging and stacking ensembles.</li>
  <li>Select a final model and generate challenge predictions.</li>
</ul>

<hr>

<h2>Key Results</h2>

<h3>Final Model Performance</h3>

<p>
The final model comparison was performed using three forward validation periods and 2,155 out-of-fold predictions.
</p>

<table>
  <tr>
    <th>Metric</th>
    <th>Result</th>
  </tr>
  <tr>
    <td>Selected Model</td>
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
    <td>OOF Decision Threshold</td>
    <td>0.16892</td>
  </tr>
  <tr>
    <td>Transported Final Threshold</td>
    <td>0.1222584314</td>
  </tr>
  <tr>
    <td>Maximum Review Capacity</td>
    <td>12%</td>
  </tr>
</table>

<p>
<strong>Final selection:</strong> Logistic Regression achieved the highest mean out-of-fold Average Precision among the evaluated individual and ensemble models. The ensemble alternatives did not provide sufficient evidence to justify replacing the simpler model.
</p>

<p align="center">
  <img src="tamweel_readme_images/lab5_model_selection.png" alt="Final model comparison" width="800">
</p>

<h3>Challenge Decision Results</h3>

<table>
  <tr><th>Metric</th><th>Result</th></tr>
  <tr><td>Total Challenge Applications</td><td>2,500</td></tr>
  <tr><td>Applications Above Threshold</td><td>330</td></tr>
  <tr><td>Maximum Review Capacity</td><td>300</td></tr>
  <tr><td>Final Applications Flagged</td><td><strong>300</strong></td></tr>
  <tr><td>Above-Threshold Cases Excluded</td><td>30</td></tr>
</table>

<p>
The final policy retained the 300 highest-priority applications to comply with the 12% review-capacity constraint.
</p>

<p align="center">
  <img src="tamweel_readme_images/lab5_challenge_capacity.png" alt="Challenge review capacity" width="800">
</p>

<hr>

<h2>Technical Workflow</h2>

<p>
The project was developed across five practical labs. Each lab addresses a distinct stage of the machine learning lifecycle, from baseline modeling to final model selection and challenge predictions.
</p>

<table>
  <tr><th>Lab</th><th>Focus</th><th>Main Techniques</th></tr>
  <tr>
    <td>01</td>
    <td>Baseline and Boosting</td>
    <td>Logistic Regression, XGBoost, LightGBM</td>
  </tr>
  <tr>
    <td>02</td>
    <td>Validation and Tuning</td>
    <td>Temporal Splits, Leakage Prevention, Optuna</td>
  </tr>
  <tr>
    <td>03</td>
    <td>Cost-Sensitive Decisions</td>
    <td>Class Imbalance, Thresholds, Review Capacity</td>
  </tr>
  <tr>
    <td>04</td>
    <td>Explainability and Calibration</td>
    <td>SHAP, Permutation Importance, Sigmoid Calibration</td>
  </tr>
  <tr>
    <td>05</td>
    <td>Final Model and Challenge</td>
    <td>Averaging, Stacking, Model Selection, Predictions</td>
  </tr>
</table>

<hr>

<h2>Lab 01 — Baseline Models and Boosting</h2>

<h3>Objective</h3>

<p>
Establish a baseline for financing default prediction and compare linear and gradient-boosting models using classification metrics suitable for imbalanced data.
</p>

<h3>Implementation</h3>

<p>
I began by exploring the synthetic financing dataset and examining its structure, target distribution, missing values, and predictors.
</p>

<p>
I prepared the data for machine learning and trained a Logistic Regression baseline. I then compared its performance with XGBoost and LightGBM to investigate whether gradient-boosting approaches improved predictive ranking.
</p>

<p>
The experiment considered both ROC-AUC and Average Precision. Average Precision was particularly relevant because the default class represented a relatively small proportion of the dataset.
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

<h3>Model Comparison Visualization</h3>

<p align="center">
  <img src="tamweel_readme_images/lab1_model_comparison.png" alt="Baseline model performance comparison" width="800">
</p>

<h3>Results and Interpretation</h3>

<p>
XGBoost achieved the highest preliminary Average Precision of <strong>0.3338</strong>, while Logistic Regression achieved the highest ROC-AUC of <strong>0.8213</strong>.
</p>

<p>
These results demonstrated that model rankings can change depending on the evaluation metric. The initial comparison was not fully customer-disjoint, so its results were considered preliminary rather than sufficient evidence for final model selection.
</p>

<h3>Key Takeaway</h3>

<p>
The baseline experiment established reference performance and motivated the need for stricter validation before selecting a model for decision support.
</p>

<hr>

<h2>Lab 02 — Leakage-Safe Validation and Hyperparameter Tuning</h2>

<h3>Objective</h3>

<p>
Develop a more reliable validation framework that prevents leakage, respects the chronological order of financing applications, and accounts for repeated customers.
</p>

<h3>Implementation</h3>

<p>
I investigated how validation design affects model performance and whether apparently strong results can be caused by information leakage.
</p>

<p>
The workflow included:
</p>

<ul>
  <li>Auditing feature availability at prediction time.</li>
  <li>Respecting the 90-day target-maturation window.</li>
  <li>Separating customers across training and evaluation roles.</li>
  <li>Constructing three forward-in-time validation folds.</li>
  <li>Comparing deliberately unsafe controls with clean temporal validation.</li>
  <li>Running a bounded Optuna search with eight completed trials.</li>
</ul>

<h3>Validation Strategy Comparison</h3>

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

<h3>Validation Visualization</h3>

<p align="center">
  <img src="tamweel_readme_images/lab2_validation_comparison.png" alt="Validation strategy comparison" width="800">
</p>

<h3>Results and Interpretation</h3>

<p>
The deliberately leaky control achieved nearly perfect metrics, illustrating how invalid evaluation procedures can dramatically overestimate performance.
</p>

<p>
The clean time-based and customer-aware validation provided a more realistic basis for model assessment.
</p>

<p>
The fixed configuration achieved a mean Average Precision of <strong>0.3153</strong>, slightly outperforming the tuned configuration at <strong>0.3133</strong>. This showed that hyperparameter tuning does not automatically improve generalization.
</p>

<p>
The outer validation covered <strong>5,039 eligible applications</strong>. An additional 4,961 warm-up rows were excluded from outer out-of-fold evaluation.
</p>

<h3>Key Takeaway</h3>

<p>
Reliable validation is more important than artificially high performance scores. A leakage-safe evaluation framework is necessary before interpreting model comparisons or optimizing decisions.
</p>

<hr>

<h2>Lab 03 — Cost-Sensitive Decision Making</h2>

<h3>Objective</h3>

<p>
Convert model predictions into practical review decisions while accounting for class imbalance, asymmetric classification costs, and limited review capacity.
</p>

<h3>Implementation</h3>

<p>
I evaluated different strategies for handling class imbalance, including unweighted, class-weighted, and oversampled modeling approaches.
</p>

<p>
Using out-of-fold predictions, I examined how changing the decision threshold affects false positives, false negatives, simulated loss, and the number of applications selected for review.
</p>

<h3>Decision Policy Assumptions</h3>

<table>
  <tr><th>Parameter</th><th>Value</th></tr>
  <tr><td>False Negative Cost</td><td>10 units</td></tr>
  <tr><td>False Positive Cost</td><td>1 unit</td></tr>
  <tr><td>Maximum Review Capacity</td><td>12% per period</td></tr>
</table>

<p>
I also examined alternative false-negative costs and policy scenarios to understand how operational assumptions influence the preferred decision threshold.
</p>

<h3>Selected Weighted-Model Policy</h3>

<table>
  <tr><th>Metric</th><th>Result</th></tr>
  <tr><td>Eligible OOF Applications</td><td>5,039</td></tr>
  <tr><td>Selected Threshold</td><td><strong>0.658347</strong></td></tr>
  <tr><td>Flagged Applications</td><td>526</td></tr>
  <tr><td>Recall</td><td>0.4089</td></tr>
  <tr><td>Precision</td><td>0.2985</td></tr>
  <tr><td>Simulated Cost</td><td>2,639 units</td></tr>
</table>

<h3>Threshold and Cost Analysis</h3>

<p align="center">
  <img src="tamweel_readme_images/lab3_cost_threshold.png" alt="Cost-sensitive threshold analysis" width="800">
</p>

<h3>Results and Interpretation</h3>

<p>
The selected weighted-model policy used a threshold of <strong>0.658347</strong>, flagging 526 applications and producing a simulated loss of 2,639 units.
</p>

<p>
The experiment demonstrated that optimizing predictive ranking alone is not sufficient for operational decision making. Threshold selection must also consider the relative consequences of missed defaults and unnecessary reviews.
</p>

<p>
I additionally examined descriptive regional false-positive-rate differences. These comparisons were exploratory and did not constitute a formal fairness certification.
</p>

<p>
The selected Lab 03 threshold belongs to this weighted-model experiment and should not be confused with the final Lab 05 decision threshold.
</p>

<h3>Key Takeaway</h3>

<p>
An effective risk-review policy must balance model performance, error costs, and the capacity of the team responsible for reviewing flagged applications.
</p>

<hr>

<h2>Lab 04 — Model Explainability and Probability Calibration</h2>

<h3>Objective</h3>

<p>
Understand the factors influencing model predictions, evaluate feature importance, and assess the reliability of predicted probabilities.
</p>

<h3>Implementation</h3>

<p>
I used TreeSHAP to investigate global feature contributions and individual predictions. I also applied held-out permutation importance to estimate how much model performance depended on particular predictors.
</p>

<p>
SHAP contributions were interpreted in log-odds for the weighted tree model, rather than as direct additive changes in probability.
</p>

<h3>Feature Importance Results</h3>

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

<h3>SHAP Explainability Analysis</h3>

<p align="center">
  <img src="tamweel_readme_images/lab4_shap.png" alt="SHAP feature importance and explanations" width="800">
</p>

<p>
Bureau score and debt-to-income ratio showed the strongest reported held-out permutation effects. These findings describe the model's predictive dependence on the features, not causal relationships.
</p>

<h3>Probability Calibration</h3>

<p>
I applied sigmoid calibration to the frozen weighted model and compared raw and calibrated probability estimates on <strong>1,733 evaluation applications</strong>.
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

<h3>Calibration Analysis</h3>

<p align="center">
  <img src="tamweel_readme_images/lab4_calibration.png" alt="Raw and calibrated probability comparison" width="800">
</p>

<h3>Results and Interpretation</h3>

<p>
Sigmoid calibration reduced the Brier Score from <strong>0.113027</strong> to <strong>0.067112</strong> and Expected Calibration Error from <strong>0.146871</strong> to <strong>0.022486</strong>.
</p>

<p>
Average Precision remained unchanged at 0.258677, indicating that calibration improved probability quality without changing the reported ranking performance.
</p>

<p>
The operational review-band analysis returned <code>CAPACITY_REVIEW_REQUIRED</code> because the evaluated scenario exceeded the available review capacity. This limitation was retained rather than using evaluation outcomes to retune the policy.
</p>

<h3>Key Takeaway</h3>

<p>
Explainability and calibration provide complementary evidence. SHAP helps describe why the model produces particular scores, while calibration assesses whether those scores represent reliable probabilities. Neither automatically guarantees operational feasibility or fairness.
</p>

<hr>

<h2>Lab 05 — Final Model Selection and Challenge Predictions</h2>

<h3>Objective</h3>

<p>
Compare individual models and ensemble approaches using forward-validation evidence, select a justified final model, and generate predictions for the synthetic challenge dataset.
</p>

<h3>Implementation</h3>

<p>
I evaluated three individual models:
</p>

<ul>
  <li>Logistic Regression</li>
  <li>XGBoost</li>
  <li>LightGBM</li>
</ul>

<p>
I also evaluated three ensemble approaches:
</p>

<ul>
  <li>Equal-weight Averaging</li>
  <li>Weighted Averaging</li>
  <li>Stacking</li>
</ul>

<p>
The comparison used three forward validation periods and 2,155 out-of-fold predictions. I evaluated Average Precision, fold-to-fold variability, and whether ensemble methods provided sufficient improvement to justify additional complexity.
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

<h3>Final Model Selection Visualization</h3>

<p align="center">
  <img src="tamweel_readme_images/lab5_model_selection.png" alt="Final individual and ensemble model comparison" width="800">
</p>

<h3>Final Model Decision</h3>

<p>
<strong>Logistic Regression was selected as the final model.</strong>
</p>

<p>
It achieved the highest mean out-of-fold Average Precision of <strong>0.39166</strong>, with a fold standard deviation of 0.02981 and mean Brier Score of 0.06327.
</p>

<p>
Although XGBoost performed best in the initial Lab 01 Average Precision comparison, Lab 05 used a separate and more extensive validation protocol. The scores from these experiments should not be interpreted as directly comparable improvements.
</p>

<p>
The ensemble approaches did not satisfy the acceptance criteria required to replace the simpler Logistic Regression model.
</p>

<h3>Final Decision Threshold</h3>

<table>
  <tr><th>Metric</th><th>Result</th></tr>
  <tr><td>OOF Threshold</td><td><strong>0.16892</strong></td></tr>
  <tr><td>Flagged OOF Applications</td><td>245 / 2,155</td></tr>
  <tr><td>Recall</td><td>0.46927</td></tr>
  <tr><td>Precision</td><td>0.34286</td></tr>
  <tr><td>Maximum Per-Period Flagged Fraction</td><td>11.749%</td></tr>
  <tr><td>Transported Final Threshold</td><td>0.1222584314</td></tr>
</table>

<p>
The out-of-fold policy satisfied the 12% per-period review-capacity constraint.
</p>

<h3>Challenge Predictions</h3>

<p>
After final fitting and calibration, the transported threshold was applied to a synthetic challenge batch containing 2,500 applications.
</p>

<p>
A total of 330 applications exceeded the transported threshold. To respect the 12% review-capacity limit, only the 300 highest-priority applications were selected.
</p>

<table>
  <tr><th>Metric</th><th>Result</th></tr>
  <tr><td>Total Applications</td><td>2,500</td></tr>
  <tr><td>Above-Threshold Applications</td><td>330</td></tr>
  <tr><td>Maximum Review Capacity</td><td>300</td></tr>
  <tr><td>Selected for Review</td><td><strong>300</strong></td></tr>
  <tr><td>Excluded Above-Threshold Cases</td><td>30</td></tr>
</table>

<h3>Challenge Capacity Visualization</h3>

<p align="center">
  <img src="tamweel_readme_images/lab5_challenge_capacity.png" alt="Final challenge review-capacity analysis" width="800">
</p>

<h3>Results and Interpretation</h3>

<p>
The final workflow combined predictive ranking, threshold selection, and capacity-aware prioritization.
</p>

<p>
The challenge results showed that operational capacity can prevent some above-threshold applications from being selected for review, even when their predicted scores exceed the policy threshold.
</p>

<p>
The final notebook reported <code>PROJECT_WORK_REQUIRED</code> because some required supporting reports and presentation materials were unavailable during that execution. The model-selection results therefore do not certify the entire submission package as complete.
</p>

<h3>Key Takeaway</h3>

<p>
The final model was selected based on forward-validation evidence rather than complexity alone. Logistic Regression provided the strongest reported mean Average Precision among the evaluated candidates, while the final decision policy enforced the available review capacity.
</p>

<hr>

<h2>Decision Policy and Human Oversight</h2>

<p>
Tamweel Lite is designed as a risk-based review-support workflow, not an automated financing approval system.
</p>

<ul>
  <li>Predicted scores are used to prioritize applications for human review.</li>
  <li>False negatives and false positives are evaluated using simulated costs.</li>
  <li>Review capacity is limited to 12% per period.</li>
  <li>Thresholds are selected using designated policy or out-of-fold evidence.</li>
  <li>A flagged application does not indicate a confirmed default.</li>
  <li>Applications selected for review are not automatically rejected.</li>
  <li>Human oversight remains necessary for interpreting and acting on predictions.</li>
</ul>

<hr>

<h2>Repository Structure</h2>

<p>
The following shows the intended project organization. Required submission artifacts should be verified against the actual repository contents.
</p>

<pre>
Shahad-Advanced-Machine-Learning-Methods-Tamweel-Lite-211/
|
|-- README.md
|
|-- tamweel_readme_images/
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

<h2>Quick Start</h2>

<h3>1. Open in Google Colab</h3>

<p>
Use the Google Colab badge at the top of this README to open the linked project notebook.
</p>

<h3>2. Prepare the Environment</h3>

<p>
Start a fresh Google Colab runtime and follow the dependency installation and data-verification instructions provided in the notebook.
</p>

<h3>3. Run the Experiments</h3>

<p>
Execute the notebook cells in their intended order and inspect the resulting evaluation metrics, visualizations, and decision-policy outputs.
</p>

<h3>4. Preserve Validation Integrity</h3>

<p>
Maintain the intended temporal and customer-aware separation. Do not replace it with random splitting or bypass dataset integrity checks.
</p>

<h3>5. Export the Deliverables</h3>

<p>
Download the executed notebooks, supporting reports, prediction file, and presentation required for submission.
</p>

<hr>

<h2>Interpretation and Limitations</h2>

<ul>
  <li><strong>Synthetic data:</strong> The dataset is intended for educational experimentation.</li>
  <li><strong>Real-world validity:</strong> Results have not been validated for operational lending decisions.</li>
  <li><strong>Validation:</strong> Temporal and customer-level separation are necessary for meaningful evaluation.</li>
  <li><strong>Explainability:</strong> SHAP and permutation importance describe model behavior but do not establish causality or fairness.</li>
  <li><strong>Calibration:</strong> Better probability calibration does not necessarily improve ranking performance or operational feasibility.</li>
  <li><strong>Evaluation reuse:</strong> Some evaluation data appeared earlier in the course and should not be described as a completely untouched final test.</li>
  <li><strong>Fairness:</strong> Descriptive regional error-rate comparisons do not constitute formal fairness certification.</li>
  <li><strong>Capacity:</strong> Review limits can exclude applications whose scores exceed the selected threshold.</li>
  <li><strong>Human oversight:</strong> Risk scores must not be treated as automatic financing decisions.</li>
</ul>

<hr>

<h2>Submission Deliverables</h2>

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
This README documents the experimental workflow and reported results. It does not replace the required submission artifacts.
</p>

<hr>

<h2>Training Program and Acknowledgments</h2>

<p>
This project was developed as part of <strong>SDA-DSC-211 — Advanced Machine Learning Methods</strong>, associated with <strong>SDAIA Academy</strong>.
</p>

<p>
<strong>Training Organization:</strong>
<a href="https://sdaia.gov.sa/">Saudi Data &amp; Artificial Intelligence Authority (SDAIA)</a>
</p>

<p>
<strong>Training Program:</strong>
<a href="https://almiyead-rgb.github.io/advanced-machine-learning-methods-sda-dsc-211/#start">Advanced Machine Learning Methods — SDA-DSC-211</a>
</p>

<p>
<strong>SDAIA Academy Course Materials on GitHub:</strong>
<a href="https://github.com/almiyead-rgb">Course Materials</a>
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
