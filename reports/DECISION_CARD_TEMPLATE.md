# Tamweel Lite — Decision Card

**Course:** Advanced Machine Learning Methods (SDA-DSC-211)  
**Project:** Tamweel Lite  
**Decision Stage:** Lab 03 — Cost-Sensitive Decision Making

## 1. Task and Positive Class

The objective is to estimate the probability that a financing applicant will default within **90 days after the application**.

The positive class (`1`) represents an applicant who experiences the defined default event within the prediction horizon. The negative class (`0`) represents an applicant who does not experience that event.

Predictions are generated using information available at the application decision point. Information collected after that point must not be used as a predictive feature.

This is an **educational simulation using synthetic data**. A positive prediction indicates that an application should be prioritized for review. It does not represent an actual financing approval or rejection.

## 2. Validation and Out-of-Fold Predictions

The project uses a time-aware and customer-aware validation approach to reduce information leakage.

The validation process considers:

- **Time separation:** Validation observations are evaluated using earlier training information.
- **Customer separation:** Repeated observations from the same customer must not cross the training and validation boundary.
- **Outcome maturity:** The 90-day outcome must be observable before a row is eligible for evaluation.
- **Preprocessing integrity:** Data transformations must be fitted on training data only.

The cleaned time/group validation experiment reported:

| Metric | Result |
|---|---:|
| Eligible evaluation applications | 5,039 |
| ROC-AUC | 0.7976 |
| Average Precision | 0.3153 |

The tuned experiment reported ROC-AUC of **0.7855** and Average Precision of **0.3133**, based on eight Optuna trials.

The exact OOF coverage, number of rows without OOF predictions, validation periods, and execution configuration should be confirmed from the saved Lab 03 notebook outputs before final submission.

## 3. Cost Function and Decision Threshold

The project applies the following simulated error costs:

| Error | Educational cost |
|---|---:|
| False Negative (FN) | 10 units |
| False Positive (FP) | 1 unit |

The total simulated loss is:

**Loss = 10 × FN + FP**

A false negative is assigned a higher cost because it represents a defaulting applicant who was not identified for review.

The decision rule is:

`Flag for review if score >= threshold`

The selected threshold from Lab 03 was:

**Threshold = 0.658347**

This threshold was selected while considering the simulated loss function and operational review capacity.

## 4. Review Capacity and Decision Results

The review capacity was limited to **12%** of eligible applications.

The reported Lab 03 results were:

| Measure | Result |
|---|---:|
| Eligible applications | 5,039 |
| Selected threshold | 0.658347 |
| Applications flagged | 526 |
| Recall | 0.4089 |
| Precision | 0.2985 |
| Simulated loss | 2,639 units |

The selected policy identifies higher-risk applications for manual review while controlling the volume of flagged applications.

## 5. Interpretation and Trade-offs

The threshold reflects a trade-off between detecting applicants who may default and limiting unnecessary reviews.

Lowering the threshold may identify more positive cases, but it can increase false positives and review workload.

Raising the threshold may reduce unnecessary reviews, but it can also increase missed positive cases.

The selected policy therefore considers both prediction quality and operational constraints rather than relying on classification accuracy alone.

## 6. Limitations

- The dataset is synthetic and does not represent actual financing customers.
- Error costs are educational assumptions rather than verified financial losses.
- Predictive performance may change across time periods or populations.
- A review flag is not an automated approval or rejection decision.
- Further monitoring, fairness assessment, calibration, and operational validation would be necessary before any real-world use.

## 7. Final Decision

For Lab 03, the documented decision policy uses a **0.658347 probability threshold** with a simulated loss function of **10 × FN + FP** and a **12% review-capacity constraint**.

This decision card documents the Lab 03 policy. The final model selection and transported threshold developed in Lab 05 are separate final-stage decisions and should be documented accordingly.
