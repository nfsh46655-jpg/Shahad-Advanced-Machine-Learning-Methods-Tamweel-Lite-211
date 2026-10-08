# Tamweel Lite — Model Card

**Course:** Advanced Machine Learning Methods | SDA-DSC-211  
**Lab:** 05 — Final Model Selection and Decision Policy  
**Student:** Shahad Mamdouh Abu Shaheen  
**Selected Model:** Logistic Regression  
**Project Type:** Educational Machine Learning Project

---

## 1. Purpose

Tamweel Lite is an educational machine learning project designed to predict the probability of financing default within 90 days after an application.

The project demonstrates a complete machine learning workflow, including data preparation, leakage-aware validation, model comparison, probability calibration, cost-sensitive decision-making, and capacity-constrained application review.

The main objective is to identify applications that may require additional review while minimizing simulated decision costs and respecting operational capacity.

## 2. Intended Use and Non-Use

**Intended Use**

- Educational financing risk prediction using synthetic data.
- Comparing machine learning algorithms and ensemble methods.
- Evaluating predictive performance and probability calibration.
- Simulating cost-sensitive review prioritization.
- Demonstrating capacity-constrained decision policies.

**Non-Use**

The model is not intended for real financing approvals or rejections, automated decisions affecting actual customers, or production deployment without independent validation.

Its predictions and explanations must not be treated as verified evidence of real-world financial risk.

## 3. Synthetic Data and Target

The project uses a synthetic dataset of 10,000 financing applications.

The prediction target is a binary indicator of whether an application results in default within 90 days.

The dataset contains approximately 7.89% positive cases, creating a class-imbalanced prediction problem.

### Final-Day Data Allocation

| Partition | Rows | Customers | Positive Cases |
|---|---:|---:|---:|
| Fit and Selection | 6,576 | 3,931 | 537 |
| Calibration | 836 | 788 | 78 |

The fit-and-selection period covers January 2022 through April 2024. The calibration period covers July through September 2024.

An additional 2,588 rows were excluded under the final-day eligibility and separation rules.

These exclusions help preserve chronological separation and reduce the risk of information leakage.

## 4. Features and Timing

The model uses financial and application-related information available at the time of the financing request.

Relevant predictors include bureau score, debt-to-income ratio, loan amount, and other application-time characteristics.

Information collected after the financing decision is excluded because it would not be available when making the prediction.

Missing-value imputation and other learned preprocessing operations are fitted using training data within each validation boundary.

This approach helps prevent future information from influencing model development.

## 5. Validation and Leakage Controls

The project uses nested forward out-of-fold (OOF) validation with chronological and customer-aware separation.

The validation design includes:

- Three forward validation periods.
- 2,155 eligible OOF prediction rows.
- Customer separation across validation boundaries.
- A 90-day target maturity requirement.
- Training-only preprocessing within each validation fold.
- Warm-up observations that do not receive outer OOF predictions.

These controls reduce the likelihood of overly optimistic performance estimates caused by repeated customers, future information, or preprocessing leakage.

**OOF Limitation:** OOF performance estimates describe the eligible historical validation observations. They are not equivalent to independent production-test results and do not guarantee future performance.

## 6. Models and Selection

Six candidate modeling approaches were compared using mean OOF Average Precision (AP).

| Model | Mean OOF AP | Mean Brier Score |
|---|---:|---:|
| LightGBM | 0.34549 | 0.06608 |
| XGBoost | 0.35263 | 0.06566 |
| **Logistic Regression** | **0.39166** | **0.06327** |
| Equal Averaging | 0.37170 | 0.06435 |
| Weighted Averaging | 0.38942 | 0.06332 |
| Stacking | 0.38314 | 0.06603 |

### Final Model Selection

**Logistic Regression was selected as the final model** because it achieved the highest mean OOF Average Precision of 0.39166.

