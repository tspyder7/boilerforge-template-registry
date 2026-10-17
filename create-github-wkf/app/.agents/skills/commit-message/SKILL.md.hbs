---
name: commit-message
description:
    Generate detailed conventional commit messages automatically. Use when the user runs git commit,
    stages changes, or asks for commit message help. Analyzes staged changes using git diff to create
    a conventional commit message with a concise subject and a detailed bullet-point body describing
    the changes. Triggers on git commit, staged changes, or commit message requests.
compatibility: opencode
metadata:
    audience: developers
    workflow: git
---

## Rules

1. Run `git diff --staged` to inspect staged changes. If no staged changes exist, prompt the user to stage files and **STOP**.
2. Generate a conventional commit message using the format:
   - Subject: `type(scope): subject`
     - Imperative mood
     - Maximum 72 characters
     - No trailing period
   - Body:
     - Bullet-point list (`-`)
     - Describe **what changed** and **why**
     - Avoid implementation details unless they provide important context
     - Group related changes together
     - Omit the body if the change is trivial
   - Footer (optional):
     - `Closes #123`
     - `Refs #123`
     - `BREAKING CHANGE: ...`
3. Display both the formatted commit message and a copyable `git commit` command, then **STOP**.
4. Wait for user input:
   - `yes` / `y` → Run `git commit`
   - `edit` / `e` → Allow editing and show confirmation again
   - `no` / `n` → Generate a different commit message
   - `cancel` / `c` → Abort without committing
5. **Never**:
   - Run `git add` or stage files
   - Modify source code
   - Skip Git hooks (`--no-verify`)
   - Retry automatically after a failed commit
6. If `git commit` fails, report the error and **STOP**.

---

## Commit Message Guidelines

### Subject

Format:

```
type(scope): concise summary
```

Examples:

```
feat(auth): add GitHub App authentication
fix(router): prevent duplicate request handling
refactor(config): simplify repository validation
```

### Body

Use concise bullet points.

Good example:

```
- Add repository existence validation before provisioning
- Improve error messages for invalid request labels
- Refactor workflow dispatch logic to reduce duplication
- Update request state transitions to support retries
```

Avoid:

- Long paragraphs
- Repeating the subject
- File-by-file summaries
- Low-level implementation details

### Footer

Include only when applicable.

Examples:

```
Closes #123
Refs #456
BREAKING CHANGE: request schema has been updated
```

---

## Confirmation Gate

```text
─────────────────────────────────────────
  Proposed commit message:

  <type>(scope): subject

  - First change
  - Second change
  - Third change

  Optional footer
─────────────────────────────────────────

  git commit -m "<type>(scope): subject

  - First change
  - Second change
  - Third change

  Optional footer"

─────────────────────────────────────────
  [yes / edit / no / cancel]
```

| Reply | Action |
|--------|--------|
| `yes` / `y` | Run `git commit -m "..."`. If it fails, report the error and stop. |
| `edit` / `e` | Allow the user to edit the commit message, then show the confirmation gate again. |
| `no` / `n` | Generate a different commit message and show the confirmation gate again. |
| `cancel` / `c` | Abort without committing. |

---

## Change Types

| Observation | Type |
|-------------|------|
| New feature | `feat` |
| Bug fix | `fix` |
| Critical production fix | `hotfix` |
| Refactoring without behavior changes | `refactor` |
| Tests only | `test` |
| Documentation | `docs` |
| Dependencies or tooling | `chore` |
| CI/CD, workflows, automation | `ci` |
| Performance improvements | `perf` |
| Breaking changes | Append `!` to the type and include a `BREAKING CHANGE:` footer |

---

## Example

```text
─────────────────────────────────────────
  feat(provisioning): add repository validation

  - Validate repository ownership before provisioning
  - Prevent duplicate provisioning requests
  - Improve error reporting for invalid repositories
  - Add unit tests covering validation failures

  Closes #42
─────────────────────────────────────────

  git commit -m "feat(provisioning): add repository validation

  - Validate repository ownership before provisioning
  - Prevent duplicate provisioning requests
  - Improve error reporting for invalid repositories
  - Add unit tests covering validation failures

  Closes #42"

─────────────────────────────────────────
  [yes / edit / no / cancel]
```
