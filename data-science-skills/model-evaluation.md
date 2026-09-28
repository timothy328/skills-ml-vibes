# Model Evaluation

## Purpose

Assess whether a specified model meets defined predictive requirements on data
that was not improperly used to train, select, or tune it. Evaluation describes
observed evidence; it does not by itself establish causality, fairness, safety,
or future performance.

## Required inputs

Identify:

- The model artifact and its preprocessing, feature, and output contracts.
- The evaluation dataset, version, provenance, and permitted use.
- The target definition, prediction unit, and any prediction-time constraints.
- The evaluation question and intended deployment or decision context.
- Primary metric(s), metric direction, acceptance threshold(s), and baseline.
- Relevant groups, time periods, costs of errors, or operating thresholds.
- The required report format and whether this is validation, final test, or
  ongoing monitoring.

If a primary metric or acceptance criterion is not specified, propose a
context-appropriate choice and label it as a recommendation, not an agreed
threshold.

## Requirements

1. Verify that the model and evaluation data are compatible: same target
   meaning, units, feature definitions, preprocessing, and prediction horizon.
2. Confirm the evaluation data is independent for the stated purpose. Check for
   overlap, duplicates, entity leakage, temporal leakage, and data that may
   have influenced model or threshold selection.
3. Preserve the evaluation data. Do not refit, tune, select features, or change
   the decision threshold based on final test results.
4. Define each metric precisely, including positive class, averaging method,
   threshold, weighting, and aggregation unit where applicable. Choose metrics
   that reflect the task and error costs; include a baseline for context.
5. Report the evaluated sample and class/group counts, missing or excluded
   records, and any filtering. Explain exclusions and quantify their impact
   where feasible.
6. Report uncertainty when appropriate, using a method consistent with the
   sampling and dependence structure. Do not treat correlated observations as
   independent merely to narrow confidence intervals.
7. For classification, consider threshold-dependent and threshold-independent
   measures, confusion/error counts, and calibration when relevant. For
   regression, consider scale-aware error and residual behavior. For ranking,
   forecasting, clustering, or other tasks, choose metrics appropriate to the
   task and compare to meaningful baselines.
8. Examine important slices or subgroups when justified and permitted.
   Identify small sample sizes and avoid unsupported conclusions from noisy
   slices. Do not infer protected attributes or expose sensitive records.
9. Compare like with like: identical cohorts, target, and evaluation protocol
   for model comparisons. Document any differences.
10. Make results reproducible: record model/data versions, code/configuration,
    metric implementation, split or cohort, and random seed where relevant.

## Expected deliverables

- A concise evaluation report with purpose, data/model versions, protocol, and
  metric definitions.
- Metric values with sample sizes, baselines, thresholds, and uncertainty where
  applicable.
- Error analysis and relevant subgroup or temporal findings, with limitations.
- Reproducible evaluation code or a record of the exact procedure used.
- A clear outcome against each stated acceptance criterion: pass, fail, or
  inconclusive.

## Completion checklist

- [ ] Evaluation data is appropriate and independent for the claim being made.
- [ ] No final-test feedback was used to tune the evaluated model.
- [ ] Metrics, cohort, threshold, and aggregation are fully specified.
- [ ] Baseline, sample sizes, exclusions, and uncertainty are reported.
- [ ] Relevant slices and failure modes are examined without overclaiming.
- [ ] Results are reproducible and tied to model/data versions.
- [ ] Pass/fail decisions use supplied criteria; absent criteria are not invented.
- [ ] Failed, skipped, or inconclusive checks are visible in the report.

## Reporting

State the evaluation scope first, followed by methodology, results, acceptance
status, limitations, and recommended next steps. Separate measured results from
interpretation and do not claim generalization beyond the evidence.