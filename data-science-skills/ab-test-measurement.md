# A/B Test Measurement for Production Models

## Purpose

Design, measure, and report a controlled production experiment comparing a
challenger model with the current champion. The goal is to estimate the effect
of assigning eligible traffic to the challenger under a defined production
policy, while protecting users and service reliability.

This specification covers experiment measurement and decision support. It
does not authorize a production launch, traffic change, or model promotion.
Follow the project's release, privacy, safety, and governance processes.

## Required inputs

Before the experiment, define:

- The decision to be informed and the accountable experiment owner.
- The current champion and proposed challenger, including immutable model,
  preprocessing, feature, configuration, and serving versions.
- The eligible population, exclusions, experiment start/end conditions, and
  prediction or decision unit.
- The randomization unit (for example, user, account, device, session, request,
  or cluster), assignment method, allocation ratio, and persistence period.
- The primary outcome, its exact definition, observation window, source of
  truth, and expected label delay.
- Secondary outcomes and operational, safety, and business guardrails.
- The estimand (the effect to be estimated), analysis method, uncertainty
  level, practical decision threshold, and sample-size/power plan.
- Expected traffic, treatment compliance/exposure semantics, possible
  interference between units, and any cross-device or cross-account linkage.
- Required approvals, privacy restrictions, logging/retention policy, and
  rollback/stop authority.

If a primary outcome, assignment unit, safety guardrail, or decision rule is
missing, ask for it or present a clearly marked proposal for approval. Do not
start an experiment based on unstated defaults.

## Requirements

### Experiment design

1. State a falsifiable hypothesis and define the target population, comparison,
   primary outcome, outcome window, and practical effect of interest before
   examining experiment results.
2. Treat the champion as the control and the challenger as the treatment. Keep
   both model versions, preprocessing, feature definitions, serving
   configuration, and eligibility rules fixed during the confirmatory test.
   If a material change is necessary, document it and start a new experiment
   period or analysis plan.
3. Choose a randomization unit that matches the causal question and prevents
   avoidable contamination. Keep assignment stable for that unit when repeat
   decisions or delayed outcomes could otherwise cross arms. If units interact
   (for example, marketplace participants, households, or shared inventory),
   assess interference and use cluster-level randomization or another
   justified design where needed.
4. Define eligibility and exclusions before assignment. Apply the same rules
   to both arms and log eligible, assigned, served, and outcome-observed counts.
   Do not exclude units after assignment based on model behavior, exposure,
   outcome, or other post-assignment information from the primary analysis.
5. Use the assignment-based (intention-to-treat) comparison as the primary
   estimate unless a different estimand is explicitly justified in advance.
   Report non-delivery, fallback, crossover, and noncompliance separately.
   Exposure-based analyses may be useful secondary analyses but can be biased
   because exposure can depend on treatment or user behavior.
6. Separate experiment assignment from model scoring and downstream action.
   Use a deterministic, auditable assignment mechanism where practical; make
   fallback behavior explicit and safe. Confirm that no other concurrent
   experiment changes the same outcome or population without a compatible
   design.
7. Establish the allocation ratio, expected duration, sample-size calculation,
   minimum detectable effect or precision goal, and stopping rule before
   launch. Base these on the primary metric, baseline rate/variance, randomization
   unit, dependence structure, label delay, and approved error rates. Do not
   stop early for apparent success or failure unless a valid sequential or
   group-sequential design was pre-specified.
8. Predefine safety and operational guardrails, alert thresholds, review
   cadence, and who can pause or roll back. Guardrails must be monitored during
   the experiment and must take precedence over statistical power or
   completion targets.

### Instrumentation and data quality

9. Record the minimum data needed to reconstruct assignment and measurement:
   experiment/version identifiers, randomized unit, assigned arm, assignment
   time, eligibility, model and preprocessing version, serving/exposure or
   fallback status, outcome window, and source/version of observed outcomes.
   Apply access controls, pseudonymization, retention limits, and data
   minimization.
10. Validate logging and outcome joins before relying on results. Check
    missingness, duplicate events, timestamp/order logic, delayed or revised
    labels, arm-specific logging differences, and assignment persistence.
    Do not silently drop unmatched or invalid records.
