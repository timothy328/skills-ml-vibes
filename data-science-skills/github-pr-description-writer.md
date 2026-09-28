# GitHub Pull Request Description Writer

## Purpose

Write an accurate, review-oriented pull request description from the actual
change set and verified project context. The description must help reviewers
understand why the change exists, what changed, and how it was validated.

## Required inputs

Use, when available:

- The branch diff against its intended base, including added and deleted files.
- The issue, request, or user-provided motivation.
- Relevant project conventions and existing PR template.
- Test/build/lint results and known limitations.
- Any deployment, migration, compatibility, or rollout implications.

If the base branch or intended scope is unclear, do not guess. Ask or state the
comparison assumption. Never infer test success from code inspection alone.

## Requirements

1. Inspect the complete relevant diff and understand the purpose of each
   material change. Do not describe files or behavior that are not in the
   change.
2. Follow an existing repository PR template and required labels/sections.
   Otherwise use a concise structure such as Summary, Changes, Validation, and
   Risks/Notes.
3. Lead with the user or system impact. Describe outcomes, not a raw file list;
   include implementation details only when useful for review.
4. Link issues or requirements only when their identifiers and relationship
   are verified. Do not claim an issue is fixed without evidence.
5. Report tests, builds, and checks exactly as run. Distinguish passed, failed,
   skipped, and not run; include useful command/context when available.
6. Call out behavior changes, migrations, compatibility concerns, security or
   data implications, and known limitations. Do not hide breaking changes.
7. Keep statements factual, concise, and understandable to the intended
   reviewer. Avoid unsupported claims such as "fully tested" or "production
   ready."
8. Do not include secrets, private user data, or sensitive internal details.
   Use stable links only when appropriate and available.
9. Preserve useful checklist items in a project template; do not mark a box
   complete unless the corresponding work was done.
10. If the diff is empty, incomplete, or inaccessible, say so rather than
    drafting a change narrative from assumptions.

## Expected deliverable

A Markdown PR description ready to paste into the hosting platform, with
verified summary, rationale, material changes, validation status, and relevant
risks or follow-up items.

## Completion checklist

- [ ] Description matches the inspected diff and stated request.
- [ ] No behavior or test result was invented.
- [ ] Validation clearly distinguishes passed, failed, skipped, and unrun.
- [ ] Risks, migrations, and compatibility changes are surfaced.
- [ ] Existing project template and checklist conventions are followed.
- [ ] No sensitive information or unjustified claims are included.

## Reporting

Provide the description directly, then briefly note any information that could
not be verified and was therefore omitted or marked unknown.