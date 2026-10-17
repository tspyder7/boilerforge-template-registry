# generate-commit-message

Generate conventional commit messages automatically. Analyzes `git diff --staged` and proposes a ready-to-run `git commit -m "..."` command with a `[yes / edit / no / cancel]` confirmation gate.

## What it does

Runs `git diff --staged`, then proposes a conventional commit message (`type(scope): subject`, imperative mood, no period, max 72 chars) plus a copyable commit command. The user replies:

| Reply | Action |
|---|---|
| `yes` / `y` | Run `git commit -m "..."` |
| `edit` / `e` | Revise the message, re-show the gate |
| `no` / `n` | Regenerate a new suggestion |
| `cancel` / `c` | Abort — discard, do nothing |

Guarantees: never runs `git add`, never skips husky hooks (`--no-verify`), and on commit failure reports the error and stops — never auto-fixes.

## How to invoke

```
git commit            # stage first; the skill takes over from there
git commit -m "..."
```

Or ask directly: "write a commit message for my staged changes", "help me commit this".

## Change types

| Observation | Type |
|---|---|
| New feature | `feat` |
| Bug fix | `fix` |
| Urgent patch | `hotfix` |
| Restructure (no behavior change) | `refactor` |
| Tests only | `test` |
| Docs | `docs` |
| deps/tooling | `chore` |
| CI/actions/workflows | `ci` |
| Performance | `perf` |
| Breaking | `!` after type + `BREAKING CHANGE:` footer |

## Example output

```
─────────────────────────────────────────
  feat(auth): add JWT-based authentication

  - Implement login/logout flow
  - Add token management service
  - Guard protected routes with auth middleware

  Closes #42
─────────────────────────────────────────

  git commit -m "feat(auth): add JWT-based authentication
  ...
  Closes #42"
─────────────────────────────────────────
  [yes / edit / no / cancel]
```

## See also

- [`SKILL.md`](./SKILL.md) — full LLM-facing instructions
