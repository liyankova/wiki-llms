---
url: https://bun.com/docs/test
title: Test runner - Bun
source_domain: bun.com
---

# Test runner - Bun

Bun ships with a fast, built-in, Jest-compatible test runner. Tests are executed with the Bun runtime, and support the following features.

* TypeScript and JSX
* Lifecycle hooks
* Snapshot testing
* UI & DOM testing
* Watch mode with `--watch`
* Script pre-loading with `--preload`

Bun aims for compatibility with Jest, but not everything is implemented. To track compatibility, see [this tracking
issue](https://github.com/oven-sh/bun/issues/1825).

## [​](https://bun.com/docs/test#run-tests) Run tests

terminal

Copy

```
bun test
```

Tests are written in JavaScript or TypeScript with a Jest-like API. Refer to [Writing tests](https://bun.com/docs/test/writing-tests) for full documentation.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { expect, test } from "bun:test";

test("2 + 2", () => {
  expect(2 + 2).toBe(4);
});
```

The runner recursively searches the working directory for files that match the following patterns:

* `*.test.{js|jsx|ts|tsx}`
* `*_test.{js|jsx|ts|tsx}`
* `*.spec.{js|jsx|ts|tsx}`
* `*_spec.{js|jsx|ts|tsx}`

You can filter the set of *test files* to run by passing additional positional arguments to `bun test`. Any test file with a path that matches one of the filters will run. Commonly, these filters will be file or directory names; glob patterns are not yet supported.

terminal

Copy

```
bun test <filter> <filter> ...
```

To filter by *test name*, use the `-t`/`--test-name-pattern` flag.

terminal

Copy

```
# run all tests or test suites with "addition" in the name
bun test --test-name-pattern addition
```

To run a specific file in the test runner, make sure the path starts with `./` or `/` to distinguish it from a filter name.

terminal

Copy

```
bun test ./test/specific-file.test.ts
```

The test runner runs all tests in a single process. It loads all `--preload` scripts (see [Lifecycle](https://bun.com/docs/test/lifecycle) for details), then runs all tests. If a test fails, the test runner will exit with a non-zero exit code.

## [​](https://bun.com/docs/test#ci/cd-integration) CI/CD integration

`bun test` supports a variety of CI/CD integrations.

### [​](https://bun.com/docs/test#github-actions) GitHub Actions

`bun test` automatically detects if it’s running inside GitHub Actions and will emit GitHub Actions annotations to the console directly.
No configuration is needed, other than installing `bun` in the workflow and running `bun test`.

#### [​](https://bun.com/docs/test#how-to-install-bun-in-a-github-actions-workflow) How to install `bun` in a GitHub Actions workflow

To use `bun test` in a GitHub Actions workflow, add the following step:

.github/workflows/test.yml

Copy

```
jobs:
  build:
    name: build-app
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Install bun
        uses: oven-sh/setup-bun@v2
      - name: Install dependencies # (assuming your project has dependencies)
        run: bun install # You can use npm/yarn/pnpm instead if you prefer
      - name: Run tests
        run: bun test
```

From there, you’ll get GitHub Actions annotations.

### [​](https://bun.com/docs/test#junit-xml-reports-gitlab,-etc) JUnit XML reports (GitLab, etc.)

To use `bun test` with a JUnit XML reporter, you can use the `--reporter=junit` in combination with `--reporter-outfile`.

terminal

Copy

```
bun test --reporter=junit --reporter-outfile=./bun.xml
```

This will continue to output to stdout/stderr as usual, and also write a JUnit
XML report to the given path at the very end of the test run.
JUnit XML is a popular format for reporting test results in CI/CD pipelines.

## [​](https://bun.com/docs/test#timeouts) Timeouts

Use the `--timeout` flag to specify a *per-test* timeout in milliseconds. If a test times out, it will be marked as failed. The default value is `5000`.

terminal

Copy

```
# default value is 5000
bun test --timeout 20
```

## [​](https://bun.com/docs/test#concurrent-test-execution) Concurrent test execution

By default, Bun runs all tests sequentially within each test file. You can enable concurrent execution to run async tests in parallel, significantly speeding up test suites with independent tests.

### [​](https://bun.com/docs/test#concurrent-flag) `--concurrent` flag

Use the `--concurrent` flag to run all tests concurrently within their respective files:

terminal

Copy

```
bun test --concurrent
```

When this flag is enabled, all tests will run in parallel unless explicitly marked with `test.serial`.

### [​](https://bun.com/docs/test#max-concurrency-flag) `--max-concurrency` flag

Control the maximum number of tests running simultaneously with the `--max-concurrency` flag:

terminal

Copy

```
# Limit to 4 concurrent tests
bun test --concurrent --max-concurrency 4

# Default: 20
bun test --concurrent
```

This helps prevent resource exhaustion when running many concurrent tests. The default value is 20.

### [​](https://bun.com/docs/test#test-concurrent) `test.concurrent`

Mark individual tests to run concurrently, even when the `--concurrent` flag is not used:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { test, expect } from "bun:test";

// These tests run in parallel with each other
test.concurrent("concurrent test 1", async () => {
  await fetch("/api/endpoint1");
  expect(true).toBe(true);
});

test.concurrent("concurrent test 2", async () => {
  await fetch("/api/endpoint2");
  expect(true).toBe(true);
});

// This test runs sequentially
test("sequential test", () => {
  expect(1 + 1).toBe(2);
});
```

### [​](https://bun.com/docs/test#test-serial) `test.serial`

Force tests to run sequentially, even when the `--concurrent` flag is enabled:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { test, expect } from "bun:test";

let sharedState = 0;

// These tests must run in order
test.serial("first serial test", () => {
  sharedState = 1;
  expect(sharedState).toBe(1);
});

test.serial("second serial test", () => {
  // Depends on the previous test
  expect(sharedState).toBe(1);
  sharedState = 2;
});

// This test can run concurrently if --concurrent is enabled
test("independent test", () => {
  expect(true).toBe(true);
});

// Chaining test qualifiers
test.failing.each([1, 2, 3])("chained qualifiers %d", input => {
  expect(input).toBe(0); // This test is expected to fail for each input
});
```

## [​](https://bun.com/docs/test#rerun-tests) Rerun tests

Use the `--rerun-each` flag to run each test multiple times. This is useful for detecting flaky or non-deterministic test failures.

terminal

Copy

```
bun test --rerun-each 100
```

## [​](https://bun.com/docs/test#randomize-test-execution-order) Randomize test execution order

Use the `--randomize` flag to run tests in a random order. This helps detect tests that depend on shared state or execution order.

terminal

Copy

```
bun test --randomize
```

When using `--randomize`, the seed used for randomization will be displayed in the test summary:

terminal

Copy

```
bun test --randomize
```

Copy

```
# ... test output ...
 --seed=12345
 2 pass
 8 fail
Ran 10 tests across 2 files. [50.00ms]
```

### [​](https://bun.com/docs/test#reproducible-random-order-with-seed) Reproducible random order with `--seed`

Use the `--seed` flag to specify a seed for the randomization. This allows you to reproduce the same test order when debugging order-dependent failures.

terminal

Copy

```
# Reproduce a previous randomized run
bun test --seed 123456
```

The `--seed` flag implies `--randomize`, so you don’t need to specify both. Using the same seed value will always produce the same test execution order, making it easier to debug intermittent failures caused by test interdependencies.

## [​](https://bun.com/docs/test#bail-out-with-bail) Bail out with `--bail`

Use the `--bail` flag to abort the test run early after a pre-determined number of test failures. By default Bun will run all tests and report all failures, but sometimes in CI environments it’s preferable to terminate earlier to reduce CPU usage.

terminal

Copy

```
# bail after 1 failure
bun test --bail

# bail after 10 failure
bun test --bail=10
```

## [​](https://bun.com/docs/test#watch-mode) Watch mode

Similar to `bun run`, you can pass the `--watch` flag to `bun test` to watch for changes and re-run tests.

terminal

Copy

```
bun test --watch
```

## [​](https://bun.com/docs/test#lifecycle-hooks) Lifecycle hooks

Bun supports the following lifecycle hooks:

| Hook | Description |
| --- | --- |
| `beforeAll` | Runs once before all tests. |
| `beforeEach` | Runs before each test. |
| `afterEach` | Runs after each test. |
| `afterAll` | Runs once after all tests. |

These hooks can be defined inside test files, or in a separate file that is preloaded with the `--preload` flag.

terminal

Copy

```
bun test --preload ./setup.ts
```

See [Test > Lifecycle](https://bun.com/docs/test/lifecycle) for complete documentation.

## [​](https://bun.com/docs/test#mocks) Mocks

Create mock functions with the `mock` function.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { test, expect, mock } from "bun:test";
const random = mock(() => Math.random());

test("random", () => {
  const val = random();
  expect(val).toBeGreaterThan(0);
  expect(random).toHaveBeenCalled();
  expect(random).toHaveBeenCalledTimes(1);
});
```

Alternatively, you can use `jest.fn()`, it behaves identically.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { test, expect, mock } from "bun:test"; 
import { test, expect, jest } from "bun:test"; 

const random = mock(() => Math.random()); 
const random = jest.fn(() => Math.random());
```

See [Test > Mocks](https://bun.com/docs/test/mocks) for complete documentation.

## [​](https://bun.com/docs/test#snapshot-testing) Snapshot testing

Snapshots are supported by `bun test`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
// example usage of toMatchSnapshot
import { test, expect } from "bun:test";

test("snapshot", () => {
  expect({ a: 1 }).toMatchSnapshot();
});
```

To update snapshots, use the `--update-snapshots` flag.

terminal

Copy

```
bun test --update-snapshots
```

See [Test > Snapshots](https://bun.com/docs/test/snapshots) for complete documentation.

## [​](https://bun.com/docs/test#ui-&-dom-testing) UI & DOM testing

Bun is compatible with popular UI testing libraries:

* [HappyDOM](https://github.com/capricorn86/happy-dom)
* [DOM Testing Library](https://testing-library.com/docs/dom-testing-library/intro/)
* [React Testing Library](https://testing-library.com/docs/react-testing-library/intro)

See [Test > DOM Testing](https://bun.com/docs/test/dom) for complete documentation.

## [​](https://bun.com/docs/test#performance) Performance

Bun’s test runner is fast.

![Running 266 React SSR tests faster than Jest can print its version number.](https://mintcdn.com/bun-1dd33a4e/DJXb5ll7I0cV-M4b/images/buntest.jpeg?fit=max&auto=format&n=DJXb5ll7I0cV-M4b&q=85&s=385ddc5e64d35dd0534663d0f70ab116)

## [​](https://bun.com/docs/test#ai-agent-integration) AI Agent Integration

When using Bun’s test runner with AI coding assistants, you can enable quieter output to improve readability and reduce context noise. This feature minimizes test output verbosity while preserving essential failure information.

### [​](https://bun.com/docs/test#environment-variables) Environment Variables

Set any of the following environment variables to enable AI-friendly output:

* `CLAUDECODE=1` - For Claude Code
* `REPL_ID=1` - For Replit
* `AGENT=1` - Generic AI agent flag

### [​](https://bun.com/docs/test#behavior) Behavior

When an AI agent environment is detected:

* Only test failures are displayed in detail
* Passing, skipped, and todo test indicators are hidden
* Summary statistics remain intact

terminal

Copy

```
# Example: Enable quiet output for Claude Code
CLAUDECODE=1 bun test

# Still shows failures and summary, but hides verbose passing test output
```

This feature is particularly useful in AI-assisted development workflows where reduced output verbosity improves context efficiency while maintaining visibility into test failures.

---

# [​](https://bun.com/docs/test#cli-usage) CLI Usage

Copy

```
bun test <patterns>
```

### [​](https://bun.com/docs/test#execution-control) Execution Control

[​](https://bun.com/docs/test#param-timeout)

--timeout

number

default:"5000"

Set the per-test timeout in milliseconds (default 5000)

[​](https://bun.com/docs/test#param-rerun-each)

--rerun-each

number

Re-run each test file `NUMBER` times, helps catch certain bugs

[​](https://bun.com/docs/test#param-concurrent)

--concurrent

boolean

Treat all tests as `test.concurrent()` tests

[​](https://bun.com/docs/test#param-randomize)

--randomize

boolean

Run tests in random order

[​](https://bun.com/docs/test#param-seed)

--seed

number

Set the random seed for test randomization

[​](https://bun.com/docs/test#param-bail)

--bail

number

default:"1"

Exit the test suite after `NUMBER` failures. If you do not specify a number, it defaults to 1.

[​](https://bun.com/docs/test#param-max-concurrency)

--max-concurrency

number

default:"20"

Maximum number of concurrent tests to execute at once (default 20)

### [​](https://bun.com/docs/test#test-filtering) Test Filtering

[​](https://bun.com/docs/test#param-todo)

--todo

boolean

Include tests that are marked with `test.todo()`

[​](https://bun.com/docs/test#param-test-name-pattern)

--test-name-pattern

string

Run only tests with a name that matches the given regex. Alias: `-t`

### [​](https://bun.com/docs/test#reporting) Reporting

[​](https://bun.com/docs/test#param-reporter)

--reporter

string

Test output reporter format. Available: `junit` (requires —reporter-outfile), `dots`. Default:
console output.

[​](https://bun.com/docs/test#param-reporter-outfile)

--reporter-outfile

string

Output file path for the reporter format (required with —reporter)

[​](https://bun.com/docs/test#param-dots)

--dots

boolean

Enable dots reporter. Shorthand for —reporter=dots

### [​](https://bun.com/docs/test#coverage) Coverage

[​](https://bun.com/docs/test#param-coverage)

--coverage

boolean

Generate a coverage profile

[​](https://bun.com/docs/test#param-coverage-reporter)

--coverage-reporter

string

default:"text"

Report coverage in `text` and/or `lcov`. Defaults to `text`

[​](https://bun.com/docs/test#param-coverage-dir)

--coverage-dir

string

default:"coverage"

Directory for coverage files. Defaults to `coverage`

### [​](https://bun.com/docs/test#snapshots) Snapshots

[​](https://bun.com/docs/test#param-update-snapshots)

--update-snapshots

boolean

Update snapshot files. Alias: `-u`

## [​](https://bun.com/docs/test#examples) Examples

Run all test files:

terminal

Copy

```
bun test
```

Run all test files with “foo” or “bar” in the file name:

terminal

Copy

```
bun test foo bar
```

Run all test files, only including tests whose names includes “baz”:

terminal

Copy

```
bun test --test-name-pattern baz
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test)

⌘I