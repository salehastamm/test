---
name: create-branch
description: Create a new git branch following this project's naming standard. Use whenever the user asks to make, create, start, or check out a new branch — or before starting any new piece of work that should live on its own branch.
---

# Create Branch

When asked to make a new branch, follow this standard exactly. Do not invent ad-hoc names.

## Naming standard

Format: `<type>/<short-description>`

- **type** — one of:
  - `feature` — new functionality
  - `fix` — bug fix
  - `docs` — documentation only
  - `refactor` — code change that neither fixes a bug nor adds a feature
  - `chore` — tooling, config, dependencies, housekeeping
  - `test` — adding or fixing tests
- **short-description** — kebab-case (lowercase, words separated by hyphens),
  3–5 words max, describing the work. No spaces, no uppercase, no underscores.

Examples:
- `feature/user-login`
- `fix/null-pointer-on-checkout`
- `docs/update-readme`
- `chore/bump-dependencies`

If the work maps to an issue/ticket number, optionally append it:
`feature/user-login-42`.

## Procedure

Before creating the branch:

1. Make sure the working tree is clean (`git status`). If there are uncommitted
   changes, ask the user whether to commit, stash, or bring them along.
2. Start from an up-to-date default branch unless the user says otherwise:
   ```bash
   git checkout main
   git pull origin main
   ```
3. Create and switch to the new branch:
   ```bash
   git switch -c <type>/<short-description>
   ```

After creating it, confirm the branch name back to the user and state which
branch it was based on.

## Rules

- Always confirm the proposed branch name with the user before creating it if
  the type or description is ambiguous.
- One branch = one logical piece of work. Don't reuse a branch for unrelated changes.
- Never create a branch directly named `main` or `master`.
- Keep names short but descriptive enough to tell what the branch is for at a glance.
