# Model Building

## Purpose

Build a model for a defined prediction or estimation task, with a reproducible
training process and an artifact that can be evaluated independently. This
specification does not authorize deployment, production data access, or changes
to an external system.

## Required inputs

Before implementation, identify and record:

- The problem type and intended use of predictions.
- The target definition, prediction unit, and prediction time.
- The approved training data, its provenance, and any usage restrictions.
- The unit of observation, available features, and relevant time or group
  identifiers.
- The required split strategy, evaluation metric, and baseline, if specified.
- Runtime, interpretability, fairness, latency, or resource constraints.
- The required output artifact, interface, and location.

If essential information is unavailable, ask for it. If proceeding is safe and
useful, state each assumption and keep it configurable; do not present an
assumption as a user requirement.

## Requirements

1. Inspect the project and reuse its established data, training, and evaluation
   conventions. Prefer the smallest change that satisfies the task.
2. Verify the target and feature definitions. Exclude identifiers, post-outcome
   information, target-derived values, and other unavailable-at-prediction-time
   inputs unless their use is explicitly justified.
3. Select validation splits that reflect the intended use. Keep related entities
   together when required; respect time ordering for temporal prediction. Do not
   assume a random row split is valid.
4. Establish a simple baseline before adding complexity when feasible. Record
   the model family, feature set, split method, metric, and relevant
   configuration.
5. Fit all learned transformations, feature selection, resampling, and tuning
   only on training partitions. Apply the fitted transformations to validation
   or test partitions without refitting.
6. Keep the final test set untouched until model selection is complete. Do not
   use test results to tune features, hyperparameters, thresholds, or model
   choice.
7. Make randomness and configuration explicit where applicable. Keep training
   reproducible from documented inputs, code, and configuration; do not embed
   credentials or private data in source or artifacts.
8. Use a suitable loss/objective and optimization procedure for the problem.
   Handle class imbalance, missing values, and class/feature encoding
   deliberately rather than relying on undocumented defaults.
9. Save the minimum artifacts required to reproduce and use the model, such as
   fitted preprocessing, model parameters, feature names/order, configuration,
   and dependency/runtime metadata. Do not serialize unnecessary private data.
10. Do not claim the model is fair, causal, safe, production-ready, or
    state-of-the-art without appropriate evidence and a defined assessment.

## Expected deliverables

- Training code or a clear description of the implementation location.
- A reproducible configuration and documented input/split assumptions.
- The trained model artifact and any required fitted preprocessing artifact,
  when artifact creation is in scope.
- A concise training summary identifying data version, model, features,
  validation strategy, metric, and known limitations.
- Tests or checks appropriate to the changed code and artifact interface.

## Completion checklist

- [ ] Target, prediction unit, and intended use are explicit.
- [ ] Split strategy is appropriate and leakage risks have been checked.
- [ ] Preprocessing and selection are fitted using training data only.
- [ ] Baseline and model configuration are recorded.
- [ ] The artifact can be loaded and accepts the documented feature contract.
- [ ] Training is repeatable to the extent supported by the environment.
- [ ] Validation and test results are not misrepresented as guarantees.
- [ ] Relevant tests/checks pass, or failures and unrun checks are reported.

## Reporting

Report what was built, the exact data and validation strategy used, key results
with metric definitions, artifacts created, checks run, assumptions, and
limitations. Distinguish completed work from recommendations or unverified
claims.