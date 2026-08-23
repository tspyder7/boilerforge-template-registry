---
name: create-forge-template
description:
    Generate a new boilerforge template from an existing project. Use when the user gives a path
    to a project and wants to turn it into a boilerforge template (forge.config.json,
    forge.prompt.json, schema, app/*.hbs). Triggers on "create template", "generate template",
    "make a boilerforge template", "convert this project to a template", or when the user shares
    a project path asking to templatize/forge it.
compatibility: opencode
metadata:
    audience: developers
    workflow: boilerforge-templating
---

## What I do

- Analyze an existing project (path provided by user) and convert it into a
  [boilerforge](https://github.com/tspyder7/boilerforge) template inside this registry
- **ALWAYS ask the user** about: template name, which files to include, which values to
  templatize into prompts, and conditional file groups — before writing anything
- Produce a valid template structure:

```
<template-name>/
├── forge.config.json      # metadata + optional Jexl fileConfig
├── forge.prompt.json      # prompt definitions (text / select / multiselect / toggle)
├── schema/
│   └── prompt.schema.json # copied verbatim from this skill's assets/prompt.schema.json
└── app/                   # every included file copied with .hbs appended
```

### Reference assets (`assets/`)

Canonical template-level schemas live in `assets/` next to this file. **Always model output on
these files — never invent structure.** They are copies of real registry templates:

| Asset | Use as reference for |
|---|---|
| `assets/prompt.schema.json` | The JSON Schema (draft-07) validating `forge.prompt.json`. Copy verbatim into `<template-name>/schema/prompt.schema.json` for every new template. |
| `assets/forge.config.json` | Minimal `forge.config.json` shape (`metadata.name` must equal the directory name). |
| `assets/forge.prompt.json` | Text-only prompts: required `name` prompt, `defaultValue` Jexl, `validate.{expression,error}`. |
| `assets/forge.prompt.select.json` | A `select` prompt with `choices: [{name, value}]`, index-string `defaultValue` (`"3"`), and membership validation (`input in [...]`). |

Read an asset whenever you need the exact field names, nesting, or Jexl idiom — do not rely on memory.

## Hard rules

1. The source project is **READ-ONLY**. Never modify, move, or delete anything in it.
2. New templates are created at the **registry root** (same level as `create-cli-app/`).
3. `metadata.name` in `forge.config.json` MUST equal the template directory name.
4. `forge.prompt.json` MUST contain at least one prompt with `name: "name"`, `type: "text"`.
   All prompt names must be unique and valid identifiers (`[a-zA-Z][a-zA-Z0-9]*`).
5. Every key in `fileConfig` must have a matching `app/<key>.hbs` file (forward slashes, no
   `.hbs` extension in the key). Files NOT listed in `fileConfig` are always included.
6. Never write binary files into `app/`. Never include secrets (`.env*`, keys, tokens).
7. **NEVER create any file until Gate 3 is answered `yes`.**

---

## ⚠️ Mandatory Gates

There are three user gates. Do not skip any.

### Gate 1 — File selection
After analyzing the source project, present the proposed include/exclude table and ask the
user to confirm or adjust. Use the question tool or plain text; wait for an answer.

### Gate 2 — Prompt design
Present the proposed prompt variables and conditional toggles. Ask what to add/remove/rename.
Wait for an answer.

### Gate 3 — Final confirmation (MOST IMPORTANT)
Before creating ANY file, output the full plan summary and then **STOP**:

```
─────────────────────────────────────────
  Template plan:

  Name:     <template-name>
  Location: <registry-root>/<template-name>/
  Files:    N files → app/**/*.hbs

  Prompts:
    - name        (text)    Project name [getCwdDirName()]
    - version     (text)    Version ['1.0.0'] validated by Regex.VERSION
    ...

  Conditional files (fileConfig):
    tsconfig.json          → isTypescript == true
    ...
─────────────────────────────────────────
  Generate this template? [yes / edit / no]
```

| User reply | Action |
|---|---|
| `yes` / `y` | Generate everything, then run Phase 4 validation |
| `edit` / `e` | Ask what to change, show updated plan, show gate again |
| `no` / `n` | Discard plan; restart from Phase 1 or abort per user's wish |
| Anything else | Treat as `no`; ask for clarification |

---

## Phase 0 — Resolve input

- If no path was given, ask for it.
- Verify the path exists and is a directory. If not, report and re-ask.
- Record `SOURCE_DIR` and its basename (used for default suggestions).

## Phase 1 — Analyze source project

1. Detect project type from markers: `package.json`, `pyproject.toml`, `go.mod`,
   `Cargo.toml`, `pom.xml`, etc.
2. List all files recursively. Auto-exclude (but list them so the user can override):

   | Category | Patterns |
   |---|---|
   | Dependencies/build | `node_modules/`, `dist/`, `build/`, `out/`, `target/`, `vendor/`, `__pycache__/`, `.venv/` |
   | VCS | `.git/` |
   | Lockfiles | `pnpm-lock.yaml`, `package-lock.json`, `yarn.lock`, `Cargo.lock`, `poetry.lock` |
   | Secrets | `.env`, `.env.*`, `*.pem`, `*.key` |
   | Binaries | images/media/archives, anything non-text |

3. Read candidate identity values: project name, description, version, author, license,
   repo URL — note every file+line where they appear.
4. Spot optional feature groups for toggles, e.g.: CI workflows, Dockerfile, lint/format
   configs, test setup, docs.
5. Scan included files for existing `{{` sequences (Handlebars conflicts). Flag each one;
   these need escaping as `\{{` during generation or must be excluded.

## Phase 2 — Gate 1: file selection

Present a table like:

```
  INCLUDE  README.md
  INCLUDE  src/index.ts
  EXCLUDE  pnpm-lock.yaml      (lockfile)
  EXCLUDE  .env                (secret)
```

Ask: confirm? exclude more? include something currently excluded?

## Phase 3 — Gate 2: prompt design

Propose prompts derived from analysis. Standard starter set (adjust to the project):

| name | type | message | defaultValue (Jexl) | validate |
|---|---|---|---|---|
| `name` | text | Project name | `getCwdDirName()` | — |
| `description` | text | Description | `''` | — |
| `version` | text | Version | `'1.0.0'` | `matches(input, Regex.VERSION)` |
| `author` | text | Author | `''` | — |

Jexl rules for `defaultValue` / `validate.expression` / `skip`:

- Strings must be single-quoted: `''`, `'5.8'`
- Numbers/booleans bare: `true`, `3`
- Available functions/context: `getCwdDirName()`, `matches(input, Regex.PROJECT_NAME)`,
  `matches(input, Regex.VERSION)`, `isBoolean(input)`, `input in ['a','b']`, earlier prompt vars
- Toggle validate: `isBoolean(input)`
- Select/multiselect require `choices: [{name, value}]` and `defaultValue` is the index as a
  string (`"0"`); validate membership: `input in [...]`

For exact shapes, read the assets: `assets/forge.prompt.json` (text prompts),
`assets/forge.prompt.select.json` (select prompt), and validate designs against
`assets/prompt.schema.json`.

For each conditional file group propose a toggle (`isTypescript`, `isEslintPrettier`,
`hasCi`, ...) that maps to `fileConfig` entries.

Ask the user: which variables to templatize (or keep literal), renames, extra custom
prompts (select/toggle), and which groups should be conditional.

## Phase 4 — Generate (only after Gate 3 `yes`)

Run inside the registry root (`create-cli-app/` lives here):

1. `mkdir -p <template-name>/schema <template-name>/app`
2. Copy the canonical schema verbatim from this skill's assets:
   ```bash
   cp .agents/skills/create-forge-template/assets/prompt.schema.json \
      <template-name>/schema/prompt.schema.json
   ```
   (If the assets dir is missing, fall back to any existing template:
   `cp create-cli-app/schema/prompt.schema.json <template-name>/schema/prompt.schema.json`.)
3. For each included source file, copy to `app/<relative-path>.hbs` while:
   - Replacing identity values found in Phase 1 with `{{varName}}` (e.g. old project name →
     `{{name}}`)
   - Escaping pre-existing `{{` as `\{{` where templating is not intended
   - Preserving directory structure exactly
4. Write `<template-name>/forge.config.json`:
   ```json
   {
       "metadata": { "name": "<template-name>", "version": "1.0.0" },
       "fileConfig": { "<rel/path.ext>": "<jexl condition>" }
   }
   ```
   Omit `fileConfig` entirely if there are no conditions.
5. Write `<template-name>/forge.prompt.json` with the agreed prompts (structure: top-level
   `{ "prompts": [ ... ] }`; each item needs `type`, `name`, `description`, `prompt.message`;
   optional `prompt.defaultValue`, `validate.{expression,error}`, `skip`, `choices`, `options`).
   Model it on `assets/forge.prompt.json` (text) and/or
   `assets/forge.prompt.select.json` (select).
6. Ask the user if the root `README.md` Templates table should be updated; if yes, add a row.

## Phase 5 — Validate & report

Run all checks; fix failures before reporting success:

```bash
# JSON validity
node -e "['forge.config.json','forge.prompt.json','schema/prompt.schema.json'].forEach(f => JSON.parse(require('fs').readFileSync('<template-name>/'+f,'utf8')))"
```

Checklist:
- [ ] Directory name == `metadata.name`
- [ ] Exactly one prompt named `name` of type `text`; all names unique & identifier-safe
- [ ] select/multiselect → has `choices`; toggle → has `options{enabled,disabled}`
- [ ] `validate` objects always have both `expression` and `error`
- [ ] Every `fileConfig` key resolves to an existing `app/<key>.hbs`
- [ ] No binaries/secrets under `app/`; no unescaped stray `{{` conflicts
- [ ] `defaultValue` strings are single-quoted Jexl literals

Then print test instructions:

```bash
boilerforge list-templates            # after registering/symlinking the template dir
boilerforge show-config <template-name>
boilerforge create <template-name>
boilerforge create <template-name> --cli-config "name=demo;version=1.0.0"
```

Finally remind the user: nothing is committed unless they explicitly ask.
