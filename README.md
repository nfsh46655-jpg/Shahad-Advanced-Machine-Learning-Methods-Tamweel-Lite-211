
<div align="center">

<h1>Advanced Machine Learning Methods-Tamweel Lite</h1>

<p>
An end-to-end machine learning capstone for predicting financing default risk, evaluating advanced classification models, explaining predictions, and optimizing review decisions under operational constraints.
</p>

<p>
<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
<img src="https://img.shields.io/badge/Machine%20Learning-Advanced-6C63FF?style=flat-square" alt="Machine Learning">
<img src="https://img.shields.io/badge/SDAIA-Academy-008C87?style=flat-square" alt="SDAIA Academy">
</p>

<p>
<strong>Developer:</strong> Shahad Mamdouh Abu Shaheen<br>
<strong>Project Type:</strong> Individual Capstone Project
</p>

<a href="https://colab.research.google.com/drive/1Cw8_A6PngwrjMEweEB4MoIC0d07aF6wV?usp=sharing">
<img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab">
</a>

</div>

<hr>

<h2>Project Overview</h2>

<p>
<strong>Tamweel Lite</strong> is a machine learning project designed to predict the probability of financing default within 90 days using synthetic financing application data.
</p>

<p>
The project covers data exploration, baseline classification, gradient boosting, leakage-safe validation, hyperparameter tuning, cost-sensitive learning, explainable AI, probability calibration, ensemble modeling, and final risk-based decision optimization.
</p>

<p>
The objective is to develop reliable predictive models and translate their outputs into practical review decisions while respecting operational constraints.
</p>

<h3>Dataset</h3>

<table>
<tr><th>Property</th><th>Value</th></tr>
<tr><td>Applications</td><td>10,000</td></tr>
<tr><td>Predictor Features</td><td>22</td></tr>
<tr><td>Target</td><td>Default within 90 days</td></tr>
<tr><td>Default Rate</td><td>7.89%</td></tr>
<tr><td>Missing Values</td><td>766</td></tr>
<tr><td>Dataset Type</td><td>Synthetic financing data</td></tr>
</table>

<hr>

<h2>Key Results</h2>

<table>
<tr><th>Metric</th><th>Result</th></tr>
<tr><td>Final Selected Model</td><td><strong>Logistic Regression</strong></td></tr>
<tr><td>Mean Out-of-Fold Average Precision</td><td><strong>0.39166</strong></td></tr>
<tr><td>OOF AP Standard Deviation</td><td>0.02981</td></tr>
<tr><td>Mean OOF Brier Score</td><td>0.06327</td></tr>
<tr><td>Final Decision Threshold</td><td>0.1222584314</td></tr>
<tr><td>Review Capacity</td><td>12%</td></tr>
<tr><td>Challenge Applications</td><td>2,500</td></tr>
<tr><td>Selected for Review</td><td><strong>300</strong></td></tr>
</table>

<p>
Logistic Regression achieved the highest mean Average Precision in the final forward-validation comparison, outperforming the evaluated boosting and ensemble alternatives.
</p>

<hr>

<h2>Lab 01 — Baseline Models and Gradient Boosting</h2>

<h3>Objective</h3>

<p>
Build baseline classification models and compare their performance in predicting financing default risk.
</p>

<h3>Implementation</h3>

<p>
I explored the dataset, examined class imbalance and missing values, prepared the features, and trained Logistic Regression, XGBoost, and LightGBM models.
</p>

<p>
Model performance was evaluated using ROC-AUC and Average Precision, with particular attention to the minority default class.
</p>

<h3>Results</h3>

<table>
<tr><th>Model</th><th>ROC-AUC</th><th>Average Precision</th></tr>
<tr><td>Logistic Regression</td><td><strong>0.8213</strong></td><td>0.3258</td></tr>
<tr><td>XGBoost</td><td>0.8124</td><td><strong>0.3338</strong></td></tr>
<tr><td>LightGBM</td><td>0.8138</td><td>0.3248</td></tr>
</table>

<p align="center">
<img src="tamweel_readme_images/assets/lab1_model_comparison.png" alt="Lab 1 Model Comparison" width="800">
</p>

<p>
<strong>Outcome:</strong> XGBoost achieved the highest preliminary Average Precision, while Logistic Regression achieved the highest ROC-AUC. These baseline results motivated further investigation using stricter validation.
</p>

<hr>

