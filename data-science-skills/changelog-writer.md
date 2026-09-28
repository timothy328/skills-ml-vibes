# Changelog Writer

## Purpose

Produce a user-facing record of notable changes for a release or development
period, grounded in merged or otherwise confirmed changes. A changelog is not
a substitute for commit history or release notes requiring project-specific
approval.

## Required inputs

Identify:

- The changelog file and the project's existing format and conventions.
- The release/version or date range being documented.
- The source of truth for included changes (for example, merged PRs or tagged
  commits).
- Whether unreleased, breaking, security, migration, or dependency changes
  should be included.
- Audience and whether entries should be grouped into categories.

If the scope cannot be verified, request it or clearly state the scope used.

## Requirements

1. Inspect the existing changelog and preserve its format, heading conventions,
   ordering, and tone. If no convention exists, use a readable date/version
   heading and concise categories such as Added, Changed, Fixed, and Removed.
2. Include only changes confirmed to belong to the requested release/scope.
   Derive user-facing meaning from verified change descriptions and code; do
   not invent features, fixes, dates, or versions.
3. Describe impact and relevant behavior, not internal implementation trivia.
   Keep each entry specific enough for users to understand what changed.
4. Highlight breaking changes, deprecations, migrations, security-relevant
   updates, and required user actions where applicable.
5. Avoid duplicate entries, vague claims, raw commit-message dumps, and
   promotional language.
6. Include issue/PR references or links only when identifiers and relevance are
   verified and consistent with project convention.
7. Do not edit unrelated historical entries. Preserve prior release content
   unless the task explicitly requests corrections.
8. Do not claim a change is released if it is only proposed, unmerged, or
   otherwise outside the confirmed scope.
9. Use a stable, agreed date/version. If unavailable, use a clearly marked
   placeholder rather than fabricating one.
10. Keep confidential details out of the public changelog; follow disclosure
    policy for security fixes.

## Expected deliverable

A focused changelog update in the project's established location and format,
with entries that accurately summarize the confirmed scope and any user action
required.

## Completion checklist

- [ ] Release/date range and inclusion scope are clear.
- [ ] Entries are supported by verified changes.
- [ ] User impact and breaking changes are easy to identify.
- [ ] Existing style and historical content are preserved.
- [ ] No unsupported versions, links, dates, or claims were added.
- [ ] Sensitive details are handled according to disclosure policy.

## Reporting

Summarize the scope documented and identify unresolved release details,
placeholders, or excluded changes. Do not imply a release was published unless
that action is verified.