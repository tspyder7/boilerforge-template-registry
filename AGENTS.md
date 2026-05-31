# Boilerforge Template Registry

## Structure

- Root `README.md`: brief registry description (non-executable prose — trust config/code)
- Root has no `package.json`, tests, CI, linter, or formatter config. This is a **template collection**, not an application.
- Each template lives in its own subdirectory (currently: `create-cli-app/`)

## Templates

### `create-cli-app/`

Generates a TypeScript CLI application scaffolded for [boilerforge](https://github.com/tspyder7/boilerforge).

**Key files per template:**
- `forge.config.json` — template metadata (name, version)
- `forge.prompt.json` — user-facing prompts (text inputs: name, description, version, author, gitUrl)
- `schema/prompt.schema.json` — JSON Schema (draft-07) validating `forge.prompt.json` structure

**Template content** lives under `app/` — all `.hbs` (Handlebars) files are rendered at generation time with prompt response variables.

**Generated project characteristics** (from `app/package.json.hbs`):
- TypeScript, pnpm (`pnpm@10.9.0`), Node >= 24
- Entry: `bin/cli.ts` → `dist/cli.js`
- Build: `esbuild`, invoked via `pnpm run build` (runs clean → lint → format → build)
- Dev: `pnpm run dev` (runs via `ts-node`)
- Test: placeholder (`echo "Error: no test specified"`)
- Lint: ESLint — `pnpm run lint` (eslint --ext .js,.ts .)
- Format: Prettier — `pnpm run format` (prettier --write "**/*.+(js|ts)")
- Hooks: Husky + commitlint (conventional commits)
- Dependencies: Commander (CLI), Enquirer (prompts), Jexl (expressions), Listr2 (tasks), AJV (validation), Handlebars (rendering), chalk, execa, globby, inquirer

**Architecture** (`app/src/`):
- `core/` — context singletons (AppContext, CLIContext, ExecutionContext, ExprContext, PromptContext)
- `modules/cli/` — Commander-based CLI with sub-command pattern (BaseCommand + ISubCommand interface)
- `modules/expr/` — Jexl expression evaluation with custom functions (`getCwdDirName`, `matches`, `isBoolean`)
- `modules/filesystem/` — FileResource / FileHandler (CRUD on generated files)
- `modules/prompter/` — PromptParser + Enquirer dispatch, AJV schema validation
- `modules/task/` — Listr2 task orchestration with rollback
- `types/` — shared TypeScript interfaces and type definitions
- `utils/` — logger, path helpers, schema validator, UUID generation, CLI version
- `constants/` — Regex patterns, CLI metadata

## Notes for agents

- **No root-level project commands exist.** Do not try to `npm install`, `npm run build`, or `npm test` at root.
- **No CI/CD** exists in this repo.
- **All template source files are `.hbs`** (Handlebars) with `{{variable}}` interpolation. Edits to template logic must preserve this syntax.
- Prompt schemas use **Jexl expressions** for defaults, validation, and skip conditions (not JS).
- `app/.opencode/skills/` contains OpenCode skill templates (`.hbs` rendered into the generated project's `.opencode/skills/`).
- The generated project's `packageManager` is `pnpm@10.9.0` — not npm or yarn.