<h2>Lab 02 — Validation and Hyperparameter Optimization</h2>

<h3>Objective</h3>

<p>
Improve model evaluation reliability by preventing data leakage and applying time-based, customer-aware validation.
</p>

<h3>Implementation</h3>

<p>
I implemented forward-in-time validation, investigated customer overlap and target-maturation leakage, and compared unsafe random controls against clean validation strategies.
</p>

<p>
I also performed hyperparameter optimization using Optuna to assess whether tuning improved model generalization.
</p>

<h3>Results</h3>

<table>
<tr><th>Validation Strategy</th><th>ROC-AUC</th><th>Average Precision</th></tr>
<tr><td>Leaky Random Control</td><td>0.9999</td><td>0.9988</td></tr>
<tr><td>Clean Random Control</td><td>0.8010</td><td>0.3110</td></tr>
<tr><td>Clean Time/Group — Fixed</td><td><strong>0.7976</strong></td><td><strong>0.3153</strong></td></tr>
<tr><td>Clean Time/Group — Tuned</td><td>0.7855</td><td>0.3133</td></tr>
</table>

<p align="center">
<img src="tamweel_readme_images/assets/lab2_validation_comparison.png" alt="Lab 2 Validation Comparison" width="800">
</p>

<p>
<strong>Outcome:</strong> The leaky control produced unrealistically high scores. Clean temporal validation provided more trustworthy results, and the fixed configuration slightly outperformed the tuned model.
</p>

<hr>

<h2>Lab 03 — Cost-Sensitive Learning and Threshold Optimization</h2>

<h3>Objective</h3>

<p>
Optimize classification decisions by considering class imbalance, asymmetric error costs, and limited review capacity.
</p>

<h3>Implementation</h3>

<p>
I compared imbalance-handling strategies, evaluated false-positive and false-negative costs, and analyzed decision thresholds using out-of-fold predictions.
</p>

<p>
The simulated decision policy assigned a higher cost to missed defaults and limited the number of applications that could be flagged for review.
</p>

<h3>Results</h3>

<table>
<tr><th>Metric</th><th>Result</th></tr>
<tr><td>False Negative Cost</td><td>10</td></tr>
<tr><td>False Positive Cost</td><td>1</td></tr>
<tr><td>Selected Threshold</td><td><strong>0.658347</strong></td></tr>
<tr><td>Flagged Applications</td><td>526 / 5,039</td></tr>
<tr><td>Recall</td><td>0.4089</td></tr>
<tr><td>Precision</td><td>0.2985</td></tr>
<tr><td>Simulated Cost</td><td>2,639</td></tr>
</table>

<p align="center">
<img src="tamweel_readme_images/assets/lab3_cost_threshold.png" alt="Lab 3 Cost and Threshold Analysis" width="800">
</p>

<p>
<strong>Outcome:</strong> The experiment demonstrated how decision thresholds influence financial risk, missed defaults, and operational workload. The selected policy balanced simulated error costs with review constraints.
</p>

<hr>

<h2>Lab 04 — Explainable AI and Probability Calibration</h2>

<h3>Objective</h3>

<p>
Interpret model predictions, identify influential features, and improve the reliability of predicted probabilities.
</p>

<h3>Implementation</h3>

<p>
I applied SHAP and permutation importance to investigate model behavior and understand which features contributed most strongly to risk predictions.
</p>

<p>
I then evaluated sigmoid probability calibration and compared probability quality before and after calibration.
</p>

<h3>Feature Importance</h3>

<table>
<tr><th>Feature</th><th>Permutation AP Decrease</th></tr>
<tr><td>bureau_score</td><td><strong>0.1270</strong></td></tr>
<tr><td>dti</td><td>0.0690</td></tr>
</table>

<p align="center">
<img src="tamweel_readme_images/assets/lab4_shap.png" alt="Lab 4 SHAP Explainability" width="800">
</p>

<h3>Calibration Results</h3>

<table>
<tr><th>Metric</th><th>Before</th><th>After</th></tr>
<tr><td>Average Precision</td><td>0.258677</td><td>0.258677</td></tr>
<tr><td>Brier Score</td><td>0.113027</td><td><strong>0.067112</strong></td></tr>
<tr><td>Expected Calibration Error</td><td>0.146871</td><td><strong>0.022486</strong></td></tr>
</table>

