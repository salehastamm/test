---
name: create-pr
description: Open a GitHub pull request following this project's standard. Use whenever the user asks to make, open, create, or raise a pull request or PR.
---

# Create Pull Request

When asked to open a pull request, follow this standard exactly. Create it with
the `gh` CLI against the `origin` remote. Do not invent ad-hoc formats.

## Base branch

PRs target **`main`** by default. Only use a different base if the user
explicitly asks for one.

## Title standard

Derive the title from the current **branch name**, which follows the
[create-branch] standard (`<type>/<short-description>`):

- Map the branch `type` to a capitalized prefix in brackets, then turn the
  kebab-case description into a readable sentence-case phrase.
- Branch types map to prefixes:
  `feature` → `[Feature]`, `fix` → `[Fix]`, `docs` → `[Docs]`,
  `refactor` → `[Refactor]`, `chore` → `[Chore]`, `test` → `[Test]`.

Examples:
- Branch `feature/user-login` → `[Feature] User login`
- Branch `fix/null-pointer-on-checkout` → `[Fix] Null pointer on checkout`
- Branch `docs/update-readme` → `[Docs] Update readme`

If the branch name doesn't follow the standard, propose a title that fits the
format and confirm it with the user.

## Body template

```markdown
## Summary
<One or two sentences: what this PR changes and why.>

## Changes
<Bulleted list of the notable changes in this PR.>
- ...
- ...
```

## Procedure

Before opening the PR:

1. Confirm the working tree is clean and the branch is pushed. If there are
   uncommitted changes, ask whether to commit them first. Push the branch and
   set upstream if it isn't on the remote yet:
   ```bash
   git push -u origin HEAD
   ```
2. Never open a PR from `main` (or `dev`) into `main`. The head branch must be a
   topic branch. If the user is on `main`, stop and ask them to branch first
   (see [create-branch]).
3. Draft the **title** from the branch name and the **body** from the template,
   filling the Summary and Changes from the actual commits/diff on the branch.
4. Show the user the proposed title and body for confirmation.
5. Create the PR:
   ```bash
   gh pr create \
     --base main \
     --title "[Type] Short description" \
     --body "<rendered body>"
   ```
6. Report the resulting PR URL back to the user.

## Rules

- One PR = one logical piece of work, matching the branch it comes from.
- Always base PRs on `main` unless told otherwise.
- Never open a PR with `main` as the head branch.
- Fill Summary and Changes from the real diff — don't fabricate changes.
- Confirm the title and body with the user before creating when anything is
  ambiguous.

🤖 PR bodies created via this skill end with:
🤖 Generated with [Claude Code](https://claude.com/claude-code)
