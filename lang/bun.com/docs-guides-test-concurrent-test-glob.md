---
url: https://bun.com/docs/guides/test/concurrent-test-glob
title: Selectively run tests concurrently with glob patterns - Bun
source_domain: bun.com
---

# Selectively run tests concurrently with glob patterns - Bun

This guide demonstrates how to use the `concurrentTestGlob` option to selectively run tests concurrently based on file naming patterns.

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#project-structure) Project Structure

Project Structure

Copy

```
my-project/
├── bunfig.toml
├── tests/
│   ├── unit/
│   │   ├── math.test.ts          # Sequential
│   │   └── utils.test.ts         # Sequential
│   └── integration/
│       ├── concurrent-api.test.ts     # Concurrent
│       └── concurrent-database.test.ts # Concurrent
```

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#configuration) Configuration

Configure your `bunfig.toml` to run test files with “concurrent-” prefix concurrently:

bunfig.toml

Copy

```
[test]
# Run all test files with "concurrent-" prefix concurrently
concurrentTestGlob = "**/concurrent-*.test.ts"
```

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#test-files) Test Files

### [​](https://bun.com/docs/guides/test/concurrent-test-glob#unit-test-sequential) Unit Test (Sequential)

Sequential tests are good for tests that share state or have specific ordering requirements:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)tests/unit/math.test.ts

Copy

```
import { test, expect } from "bun:test";

// These tests run sequentially by default
let sharedState = 0;

test("addition", () => {
  sharedState = 5 + 3;
  expect(sharedState).toBe(8);
});

test("uses previous state", () => {
  // This test depends on the previous test's state
  expect(sharedState).toBe(8);
});
```

### [​](https://bun.com/docs/guides/test/concurrent-test-glob#integration-test-concurrent) Integration Test (Concurrent)

Tests in files matching the glob pattern automatically run concurrently:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)tests/integration/concurrent-api.test.ts

Copy

```
import { test, expect } from "bun:test";

// These tests automatically run concurrently due to filename matching the glob pattern.
// Using test() is equivalent to test.concurrent() when the file matches concurrentTestGlob.
// Each test is independent and can run in parallel.

test("fetch user data", async () => {
  const response = await fetch("/api/user/1");
  expect(response.ok).toBe(true);
});

// can also use test.concurrent() for explicitly marking it as concurrent
test.concurrent("fetch posts", async () => {
  const response = await fetch("/api/posts");
  expect(response.ok).toBe(true);
});

// can also use test.serial() for explicitly marking it as sequential
test.serial("fetch comments", async () => {
  const response = await fetch("/api/comments");
  expect(response.ok).toBe(true);
});
```

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#running-tests) Running Tests

terminal

Copy

```
# Run all tests - concurrent-*.test.ts files will run concurrently
bun test

# Override: Force ALL tests to run concurrently
# Note: This overrides bunfig.toml and runs all tests concurrently, regardless of glob
bun test --concurrent

# Run only unit tests (sequential)
bun test tests/unit

# Run only integration tests (concurrent due to glob pattern)
bun test tests/integration
```

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#benefits) Benefits

1. **Gradual Migration**: Migrate to concurrent tests file by file by renaming them
2. **Clear Organization**: File naming convention indicates execution mode
3. **Performance**: Integration tests run faster in parallel
4. **Safety**: Unit tests remain sequential where needed
5. **Flexibility**: Easy to change execution mode by renaming files

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#migration-strategy) Migration Strategy

To migrate existing tests to concurrent execution:

1. **Start with independent integration tests** - These typically don’t share state
2. **Rename files to match the glob pattern**: `mv api.test.ts concurrent-api.test.ts`
3. **Verify tests still pass** - Run `bun test` to ensure no race conditions
4. **Monitor for shared state issues** - Watch for flaky tests or unexpected failures
5. **Continue migrating stable tests incrementally** - Don’t rush the migration

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#tips) Tips

* **Use descriptive prefixes**: `concurrent-`, `parallel-`, `async-`
* **Keep related sequential tests together** in the same directory
* **Document why certain tests must remain sequential** with comments
* **Use `test.concurrent()` for fine-grained control** in sequential files
  (Note: In files matched by `concurrentTestGlob`, plain `test()` already runs concurrently)

## [​](https://bun.com/docs/guides/test/concurrent-test-glob#multiple-patterns) Multiple Patterns

You can specify multiple patterns for different test categories:

bunfig.toml

Copy

```
[test]
concurrentTestGlob = [
  "**/integration/*.test.ts",
  "**/e2e/*.test.ts",
  "**/concurrent-*.test.ts"
]
```

This configuration will run tests concurrently if they match any of these patterns:

* All tests in `integration/` directories
* All tests in `e2e/` directories
* All tests with `concurrent-` prefix anywhere in the project

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/concurrent-test-glob.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/concurrent-test-glob)

⌘I