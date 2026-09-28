# Deployment Preparation

## Purpose

Prepare a validated model and its dependencies for a controlled deployment to
an intended environment. Preparation includes release readiness, operational
requirements, and rollout/rollback planning. This skill does not itself
authorize deployment or make production changes.

## Required inputs

Establish:

- The approved model artifact and its version, provenance, and evaluation
  results.
- The intended use, deployment environment, consumers, and accountable owner.
- Model, preprocessing, request, and response interface contracts.
- Runtime, resource, latency, availability, throughput, and scaling
  requirements, where defined.
- Data access, privacy, security, retention, and regulatory constraints.
- Release process, approval requirements, maintenance windows, and change
  controls.
- Monitoring, alert ownership, rollback triggers, rollback method, and
  recovery expectations.
- Any migration, compatibility, dependency, or infrastructure changes.

Ask for missing decisions that materially affect safety or release readiness.
Label assumptions and proposed thresholds; do not treat them as approved
requirements.

## Requirements

1. Verify that the exact artifact proposed for release is the artifact that was
   evaluated. Record immutable identifiers or checksums where supported,
   training/data versions, preprocessing version, configuration, and
   dependencies.
2. Confirm the intended use and release scope. Check that evaluation covers
   relevant populations, operating conditions, failure modes, and stated
   acceptance criteria. Surface gaps rather than implying approval.
3. Validate the end-to-end interface, including input schema, feature meaning
   and order, preprocessing, output schema, error behavior, and compatibility
   with consumers. Test representative and boundary cases.
4. Assess operational readiness using the project's existing practices:
   startup/load behavior, resource limits, concurrency, timeouts, retries,
   dependency availability, and behavior during partial failure, as relevant.
   Do not add environment-specific assumptions without confirmation.
5. Review security and privacy controls, including least-privilege access,
   secret handling, data minimization, encryption requirements, logging
   redaction, artifact integrity, and permitted data flows.
6. Define release checks and acceptance criteria before rollout. Criteria
   should be measurable, owned, and appropriate to the impact of model
   decisions; do not invent an SLO or safety threshold.
7. Plan a rollout proportionate to risk, such as staged exposure, shadow
   evaluation, or canary traffic when supported. Define how traffic is routed
   and how comparisons remain valid.
8. Document rollback triggers, decision authority, steps, dependencies, and
   expected recovery behavior. Verify that the prior known-good version and
   required configuration/data compatibility remain available.
9. Identify required approvals, communication, runbooks, ownership, and
   support coverage. Do not bypass established release, governance, or
   compliance controls.
10. Keep preparation separate from execution. Do not publish artifacts, alter
    live configuration, route production traffic, or perform irreversible
    migrations without explicit authorization through the applicable process.
11. Ensure the deployment plan includes a way to detect issues and stop or
    reverse the rollout. If rollback is not technically possible, disclose the
    limitation and obtain an explicit risk decision before release.
12. Record unresolved risks and assign an owner or next action. A checklist
    must not mark a requirement complete without evidence.

## Expected deliverables

- A release-readiness summary identifying the exact model and dependency
  versions.
- Verified interface, compatibility, operational, and security/privacy checks.
- A deployment and rollout plan with stages, acceptance criteria, and
  authorized decision points.
- Monitoring and alert ownership appropriate to the intended service.
- A tested or reviewed rollback/recovery plan and runbook references.
- A list of open risks, approvals, and actions, with owners where known.

## Completion checklist

- [ ] Release artifact matches the evaluated and approved artifact.
- [ ] Model, preprocessing, input/output, and dependency versions are recorded.
- [ ] Interface and operational behavior have been tested against the contract.
- [ ] Privacy, security, access, and data-flow requirements are addressed.
- [ ] Rollout stages and measurable acceptance/stop criteria are approved.
- [ ] Rollback/recovery steps and decision ownership are documented.
- [ ] Monitoring, support, and incident ownership are assigned.
- [ ] Required approvals are recorded; no production action was taken without
      authorization.
- [ ] Open risks and unverified items are visible and not presented as passed.

## Reporting

Report readiness as ready, not ready, or conditional, with evidence for each
critical check. State the target environment and rollout scope, approvals
obtained or pending, operational and rollback plan, and remaining risks. Do not
claim deployment occurred unless it is verified.
