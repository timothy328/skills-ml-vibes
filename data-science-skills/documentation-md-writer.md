# Documentation Markdown Writer

## Purpose

Create or update Markdown documentation that is accurate, discoverable,
accessible, and maintainable for its intended audience. Documentation must
describe verified behavior and the current project rather than an assumed
design.

## Required inputs

Identify:

- The documentation goal, audience, and expected level of detail.
- The target file or appropriate location and existing documentation structure.
- The feature, workflow, API, or process being documented.
- Authoritative source material, implementation, examples, and constraints.
- Required style, localization, versioning, and link conventions.
- Whether examples may use real data, credentials, or network access.

If behavior or an example cannot be verified, label it as illustrative or ask
for clarification rather than presenting it as fact.

## Requirements

1. Inspect existing documentation and follow its tone, terminology, heading
   hierarchy, link style, and placement. Avoid duplicating information that
   already has a canonical home.
2. Write for the stated audience. Define specialized terms when first needed;
   use direct language and actionable steps.
3. Verify commands, options, paths, defaults, outputs, and API behavior against
   the implementation or an authoritative source. Do not invent flags or
   configuration.
4. State prerequisites, inputs, expected results, and failure or recovery
   behavior for procedural content. Distinguish required steps from optional
   ones.
5. Use runnable, minimal examples where useful. Keep examples safe and
   environment-agnostic where the project permits; use placeholders for
   credentials and private values.
6. Use descriptive headings, meaningful link text, readable lists/tables, and
   fenced code blocks with an appropriate language identifier. Keep heading
   levels nested logically.
7. Check relative links, anchors, file references, and cross-references. Avoid
   fragile references to temporary or user-specific locations.
8. Describe limitations, compatibility, security, privacy, and data handling
   when relevant. Do not promise guarantees unsupported by the implementation.
9. Keep changes scoped. Update adjacent indexes or references when directly
   required, but do not rewrite unrelated documentation.
10. Do not include secrets, unnecessary personal information, or copyrighted
    text copied from unapproved sources. Respect the project's license and
    attribution requirements.
11. Ensure instructions do not recommend destructive or external actions
    without appropriate warnings, authorization, and recovery guidance.
12. Validate Markdown formatting and examples using existing project checks
    when available. Report checks that were not run.

## Expected deliverable

A Markdown document or focused edit that meets the stated audience and purpose,
fits the project's documentation structure, and accurately reflects verified
behavior. Include references to relevant canonical docs where helpful.

## Completion checklist

- [ ] Audience, purpose, prerequisites, and expected outcome are clear.
- [ ] Technical claims and examples are verified or explicitly labeled.
- [ ] Links and references resolve or are identified as unverified.
- [ ] Formatting, accessibility, and project conventions are followed.
- [ ] Security-sensitive and destructive steps include appropriate safeguards.
- [ ] No unrelated documentation or historical content was changed.
- [ ] Available documentation checks were run and their status is reported.

## Reporting

State which documentation was added or updated, what source behavior it
describes, and what validation was performed. Identify any unverified details
that remain.