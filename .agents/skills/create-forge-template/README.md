# create-forge-template

Generate a new [boilerforge](https://github.com/tspyder7/boilerforge) template inside this registry from an existing project.

## What it does

Analyzes a source project (path provided by you) and converts it into a registry-compatible boilerforge template:

```
<template-name>/
├── forge.config.json      # metadata + optional Jexl fileConfig
├── forge.prompt.json      # prompt definitions (text / select / multiselect / toggle)
├── schema/
│   └── prompt.schema.json # canonical prompt schema (copied from assets/)
└── app/                   # every included file copied with .hbs appended
```

Key behaviors:

- **Read-only source** — the input project is never modified, moved, or deleted.
- **Three mandatory gates** — file selection, prompt design, and final confirmation. No file is written until the final gate is answered `yes`.
- **Templatization** — identity values (name, version, author, repo URL) found in the source are replaced with `{{varName}}` Handlebars placeholders; pre-existing `{{` sequences are escaped as `\{{`.
- **Prompts with Jexl** — defaults, validation, and skip conditions use Jexl expressions (`getCwdDirName()`, `matches(input, Regex.VERSION)`, `input in ['a','b']`, ...).
- **Conditional files** — optional feature groups map to toggles and `fileConfig` entries in `forge.config.json`.
- **Validation** — after generation the template is checked against a checklist (unique prompt names, schema conformance, `fileConfig` → file resolution, no secrets/binaries).

## How to invoke

```
create a template from ~/projects/my-app
generate a boilerforge template
make a boilerforge template
convert this project to a template
templatize / forge this project: <path>
```

If no path is given, the skill asks for one.

## Reference assets

Canonical template-level schemas live in [`assets/`](./assets/) — consult them instead of guessing structure:

| Asset | Purpose |
|---|---|
| [`prompt.schema.json`](./assets/prompt.schema.json) | JSON Schema (draft-07) validating `forge.prompt.json` — copied verbatim into every new template |
| [`forge.config.json`](./assets/forge.config.json) | Minimal `metadata` config reference |
| [`forge.prompt.json`](./assets/forge.prompt.json) | Text-only prompts (`name`, `description`, `version`, `author`, `gitUrl`) |
| [`forge.prompt.select.json`](./assets/forge.prompt.select.json) | Adds a `select` prompt with `choices`, index-based `defaultValue`, and membership validation |

## Example output

Given `~/projects/my-api`, the skill produces:

```text
my-api/
├── forge.config.json
├── forge.prompt.json
├── schema/prompt.schema.json
└── app/
    ├── package.json.hbs        # "name": "{{name}}", "version": "{{version}}"
    ├── README.md.hbs
    └── src/index.ts.hbs
```

…after presenting an include/exclude table, proposed prompts, and a final plan summary for approval.

## See also

- [`SKILL.md`](./SKILL.md) — full LLM-facing instructions (gates, phases, hard rules)
