---
name: code-review
description: Review the current git diff (or a specified PR/branch) for correctness bugs, security issues, and clarity problems. Use when the user asks to review changes, check a diff, look over a PR, or validate code before committing or pushing.
---

# Code Review

Perform a focused, high-signal review of code changes. Prioritize real bugs over nitpicks.

## Scope

Determine what to review, in this order of preference:

1. If the user names a specific PR, branch, or commit range, review that.
2. Otherwise review the working diff: staged + unstaged changes against the merge-base with the default branch.

Useful commands:

```bash
git diff --merge-base origin/main        # changes vs default branch
git diff                                  # unstaged
git diff --staged                         # staged
```

Read enough surrounding context (the full function/file, not just the hunk) before judging any change.

## What to look for

Review for these dimensions, roughly in priority order:

1. **Correctness** — logic errors, off-by-one, wrong conditionals, unhandled
   null/empty/error cases, broken edge cases, incorrect async/await usage.
2. **Security** — injection, unsafe deserialization, secrets in code, missing
   authz/authn checks, unvalidated input, path traversal.
3. **Data & concurrency** — race conditions, unguarded shared state, resource
   leaks (unclosed files/connections), N+1 queries.
4. **API contracts** — breaking changes, inconsistent return types, mismatched
   signatures with callers.
5. **Clarity** — confusing names, dead code, duplicated logic that should be
   reused. Keep these brief and clearly secondary.

## How to report

- Group findings by severity: **Blocking**, **Should fix**, **Nit**.
- For each finding: cite `file:line`, explain *why* it's a problem (the failure
  case), and suggest a concrete fix.
- Only flag things you're confident about. If you're unsure, say so explicitly
  rather than presenting a guess as fact.
- If the diff is clean, say so plainly — do not invent issues to look thorough.
- End with a one-line verdict: ready to merge, or what blocks it.
