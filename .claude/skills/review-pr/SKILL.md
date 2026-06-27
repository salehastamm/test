---
name: review-pr
description: Review a GitHub pull request against this project's standards. Use whenever the user asks to review, look over, or give feedback on a pull request or PR.
---

# Review Pull Request

When asked to review a PR, follow this procedure exactly. Use the `gh` CLI to
read the PR and post the review against the `origin` remote.

## What to review

Check the PR across all four dimensions. Anchor findings to specific files and
lines.

1. **Correctness / bugs** — logic errors, unhandled edge cases, off-by-one,
   null/undefined handling, broken or missing behavior, race conditions.
2. **Standards compliance** — the PR follows this project's conventions:
   - Branch name matches the [create-branch] standard (`<type>/<short-description>`).
   - PR title and body match the [create-pr] standard (`[Type] Description`,
     Summary + Changes sections, based on `main`).
   - Any linked issue matches the [create-issue] standard.
   - One PR = one logical piece of work.
3. **Style / readability** — naming, structure, and idioms match the
   surrounding code. Comment density consistent with the file. No dead code or
   leftover debug output.
4. **Security** — injection, command/SQL/path traversal, hardcoded secrets or
   credentials, missing authz/authn, unsafe deserialization, unvalidated input.

## Severity

Label each finding:

- **blocker** — must be fixed before merge (bugs, security holes, standards
  violations that break the workflow).
- **suggestion** — should be improved but won't block.
- **nit** — minor/optional (style, wording).

## Procedure

1. Identify the PR. If the user gives a number/URL, use it; otherwise use the PR
   for the current branch:
   ```bash
   gh pr view --json number,title,headRefName,baseRefName,body
   gh pr diff <number>
   ```
2. Read the diff and assess it against all four dimensions above.
3. Post findings as **inline comments** on the relevant lines, each prefixed
   with its severity, e.g. `**blocker:** ...`. Use:
   ```bash
   gh pr review <number> --comment   # while adding line comments
   ```
   (Add line-level comments via the GitHub API / review comments where inline
   placement is needed.)
4. Submit a **summary review** that lists the findings grouped by severity and
   states the overall verdict.

## Verdict

Conclude with an explicit verdict based on the findings:

- **Request changes** if there is **any** blocker:
  ```bash
  gh pr review <number> --request-changes --body "<summary>"
  ```
- **Approve** if there are no blockers (suggestions/nits are fine):
  ```bash
  gh pr review <number> --approve --body "<summary>"
  ```

## Rules

- Never approve a PR that has an unresolved blocker.
- Be specific: every finding cites a file and line and explains the concern.
- Don't invent problems. If the PR is clean, say so and approve.
- Review only what changed in the diff; don't demand unrelated rework.
- Report the submitted review URL back to the user.
