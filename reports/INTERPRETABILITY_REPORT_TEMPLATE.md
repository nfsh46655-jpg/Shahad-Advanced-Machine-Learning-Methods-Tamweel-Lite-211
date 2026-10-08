
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tamweel Lite | Interpretability & Calibration Report</title>
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Arial, sans-serif;
      line-height: 1.7;
      color: #243247;
      background: #f4f7fb;
      margin: 0;
      padding: 32px 16px;
    }

    main {
      max-width: 960px;
      margin: auto;
      background: white;
      padding: 48px;
      border-radius: 14px;
      box-shadow: 0 6px 25px rgba(0,0,0,.06);
    }

    h1 { color: #17365d; margin-bottom: 8px; }
    h2 {
      color: #17365d;
      border-bottom: 2px solid #dbe5f0;
      padding-bottom: 8px;
      margin-top: 36px;
    }
    h3 { color: #315b86; }

    .subtitle { color: #66788d; }
    .notice {
      background: #fff8e8;
      border-left: 4px solid #d5a03c;
      padding: 14px 18px;
      margin: 20px 0;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin: 18px 0;
    }
    th, td {
      border: 1px solid #dce4ed;
      padding: 11px;
      text-align: left;
    }
    th { background: #eaf1f9; color: #17365d; }

    code {
      background: #eef2f6;
      padding: 3px 6px;
      border-radius: 4px;
    }

    .footer {
      border-top: 1px solid #dce4ed;
      margin-top: 40px;
      padding-top: 16px;
      font-size: 13px;
      color: #66788d;
    }

    @media (max-width: 600px) {
      main { padding: 22px; }
      body { padding: 10px; }
    }

    @media print {
      body { background: white; padding: 0; }
      main { box-shadow: none; padding: 0; }
    }
  </style>
</head>

<body>
<main>

  <h1>Tamweel Lite</h1>
  <p class="subtitle">
    Interpretability & Calibration Report<br>
    Advanced Machine Learning Methods | SDA-DSC-211<br>
    Lab 04 — Explainability, Calibration & Decision Review
  </p>

  <h2>1. Project Overview</h2>
  <p>
    Tamweel Lite is an educational machine learning project
    that predicts the probability of financing default within
    90 days after an application.
  </p>
  <p>
    This report examines model interpretability, probability
    calibration, prediction stability, and operational review
    capacity. All data are synthetic, and the predictions are
    intended for educational review prioritization rather than
    real financing approval or rejection.
  </p>

  <h2>2. Model and Data Separation</h2>
  <p>
    The experiment distinguishes four data roles:
  </p>
  <ul>
    <li><strong>Fit:</strong> Training the predictive model.</li>
    <li><strong>Calibration:</strong> Fitting the sigmoid calibrator.</li>
    <li><strong>Policy:</strong> Selecting the decision threshold.</li>
    <li><strong>Evaluation:</strong> Assessing the frozen model and policy.</li>
  </ul>
  <p>
    Time-aware validation, customer separation, and maturity
    of the 90-day target are required to reduce data leakage.
    The evaluation in Lab 04 is not the final course test.
  </p>

  <div class="notice">
    <strong>Notebook verification required:</strong>
    Confirm the explanation source (LIVE or
    EDUCATIONAL_EXAMPLE), model configuration, role-specific
    row counts, customer counts, positive cases, and date
    boundaries from the executed Lab 04 notebook.
  </div>

  <h2>3. Global Feature Importance</h2>
  <p>
    Three complementary explanation methods are considered:
  </p>
  <ul>
    <li>
      <strong>Gain:</strong> Measures feature contributions
      to tree-based splitting improvements.
    </li>
    <li>
      <strong>Permutation importance:</strong> Measures
      performance deterioration when feature values
      are shuffled.
    </li>
    <li>
      <strong>SHAP:</strong> Estimates feature contributions
      relative to a reference prediction.
    </li>
  </ul>

  <h3>Permutation Importance Results</h3>
  <table>
    <thead>
      <tr>
        <th>Feature</th>
        <th>Average Precision Decrease</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>bureau_score</td><td>0.1270</td></tr>
      <tr><td>dti</td><td>0.0690</td></tr>
    </tbody>
  </table>

  <p>
    Bureau score and debt-to-income ratio were influential
    predictors in the evaluated model. These results indicate
    model dependence, not causal effects.
  </p>

  <h2>4. SHAP Explanations</h2>
  <p>
    When SHAP is calculated on the model's raw log-odds output,
    its contributions follow:
  </p>
  <p>
    <code>Raw model output = Base value + Sum(SHAP values)</code>
  </p>
  <p>
    Positive SHAP values increase the raw predicted default
    risk relative to the reference output, while negative
    values decrease it.
  </p>
  <p>
    The background data should come from the training
    partition. Correlated predictors may share predictive
    information, so SHAP contributions must not be
    interpreted as causal explanations.
  </p>

  <h3>Local Explanation</h3>
  <p>
    A local explanation describes one application selected
    through a documented rule that does not rely on knowing
    the eventual outcome.
  </p>
  <p>
    The report should identify no more than three positive
    contributing factors, their SHAP values, and whether
    any corresponding feature values were imputed.
  </p>
  <p>
    Local SHAP values from the raw predictive model should
    not be presented as direct explanations of the
    calibrated probability.
  </p>

  <div class="notice">
    <strong>To complete:</strong> Local application ID,
    selection rule, up to three contributing factors,
    SHAP values, imputation indicators, and the
    SHAP additivity check.
  </div>

  <h2>5. Probability Calibration</h2>
  <p>
    Sigmoid calibration was used to improve the agreement
    between predicted default probabilities and observed
    event frequencies.
  </p>
  <p>
    The calibrator must be fitted using the calibration
    partition and evaluated on separate observations.
  </p>

  <h3>Calibration Metrics</h3>
  <table>
    <thead>
      <tr>
        <th>Metric</th>
        <th>Before Calibration</th>
        <th>After Calibration</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Average Precision</td>
        <td>0.258677</td>
        <td>0.258677</td>
      </tr>
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
        <td>Not verified</td>
        <td>Not verified</td>
      </tr>
      <tr>
        <td>ROC-AUC</td>
        <td>Not verified</td>
        <td>Not verified</td>
      </tr>
    </tbody>
  </table>

  <h3>Calibration Interpretation</h3>
  <p>
    The Brier Score decreased from 0.113027 to 0.067112,
    indicating improved probability accuracy.
    Expected Calibration Error decreased from 0.146871
    to 0.022486.
  </p>
  <p>
    Average Precision remained at 0.258677.
    These findings support improved calibration in the
    evaluated sample but do not establish perfect
    calibration or guarantee future performance.
  </p>

  <div class="notice">
    <strong>To complete:</strong> Evaluation sample size,
    number of positive outcomes, log-loss, ROC-AUC,
    and the observed counts in all ten calibration bins.
  </div>

  <h2>6. Stability and Bootstrap Analysis</h2>
  <p>
    Customer-level bootstrap resampling can be used
    to examine the stability of evaluation metrics.
  </p>
  <p>
    Paired comparisons should use the same sampled
    customers for both predictions while keeping the
    trained model and calibrator fixed.
  </p>
  <p>
    Bootstrap intervals reflect sampling variability
    under the chosen procedure. They are not confidence
    intervals for an individual applicant's default
    probability or guarantees of future results.
  </p>
  <p>
    Differences across time periods and any
    <code>bureau_score +/- 1</code> sensitivity experiment
    should be documented using actual notebook outputs.
  </p>

  <div class="notice">
    <strong>To complete:</strong> Bootstrap interval bounds,
    number of valid draws, paired metric differences,
    period comparisons, and sensitivity-test results
    if performed.
  </div>

  <h2>7. Decision Threshold and Review Capacity</h2>
  <p>
    Applications are flagged using:
  </p>
  <p><code>Flag for review if score &gt;= threshold</code></p>

  <p>
    The operational review-capacity limit is
    <strong>12% per period</strong>.
    The near-threshold diagnostic margin is
    <strong>+/- 0.02</strong>.
  </p>
  <p>
    This margin identifies predictions near the decision
    boundary. It is not a statistical confidence interval.
  </p>

  <h3>Reported Capacity Diagnostics</h3>
  <table>
    <thead>
      <tr>
        <th>Measure</th>
        <th>Reported Result</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Threshold</td><td>0.588195</td></tr>
      <tr><td>Flagged applications</td><td>68</td></tr>
      <tr><td>Overall capacity</td><td>70</td></tr>
      <tr>
        <td>2024 Q3 near-threshold candidates</td>
        <td>109</td>
      </tr>
      <tr>
        <td>2024 Q3 capacity</td>
        <td>100</td>
      </tr>
      <tr>
        <td>2024 Q4 near-threshold candidates</td>
        <td>122</td>
      </tr>
      <tr>
        <td>2024 Q4 capacity</td>
        <td>107</td>
      </tr>
    </tbody>
  </table>

  <h3>Capacity Finding</h3>
  <p>
    The observed diagnostic returned
    <code>CAPACITY_REVIEW_REQUIRED</code>.
  </p>
  <p>
    The additional near-threshold review workload exceeded
    the available capacity in two periods.
    A revised operational policy would require separate
    development and evaluation before being adopted.
  </p>
  <p>
    The raw threshold, transported threshold, flagged
    counts, near-threshold counts, and deduplicated union
    totals should be confirmed from the notebook.
  </p>

  <h2>8. Interpretation and Limitations</h2>
  <ul>
    <li>
      Global explanations summarize model behavior
      across observations; local explanations describe
      one prediction.
    </li>
    <li>
      Raw-output SHAP contributions are expressed in
      log-odds, not calibrated probabilities.
    </li>
    <li>
      Feature importance does not establish causation.
    </li>
    <li>
      Calibration improvements are specific to the
      evaluated data and metrics.
    </li>
    <li>
      Bootstrap results cannot guarantee performance
      under future population or economic changes.
    </li>
    <li>
      Near-threshold review workload must be considered
      alongside the standard review capacity.
    </li>
  </ul>

  <h2>9. Evidence and Review Readiness</h2>
  <p>
    Supporting evidence should include the executed
    Lab 04 notebook, explanation outputs, calibration
    diagnostics, bootstrap summaries, and review-capacity
    calculations.
  </p>
  <p>
    A reflection status of <code>READY_FOR_REVIEW</code>
    indicates that required reflection fields were
    completed. It does not automatically certify that
    every operational constraint has been satisfied.
  </p>

  <h2>10. Conclusion</h2>
  <p>
    Lab 04 illustrates how explainability, calibration,
    uncertainty assessment, and operational review
    capacity contribute to responsible model evaluation.
  </p>
  <p>
    Reported sigmoid calibration improved the Brier
    Score and Expected Calibration Error while Average
    Precision remained unchanged.
  </p>
  <p>
    Permutation importance highlighted bureau_score
    and dti as influential features. The review-capacity
    diagnostic also identified additional workload
    beyond the available capacity in some periods.
  </p>
  <p>
    The experiment remains educational and uses
    synthetic financing data. All unverified details
    must be completed from the actual executed notebook
    before final submission.
  </p>

  <div class="footer">
    Training-program reference:
    <a href="https://github.com/SDAIAAcademy">
      SDAIA Academy on GitHub
    </a>
  </div>

</main>
</body>
</html>
