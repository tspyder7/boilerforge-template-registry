# Boilerforge Template Registry

Repository for [boilerforge](https://github.com/tspyder7/boilerforge) — a scaffolding CLI that generates fully functional project boilerplates from parameterized Handlebars templates with Jexl-powered prompts, AJV validation, and interactive user flows.

## Templates

| Template | Version | Purpose |
|----------|---------|---------|
| create-cli-app | 2.0.0 | Interactive CLI scaffolding tool with Commander-based subcommand architecture, Enquirer prompt flow with AJV/Jexl validation, Listr2 task orchestration with rollback, esbuild bundling, Express-style file resource management, and full dev tooling (ESLint, Prettier, Husky, commitlint, pnpm) |
| create-node-lib | 1.0.0 | TypeScript ESM library scaffold with tsc build, Vitest (100% coverage thresholds), ESLint + Prettier, Husky + commitlint, release-please config, and a GitHub Actions release pipeline — package manager selectable (npm/yarn/pnpm/bun) |
| create-github-wkf | 1.0.0 | TypeScript scaffold for GitHub workflow automation — Bun runtime, Vitest (100% coverage thresholds), ESLint + Prettier, Husky + commitlint + lint-staged, OpenCode agent tooling (rules, skills, commands), and a minimal pino-ready src entry |
| create-next-app | 1.0.0 | Next.js 16 App Router starter — React 19, TypeScript 5, Tailwind CSS v4, pnpm, husky + commitlint + lint-staged, and OpenCode agent tooling (rules, skills, commands) |