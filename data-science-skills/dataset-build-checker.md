# Dataset Build Checker

## Purpose

Check whether a built dataset is structurally valid, reproducible, and
consistent with its declared data contract and intended use. A successful
check does not prove the data is unbiased, legally usable, or fit for every
downstream purpose.

## Required inputs

Obtain:

- The dataset build output and, when available, its source inputs and build
  configuration.
- The declared schema, including column names, types, nullability, units, and
  allowed values or ranges.
- The row grain (what one row represents), keys, and expected uniqueness.
- Required columns, constraints, and expected relationships between columns.
- Expected row-count or freshness bounds, if known.
- The build command/process, expected output location, and reproducibility
  requirements.
- Privacy, access, retention, and data handling constraints.

Do not invent authoritative thresholds. If a constraint is unknown, report it as
unspecified and make only descriptive checks.

## Requirements

1. Inspect metadata and a limited, privacy-safe sample before reading or
   printing full records. Avoid exposing sensitive values in logs or reports.
2. Verify that the output exists, is readable by the intended consumer, and
   conforms to the declared file/table format and schema.
3. Check required columns, unexpected columns, duplicate column names, data
   types, nullability, parse failures, and safe conversion behavior. Do not
   silently coerce or discard values to make checks pass.
4. Check row grain and key constraints: duplicate keys, null keys, unexpected
   cardinality, and valid relationships among tables where specified.
5. Check declared domain rules, ranges, enumerations, cross-column invariants,
   timestamp ordering, and referential integrity where applicable.
6. Measure row counts, missingness, duplicates, and relevant distributions.
   Compare against historical or expected values only when comparable baselines
   and thresholds are provided.
7. Check build lineage and reproducibility: source versions, configuration,
   transformation version, build time, and any deterministic requirements.
   Rebuild only when authorized and safe.
8. Check that train/validation/test datasets are separated according to the
   declared entity/time strategy and do not contain prohibited overlap.
9. Report each check as pass, fail, warning, or not checked. Include the rule,
   observed value/count, expected condition, and a safe-to-share diagnostic.
10. Never modify the dataset during validation. If a repair is requested,
    create a separate output and document the transformation; preserve the
    original.

## Expected deliverables

- A check report with dataset identity/version, timestamp, and validation
  configuration.
- A result for every declared rule, including failed and skipped checks.
- Summary counts for rows, columns, nulls, duplicates, and violations where
  applicable.
- Actionable findings that avoid disclosing raw sensitive records.
- A reproducible check procedure and explicit limitations.

## Completion checklist

- [ ] The checked dataset is identified by an unambiguous version or location.
- [ ] Declared schema and constraints were checked without silent coercion.
- [ ] Row grain, key, null, domain, and relationship rules were considered.
- [ ] Split overlap and lineage were checked when relevant.
- [ ] Every check has a visible status and useful diagnostic.
- [ ] Unknown thresholds are not presented as pass/fail requirements.
- [ ] The original dataset was not changed.
- [ ] Privacy restrictions were followed in samples, logs, and reports.

## Reporting

Summarize the overall outcome and blockers, then list failures, warnings, and
unchecked rules. An overall "pass" is permitted only when all required checks
pass; warnings must not hide a required failure.