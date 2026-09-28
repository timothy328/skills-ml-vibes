# Uniform Preprocessor

## Purpose

Define and apply a consistent, reusable transformation from raw input features
to model-ready features. Training and inference must use the same fitted
transformation and feature contract.

## Required inputs

Identify:

- Raw data schema, feature meanings, units, and row grain.
- Target and columns that must never enter preprocessing or the model.
- Training/validation/inference data boundaries.
- Required output schema, feature order, and data types.
- Missing, invalid, unseen-category, and outlier policies.
- Any domain-approved transformations and constraints.
- Serialization, versioning, and compatibility requirements for the fitted
  preprocessor.

If behavior for missing or unseen values is unspecified, choose an explicit,
configurable policy appropriate to the project and document it before use.

## Requirements

1. Separate raw input validation, transformation fitting, and transformation
   application. Expose a stable fit/transform contract or equivalent.
2. Fit data-dependent operations only on the training partition. This includes
   imputation statistics, scaling parameters, category vocabularies, feature
   selection, outlier thresholds, and dimensionality reduction.
3. Apply the learned parameters unchanged to validation, test, and inference
   inputs. Do not refit implicitly on new batches or test data.
4. Make feature inclusion explicit. Exclude targets, identifiers, leakage
   columns, and metadata not available at prediction time.
5. Define deterministic handling of missing values, invalid values, unseen
   categories, constant columns, and type mismatches. Prefer explicit
   diagnostics or configured behavior over silent dropping or conversion.
6. Preserve row identity and order unless the contract explicitly allows
   otherwise. If rows are filtered or expanded, record a mapping and reason.
7. Ensure output column names, ordering, types, units, and dimensionality are
   stable and documented. Prevent train/inference feature drift caused by
   implicit column ordering.
8. Avoid mutating caller-owned input data. Avoid storing raw records in fitted
   preprocessing artifacts unless necessary and explicitly permitted.
9. Version the preprocessing configuration and artifact together with the
   associated model. Validate that incompatible model/preprocessor versions
   cannot be silently combined.
10. Keep transformation logic environment-agnostic; use the project's existing
    stack and avoid adding dependencies unless needed and approved.

## Expected deliverables

- Reusable preprocessing implementation and explicit raw/output feature
  contracts.
- Fitted preprocessing artifact, when the task includes training.
- Configuration describing policies and learned/declared transformations.
- Tests for normal input, missing/invalid values, unseen categories, schema
  mismatch, row preservation, and train/inference parity.
- Usage notes covering fit boundaries, artifact loading, and version
  compatibility.

## Completion checklist

- [ ] All fitted state comes from training data only.
- [ ] Inference uses the same persisted transformation state as training.
- [ ] Feature inclusion, order, types, and exceptional-value policies are clear.
- [ ] Row changes and coercions cannot happen silently.
- [ ] Inputs are not mutated and sensitive data is not unnecessarily persisted.
- [ ] Compatibility and reproducibility checks exist.
- [ ] Tests demonstrate train/inference parity and edge-case behavior.

## Reporting

List transformations, fit data boundary, exception policies, output contract,
artifact/version details, and test results. Clearly state any input assumptions
or unsupported input cases.