<p align="center">
<img src="tamweel_readme_images/assets/lab4_calibration.png" alt="Lab 4 Probability Calibration" width="800">
</p>

<p>
<strong>Outcome:</strong> Bureau score and debt-to-income ratio were influential predictors. Calibration substantially improved probability reliability while preserving the reported Average Precision.
</p>

<hr>

<h2>Lab 05 — Ensemble Learning and Final Model Selection</h2>

<h3>Objective</h3>

<p>
Compare individual and ensemble models, select the best-supported approach, and generate final challenge predictions.
</p>

<h3>Implementation</h3>

<p>
I evaluated Logistic Regression, XGBoost, LightGBM, equal-weight averaging, weighted averaging, and stacking using three forward-validation periods.
</p>

<p>
After comparing predictive performance and stability, I selected the final model and applied a capacity-aware decision policy to the challenge dataset.
</p>

<h3>Model Comparison</h3>

<table>
<tr><th>Model</th><th>Mean OOF AP</th><th>Standard Deviation</th></tr>
<tr><td>LightGBM</td><td>0.34549</td><td>0.04348</td></tr>
<tr><td>XGBoost</td><td>0.35263</td><td>0.02904</td></tr>
<tr><td><strong>Logistic Regression</strong></td><td><strong>0.39166</strong></td><td>0.02981</td></tr>
<tr><td>Equal Averaging</td><td>0.37170</td><td>0.03258</td></tr>
<tr><td>Weighted Averaging</td><td>0.38942</td><td>0.02906</td></tr>
<tr><td>Stacking</td><td>0.38314</td><td>0.02949</td></tr>
</table>

<p align="center">
<img src="tamweel_readme_images/assets/lab5_model_selection.png" alt="Lab 5 Model Selection" width="800">
</p>

<h3>Challenge Results</h3>

<table>
<tr><th>Metric</th><th>Result</th></tr>
<tr><td>Challenge Applications</td><td>2,500</td></tr>
<tr><td>Applications Above Threshold</td><td>330</td></tr>
<tr><td>Review Capacity</td><td>300</td></tr>
<tr><td>Final Flagged Applications</td><td><strong>300</strong></td></tr>
<tr><td>Final Threshold</td><td>0.1222584314</td></tr>
</table>

<p align="center">
<img src="tamweel_readme_images/assets/lab5_challenge_capacity.png" alt="Lab 5 Challenge Review Capacity" width="800">
</p>

<p>
<strong>Outcome:</strong> Logistic Regression achieved the strongest mean out-of-fold Average Precision. The final policy selected the 300 highest-priority applications while respecting the 12% review-capacity limit.
</p>

<hr>

<h2>Technical Pipeline</h2>

<ol>
<li>Explore and validate the synthetic financing dataset.</li>
<li>Prepare features and train baseline classification models.</li>
<li>Compare Logistic Regression, XGBoost, and LightGBM.</li>
<li>Apply leakage-safe temporal and customer-aware validation.</li>
<li>Optimize hyperparameters using Optuna.</li>
<li>Evaluate class imbalance and cost-sensitive thresholds.</li>
<li>Interpret model predictions using SHAP and permutation importance.</li>
<li>Evaluate probability calibration.</li>
<li>Compare individual models and ensemble methods.</li>
<li>Select the final model and generate capacity-constrained challenge predictions.</li>
</ol>

<hr>

<h2>Run the Project</h2>

<p>
Open the executed project notebook in Google Colab:
</p>

<p>
<a href="https://colab.research.google.com/drive/1Cw8_A6PngwrjMEweEB4MoIC0d07aF6wV?usp=sharing">
<img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab">
</a>
</p>

<p>
Follow the notebook instructions to configure the environment, access the dataset, and execute the machine learning experiments.
</p>

<hr>

<h2>Interpretation and Limitations</h2>

<ul>
<li>The dataset is synthetic and intended for educational experimentation.</li>
<li>Model performance has not been validated on real-world financing applications.</li>
<li>Data leakage can produce misleading evaluation results.</li>
<li>Feature explanations indicate model behavior, not causation.</li>
<li>Review capacity may limit the number of high-risk applications selected.</li>
<li>Predictions are intended to support human review rather than automatic financing decisions.</li>
</ul>

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
<p><strong>Developed by Shahad Mamdouh Abu Shaheen</strong></p>
<p>Advanced Machine Learning Methods | SDAIA Academy</p>
</div>
