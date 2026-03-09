---
name: git-commit
description: Stages files, analyzes the diff, and commits with a conventional commit message.
---

# Git Commit

## Format

```
<type>[scope]: <description>
```

| Type | When to use |
|------|-------------|
| `feat` | A new capability, component, or behavior the project didn't have before (new skill, feature, command, config option). Not just any new file — purpose matters. |
| `fix` | Correcting broken or incorrect behavior |
| `docs` | Changes to documentation only (README, comments, markdown) |
| `refactor` | Restructuring existing code without changing behavior or adding features |
| `chore` | Routine upkeep with no behavior change — bumping versions, updating lockfiles, adding `.gitignore`, renaming |
| `test` | Adding or updating tests |
| `ci` | Changes to CI/CD pipelines or workflow files |
| `revert` | Undoing a previous commit |

Add `!` after type/scope for breaking changes (e.g. `feat!:`).

## Workflow

1. Check if anything is staged:
   ```bash
   git diff --cached --name-only
   ```
   - If files are listed → skip to step 3
   - If nothing → continue to step 2

2. If nothing is staged, inspect all changes including untracked files:
   ```bash
   git status --short             # list all changed and untracked files
   git diff --name-only           # list modified files
   git diff                       # full diff of modified files
   ```
   If there is nothing to commit (no changes, no untracked files), stop and tell the user there is nothing to commit.

   Otherwise, group the files by logical concern (e.g. feature code, tests, config, deps).
   If changes span multiple unrelated concerns, **stage only one group** and handle the rest in subsequent commits.
   ```bash
   git add <file1> <file2>        # stage only the logical group (works for both modified and untracked files)
   ```

3. Read the full staged diff, then analyze it to generate a commit message:
   ```bash
   git diff --cached
   ```
   - **Type**: What kind of change?
   - **Scope**: What module/area is affected?
   - **Description**: One-line summary (<72 chars, present tense, imperative)

4. **STOP. Do not run any git commands yet.**

   Output exactly this (with the actual generated message substituted in):

   ---
   **Proposed commit message:**
   `<generated message>`

   **What would you like to do?**
   - `1` Commit
   - `2` Edit message
   - `3` Cancel
   ---

   Then stop and wait for the user to reply before doing anything.

5. Act on the reply:
   - `1` → run `git commit -m "<generated message>"`
   - `2` → ask for the new message, then repeat from step 4
   - `3` → abort, do nothing

   If unstaged changes remain after committing, repeat from step 2.

## Rules

- Never use --no-verify
- Never use --force
- Never modify git config
- Never stage `.env`, credentials, or private keys
- If a hook fails, stop and report the error to the user — do not modify any files
- If nothing is staged after `git add`, stop and tell the user
