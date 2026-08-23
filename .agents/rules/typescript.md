---
description: TypeScript coding standards for backend services
globs:
  - "**/*.ts"
alwaysApply: true
---

# TypeScript Standards

## General

- Always use strict TypeScript.
- Never use `any`.
- Prefer `unknown` over `any`.
- Prefer explicit return types for exported functions.
- Avoid non-null assertions (`!`) unless absolutely required.
- Use ES modules.
- Keep files focused on a single responsibility.

## Imports

- Use named imports whenever possible.
- Group imports in this order:
  1. Node built-in modules
  2. External packages
  3. Internal modules
  4. Types (`import type`)
- Remove unused imports.
- Prefer `import type` for type-only imports.

Example:

```ts
import fs from 'node:fs';

import { z } from 'zod';

import { logger } from '../logger';

import type { Request } from '../types';
```

## Functions

- Prefer pure functions.
- Keep nesting shallow.
- Return early instead of large if/else blocks.
- Prefer ternary operator instead of if/else block wherever possible
- Prefer async/await over promise chains.
- Throw typed errors instead of returning error objects.

Prefer

```ts
if (!user) {
    throw new Error('User not found');
}

return user;
```

instead of

```ts
if (user) {
    ...
} else {
    ...
}
```

## Naming

Classes:
- PascalCase

Functions:
- camelCase

Constants:
- UPPER_SNAKE_CASE only for true constants

Variables:
- camelCase

Interfaces:
- Avoid `I` prefix.

Enums:
- Prefer string enums.

## Types

Prefer

```ts
type User = {}
```

instead of

```ts
interface User {}
```

unless declaration merging is required.

Avoid unnecessary generic abstractions.

## Error Handling

Never silently swallow exceptions.

Prefer

```ts
try {
    ...
} catch (error) {
    logger.error(error);
    throw error;
}
```

## Backend Practices

- Validate all external input.
- Never trust GitHub webhook payloads.
- Keep business logic separate from transport layer.
- Avoid global mutable state.
- Use dependency injection where practical.

## Comments

Avoid comments explaining *what* code does.

Only comment:

- business rules
- security assumptions
- non-obvious implementation details

## Formatting

- Maximum readability over compact code.
- Keep functions under ~60 lines when possible.
- Avoid deeply nested logic.
- One exported entity per file when practical.
