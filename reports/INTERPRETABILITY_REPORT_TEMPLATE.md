
<article>
  <h1>Tamweel Lite — Interpretability and Calibration Report</h1>
  <p><strong>Course:</strong> Advanced Machine Learning Methods (SDA-DSC-211)</p>
  <p><strong>Project:</strong> Tamweel Lite</p>
  <p><strong>Lab:</strong> Day 04 — Explainability, Calibration and Review Policy</p>

  <h2>1. Source, Model and Data Roles</h2>

  <p>
    This report documents the Day 04 interpretation and calibration
    experiment. The prediction task is to estimate the probability
    of default within 90 days after a financing application.
    All data are synthetic and used for educational purposes.
  </p>

  <p>
    <strong>Explanation source:</strong>
    The exact LIVE or EDUCATIONAL_EXAMPLE setting must be confirmed
    from the saved notebook output. Educational examples must not
    be presented as results from a live experiment.
  </p>

  <p>
    <strong>Model configuration:</strong>
    The trained model and its exact hyperparameters must be copied
    from the Day 04 execution record.
  </p>

  <table border="1" cellpadding="7">
    <tr>
      <th>Data role</th>
      <th>Rows</th>
      <th>Unique customers</th>
      <th>Positive outcomes</th>
    </tr>
    <tr><td>Fit</td><td>Not verified</td><td>Not verified</td><td>Not verified</td></tr>
    <tr><td>Calibration</td><td>Not verified</td><td>Not verified</td><td>Not verified</td></tr>
    <tr><td>Policy</td><td>Not verified</td><td>Not verified</td><td>Not verified</td></tr>
    <tr><td>Evaluation</td><td>Not verified</td><td>Not verified</td><td>Not verified</td></tr>
  </table>

  <p>
    Fit, calibration, policy and evaluation data serve distinct
    purposes. Validation must respect customer separation,
    chronological ordering and 90-day outcome maturity.
    Evaluation in Day 04 is not the final course challenge test.
  </p>

  <h2>2. Global and Local Interpretability</h2>

  <p>
    Three interpretation approaches are considered:
  </p>

  <ul>
    <li><strong>Gain:</strong> Measures a feature's contribution to improvements in tree splits.</li>
    <li><strong>Permutation importance:</strong> Measures performance deterioration when a feature is shuffled.</li>
    <li><strong>SHAP:</strong> Attributes individual model outputs to feature contributions.</li>
  </ul>

  <p>
    The recorded permutation-importance experiment showed
    the following decreases in Average Precision:
  </p>

  <table border="1" cellpadding="7">
    <tr><th>Feature</th><th>AP decrease</th></tr>
    <tr><td>bureau_score</td><td>0.1270</td></tr>
    <tr><td>dti</td><td>0.0690</td></tr>
  </table>

  <p>
    These results indicate that bureau_score and debt-to-income
    ratio were influential for the evaluated model.
    Feature importance does not establish causation.
    Correlated features can share or redistribute importance.
  </p>

  <p>
    For a binary classifier explained on the raw margin,
    SHAP values are expressed in log-odds units.
    The local consistency check is:
  </p>

  <pre>raw_model_output ≈ base_value + sum(SHAP_values)</pre>

  <p>
    The background distribution should come from training data,
    not from the final evaluation sample.
    Positive SHAP contributions increase the raw model output;
    negative contributions decrease it.
  </p>

  <p>
    <strong>Local explanation:</strong>
    The selected application, selection rule, up to three positive
    contributing features, their values and missing-value
    imputation status must be verified from the saved Day 04 output.
    The actual observed outcome should not be used to select
    or explain the case.
  </p>

  <p>
    Raw-model SHAP explanations must not be described as direct
    explanations of the calibrated probability.
  </p>

  <h2>3. Calibration Evidence</h2>

  <p>
    Sigmoid calibration was evaluated to improve the relationship
    between predicted probabilities and observed event frequencies.
    The sigmoid calibrator must be fitted on calibration data
    separate from the evaluation data.
  </p>

  <table border="1" cellpadding="7">
    <tr><th>Metric</th><th>Before calibration</th><th>After calibration</th></tr>
    <tr><td>Brier score</td><td>0.113027</td><td>0.067112</td></tr>
    <tr><td>ECE</td><td>0.146871</td><td>0.022486</td></tr>
    <tr><td>Average Precision</td><td>0.258677</td><td>0.258677</td></tr>
    <tr><td>Log-loss</td><td>Not verified</td><td>Not verified</td></tr>
    <tr><td>ROC-AUC</td><td>Not verified</td><td>Not verified</td></tr>
  </table>

  <p>
    The recorded Brier score decreased from 0.113027 to 0.067112,
    while ECE decreased from 0.146871 to 0.022486.
    Average Precision remained unchanged at 0.258677.
  </p>

  <p>
    These results support improved probability calibration on
    the evaluated sample without demonstrating improved ranking.
    They do not prove perfect calibration or future performance.
  </p>

  <p>
    <strong>Required calibration diagnostics:</strong>
    The evaluation sample size, positive count and counts in
    each of the ten probability bins must be inserted from
    the saved notebook outputs.
  </p>

  <h2>4. Stability and Its Limitations</h2>

  <p>
    Customer-level bootstrap resampling is used to assess
    variability while accounting for repeated customer records.
    The trained model and sigmoid calibrator should remain fixed
    throughout the resampling procedure.
  </p>

  <p>
    Before-and-after calibration metrics should be calculated
    on the same bootstrap draw so that comparisons are paired.
    The number of valid draws and the bootstrap interval
    endpoints must be taken from the experiment outputs.
  </p>

  <p>
    <strong>Valid bootstrap draws:</strong> Not verified.<br>
    <strong>Bootstrap intervals:</strong> Not verified.<br>
    <strong>Period-level differences:</strong> Not verified.<br>
    <strong>bureau_score ±1 sensitivity test:</strong>
    Execution and results not verified.
  </p>

  <p>
    Bootstrap intervals summarize uncertainty in the measured
    sample-level performance. They do not guarantee future
    performance and are not confidence intervals for the
    default probability of an individual application.
  </p>

  <h2>5. Threshold and Review Region</h2>

  <p>
    The policy flags applications according to:
  </p>

  <pre>flag_for_review = score &gt;= threshold</pre>

  <p>
    The threshold is selected using the policy data, not
    optimized after observing evaluation outcomes.
    The raw threshold and its calibrated transported equivalent
    must be confirmed from the Day 04 notebook.
  </p>

  <p>
    <strong>Recorded threshold:</strong> 0.588195.
    Its exact role as raw or transported threshold
    must be confirmed from the saved output.
  </p>

  <p>
    The review capacity is limited to 12% per period.
    A diagnostic near-threshold region of ±0.02 was also examined.
    This region is not a statistical confidence interval.
  </p>

  <table border="1" cellpadding="7">
    <tr>
      <th>Period</th>
      <th>Near-threshold review candidates</th>
      <th>Capacity</th>
      <th>Status</th>
    </tr>
    <tr>
      <td>2024 Q3</td>
      <td>109</td>
      <td>100</td>
      <td>Capacity exceeded</td>
    </tr>
    <tr>
      <td>2024 Q4</td>
      <td>122</td>
      <td>107</td>
      <td>Capacity exceeded</td>
    </tr>
  </table>

  <p>
    One recorded result contained 68 flagged applications
    against an overall capacity of 70.
    However, the expanded near-threshold review workload
    exceeded the available capacity in the periods shown above.
  </p>

  <p>
    The counts of flagged applications, near-threshold candidates
    and their unique union must be documented separately to
    avoid double-counting overlapping applications.
  </p>

  <p>
    The recorded status CAPACITY_REVIEW_REQUIRED indicates that
    the proposed review region cannot be adopted unchanged
    within the stated operational constraint.
  </p>

  <p>
    A revised review policy would require a new development
    and evaluation process. The observed evaluation results
    should not be retrospectively altered to make the policy
    appear compliant.
  </p>

  <h2>6. Reasoning and Supporting Files</h2>

  <p>
    <strong>Global versus local explanations:</strong>
    Global explanations describe overall model behavior,
    whereas local explanations describe contributions
    for one selected application.
  </p>

  <p>
    <strong>SHAP units:</strong>
    SHAP contributions on the raw binary classification margin
    are in log-odds units, not probability percentage points.
  </p>

  <p>
    <strong>Limitations of reason codes:</strong>
    Feature contributions describe model associations.
    They do not establish causal explanations or justify
    real financing decisions on their own.
  </p>

  <p>
    <strong>Calibration evidence:</strong>
    Brier score and ECE improved in the recorded experiment,
    while Average Precision remained unchanged.
  </p>

  <p>
    <strong>Stability limitations:</strong>
    Bootstrap and sensitivity analyses describe observed
    variability under their assumptions; they are not
    guarantees about future applications.
  </p>

  <p>
    <strong>Capacity implications:</strong>
    Expanding review to near-threshold applications
    can exceed the available review capacity.
    This requires explicit policy reconsideration.
  </p>

  <p>
    <strong>Supporting materials:</strong>
    Include the executed Day 04 notebook, generated plots,
    calibration diagnostics and the experiment artifact bundle.
    Any EDUCATIONAL_EXAMPLE output must be clearly labeled
    and must not be claimed as a personal experiment.
  </p>

  <p>
    A READY_FOR_REVIEW reflection status means that required
    reflection fields have been completed. It is not an
    automatic grade or proof that all operational constraints
    have been satisfied.
  </p>
</article>