The weighted ensemble achieved a competitive AP of 0.38942, but it did not outperform Logistic Regression.

The selected model therefore provided the strongest observed ranking performance among the evaluated candidates.

## 7. Metrics and Calibration

### Selected Model — OOF Performance

| Metric | Result |
|---|---:|
| Mean OOF Average Precision | 0.39166 |
| AP Fold Standard Deviation | 0.02981 |
| Mean OOF Brier Score | 0.06327 |
| Mean OOF ECE | 0.01882 |

After selecting Logistic Regression, sigmoid calibration was fitted using the reserved calibration partition.

### Calibration-Fit Diagnostics

| Metric | Raw | Sigmoid-Calibrated |
|---|---:|---:|
| ROC-AUC | 0.789037 | 0.789037 |
| Average Precision | 0.287803 | 0.287803 |
| Brier Score | 0.076473 | 0.078058 |
| Log-loss | 0.266489 | 0.277296 |
| ECE | 0.021121 | 0.034871 |

These results were measured on 836 calibration observations containing 78 positive cases.

Sigmoid calibration did not improve Brier Score, log-loss, or ECE on this partition. ROC-AUC and Average Precision remained unchanged.

**Important limitation:** These calibration diagnostics were calculated on the same partition used to fit the calibrator. They are diagnostic measurements, not independent evidence that calibration will generalize to unseen data.

The selected Logistic Regression model is also different from the LightGBM model explained in Lab 04. Therefore, Lab 04 SHAP explanations must not be presented as direct explanations of the final Logistic Regression model.

## 8. Decision Policy and Capacity

The decision policy uses a simulated cost function that assigns a higher penalty to missed defaults:

**Simulated Loss = 10 × False Negatives + False Positives**

The OOF decision threshold was selected using historical validation predictions.

### OOF Policy Results

| Measure | Result |
|---|---:|
| Raw OOF Threshold | 0.16892 |
| OOF Observations | 2,155 |
| Flagged Applications | 245 |
| True Positives | 84 |
| False Positives | 161 |
| False Negatives | 95 |
| Recall | 0.46927 |
| Precision | 0.34286 |
| Simulated Loss | 1,111 units |

The raw OOF threshold was transported through the fitted sigmoid calibration mapping.

**Final calibrated threshold: 0.12225843144286948**

An application is eligible for review when its calibrated probability is greater than or equal to the threshold.

### Challenge Batch Results

| Measure | Result |
|---|---:|
| Total Applications | 2,500 |
| Review Capacity | 300 |
| Capacity Limit | 12% |
| Applications Above Threshold | 330 |
| Final Selected Applications | 300 |
| Excluded Due to Capacity | 30 |

Of the 2,500 challenge applications, 330 exceeded the calibrated decision threshold.

Because the operational review capacity was limited to 12%, only the 300 highest-ranked eligible applications were selected for review.

The remaining 30 threshold-eligible applications were excluded by the capacity constraint.

The challenge batch does not provide observed default outcomes at scoring time. Therefore, realized precision, recall, and decision cost cannot be calculated for that batch.

The project demonstrates the difference between identifying risk and operating under limited review resources.

## 9. Fairness and Limitations

The final model has several important limitations.

**Synthetic Data:** The dataset is artificial and may not represent actual financing populations, customer behavior, or economic conditions.

**Class Imbalance:** Default cases represent a relatively small percentage of observations, making Average Precision particularly relevant.

**Historical Validation:** OOF metrics describe past eligible observations and do not guarantee future performance.

**Calibration:** The final calibration-fit diagnostics are not independent validation results.

**Operational Capacity:** Some applications exceeding the risk threshold may not receive review because capacity is limited.

**Model Explanations:** Explanations from the Day 4 LightGBM model cannot automatically be attributed to the final Logistic Regression model.

**Fairness:** Model performance and review allocation may differ across customer groups or geographic regions. Such differences require dedicated subgroup evaluation before any real-world use.

