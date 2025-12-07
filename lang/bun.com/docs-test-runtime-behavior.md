---
url: https://bun.com/docs/test/runtime-behavior
title: Runtime behavior - Bun
source_domain: bun.com
---

# Runtime behavior - Bun

`bun test` is deeply integrated with Bun’s runtime. This is part of what makes `bun test` fast and simple to use.

## [​](https://bun.com/docs/test/runtime-behavior#environment-variables) Environment Variables

### [​](https://bun.com/docs/test/runtime-behavior#node-env) NODE\_ENV

`bun test` automatically sets `$NODE_ENV` to `"test"` unless it’s already set in the environment or via `.env` files. This is standard behavior for most test runners and helps ensure consistent test behavior.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("NODE_ENV is set to test", () => {
  expect(process.env.NODE_ENV).toBe("test");
});
```

You can override this by setting `NODE_ENV` explicitly:

terminal

Copy

```
NODE_ENV=development bun test
```

### [​](https://bun.com/docs/test/runtime-behavior#tz-timezone) TZ (Timezone)

By default, all `bun test` runs use UTC (`Etc/UTC`) as the time zone unless overridden by the `TZ` environment variable. This ensures consistent date and time behavior across different development environments.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("timezone is UTC by default", () => {
  const date = new Date();
  expect(date.getTimezoneOffset()).toBe(0);
});
```

To test with a specific timezone:

terminal

Copy

```
TZ=America/New_York bun test
```

## [​](https://bun.com/docs/test/runtime-behavior#test-timeouts) Test Timeouts

Each test has a default timeout of 5000ms (5 seconds) if not explicitly overridden. Tests that exceed this timeout will fail.

### [​](https://bun.com/docs/test/runtime-behavior#global-timeout) Global Timeout

Change the timeout globally with the `--timeout` flag:

terminal

Copy

```
bun test --timeout 10000  # 10 seconds
```

### [​](https://bun.com/docs/test/runtime-behavior#per-test-timeout) Per-Test Timeout

Set timeout per test as the third parameter to the test function:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("fast test", () => {
  expect(1 + 1).toBe(2);
}, 1000); // 1 second timeout

test("slow test", async () => {
  await new Promise(resolve => setTimeout(resolve, 8000));
}, 10000); // 10 second timeout
```

### [​](https://bun.com/docs/test/runtime-behavior#infinite-timeout) Infinite Timeout

Use `0` or `Infinity` to disable timeout:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
test("test without timeout", async () => {
  // This test can run indefinitely
  await someVeryLongOperation();
}, 0);
```

## [​](https://bun.com/docs/test/runtime-behavior#error-handling) Error Handling

### [​](https://bun.com/docs/test/runtime-behavior#unhandled-errors) Unhandled Errors

`bun test` tracks unhandled promise rejections and errors that occur between tests. If such errors occur, the final exit code will be non-zero (specifically, the count of such errors), even if all tests pass.
This helps catch errors in asynchronous code that might otherwise go unnoticed:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test } from "bun:test";

test("test 1", () => {
  // This test passes
  expect(true).toBe(true);
});

// This error happens outside any test
setTimeout(() => {
  throw new Error("Unhandled error");
}, 0);

test("test 2", () => {
  // This test also passes
  expect(true).toBe(true);
});

// The test run will still fail with a non-zero exit code
// because of the unhandled error
```

### [​](https://bun.com/docs/test/runtime-behavior#promise-rejections) Promise Rejections

Unhandled promise rejections are also caught:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test } from "bun:test";

test("passing test", () => {
  expect(1).toBe(1);
});

// This will cause the test run to fail
Promise.reject(new Error("Unhandled rejection"));
```

### [​](https://bun.com/docs/test/runtime-behavior#custom-error-handling) Custom Error Handling

You can set up custom error handlers in your test setup:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test-setup.ts

Copy

```
process.on("uncaughtException", error => {
  console.error("Uncaught Exception:", error);
  process.exit(1);
});

process.on("unhandledRejection", (reason, promise) => {
  console.error("Unhandled Rejection at:", promise, "reason:", reason);
  process.exit(1);
});
```

## [​](https://bun.com/docs/test/runtime-behavior#cli-flags-integration) CLI Flags Integration

Several Bun CLI flags can be used with `bun test` to modify its behavior:

### [​](https://bun.com/docs/test/runtime-behavior#memory-usage) Memory Usage

terminal

Copy

```
# Reduces memory usage for the test runner VM
bun test --smol
```

### [​](https://bun.com/docs/test/runtime-behavior#debugging) Debugging

terminal

Copy

```
# Attaches the debugger to the test runner process
bun test --inspect
bun test --inspect-brk
```

