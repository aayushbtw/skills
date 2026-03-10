---
name: git-commit
description: Stages files, analyzes the diff, and commits with a conventional commit message. Use this skill whenever the user wants to commit, says things like "commit this", "make a commit" or "ship it".
---

# Git Commit

## Format

```
<type>(<scope>): <description>
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
   git diff --name-only           # list modified files with actual diff content
   ```
   Cross-check: only include a file if it actually has a diff or is genuinely untracked. Do not include files that appear in `git status` but have no real changes in `git diff`.

   If there is nothing to commit, stop and tell the user.

   Otherwise, analyze every changed/untracked file and sort them into logical groups. Two files belong in the same group only if they serve the **same purpose** (e.g. a feature file and its test). Files that touch different concerns, scopes, or types MUST go in separate groups — never combine them into one commit.

   If there are multiple groups, tell the user how many commits will be made, then focus only on the **first group** for now. Stage only those files:
   ```bash
   git add <file1> <file2>
   ```
   The remaining groups will be handled automatically after each commit (step 5 loops back here).

3. Read the full staged diff, then analyze it to generate a commit message:
   ```bash
   git diff --cached
   ```
   - **Type**: What kind of change?
   - **Scope**: What module/area is affected? (required)
   - **Description**: Present tense imperative, no period, ≤50 chars

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

- ALWAYS include scope in parentheses
- ALWAYS use present tense imperative verb for the subject
- NEVER end subject with a period
- NEVER exceed 50 chars in the subject line
- NEVER use generic messages ("update code", "fix bug", "changes")
- NEVER use --no-verify
- NEVER use --force
- NEVER modify git config
- NEVER stage `.env`, credentials, or private keys
- Group related changes into a single focused commit; stage unrelated changes in separate commits
- If a pre-commit hook fails, stop and report the error — do not attempt to fix or bypass it
- If nothing is staged after `git add`, stop and tell the user
- NEVER add `Co-Authored-By` trailers or any attribution footers to commit messages
