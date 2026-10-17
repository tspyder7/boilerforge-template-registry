---
name: pr-description
description:
    Generate clear, well-structured pull request descriptions from code diffs, commit messages,
    branch names, or plain summaries. Use this skill whenever the user wants to write a PR
    description, draft a pull request body, create a GitHub/GitLab/Bitbucket PR summary, or document
    what a set of changes does. Trigger on phrases like "write a PR description", "draft my pull
    request", "describe my changes", "create PR body", "PR summary", "what should I put in my PR",
    or any time the user mentions a pull request and wants help writing about their changes — even
    if they just paste a diff or commit log and ask "help me write this up".
compatibility: opencode
metadata:
    audience: developers
    workflow: git
---

# PR Description Skill

Generate professional, clear pull request descriptions that help reviewers understand changes
quickly and merge with confidence.

---

## When to trigger

- User says "write a PR description", "draft my pull request", "help me write my PR"
- User pastes a diff, commit log, or branch name and asks for a description
- User wants to document changes for code review
- User mentions GitHub, GitLab, Bitbucket PR, or merge request body

---

## Inputs (use whatever the user provides)

Accept any combination of:

- **Git diff** (`git diff main...feature-branch` or raw diff output)
- **Commit messages** (`git log --oneline`)
- **Branch name** (e.g., `feature/JIRA-123-add-user-auth`)
- **Plain summary** (user describes in words what they changed)
- **File list** (which files were changed)
- **Ticket/issue number** (Jira, GitHub issue, Linear, etc.)

If the user provides nothing, ask for at minimum: what changed and why.

---

## Output format

Use the PR template in `assets/pr-template.md` — read it and follow it exactly: no extra sections,
no reordering. That file is the single source of truth for the template; if it changes, follow the
updated template.

Fill it in like this:

- **Title**: A short, imperative-mood subject line (50 chars or less). Format:
  `[type]: short description` where type is one of `feat`, `fix`, `refactor`, `chore`, `docs`,
  `test`. Example: `feat: add rate limiting to auth endpoints`.
- **Description**: 2–4 sentences of plain-English explanation of what the PR does and why. Write for
  someone who hasn't seen the code. Avoid vague phrases like "various fixes" or "updates stuff".
- **Changes**: Bullet list of meaningful changes using action verbs (Add, Fix, Remove, Refactor,
  Update). One idea per bullet. Skip mechanical noise (formatting, lint) unless that's the whole PR.
  Add more bullets if needed — don't limit to 3.
- **Related Issue**: Fill in the issue number if known (e.g., `Closes #42`). If unknown or not
  provided, leave as `Closes #` with a note to the user to fill it in.

---

## Writing guidelines

**Description**: Write for someone who hasn't seen the code. Avoid "this PR", "this commit", or
vague phrases like "various fixes". Be specific: "Adds JWT-based authentication to the `/api/user`
endpoints" not "Updates auth stuff".

**Changes list**:

- Use action verbs: Add, Fix, Remove, Refactor, Update, Extract, Move
- One idea per bullet; add as many bullets as needed
- Skip mechanical changes (formatting, lint) unless that's the whole PR

**Related Issue**: Use `Closes #<number>` to auto-close the issue on merge. If the user provides a
Jira/Linear ticket instead of a GitHub issue number, put it here anyway (e.g., `Closes JIRA-456`).
If no issue is known, leave it blank and note it to the user.

**Tone**: Professional but readable. No corporate filler. Short sentences.

---

## Suggested labels

After the description, suggest labels for the PR. The complete list of labels supported by this
repo lives in `assets/labels.md` — read it and pick only from those.

Rules:

- **Type**: pick exactly one `type:*` label that best matches the dominant change in the PR
  (feature → `type:feature`, fix → `type:bug` or `type:hotfix`, etc.). If it's a
  dependency-only change use `type:dependencies`; docs-only → `type:docs`;
  tests-only → `type:test`; CI-only → `type:ci`.
- **Status / Priority**: do NOT suggest `status:*` or `priority:*` labels unless the user
  explicitly asks for them. If the user asks, pick one of each per the table in
  `assets/labels.md` and ask them to confirm the values.
- Never invent a label that isn't in `assets/labels.md`.

Present the suggested labels as a single line, e.g.:

`Labels: type:feature`

Ask the user if the type label looks right; adjust on request.

---

## Handling limited input

| Input                   | Approach                                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------- |
| Only a diff             | Infer intent from changed code; ask for ticket link if unclear                                    |
| Only commit messages    | Synthesize into coherent summary; note uncertainty                                                |
| Only branch name        | Extract intent from name (e.g., `fix/login-redirect` → fixed login redirect); ask for more detail |
| Plain English summary   | Write directly from that; fill in standard sections                                               |
| Large diff (>300 lines) | Focus on high-level changes; don't enumerate every file                                           |

If the input is ambiguous, make a reasonable attempt first, then ask targeted questions at the end —
don't interrogate before attempting.

---

## Examples

### Example 1 — From commit log

**Input:**

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

**Suggested labels:** `type:feature`

---

### Example 2 — From branch name only

**Input:** `fix/JIRA-891-cart-total-rounding`

**Output:**

```markdown
**Title:** fix: correct cart total floating-point rounding

## Description

Fixes an incorrect cart total calculation caused by floating-point rounding errors. Customers were
seeing totals off by ±$0.01 on certain order amounts.

## Changes

- Fix cart total rounding to use precise decimal arithmetic

## Related Issue

Closes JIRA-891
```

**Suggested labels:** `type:bug`

---

## Output delivery

- Present the description in a code block (so it's easy to copy)
- After the block, show the suggested labels (see [Suggested labels](#suggested-labels))
- Then offer: "Want me to adjust the tone, add more detail to any section, or shorten
  it?"
- If you made assumptions (e.g., inferred the ticket number from the branch name), call them out
  briefly below the description
