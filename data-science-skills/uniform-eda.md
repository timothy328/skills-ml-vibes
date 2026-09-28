# Uniform Exploratory Data Analysis (EDA)

## Purpose

Produce a repeatable, privacy-conscious overview of a dataset that helps users
understand its structure, quality, distributions, and relationships. EDA is
descriptive and hypothesis-generating; it does not establish causation.

## Required inputs

Identify:

- Dataset location, version, provenance, and permitted use.
- Intended question or downstream task, if known.
- Data dictionary or definitions, units, row grain, and key columns.
- Sensitive fields and restrictions on display, retention, or sharing.
- Relevant time, group, target, and sampling fields.
- Desired report audience and output format.

When definitions are missing, label inferred types or interpretations as
tentative. Do not infer or disclose sensitive attributes.

## Requirements

1. Verify the dataset identity, dimensions, schema, data types, and row grain
   before analyzing it. Avoid loading more data than necessary.
2. Summarize missingness, duplicates, key uniqueness, ranges, invalid values,
   category cardinality, and data freshness where relevant.
3. Describe numeric and categorical distributions with suitable summaries and
   visualizations. Make units, denominators, and sample sizes clear.
4. Examine target distributions, time patterns, or group structure only when
   relevant and permitted. Avoid leaking private values in tables or plots.
5. Examine correlations and associations as descriptive results. State
   limitations, confounding, sampling bias, and multiple-comparison risks where
   material; never phrase association as causation without a causal design.
6. Check data-quality issues and distribution anomalies against domain
   definitions or supplied expectations. Mark unverified thresholds as
   exploratory observations, not violations.
7. Use privacy-safe aggregation. Suppress or coarsen small groups when
   disclosure risk warrants it; do not include raw personal or confidential
   records in reports.
8. Keep analysis reproducible: record dataset version, code/configuration,
   filtering, sampling, and random seed if sampling is used.
9. Do not alter the source dataset. Clearly separate exploratory cleaning or
   display transformations from authoritative preprocessing.
10. Make plots readable and accessible with labeled axes, units, legends, and
    non-color-only distinctions where practical.

## Expected deliverables

- A concise report describing dataset scope and methods.
- Schema and data-quality summaries with counts and denominators.
- Relevant univariate, temporal, or relationship summaries/plots.
- Findings prioritized by impact and evidence, including caveats.
- Reproducible analysis code or a clear record of the procedure.

## Completion checklist

- [ ] Dataset, version, row grain, and relevant definitions are stated.
- [ ] Missingness, duplicates, types, ranges, and unusual values are reviewed.
- [ ] Summaries identify their sample, filters, and denominators.
- [ ] Claims are descriptive and not overstated as causal or representative.
- [ ] Sensitive values and small groups are handled safely.
- [ ] Exploratory transformations are not confused with production processing.
- [ ] Report and plots can be reproduced from recorded inputs and settings.

## Reporting

Start with dataset scope and the most consequential findings. Distinguish
observed facts, interpretations, and proposed follow-up work. Include
limitations and disclose incomplete analyses.