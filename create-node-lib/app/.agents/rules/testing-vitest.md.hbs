---
description: Vitest testing standards
globs:
  - "**/*.test.ts"
  - "**/*.spec.ts"
alwaysApply: true
---

# Testing Standards

## General

- Every public function should have tests.
- Tests should verify behaviour, not implementation.
- Follow Arrange → Act → Assert.
- Each test should validate one behaviour.

Example

```ts
it('throws when repository does not exist', async () => {
    // Arrange

    // Act

    // Assert
});
```

## Naming

Use descriptive test names.

Prefer

```ts
it('returns cached client when already initialized')
```

instead of

```ts
it('test init')
```

## Mocking

Prefer mocking boundaries:

- GitHub API
- filesystem
- network
- process
- environment

Avoid mocking internal implementation whenever possible.

Never mock the function under test.

Mock dependencies instead.

## Vitest APIs

Prefer

```ts
vi.mock(...)
vi.spyOn(...)
vi.stubEnv(...)
vi.restoreAllMocks()
vi.clearAllMocks()
```

Restore state after every test.

```ts
afterEach(() => {
    vi.restoreAllMocks();
});
```

## Singleton Testing

Reset singleton state between tests.

Never allow state leakage.

## Assertions

Use explicit assertions.

Prefer

```ts
expect(result).toEqual(...)
```

instead of snapshot testing unless snapshots add clear value.

Verify thrown errors.

```ts
await expect(fn()).rejects.toThrow(...)
```

## Async

Always await async expectations.

Never write

```ts
expect(asyncFn()).rejects...
```

Instead

```ts
await expect(asyncFn()).rejects...
```

## Coverage

Target:

- >90% statements
- >90% branches

Do not write meaningless tests solely to increase coverage.

## Test Structure

One describe block per module.

Group related behaviour.

Example

```ts
describe('Router', () => {

    describe('routing', () => {

    });

    describe('validation', () => {

    });

});
```

## Fixtures

Prefer factory helpers over duplicated setup.

Good

```ts
const issue = createIssue({
    labels: [...]
});
```

Bad

Repeated 100-line JSON payloads.

## GitHub API

Never call real GitHub APIs.

Always mock:

- Octokit
- GitHub Actions Toolkit
- Environment variables
- Process exit
- Logger

## Logging

Assert logging only when logging is part of expected behaviour.

Do not assert every log message.

## Test Quality

Avoid:

- implementation-specific assertions
- private method testing
- testing internal variables
- testing TypeScript itself

Focus on observable behavior.
