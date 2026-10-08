
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tamweel Lite | Interpretability and Calibration Report</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 32px 16px;
      background: #f3f6fa;
      font-family: Arial, sans-serif;
      color: #243447;
      line-height: 1.7;
    }

    main {
      max-width: 980px;
      margin: auto;
      padding: 48px;
      background: #ffffff;
      border-radius: 14px;
      box-shadow: 0 8px 28px rgba(20, 40, 70, 0.07);
    }

    h1, h2, h3 {
      color: #173b63;
    }

    h1 {
      margin: 0 0 8px;
      font-size: 32px;
    }

    h2 {
      margin-top: 38px;
      padding-bottom: 8px;
      border-bottom: 2px solid #e1e9f2;
    }

    h3 {
      margin-top: 24px;
    }

    .subtitle {
      color: #687a8c;
      margin-top: 4px;
    }

    .summary {
      margin: 22px 0;
      padding: 18px;
      background: #edf4fb;
      border-left: 4px solid #3476ac;
      border-radius: 6px;
    }

    .warning {
      margin: 22px 0;
      padding: 16px;
      background: #fff8ea;
      border-left: 4px solid #d09a35;
      border-radius: 6px;
    }

    .table-wrap {
      overflow-x: auto;
      margin: 20px 0;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th, td {
      border: 1px solid #dce5ef;
      padding: 11px 12px;
      text-align: left;
      vertical-align: top;
    }

    th {
      background: #eaf1f8;
      color: #173b63;
    }

    code {
      background: #eef2f7;
      padding: 3px 6px;
      border-radius: 4px;
      overflow-wrap: anywhere;
    }

    .formula {
      padding: 16px;
      margin: 18px 0;
      background: #f7f9fc;
      border: 1px solid #dce5ef;
      border-radius: 8px;
      text-align: center;
      font-weight: bold;
    }

    footer {
      margin-top: 44px;
      padding-top: 18px;
      border-top: 1px solid #dce5ef;
      color: #687a8c;
      font-size: 13px;
    }

    @media (max-width: 650px) {
      body {
        padding: 10px;
      }

      main {
        padding: 24px;
      }

      h1 {
        font-size: 26px;
      }

      table {
        font-size: 13px;
      }
    }

    @media print {
      body {
        padding: 0;
        background: #ffffff;
      }

      main {
        padding: 0;
        border-radius: 0;
        box-shadow: none;
      }

      h2, h3 {
        break-after: avoid;
      }

      table, .summary, .warning {
        break-inside: avoid;
      }
    }
  </style>
</head>

<body>
<main>

  <header>
    <h1>Tamweel Lite</h1>
    <h2>Interpretability and Calibration Report</h2>

    <p class="subtitle">
      Advanced Machine Learning Methods | SDA-DSC-211<br>
      Lab 04 — Model Explanation and Probability Calibration<br>
      Student: Shahad Mamdouh Abu Shaheen<br>
      Project Type: Educational Machine Learning Project
    </p>
  </header>

  <div class="summary">
    <strong>Report Overview</strong>
    <p>
      This report documents the interpretability, probability
      calibration, stability analysis, and operational review
      constraints of the Tamweel Lite financing risk model.
    </p>
    <p>
      The objective is to explain model predictions, evaluate
      the reliability of predicted probabilities, and examine
      the consequences of a capacity-constrained decision policy.
    </p>
    <p>
      All findings are based on synthetic financing data.
      The results are educational and must not be used
      to make actual financing decisions.
    </p>
  </div>

  <section>
    <h2>1. Explanation Source, Model, and Data Roles</h2>

    <h3>1.1 Explanation Source</h3>

    <p>
      <strong>Explanation source:</strong> LIVE
    </p>

    <p>
      The report describes outputs produced by the executed
      Day 4 experiment. The reported metrics and explanations
      are treated as experimental outputs rather than
      educational example values.
    </p>

    <h3>1.2 Model Configuration</h3>

    <p>
      The Day 4 experiment used a weighted LightGBM
      classification model to estimate the risk of
      financing default within 90 days of application.
    </p>

    <p>
      Model explanations were generated for the original
      tree model. A separate sigmoid calibration step
      transformed its raw predicted probabilities.
    </p>

    <p>
      The experiment was executed on CPU with
      FAST_MODE enabled.
    </p>

    <h3>1.3 Dataset and Prediction Target</h3>

    <p>
      Tamweel Lite uses synthetic financing applications.
      The positive class represents an application
      associated with default within the following
      90 days.
    </p>

    <p>
      Only information available at application time
      should be used as model input. Later collections
      or other post-application outcomes are not
      valid predictors at decision time.
    </p>

    <h3>1.4 Data Partition Roles</h3>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Partition</th>
            <th>Rows</th>
            <th>Customers</th>
            <th>Positive Cases</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Model Fit</td>
            <td>2,516</td>
            <td>1,853</td>
            <td>217</td>
          </tr>
          <tr>
            <td>Calibration</td>
            <td>584</td>
            <td>538</td>
            <td>40</td>
          </tr>
          <tr>
            <td>Policy Selection</td>
            <td>589</td>
            <td>566</td>
            <td>55</td>
          </tr>
          <tr>
            <td>Evaluation</td>
            <td>1,733</td>
            <td>1,520</td>
            <td>139</td>
          </tr>
        </tbody>
      </table>
    </div>

    <h3>1.5 Leakage Prevention</h3>

    <p>
      Chronological separation and customer-aware
      partitioning were used to reduce information
      leakage between model development and evaluation.
    </p>

    <p>
      A 90-day outcome maturity requirement was applied
      so that labels would only be considered available
      after the relevant observation window.
    </p>

    <p>
      The experiment excluded 4,578 records under
      its separation and eligibility rules.
    </p>

    <p>
      The evaluation in this report is an intermediate
      Day 4 assessment. It is not the final untouched
      evaluation of the entire course project.
    </p>
  </section>

  <section>
    <h2>2. Global and Local Interpretability</h2>

    <h3>2.1 Global Feature Importance</h3>

    <p>
      Three interpretation approaches were considered:
      LightGBM gain importance, permutation importance,
      and SHAP.
    </p>

    <p>
      Gain importance measures how strongly features
      contribute to tree splits during model training.
      It describes internal model structure but does
      not directly measure held-out predictive performance.
    </p>

    <p>
      Permutation importance evaluates how much a
      performance metric changes when a feature is
      disrupted in evaluation data.
    </p>

    <p>
      SHAP provides additive feature contributions
      to model predictions. Aggregating absolute SHAP
      values can describe global influence, while
      signed values help explain individual predictions.
    </p>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Feature</th>
            <th>Permutation AP Decrease</th>
            <th>Mean Absolute SHAP</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>bureau_score</td>
            <td>0.1270</td>
            <td>0.9042</td>
          </tr>
          <tr>
            <td>dti</td>
            <td>0.0690</td>
            <td>0.5437</td>
          </tr>
        </tbody>
      </table>
    </div>

    <p>
      Bureau score and debt-to-income ratio were
      influential under both permutation importance
      and SHAP analysis.
    </p>

    <p>
      Agreement between explanation methods provides
      useful supporting evidence, but importance
      rankings may differ because the methods measure
      different properties.
    </p>

    <h3>2.2 SHAP Units and Additivity</h3>

    <p>
      SHAP values were calculated for the raw LightGBM
      model output in log-odds units.
    </p>

    <div class="formula">
      Base Value + Sum of SHAP Values = Raw Model Margin
    </div>

    <p>
      The tree model's training-path background was
      used for the explanation. The observed maximum
      additivity error was approximately
      5.70 × 10<sup>-15</sup>.
    </p>

    <p>
      This small numerical error supports consistency
      between the base value, feature contributions,
      and reconstructed raw model output.
    </p>

    <p>
      A positive SHAP value increases the model's
      predicted log-odds of default relative to
      the explanation baseline.
    </p>

    <p>
      A negative SHAP value decreases those log-odds.
      Neither direction proves that changing the
      feature would cause a corresponding change
      in real-world default risk.
    </p>

    <h3>2.3 Correlation and Causality</h3>

    <p>
      Correlated financial features may share
      predictive information. Consequently,
      feature importance and SHAP attribution
      should not be interpreted as independent
      causal effects.
    </p>

    <p>
      These explanations describe learned model
      behavior, not the underlying causes of
      financial outcomes.
    </p>

    <h3>2.4 Local Application Explanation</h3>

    <p>
      <strong>Selected application:</strong> TR-009585
    </p>

    <p>
      The application was selected from the
      sampled SHAP evaluation requests because
      it had the highest raw model margin
      within that sample.
    </p>

    <p>
      The actual default outcome was not used
      to select or explain this application.
    </p>

    <div class="table-wrap">
      <table>
        <tr>
          <th>Prediction Output</th>
          <th>Value</th>
        </tr>
        <tr>
          <td>Raw Model Probability</td>
          <td>0.9031</td>
        </tr>
        <tr>
          <td>Sigmoid-Calibrated Probability</td>
          <td>0.4795</td>
        </tr>
      </table>
    </div>

    <h3>2.5 Leading Positive Reason Codes</h3>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Feature</th>
            <th>Observed Value</th>
            <th>SHAP Contribution</th>
            <th>Imputed</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>bureau_score</td>
            <td>497</td>
            <td>+2.269325</td>
            <td>No</td>
          </tr>
          <tr>
            <td>dti</td>
            <td>1.2806</td>
            <td>+1.198145</td>
            <td>No</td>
          </tr>
          <tr>
            <td>loan_amount_sar</td>
            <td>93,437.29</td>
            <td>+0.200725</td>
            <td>No</td>
          </tr>
        </tbody>
      </table>
    </div>

    <p>
      These were the three leading positive
      contributions to the raw model margin
      for the selected application.
    </p>

    <p>
      None of these three reported feature values
      was imputed.
    </p>

    <div class="warning">
      <strong>Interpretation Limitation</strong>
      <p>
        These SHAP values explain the uncalibrated
        LightGBM prediction. They must not be
        presented as direct additive explanations
        of the sigmoid-calibrated probability.
      </p>
      <p>
        The reported reasons are predictive
        associations, not causal explanations
        or recommendations for a real financing decision.
      </p>
    </div>
  </section>

  <section>
    <h2>3. Probability Calibration Evidence</h2>

    <h3>3.1 Calibration Method</h3>

    <p>
      Sigmoid calibration was fitted using the
      reserved calibration partition.
    </p>

    <p>
      This partition contained 584 applications
      and 40 positive outcomes.
    </p>

    <p>
      Calibration performance was evaluated on
      a separate later partition containing
      1,733 applications and 139 positive outcomes.
    </p>

    <p>
      The underlying LightGBM model and the
      fitted sigmoid calibrator were kept fixed
      during this evaluation.
    </p>

    <h3>3.2 Before-and-After Metrics</h3>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Metric</th>
            <th>Raw Model</th>
            <th>Sigmoid-Calibrated</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Brier Score</td>
            <td>0.113027</td>
            <td>0.067112</td>
          </tr>
          <tr>
            <td>Expected Calibration Error</td>
            <td>0.146871</td>
            <td>0.022486</td>
          </tr>
          <tr>
            <td>Log-loss</td>
            <td>0.357993</td>
            <td>0.246749</td>
          </tr>
          <tr>
            <td>Average Precision</td>
            <td>0.258677</td>
            <td>0.258677</td>
          </tr>
          <tr>
            <td>ROC-AUC</td>
            <td>0.770804</td>
            <td>0.770804</td>
          </tr>
        </tbody>
      </table>
    </div>

    <h3>3.3 Reliability Bins</h3>

    <p>
      Calibration reliability was examined
      using ten equal-width probability bins.
    </p>

    <p>
      Each bin compares the average predicted
      probability with the observed positive
      outcome frequency.
    </p>

    <p>
      The detailed ten-bin counts and observed
      event frequencies are stored in
      <code>day4_reliability_bins.csv</code>.
    </p>

    <p>
      This report does not substitute estimated
      bin counts for the original exported values.
      The CSV should be included as supporting
      evidence when submitting the report.
    </p>

    <h3>3.4 Calibration Interpretation</h3>

    <p>
      The Brier Score decreased from 0.113027
      to 0.067112 after sigmoid calibration.
    </p>

    <p>
      ECE decreased from 0.146871 to 0.022486,
      while log-loss decreased from 0.357993
      to 0.246749.
    </p>

    <p>
      These results indicate improved probability
      quality on the evaluation partition.
    </p>

    <p>
      Average Precision and ROC-AUC remained
      unchanged, indicating that the sigmoid
      transformation did not improve the
      measured ranking performance.
    </p>

    <div class="summary">
      <strong>Calibration Conclusion</strong>
      <p>
        Sigmoid calibration improved Brier Score,
        ECE, and log-loss on the Day 4 evaluation
        partition while preserving ranking metrics.
      </p>
      <p>
        This is evidence of improvement on the
        observed evaluation sample, not proof
        of perfect calibration or future reliability.
      </p>
    </div>
  </section>

  <section>
    <h2>4. Stability Analysis and Limitations</h2>

    <h3>4.1 Customer-Level Bootstrap</h3>

    <p>
      A paired customer-cluster bootstrap was used
      to evaluate uncertainty in the observed
      performance metrics.
    </p>

    <p>
      Customers were resampled as clusters,
      preserving the grouping of repeated
      applications belonging to the same customer.
    </p>

    <p>
      The experiment requested 200 bootstrap
      replicates. The model and sigmoid calibrator
      were not refitted within these replicates.
    </p>

    <p>
      Raw and calibrated predictions were evaluated
      on the same resampled customer groups.
      This paired comparison helps isolate the
      observed change associated with calibration.
    </p>

    <h3>4.2 Bootstrap Intervals</h3>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Metric</th>
            <th>Lower Bound</th>
            <th>Upper Bound</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Raw Average Precision</td>
            <td>0.197442</td>
            <td>0.337854</td>
          </tr>
          <tr>
            <td>Calibrated Average Precision</td>
            <td>0.197442</td>
            <td>0.337854</td>
          </tr>
          <tr>
            <td>Brier Score Change</td>
            <td>-0.054177</td>
            <td>-0.037409</td>
          </tr>
        </tbody>
      </table>
    </div>

    <p>
      The reported intervals are 95% customer-level
      bootstrap intervals.
    </p>

    <p>
      The number of valid draws after any filtering
      must be read from the exported stability summary,
      <code>day4_stability_summary.json</code>.
    </p>

    <p>
      The Brier change interval was negative,
      consistent with a lower Brier Score after
      calibration in this evaluation.
    </p>

    <h3>4.3 Differences Across Time Periods</h3>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Evaluation Period</th>
            <th>Average Precision</th>
            <th>Calibrated Brier Score</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>2024Q3</td>
            <td>0.27457</td>
            <td>0.07760</td>
          </tr>
          <tr>
            <td>2024Q4</td>
            <td>0.27050</td>
            <td>0.05734</td>
          </tr>
        </tbody>
      </table>
    </div>

    <p>
      Average Precision was similar across
      these two periods, while the calibrated
      Brier Score differed.
    </p>

    <p>
      This variation demonstrates the importance
      of checking model behavior across time
      rather than relying only on a single
      aggregate evaluation metric.
    </p>

    <h3>4.4 Local Sensitivity Test</h3>

    <p>
      A local sensitivity analysis was performed
      for the selected application by changing
      <code>bureau_score</code> by -1 and +1.
    </p>

    <p>
      The small perturbations produced approximately
      unchanged raw and calibrated probabilities,
      and the same leading positive reason codes.
    </p>

    <p>
      This is a narrow diagnostic test.
      It does not demonstrate stability under
      larger changes or across other customers.
    </p>

    <h3>4.5 Limits of the Stability Evidence</h3>

    <p>
      Customer-cluster bootstrap intervals describe
      sampling variability within the evaluated
      customer population.
    </p>

    <p>
      They do not incorporate uncertainty from
      retraining the model, refitting the calibrator,
      future economic conditions, or distribution shift.
    </p>

    <p>
      These intervals must not be described
      as guarantees of future performance
      or as confidence intervals for an
      individual customer's default probability.
    </p>
  </section>

  <section>
    <h2>5. Decision Threshold and Review Zone</h2>

    <h3>5.1 Policy Selection</h3>

    <p>
      The decision threshold was selected on
      the policy partition rather than on
      the evaluation partition.
    </p>

    <p>
      The policy used a simulated cost function
      with a higher penalty for missed defaults.
    </p>

    <div class="formula">
      Simulated Loss = 10 × False Negatives
      + 1 × False Positives
    </div>

    <p>
      The review-capacity constraint was 12%
      of applications.
    </p>

    <h3>5.2 Raw and Transported Thresholds</h3>

    <div class="table-wrap">
      <table>
        <tr>
          <th>Setting</th>
          <th>Value</th>
        </tr>
        <tr>
          <td>Raw Policy Threshold</td>
          <td>0.588195</td>
        </tr>
        <tr>
          <td>Transported Calibrated Threshold</td>
          <td>0.17331</td>
        </tr>
        <tr>
          <td>Decision Operator</td>
          <td>&gt;=</td>
        </tr>
        <tr>
          <td>Review Capacity</td>
          <td>12%</td>
        </tr>
        <tr>
          <td>Near-Threshold Diagnostic Band</td>
          <td>±0.02</td>
        </tr>
      </table>
    </div>

    <p>
      The selected raw threshold was transported
      through the frozen sigmoid calibration mapping.
    </p>

    <p>
      An application is flagged when its calibrated
      probability is greater than or equal to
      the transported threshold.
    </p>

    <div class="formula">
      Flag = Calibrated Probability &gt;= 0.17331
    </div>

    <h3>5.3 Policy Partition Result</h3>

    <p>
      On the policy partition, the selected
      threshold flagged 68 applications.
      The applicable review capacity was
      70 applications.
    </p>

    <p>
      This threshold satisfied the capacity
      requirement on the policy partition.
      It was then transported and evaluated
      without selecting a new threshold
      from the evaluation outcomes.
    </p>

    <h3>5.4 Evaluation Review Workload</h3>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>Period</th>
            <th>Applications</th>
            <th>12% Cap</th>
            <th>Flags</th>
            <th>Near Threshold</th>
            <th>Unique Union</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>2024Q3</td>
            <td>836</td>
            <td>100</td>
            <td>97</td>
            <td>23</td>
            <td>109</td>
          </tr>
          <tr>
            <td>2024Q4</td>
            <td>897</td>
            <td>107</td>
            <td>109</td>
            <td>21</td>
            <td>122</td>
          </tr>
        </tbody>
      </table>
    </div>

    <p>
      The unique union combines threshold flags
      and near-threshold applications without
      counting overlapping applications twice.
    </p>

    <p>
      In 2024Q3, 109 unique review candidates
      exceeded the capacity of 100.
    </p>

    <p>
      In 2024Q4, 122 unique review candidates
      exceeded the capacity of 107.
    </p>

    <h3>5.5 Meaning of the Review Zone</h3>

    <p>
      The ±0.02 band identifies predictions
      close to the calibrated decision threshold
      for diagnostic review.
    </p>

    <p>
      It is not a statistical confidence interval
      and does not quantify uncertainty in
      an individual prediction.
    </p>

    <h3>5.6 Capacity Review Requirement</h3>

    <div class="warning">
      <strong>CAPACITY_REVIEW_REQUIRED</strong>

      <p>
        The combined workload of risk flags
        and near-threshold candidates exceeded
        the permitted 12% review capacity
        in both evaluation periods.
      </p>

      <p>
        A future policy revision should be
        developed using appropriate development
        data and assessed using new evaluation
        evidence.
      </p>

      <p>
        The observed evaluation results should
        remain unchanged. The threshold must
        not be retrospectively adjusted using
        evaluation outcomes merely to hide
        the capacity violation.
      </p>
    </div>
  </section>

  <section>
    <h2>6. Interpretation Arguments and Supporting Files</h2>

    <h3>6.1 Global Versus Local Explanations</h3>

    <p>
      Global interpretation summarizes the
      features that influence model behavior
      across many applications.
    </p>

    <p>
      Local interpretation explains the
      contributions associated with one
      selected application.
    </p>

    <p>
      A feature that is important globally
      is not necessarily a leading reason
      for every individual prediction.
    </p>

    <h3>6.2 SHAP Units</h3>

    <p>
      SHAP values in this experiment are
      expressed in raw log-odds units.
    </p>

    <p>
      They are not probability percentages
      or percentage-point changes.
    </p>

    <p>
      The base value and feature contributions
      reconstruct the raw LightGBM margin,
      not the final sigmoid-calibrated probability.
    </p>

    <h3>6.3 Limits of Reason Codes</h3>

    <p>
      Reason codes describe predictive
      associations learned by the model.
    </p>

    <p>
      They do not prove causation and should
      not be used as standalone explanations
      for real financing approvals or rejections.
    </p>

    <p>
      Correlated features, missing-value
      handling, and the selected explanation
      background may influence attribution.
    </p>

    <h3>6.4 Calibration Evidence</h3>

    <p>
      The evaluation results showed lower
      Brier Score, ECE, and log-loss after
      sigmoid calibration.
    </p>

    <p>
      Average Precision and ROC-AUC remained
      unchanged, so the observed benefit
      concerned probability quality rather
      than ranking performance.
    </p>

    <p>
      These results support improvement
      on the evaluated sample but do not
      establish perfect calibration.
    </p>

    <h3>6.5 Stability Limitations</h3>

    <p>
      The paired customer-cluster bootstrap
      provides evidence about evaluation
      variability while keeping the model
      and calibrator fixed.
    </p>

    <p>
      Period comparisons and local sensitivity
      tests provide additional diagnostics,
      but none guarantees future performance.
    </p>

    <h3>6.6 Impact of the Review Zone on Capacity</h3>

    <p>
      Including near-threshold applications
      increases the number of cases that
      may require human review.
    </p>

    <p>
      Although the selected policy satisfied
      capacity on its development partition,
      the combined review workload exceeded
      the 12% limit in both evaluation periods.
    </p>

    <p>
      This creates an operational limitation
      requiring future policy development
      and independent evaluation.
    </p>

    <h3>6.7 Reproducibility and Evidence Package</h3>

    <p>
      The executed Day 4 notebook and its
      exported evidence package are the
      primary supporting materials.
    </p>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>File</th>
            <th>Purpose</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>04_explain_calibrate.ipynb</td>
            <td>Executed analysis and outputs</td>
          </tr>
          <tr>
            <td>day4_artifacts.zip</td>
            <td>Exported evidence package</td>
          </tr>
          <tr>
            <td>day4_reliability_bins.csv</td>
            <td>Ten-bin calibration evidence</td>
          </tr>
          <tr>
            <td>day4_bootstrap.csv</td>
            <td>Bootstrap replicate results</td>
          </tr>
          <tr>
            <td>day4_stability_summary.json</td>
            <td>Bootstrap interval summary</td>
          </tr>
          <tr>
            <td>day4_reason_codes.csv</td>
            <td>Local explanation reasons</td>
          </tr>
          <tr>
            <td>day4_local_stability.csv</td>
            <td>Local sensitivity diagnostics</td>
          </tr>
          <tr>
            <td>day4_capacity.csv</td>
            <td>Period-level review workload</td>
          </tr>
        </tbody>
      </table>
    </div>

    <h3>6.8 Educational Scope and Review Readiness</h3>

    <p>
      All analyses were performed for an
      educational machine learning project
      using synthetic financing data.
    </p>

    <p>
      EDUCATIONAL_EXAMPLE material must be
      clearly labeled and must not be
      represented as personally executed
      experimental evidence.
    </p>

    <p>
      The notebook's READY_FOR_REVIEW status
      indicates completion of its reflection
      fields. It is not an automatic grade
      or an independent confirmation of
      operational readiness.
    </p>

    <p>
      The separate CAPACITY_REVIEW_REQUIRED
      finding remains an unresolved
      operational limitation.
    </p>
  </section>

  <section>
    <h2>Final Conclusion</h2>

    <p>
      The Tamweel Lite Day 4 experiment
      examined the interpretability and
      calibration of a weighted LightGBM
      financing risk model.
    </p>

    <p>
      Global importance analysis identified
      bureau_score and debt-to-income ratio
      as influential predictive features.
      Local SHAP analysis provided
      application-specific contributions
      in raw log-odds units.
    </p>

    <p>
      Sigmoid calibration improved Brier Score,
      ECE, and log-loss on the evaluation
      partition without changing Average
      Precision or ROC-AUC.
    </p>

    <p>
      Customer-level bootstrap and
      period-specific comparisons provided
      additional stability evidence, subject
      to sampling and future-distribution
      limitations.
    </p>

    <p>
      The transported decision threshold
      satisfied the policy development
      capacity constraint, but the combined
      evaluation review workload exceeded
      the 12% capacity limit.
    </p>

    <p>
      Therefore, the experiment supports
      educational conclusions about model
      explanation, calibration, and policy
      evaluation, while identifying an
      operational issue requiring future
      policy development and validation.
    </p>
  </section>

  <footer>
    <p>
      <strong>Project:</strong> Tamweel Lite<br>
      <strong>Course:</strong> Advanced Machine Learning Methods<br>
      <strong>Student:</strong> Shahad Mamdouh Abu Shaheen
    </p>

    <p>
      Training-program reference:
      <a href="https://github.com/SDAIAAcademy">
        SDAIA Academy on GitHub
      </a>
    </p>
  </footer>

</main>
</body>
</html>
