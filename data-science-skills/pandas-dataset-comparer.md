# Pandas Dataset Comparer

## Purpose

Compare two tabular datasets using pandas or an equivalent pandas-compatible
workflow and report schema, key, value, and distribution differences. The
comparison is read-only: it must not mutate either source.

## Required inputs

Specify:

- The two dataset locations/versions and how each should be loaded.
- Whether rows represent the same entities/observations.
- Key column(s) for matching rows, or confirmation that row-by-row comparison
  is intended.
- Column mappings, ignored columns, and comparison scope.
- Type, null, string normalization, and numeric tolerance policies.
- Whether ordering matters and how duplicates should be treated.
- Privacy limits and expected report format.

Do not assume row order or a key that is not defined. If matching semantics are
unknown, report independent summaries and request a key before claiming
record-level equality.

## Requirements

1. Load both inputs without modifying source files. Record their identities,
   versions, and loading options.
2. Inspect duplicate column names, schema, types, row counts, null counts, and
   candidate keys before comparing values.
3. Compare columns as sets by default. Report columns only in the left/right
   dataset, and compare shared-column types without silently coercing them.
4. For record-level comparison, use the declared key. Check key nulls and
   duplicates first; do not silently choose an arbitrary duplicate or resolve
   many-to-many matches.
5. If there is no key, compare rows positionally only when explicitly required,
   and report that ordering is assumed. Otherwise limit conclusions to
   aggregate/schema comparisons.
6. Distinguish exact equality from normalized or tolerance-based equality.
   Specify any string normalization (e.g., whitespace/case), datetime
   normalization, and numeric absolute/relative tolerance.
7. Compare missing values explicitly. Do not equate missing with empty strings,
   zero, or a literal text value unless instructed.
8. Report changed cell/row counts and representative, privacy-safe examples.
   Include denominators and distinguish unmatched rows from changed rows.
9. For large datasets, use a scalable strategy that preserves exactness or
   clearly identifies sampling/approximation. Never report sampled comparisons
   as exhaustive.
10. Treat column order and row order as differences only if the contract says
    order is meaningful. Make all normalization and excluded columns visible.
11. Do not write a merged/repaired dataset unless explicitly requested. If
    requested, write to a separate destination and preserve originals.

## Expected deliverables

- A summary of input identities and comparison assumptions.
- Schema/column differences, row/key alignment results, and value difference
  counts.
- Numeric/distribution summaries where requested, with metric definitions.
- Safe examples sufficient to investigate mismatches.
- A clear overall outcome: equal under stated rules, different, or inconclusive.

## Completion checklist

- [ ] Both inputs and their versions are identified.
- [ ] Key, ordering, type, null, and tolerance semantics are explicit.
- [ ] Duplicate or invalid keys are surfaced before alignment.
- [ ] Exact, normalized, sampled, and approximate results are distinguished.
- [ ] Differences include meaningful counts and denominators.
- [ ] No source data was mutated or sensitive raw values exposed.

## Reporting

Report the rules first, then schema differences, alignment coverage, and value
differences. State whether comparison was exhaustive. Never report "identical"
without defining the equality rules and confirming all in-scope records were
checked.