11. Check sample-ratio mismatch against the predeclared allocation, overall and
    across important dimensions. Investigate assignment, eligibility,
    logging, and delivery before interpreting outcome differences. Do not
    "correct" a mismatch by reweighting without a documented, justified method.
12. Preserve an auditable experiment configuration, analysis plan, code,
    metric definitions, model versions, data cutoff, and any deviations.
    Protect raw features and outcomes from unnecessary access or display.

### Analysis and interpretation

13. Analyze the predeclared primary outcome first. Report the effect in
    interpretable units (absolute and, when meaningful, relative), arm-level
    denominators, uncertainty interval, and analysis population.
14. Respect the randomization unit and data dependence. Use standard errors,
    intervals, or tests that account for clustering, repeated observations,
    stratification, blocking, and unequal assignment probabilities as
    applicable. Do not treat correlated rows as independent experimental units.
15. Handle delayed, missing, censored, or selectively observed outcomes
    explicitly. State the maturity cutoff and observation window. Do not
    compare arms with unequal follow-up or treat unobserved outcomes as
    negative outcomes without justification.
16. Report secondary metrics and subgroup analyses as secondary or exploratory
    unless they were pre-specified and adequately powered. Address multiplicity
    when making confirmatory claims across multiple outcomes, segments, or
    repeated looks.
17. Compare predictive metrics only when labels are valid for both arms and the
    metric answers the stated decision question. Distinguish prediction
    accuracy/calibration from downstream policy or business impact.
18. Interpret results against both statistical uncertainty and practical
    thresholds. A statistically detectable effect may be immaterial; a
    nonsignificant result is not proof of equivalence or no effect.
19. Treat a material data-quality, safety, instrumentation, or guardrail
    failure as a validity or stop issue, not as a result to explain away.
20. Do not change the primary outcome, population, analysis, or stopping rule
    after seeing results and then report it as pre-specified. Clearly label any
    post hoc analysis.

## Expected deliverables

- A pre-launch experiment plan with hypothesis, population, randomization unit,
  arms, assignment and exposure semantics, metrics, windows, power/precision
  rationale, guardrails, stopping rules, and decision criteria.
- Evidence that assignment, model-version routing, event logging, and outcome
  measurement work before full exposure.
- An analysis dataset or reproducible procedure with documented lineage and
  privacy controls.
- A results report with assignment integrity, data-quality findings,
  arm-level counts, primary effect and uncertainty, guardrails, limitations,
  and deviations.
- A recommendation to promote, continue, stop, or declare inconclusive, tied
  to the approved decision rules. Promotion remains subject to authorized
  release approval.

## Completion checklist

- [ ] Champion and challenger versions and experiment scope are fixed and
      identifiable.
- [ ] Hypothesis, population, randomization unit, primary outcome, and
      estimand are specified before results are reviewed.
- [ ] Assignment is persistent and contamination/interference risks are
      addressed.
- [ ] Eligibility, exclusions, exposure, fallback, and noncompliance are
      measured without post-assignment selection in the primary analysis.
- [ ] Sample-size/power or precision plan and stopping rules are documented.
- [ ] Safety and operational guardrails have approved thresholds and owners.
- [ ] Assignment ratio, logging, outcome joins, label maturity, and missingness
      have been checked.
- [ ] Analysis respects the assignment unit, repeated measures, clustering,
      and multiplicity as applicable.
- [ ] Effect sizes, uncertainty, sample counts, and practical significance are
      reported without overstating conclusions.
- [ ] Data access, retention, and experiment actions follow approved controls.
- [ ] Recommendation follows predeclared criteria and does not itself
      constitute deployment authorization.

## Reporting

Report the experiment question and design, exact champion/challenger versions,
population and assignment unit, dates and outcome maturity, assignment
integrity, data-quality issues, primary estimate with uncertainty, guardrails,
secondary findings, and limitations. End with the predeclared decision status:
promote for approval, continue under the planned design, stop/rollback, or
inconclusive. Explain deviations and distinguish causal conclusions supported
by the design from descriptive or exploratory observations.
