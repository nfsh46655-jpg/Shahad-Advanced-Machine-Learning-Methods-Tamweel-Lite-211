
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tamweel Lite | Final Model Card</title>
  <style>
    * { box-sizing: border-box; }

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
      background: #fff;
      border-radius: 14px;
      box-shadow: 0 8px 28px rgba(20, 40, 70, .07);
    }

    h1, h2, h3 { color: #173b63; }

    h1 {
      margin: 0 0 6px;
      font-size: 32px;
    }

    h2 {
      margin-top: 36px;
      padding-bottom: 8px;
      border-bottom: 2px solid #e1e9f2;
    }

    h3 { margin-top: 24px; }

    .subtitle {
      color: #687a8c;
      margin-top: 4px;
    }

    .summary {
      padding: 18px;
      margin: 22px 0;
      background: #edf4fb;
      border-left: 4px solid #3476ac;
      border-radius: 6px;
    }

    .warning {
      padding: 16px;
      margin: 22px 0;
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

    .figure {
      padding: 16px;
      margin: 26px 0;
      border: 1px solid #dce5ef;
      border-radius: 10px;
      text-align: center;
      break-inside: avoid;
    }

    .figure img {
      display: block;
      width: 100%;
      max-width: 850px;
      height: auto;
      margin: auto;
      border-radius: 6px;
    }

    figcaption {
      margin-top: 12px;
      color: #617386;
      font-size: 14px;
    }

    code {
      background: #eef2f7;
      padding: 3px 6px;
      border-radius: 4px;
      overflow-wrap: anywhere;
    }

    footer {
      margin-top: 44px;
      padding-top: 18px;
      border-top: 1px solid #dce5ef;
      color: #687a8c;
      font-size: 13px;
    }

    @media (max-width: 650px) {
      body { padding: 10px; }
      main { padding: 24px; }
      h1 { font-size: 26px; }
      table { font-size: 13px; }
    }

    @media print {
      body { padding: 0; background: #fff; }
      main {
        padding: 0;
        border-radius: 0;
        box-shadow: none;
      }
      h2, h3 { break-after: avoid; }
      .figure, .summary, table { break-inside: avoid; }
    }
  </style>
</head>

<body>
<main>

<header>
  <h1>Tamweel Lite — Model Card</h1>
  <p class="subtitle">
    Advanced Machine Learning Methods | SDA-DSC-211<br>
    Lab 05 — Final Model Selection and Decision Policy<br>
    Student: Shahad Mamdouh Abu Shaheen<br>
    Selected Model: Logistic Regression
  </p>
</header>

<section>
  <h2>1. Purpose</h2>

  <p>
    Tamweel Lite is an educational machine learning project
    designed to estimate the probability of financing default
    within 90 days after an application.
  </p>

  <p>
    The project demonstrates leakage-aware model development,
    forward validation, candidate model comparison,
    probability calibration, cost-sensitive decision-making,
    and capacity-constrained application review.
  </p>
</section>

<section>
  <h2>2. Intended Use and Non-Use</h2>

  <h3>Intended Use</h3>
  <ul>
    <li>Educational financing risk prediction.</li>
    <li>Comparing predictive models and ensembles.</li>
    <li>Simulating application review prioritization.</li>
    <li>Evaluating thresholds and operational capacity.</li>
  </ul>

  <h3>Non-Use</h3>
  <ul>
    <li>Real financing approval or rejection decisions.</li>
    <li>Automated decisions affecting actual customers.</li>
    <li>Production deployment without independent validation.</li>
    <li>Claims about real-world financial performance.</li>
  </ul>
</section>

<section>
  <h2>3. Synthetic Data and Target</h2>

  <p>
    The project uses synthetic financing application data.
    The positive target represents default within 90 days
    after an application.
  </p>

  <p>
    Supervised evaluation requires outcomes to be mature
    before they are included in training or validation.
  </p>

  <h3>Final-Day Data Allocation</h3>

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
          <td>Fit and selection</td>
          <td>6,576</td>
          <td>3,931</td>
          <td>537</td>
        </tr>
        <tr>
          <td>Calibration</td>
          <td>836</td>
          <td>788</td>
          <td>78</td>
        </tr>
      </tbody>
    </table>
  </div>

  <p>
    The fit-and-selection period covers January 2022
    through April 2024. The calibration period covers
    July through September 2024.
  </p>

  <p>
    An additional 2,588 rows were excluded under
    the final-day eligibility rules.
  </p>
</section>

<section>
  <h2>4. Features and Timing</h2>

  <p>
    The predictive features are restricted to information
    available at application time. Relevant financial
    indicators include bureau score and debt-to-income ratio.
  </p>

  <p>
    Post-application information is excluded because it
    would introduce future-information leakage.
  </p>

  <p>
    Missing-value imputation and other learned preprocessing
    operations must be fitted only on training data within
    each validation boundary.
  </p>
</section>

<section>
  <h2>5. Validation and Leakage Controls</h2>

  <p>
    Model comparison uses nested forward out-of-fold (OOF)
    validation with chronological separation,
    customer-aware controls, and 90-day target maturity.
  </p>

  <ul>
    <li>2,155 live OOF prediction rows.</li>
    <li>Three forward validation periods.</li>
    <li>Warm-up observations without outer OOF predictions.</li>
    <li>Customer separation across validation boundaries.</li>
    <li>Preprocessing fitted within the training partitions.</li>
  </ul>

  <p>
    OOF metrics describe performance on eligible validation
    observations and should not be interpreted as independent
    production-test performance.
  </p>
</section>

<section>
  <h2>6. Models and Selection</h2>

  <p>
    Six candidates were compared using mean OOF
    Average Precision (AP).
  </p>

  <div class="table-wrap">
    <table>
      <thead>
        <tr>
          <th>Candidate</th>
          <th>Mean OOF AP</th>
          <th>Mean Brier</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>LightGBM</td>
          <td>0.34549</td>
          <td>0.06608</td>
        </tr>
        <tr>
          <td>XGBoost</td>
          <td>0.35263</td>
          <td>0.06566</td>
        </tr>
        <tr>
          <td><strong>Logistic Regression</strong></td>
          <td><strong>0.39166</strong></td>
          <td><strong>0.06327</strong></td>
        </tr>
        <tr>
          <td>Equal Averaging</td>
          <td>0.37170</td>
          <td>0.06435</td>
        </tr>
        <tr>
          <td>Weighted Averaging</td>
          <td>0.38942</td>
          <td>0.06332</td>
        </tr>
        <tr>
          <td>Stacking</td>
          <td>0.38314</td>
          <td>0.06603</td>
        </tr>
      </tbody>
    </table>
  </div>

  <div class="summary">
    <strong>Final Selection: Logistic Regression</strong>
    <p>
      Logistic Regression achieved the highest mean
      OOF Average Precision of 0.39166.
      The ensemble alternatives did not demonstrate
      sufficient improvement to replace the selected
      single model.
    </p>
  </div>

  <figure class="figure">
    <img
      src="assets/tamweel_readme_images/lab5_model_comparison.png"
      alt="Lab 05 comparison of six candidate models"
    >
    <figcaption>
      Figure 1. Model comparison using OOF Average Precision.
      Logistic Regression achieved the highest mean AP.
    </figcaption>
  </figure>
</section>

<section>
  <h2>7. Metrics and Calibration</h2>

  <h3>Selected Model — OOF Performance</h3>

  <div class="table-wrap">
    <table>
      <tr>
        <th>Metric</th>
        <th>Value</th>
      </tr>
      <tr>
        <td>Mean OOF Average Precision</td>
        <td>0.39166</td>
      </tr>
      <tr>
        <td>AP Fold Standard Deviation</td>
        <td>0.02981</td>
      </tr>
      <tr>
        <td>Mean Brier Score</td>
        <td>0.06327</td>
      </tr>
      <tr>
        <td>Mean ECE</td>
        <td>0.01882</td>
      </tr>
    </table>
  </div>

  <p>
    After model selection, a sigmoid calibrator was fitted
    using the reserved calibration partition.
  </p>

  <h3>Calibration-Fit Diagnostics</h3>

  <div class="table-wrap">
    <table>
      <tr>
        <th>Metric</th>
        <th>Raw</th>
        <th>Sigmoid</th>
      </tr>
      <tr>
        <td>ROC-AUC</td>
        <td>0.789037</td>
        <td>0.789037</td>
      </tr>
      <tr>
        <td>Average Precision</td>
        <td>0.287803</td>
        <td>0.287803</td>
      </tr>
      <tr>
        <td>Brier Score</td>
        <td>0.076473</td>
        <td>0.078058</td>
      </tr>
      <tr>
        <td>Log-loss</td>
        <td>0.266489</td>
        <td>0.277296</td>
      </tr>
      <tr>
        <td>ECE</td>
        <td>0.021121</td>
        <td>0.034871</td>
      </tr>
    </table>
  </div>

  <p>
    These diagnostics were calculated on 836 calibration
    observations containing 78 positive cases.
  </p>

  <p>
    Sigmoid calibration did not improve Brier Score,
    log-loss, or ECE on this fitting partition.
    Ranking metrics remained unchanged.
  </p>

  <div class="warning">
    <strong>Important:</strong>
    The calibration metrics were measured on the same
    partition used to fit the calibrator. They are
    diagnostic results, not independent evidence
    of calibration generalization.
  </div>
</section>

<section>
  <h2>8. Decision Policy and Capacity</h2>

  <p>
    The OOF decision threshold was selected using
    the simulated cost function:
  </p>

  <p><code>Loss = 10 * FN + FP</code></p>

  <h3>OOF Policy Results</h3>

  <div class="table-wrap">
    <table>
      <tr>
        <th>Measure</th>
        <th>Result</th>
      </tr>
      <tr>
        <td>Raw OOF threshold</td>
        <td>0.16892</td>
      </tr>
      <tr>
        <td>OOF observations</td>
        <td>2,155</td>
      </tr>
      <tr>
        <td>Flagged</td>
        <td>245</td>
      </tr>
      <tr>
        <td>True positives</td>
        <td>84</td>
      </tr>
      <tr>
        <td>False positives</td>
        <td>161</td>
      </tr>
      <tr>
        <td>False negatives</td>
        <td>95</td>
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
        <td>Simulated loss</td>
        <td>1,111 units</td>
      </tr>
    </table>
  </div>

  <p>
    The raw OOF threshold was transported through
    the frozen sigmoid calibration mapping.
  </p>

  <div class="summary">
    <strong>Final Calibrated Threshold</strong>
    <p>0.12225843144286948</p>
  </div>

  <p>
    The final decision rule is:
  </p>

  <p>
    <code>
      Flag if calibrated probability &gt;= threshold
    </code>
  </p>

  <p>
    Applications exceeding the threshold are ranked
    by calibrated probability, subject to the
    maximum review capacity.
  </p>

  <h3>Challenge Batch Results</h3>

  <div class="table-wrap">
    <table>
      <tr>
        <th>Measure</th>
        <th>Value</th>
      </tr>
      <tr>
        <td>Total applications</td>
        <td>2,500</td>
      </tr>
      <tr>
        <td>Review capacity</td>
        <td>300</td>
      </tr>
      <tr>
        <td>Threshold-eligible applications</td>
        <td>330</td>
      </tr>
      <tr>
        <td>Final flagged applications</td>
        <td>300</td>
      </tr>
      <tr>
        <td>Excluded by capacity</td>
        <td>30</td>
      </tr>
      <tr>
        <td>Capacity limit</td>
        <td>12%</td>
      </tr>
    </table>
  </div>

  <p>
    Of the 2,500 challenge applications, 330 exceeded
    the decision threshold. The final policy selected
    300 applications for review, meeting the 12%
    capacity limit.
  </p>

  <p>
    The challenge batch does not provide observed
    default outcomes at scoring time, so realized
    precision, recall, and cost cannot be calculated.
  </p>

  <figure class="figure">
    <img
      src="assets/tamweel_readme_images/lab5_challenge_capacity.png"
      alt="Lab 05 capacity-constrained challenge batch results"
    >
    <figcaption>
      Figure 2. Challenge-batch review capacity:
      330 threshold-eligible applications and
      300 selected for review.
    </figcaption>
  </figure>
</section>

<section>
  <h2>9. Fairness and Limitations</h2>

  <p>
    The final model should be monitored for differences
    in false-positive rates, recall, and review
    allocation across relevant population groups
    and geographic regions.
  </p>

  <p>
    Regional differences observed in OOF diagnostics
    require careful interpretation because group
    sample sizes and event counts may vary.
  </p>

  <ul>
    <li>
      Synthetic data may not represent real
      financing populations.
    </li>
    <li>
      Future economic and population changes
      may reduce model performance.
    </li>
    <li>
      OOF metrics do not guarantee deployment performance.
    </li>
    <li>
      Calibration-fit diagnostics are not
      independent validation.
    </li>
    <li>
      Capacity limits may exclude some
      threshold-eligible applications.
    </li>
    <li>
      Predictive associations do not
      establish causal relationships.
    </li>
  </ul>

  <p>
    Explanations generated for a different model
    in Lab 04 must not automatically be attributed
    to the final Logistic Regression model.
  </p>
</section>

<section>
  <h2>10. Reproducibility and Ownership</h2>

  <div class="table-wrap">
    <table>
      <tr>
        <th>Setting</th>
        <th>Value</th>
      </tr>
      <tr>
        <td>Experiment source</td>
        <td>LIVE</td>
      </tr>
      <tr>
        <td>Random seed</td>
        <td>211</td>
      </tr>
      <tr>
        <td>Execution mode</td>
        <td>CPU</td>
      </tr>
      <tr>
        <td>FAST_MODE</td>
        <td>True</td>
      </tr>
      <tr>
        <td>Parallel jobs</td>
        <td>2</td>
      </tr>
      <tr>
        <td>scikit-learn</td>
        <td>1.6.1</td>
      </tr>
      <tr>
        <td>XGBoost</td>
        <td>3.4.1</td>
      </tr>
      <tr>
        <td>LightGBM</td>
        <td>4.6.0</td>
      </tr>
    </table>
  </div>

  <p>
    The notebook recorded the reproducibility status
    <code>REPLAY_MATCH</code> and bundle verification
    status <code>BUNDLE_BYTES_VERIFIED</code>.
  </p>

  <p>
    The submission audit reported
    <code>PROJECT_WORK_REQUIRED</code>,
    indicating that some supporting submission
    materials were missing from the audited
    working directory.
  </p>

  <h3>Monitoring Plan</h3>
  <ul>
    <li>Monitor AP, ROC-AUC, Brier Score, and ECE.</li>
    <li>Monitor changes in feature distributions.</li>
    <li>Review regional and subgroup performance.</li>
    <li>Track false positives and false negatives.</li>
    <li>Monitor review capacity and excluded cases.</li>
    <li>Revalidate before any real-world deployment.</li>
  </ul>
</section>

<section>
  <h2>11. Final Conclusion</h2>

  <p>
    The final Tamweel Lite experiment selected
    Logistic Regression after comparing six
    predictive modeling approaches.
  </p>

  <p>
    The selected model achieved a mean OOF
    Average Precision of 0.39166, and the
    transported calibrated threshold was
    0.12225843144286948.
  </p>

  <p>
    In the challenge batch of 2,500 applications,
    300 applications were selected for review,
    satisfying the 12% operational capacity limit.
  </p>

  <p>
    The experiment demonstrates an educational
    workflow for model selection, calibration,
    cost-sensitive thresholding, and
    capacity-constrained inference.
  </p>
</section>

<section lang="ar" dir="rtl">
  <h2>12. الملخص العربي</h2>

  <p>
    يهدف مشروع Tamweel Lite إلى التنبؤ
    باحتمالية التعثر في التمويل خلال
    90 يومًا من تقديم الطلب باستخدام
    بيانات اصطناعية لأغراض تعليمية.
  </p>

  <p>
    تمت مقارنة ستة أساليب للتنبؤ،
    وتم اختيار نموذج Logistic Regression
    لأنه حقق أعلى متوسط
    Average Precision بقيمة 0.39166.
  </p>

  <p>
    بعد معايرة النموذج النهائي،
    تم اعتماد عتبة قرار بقيمة
    0.12225843144286948.
  </p>

  <p>
    عند تطبيق النموذج على 2,500 طلب،
    تجاوز 330 طلبًا عتبة القرار،
    لكن تم اختيار 300 طلب فقط للمراجعة
    وفق سقف السعة البالغ 12%.
  </p>

  <p>
    المشروع تعليمي، ولا تصلح نتائجه
    لاتخاذ قرارات تمويل حقيقية دون
    اختبارات إضافية للأداء والعدالة
    والاستقرار التشغيلي.
  </p>
</section>

<footer>
  Training-program reference:
  <a href="https://github.com/SDAIAAcademy">
    SDAIA Academy on GitHub
  </a>
</footer>

</main>
</body>
</html>