No claim of demographic fairness or equal error rates is made without supporting subgroup evidence.

## 10. Reproducibility and Ownership

### Experiment Configuration

| Setting | Value |
|---|---|
| Experiment Source | LIVE |
| Random Seed | 211 |
| Execution Environment | CPU |
| FAST_MODE | True |
| Parallel Jobs | 2 |
| scikit-learn | 1.6.1 |
| XGBoost | 3.4.1 |
| LightGBM | 4.6.0 |

The notebook recorded the reproducibility status `REPLAY_MATCH` and bundle verification status `BUNDLE_BYTES_VERIFIED`.

These results support reproducibility within the recorded experiment configuration. They do not guarantee identical behavior across every future software environment or dataset.

The submission audit also reported `PROJECT_WORK_REQUIRED`, indicating that some supporting submission materials were missing from the audited working directory at that time.

### Monitoring Plan

If the model were developed further, monitoring should include:

- Average Precision, ROC-AUC, Brier Score, and ECE.
- Changes in feature distributions and default prevalence.
- False-positive and false-negative rates.
- Performance differences across relevant customer groups and regions.
- Review capacity utilization and threshold-eligible exclusions.
- Periodic validation using newly matured 90-day outcomes.

Any production consideration would require independent testing, fairness assessment, governance review, and appropriate human oversight.

---

## 11. Final Model Linkage and Conclusion

The final Tamweel Lite experiment selected **Logistic Regression** after comparing six candidate approaches using forward OOF validation.

The selected model achieved a mean OOF Average Precision of **0.39166**, with a mean Brier Score of **0.06327**.

A sigmoid calibrator was fitted on the reserved calibration partition, and the OOF decision threshold was transported to a final calibrated threshold of **0.12225843144286948**.

For the challenge batch of 2,500 applications, 330 applications exceeded the threshold. The capacity-constrained policy selected 300 applications for review, meeting the 12% operational limit.

The experiment demonstrates a complete educational workflow for model comparison, leakage prevention, calibration, cost-sensitive decision-making, and operational review prioritization.

Its findings remain limited to synthetic data and the recorded experimental setting.

## 12. الملخص العربي

يهدف مشروع **Tamweel Lite** إلى التنبؤ باحتمالية التعثر في التمويل خلال 90 يومًا من تقديم الطلب، باستخدام بيانات اصطناعية لأغراض تعليمية.

تمت مقارنة ستة نماذج وأساليب مختلفة، واختيار نموذج **Logistic Regression** لأنه حقق أعلى متوسط لمقياس Average Precision بقيمة **0.39166** أثناء التحقق باستخدام OOF.

اعتمد المشروع على الفصل الزمني بين البيانات، ومنع تداخل العملاء بين مجموعات التدريب والتحقق، والتأكد من اكتمال فترة الـ90 يومًا قبل استخدام النتائج الفعلية.

بعد اختيار النموذج، تم تطبيق معايرة Sigmoid، واعتماد عتبة قرار نهائية بقيمة **0.12225843144286948**.

عند تطبيق النموذج على **2,500 طلب تمويل**، تجاوز **330 طلبًا** عتبة القرار. لكن بسبب تحديد سعة المراجعة بنسبة **12%**، تم اختيار **300 طلب فقط** وفق أعلى درجات المخاطر المتوقعة.

أظهرت التجربة أهمية الموازنة بين دقة النموذج، وتكلفة الأخطاء، والقدرة التشغيلية على مراجعة الطلبات.

مع ذلك، فإن نتائج المشروع تعليمية ولا تصلح لاتخاذ قرارات تمويل حقيقية دون اختبارات مستقلة إضافية تشمل الأداء والمعايرة والعدالة والاستقرار.

---

**Training-program reference:** [SDAIA Academy on GitHub](https://github.com/SDAIAAcademy)

<=د<div class="table-wrap">
      
