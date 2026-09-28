# Inference JSON Schema Checker

## Purpose

Validate inference request and/or response JSON against an explicit schema and
the associated model interface contract. Schema validity alone does not prove
that a prediction is correct or safe.

## Required inputs

Obtain:

- The authoritative JSON Schema (including draft/version) or written interface
  contract.
- Whether request, response, or both are in scope.
- Example or actual payloads and how to identify their versions.
- Required/optional fields, nullability, types, bounds, enumerations, and
  cross-field constraints.
- Model/preprocessor version and input feature order/meaning, if applicable.
- Handling rules for additional properties, missing fields, and unknown
  versions.
- Privacy constraints for payloads and diagnostic output.

If no authoritative schema exists, do not invent one and label it authoritative.
Offer a proposed schema separately for approval.

## Requirements

1. Validate against the supplied schema version and state which schema and
   validator semantics were used. If the validator cannot support a required
   feature, report the limitation.
2. Parse JSON strictly. Distinguish malformed JSON from schema violations.
   Do not silently repair, coerce, drop, or rename payload fields.
3. Check required properties, types, formats, ranges, enumerations, array item
   constraints, nullability, additional-property policy, and declared
   cross-field rules.
4. Check model interface semantics that are not expressible in the schema,
   including feature names/order, units, batch shape, preprocessing version,
   and prediction output shape, when those contracts are provided.
5. Validate representative boundary cases: minimum/maximum values, empty
   collections, missing versus null fields, extra fields, and malformed
   values, as applicable.
6. Report each failure with payload location/path, violated rule, and a
   concise expected-versus-observed description. Avoid echoing sensitive
   values; redact or summarize them.
7. Validate batches and individual records according to the documented
   contract. Report all errors or use an explicit, documented error limit;
   never truncate errors silently.
8. Do not call a live inference endpoint or transmit payloads externally unless
   specifically authorized. Prefer local validation.
9. Keep validation read-only. If normalization is explicitly requested, report
   the original validation result separately from the normalized result.
10. Treat a valid payload as structurally conforming only; do not claim it
    produces a meaningful, accurate, or calibrated prediction without model
    evaluation evidence.

## Expected deliverables

- Schema identity/version and scope of validation.
- Overall result and counts of valid and invalid payloads.
- Detailed, privacy-safe diagnostics for each violation.
- Tests or examples covering valid, invalid, and boundary payloads.
- Any unsupported schema or semantic constraints clearly identified.

## Completion checklist

- [ ] An authoritative schema/contract and version were used.
- [ ] Parsing errors and schema errors are distinguished.
- [ ] No silent coercion, repair, or field dropping occurred.
- [ ] Relevant semantic interface constraints were checked.
- [ ] Errors identify their payload path and expected rule.
- [ ] Sensitive payload data is not unnecessarily exposed or transmitted.
- [ ] The report does not confuse structural validity with prediction quality.

## Reporting

State the schema version, payload set, checks performed, result counts, and
limitations. Include concise diagnostics and make any unvalidated constraint
explicit.