### [​](https://bun.com/docs/test/runtime-behavior#module-loading) Module Loading

terminal

Copy

```
# Runs scripts before test files (useful for global setup/mocks)
bun test --preload ./setup.ts

# Sets compile-time constants
bun test --define "process.env.API_URL='http://localhost:3000'"

# Configures custom loaders
bun test --loader .special:special-loader

# Uses a different tsconfig
bun test --tsconfig-override ./test-tsconfig.json

# Sets package.json conditions for module resolution
bun test --conditions development

# Loads environment variables for tests
bun test --env-file .env.test
```

### [​](https://bun.com/docs/test/runtime-behavior#installation-related-flags) Installation-related Flags

Copy

```
# Affect any network requests or auto-installs during test execution
bun test --prefer-offline
bun test --frozen-lockfile
```

## [​](https://bun.com/docs/test/runtime-behavior#watch-and-hot-reloading) Watch and Hot Reloading

### [​](https://bun.com/docs/test/runtime-behavior#watch-mode) Watch Mode

When running `bun test` with the `--watch` flag, the test runner will watch for file changes and re-run affected tests.

terminal

Copy

```
bun test --watch
```

The test runner is smart about which tests to re-run:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { add } from "./math.js";
import { test, expect } from "bun:test";

test("addition", () => {
  expect(add(2, 3)).toBe(5);
});
```

If you modify `math.js`, only `math.test.ts` will re-run, not all tests.

### [​](https://bun.com/docs/test/runtime-behavior#hot-reloading) Hot Reloading

The `--hot` flag provides similar functionality but is more aggressive about trying to preserve state between runs:

terminal

Copy

```
bun test --hot
```

For most test scenarios, `--watch` is the recommended option as it provides better isolation between test runs.

## [​](https://bun.com/docs/test/runtime-behavior#global-variables) Global Variables

The following globals are automatically available in test files without importing (though they can be imported from `bun:test` if preferred):

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// All of these are available globally
test("global test function", () => {
  expect(true).toBe(true);
});

describe("global describe", () => {
  beforeAll(() => {
    // global beforeAll
  });

  it("global it function", () => {
    // it is an alias for test
  });
});

// Jest compatibility
jest.fn();

// Vitest compatibility
vi.fn();
```

You can also import them explicitly if you prefer:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, it, describe, expect, beforeAll, beforeEach, afterAll, afterEach, jest, vi } from "bun:test";
```

## [​](https://bun.com/docs/test/runtime-behavior#process-integration) Process Integration

### [​](https://bun.com/docs/test/runtime-behavior#exit-codes) Exit Codes

`bun test` uses standard exit codes:

* `0`: All tests passed, no unhandled errors
* `1`: Test failures occurred
* `>1`: Number of unhandled errors (even if tests passed)

### [​](https://bun.com/docs/test/runtime-behavior#signal-handling) Signal Handling

The test runner properly handles common signals:

terminal

Copy

```
# Gracefully stops test execution
kill -SIGTERM <test-process-pid>

# Immediately stops test execution
kill -SIGKILL <test-process-pid>
```

### [​](https://bun.com/docs/test/runtime-behavior#environment-detection) Environment Detection

Bun automatically detects certain environments and adjusts behavior:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// GitHub Actions detection
if (process.env.GITHUB_ACTIONS) {
  // Bun automatically emits GitHub Actions annotations
}

// CI detection
if (process.env.CI) {
  // Certain behaviors may be adjusted for CI environments
}
```

## [​](https://bun.com/docs/test/runtime-behavior#performance-considerations) Performance Considerations

### [​](https://bun.com/docs/test/runtime-behavior#single-process) Single Process

The test runner runs all tests in a single process by default. This provides:

* **Faster startup** - No need to spawn multiple processes
* **Shared memory** - Efficient resource usage
* **Simple debugging** - All tests in one process

However, this means:

* Tests share global state (use lifecycle hooks to clean up)
* One test crash can affect others
* No true parallelization of individual tests

### [​](https://bun.com/docs/test/runtime-behavior#memory-management) Memory Management

terminal

Copy

```
# Monitor memory usage
bun test --smol  # Reduces memory footprint

# For large test suites, consider splitting files
bun test src/unit/
bun test src/integration/
```

### [​](https://bun.com/docs/test/runtime-behavior#test-isolation) Test Isolation

Since tests run in the same process, ensure proper cleanup:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { afterEach } from "bun:test";

afterEach(() => {
  // Clean up global state
  global.myGlobalVar = undefined;
  delete process.env.TEST_VAR;

  // Reset modules if needed
  jest.resetModules();
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test/runtime-behavior.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test/runtime-behavior)

⌘I