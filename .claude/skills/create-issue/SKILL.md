---
name: create-issue
description: Open a new GitHub issue following this project's standard. Use whenever the user asks to file, open, create, or report an issue, bug, or feature request.
---

# Create Issue

When asked to file an issue, follow this standard exactly. Create it with the
`gh` CLI against the repo's `origin` remote. Do not invent ad-hoc formats.

## Title standard

Format: `[Type] Short description`

- **Type** — one of (mirrors the branch-naming standard in [create-branch]):
  - `Bug` — something is broken or behaves incorrectly
  - `Feature` — new functionality
  - `Docs` — documentation only
  - `Refactor` — code change that neither fixes a bug nor adds a feature
  - `Chore` — tooling, config, dependencies, housekeeping
  - `Test` — adding or fixing tests
- **Short description** — a clear, concise summary in sentence case.
  No trailing period. Keep it scannable.

Examples:
- `[Bug] Checkout crashes when cart is empty`
- `[Feature] Add user login with email`
- `[Docs] Document the deploy procedure`

## Body template

Use this structure. Omit a section only when it genuinely does not apply
(e.g. "Steps to reproduce" for a non-bug), and say so rather than leaving it blank.

```markdown
## Summary
<One or two sentences describing the issue or request and why it matters.>

## Steps to reproduce
<For bugs. Numbered steps, then expected vs actual behavior.>
1. ...
2. ...

**Expected:** ...
**Actual:** ...

## Acceptance criteria
<A checklist describing what "done" looks like.>
- [ ] ...
- [ ] ...

## Context / links
<Related issues/PRs, screenshots, environment, or other references.>
```

## Labels

Always apply a label matching the issue type:

| Type       | Label         |
|------------|---------------|
| Bug        | `bug`         |
| Feature    | `enhancement` |
| Docs       | `documentation` |
| Refactor   | `refactor`    |
| Chore      | `chore`       |
| Test       | `test`        |

If the label does not exist in the repo, create it first
(`gh label create <name>`) or fall back to the closest existing label and
note the substitution to the user.

## Procedure

1. Determine the **type** and draft the **title** and **body** from the
   standard above. Fill the template with the user's details; ask for missing
   essentials (e.g. repro steps for a bug) rather than guessing.
2. Show the user the proposed title, body, and label for confirmation before
   creating it.
3. Create the issue:
   ```bash
   gh issue create \
     --title "[Type] Short description" \
     --body "<rendered body>" \
     --label "<type-label>"
   ```
4. Report the resulting issue URL back to the user.

## Rules

- One issue = one logical problem or request. Split unrelated concerns into
  separate issues.
- Never create an issue without a type label.
- Don't fabricate details (repro steps, error messages, versions). If you don't
  have them, ask.
- Confirm the title and body with the user before creating when anything is
  ambiguous.
