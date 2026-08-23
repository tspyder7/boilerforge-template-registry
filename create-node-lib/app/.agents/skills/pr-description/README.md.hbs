# generate-pr-description

Generate professional, well-structured pull request descriptions from diffs, commit logs, branch names, or plain summaries.

## What it does

Turns any combination of inputs — git diff, `git log --oneline`, branch name, file list, or ticket number — into a PR description following a fixed template:

```markdown
**Title:** <concise PR title>

## Description

What does this PR do?

## Changes

-

## Related Issue

Closes #
```

Key behaviors:

- **Title**: `[type]: short description` (feat, fix, refactor, chore, docs, test), ≤ 50 chars, imperative mood.
- **Description**: 2–4 plain-English sentences written for someone who hasn't seen the code.
- **Changes**: action-verb bullets (Add, Fix, Remove, Refactor) — as many as needed, no mechanical noise.
- **Related Issue**: `Closes #<number>` to auto-close on merge; Jira/Linear tickets accepted.
- Ambiguous input: makes a reasonable attempt first, then asks targeted questions — never interrogates before trying.
- Large diffs (>300 lines): summarized at a high level, not file-by-file.
- Output is delivered in a copyable code block, with assumptions called out underneath.

## How to invoke

```
write a PR description
draft my pull request
describe my changes
PR summary
```

Or paste a diff, commit log, or branch name (e.g., `fix/JIRA-891-cart-total-rounding`) and ask for a write-up. If nothing is provided, the skill asks at minimum: what changed and why.

## Example output

**Input:** commit log

```
feat: add rate limiting to auth endpoints
fix: return 429 instead of 500 on rate limit hit
chore: add redis dependency
```

**Output:**

```markdown
**Title:** feat: add rate limiting to auth endpoints

## Description

Adds rate limiting to authentication endpoints to prevent brute-force attacks. Uses Redis to track
request counts per IP and returns a proper 429 response when limits are exceeded.

## Changes

- Add rate limiting middleware for `/login` and `/register` endpoints
- Fix: return 429 Too Many Requests instead of 500 on rate limit hit
- Add Redis client dependency for distributed rate limit tracking

## Related Issue

Closes #
```

## See also

- [`SKILL.md`](./SKILL.md) — full LLM-facing instructions
