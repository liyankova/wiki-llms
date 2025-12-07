---
url: https://bun.com/docs/test/configuration
title: Test configuration - Bun
source_domain: bun.com
---

# Test configuration - Bun

Configure `bun test` via `bunfig.toml` file and command-line options. This page documents the available configuration options for `bun test`.

## [​](https://bun.com/docs/test/configuration#configuration-file) Configuration File

You can configure `bun test` behavior by adding a `[test]` section to your `bunfig.toml` file:

bunfig.toml

Copy

```
[test]
# Options go here
```

## [​](https://bun.com/docs/test/configuration#test-discovery) Test Discovery

### [​](https://bun.com/docs/test/configuration#root) root

The `root` option specifies a root directory for test discovery, overriding the default behavior of scanning from the project root.

bunfig.toml

Copy

```
[test]
root = "src"  # Only scan for tests in the src directory
```

This is useful when you want to:

* Limit test discovery to specific directories
* Exclude certain parts of your project from test scanning
* Organize tests in a specific subdirectory structure

#### [​](https://bun.com/docs/test/configuration#examples) Examples

bunfig.toml

Copy

```
[test]
# Only run tests in the src directory
root = "src"

# Run tests in a specific test directory
root = "tests"

# Run tests in multiple specific directories (not currently supported - use patterns instead)
# root = ["src", "lib"]  # This syntax is not supported
```

### [​](https://bun.com/docs/test/configuration#preload-scripts) Preload Scripts

Load scripts before running tests using the `preload` option:

bunfig.toml

Copy

```
[test]
preload = ["./test-setup.ts", "./global-mocks.ts"]
```

This is equivalent to using `--preload` on the command line:

terminal

Copy

```
bun test --preload ./test-setup.ts --preload ./global-mocks.ts
```

#### [​](https://bun.com/docs/test/configuration#common-preload-use-cases) Common Preload Use Cases

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test-setup.ts

Copy

```
// Global test setup
import { beforeAll, afterAll } from "bun:test";

beforeAll(() => {
  // Set up test database
  setupTestDatabase();
});

afterAll(() => {
  // Clean up
  cleanupTestDatabase();
});
```

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)global-mocks.ts

Copy

```
// Global mocks
import { mock } from "bun:test";

// Mock environment variables
process.env.NODE_ENV = "test";
process.env.API_URL = "http://localhost:3001";

// Mock external dependencies
mock.module("./external-api", () => ({
  fetchData: mock(() => Promise.resolve({ data: "test" })),
}));
```

## [​](https://bun.com/docs/test/configuration#timeouts) Timeouts

### [​](https://bun.com/docs/test/configuration#default-timeout) Default Timeout

Set the default timeout for all tests:

bunfig.toml

Copy

```
[test]
timeout = 10000  # 10 seconds (default is 5000ms)
```

This applies to all tests unless overridden by individual test timeouts:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// This test will use the default timeout from bunfig.toml
test("uses default timeout", () => {
  // test implementation
});

// This test overrides the default timeout
test("custom timeout", () => {
  // test implementation
}, 30000); // 30 seconds
```

## [​](https://bun.com/docs/test/configuration#reporters) Reporters

### [​](https://bun.com/docs/test/configuration#junit-reporter) JUnit Reporter

Configure the JUnit reporter output file path directly in the config file:

bunfig.toml

Copy

```
[test.reporter]
junit = "path/to/junit.xml"  # Output path for JUnit XML report
```

This complements the `--reporter=junit` and `--reporter-outfile` CLI flags:

terminal

Copy

```
# Equivalent command line usage
bun test --reporter=junit --reporter-outfile=./junit.xml
```

#### [​](https://bun.com/docs/test/configuration#multiple-reporters) Multiple Reporters

You can use multiple reporters simultaneously:

terminal

Copy

```
# CLI approach
bun test --reporter=junit --reporter-outfile=./junit.xml

# Config file approach
```

bunfig.toml

Copy

```
[test.reporter]
junit = "./reports/junit.xml"

[test]
# Also enable coverage reporting
coverage = true
coverageReporter = ["text", "lcov"]
```

## [​](https://bun.com/docs/test/configuration#memory-usage) Memory Usage

### [​](https://bun.com/docs/test/configuration#smol-mode) smol Mode

Enable the `--smol` memory-saving mode specifically for the test runner:

bunfig.toml

Copy

```
[test]
smol = true  # Reduce memory usage during test runs
```

This is equivalent to using the `--smol` flag on the command line:

terminal

Copy

```
bun test --smol
```

The `smol` mode reduces memory usage by:

* Using less memory for the JavaScript heap
* Being more aggressive about garbage collection
* Reducing buffer sizes where possible

This is useful for:

* CI environments with limited memory
* Large test suites that consume significant memory
* Development environments with memory constraints

## [​](https://bun.com/docs/test/configuration#test-execution) Test execution

### [​](https://bun.com/docs/test/configuration#concurrenttestglob) concurrentTestGlob

Automatically run test files matching a glob pattern with concurrent test execution enabled. This is useful for gradually migrating test suites to concurrent execution or for running specific test types concurrently.

bunfig.toml

Copy

```
[test]
concurrentTestGlob = "**/concurrent-*.test.ts"  # Run files matching this pattern concurrently
```

Test files matching this pattern will behave as if the `--concurrent` flag was passed, running all tests within those files concurrently. This allows you to:

* Gradually migrate your test suite to concurrent execution
* Run integration tests concurrently while keeping unit tests sequential
* Separate fast concurrent tests from tests that require sequential execution

The `--concurrent` CLI flag will override this setting when specified, forcing all tests to run concurrently regardless of the glob pattern.

#### [​](https://bun.com/docs/test/configuration#randomize) randomize

Run tests in random order to identify tests with hidden dependencies:

bunfig.toml

Copy

```
[test]
randomize = true
```

#### [​](https://bun.com/docs/test/configuration#seed) seed

Specify a seed for reproducible random test order. Requires `randomize = true`:

bunfig.toml

Copy

```
[test]
randomize = true
seed = 2444615283
```

#### [​](https://bun.com/docs/test/configuration#reruneach) rerunEach

Re-run each test file multiple times to identify flaky tests:

bunfig.toml

Copy

```
[test]
rerunEach = 3
```

## [​](https://bun.com/docs/test/configuration#coverage-options) Coverage Options

### [​](https://bun.com/docs/test/configuration#basic-coverage-settings) Basic Coverage Settings

bunfig.toml

Copy

```
[test]
# Enable coverage by default
coverage = true

# Set coverage reporter
coverageReporter = ["text", "lcov"]

# Set coverage output directory
coverageDir = "./coverage"
```

### [​](https://bun.com/docs/test/configuration#skip-test-files-from-coverage) Skip Test Files from Coverage

Exclude files matching test patterns (e.g., `*.test.ts`) from the coverage report:

bunfig.toml

Copy

```
[test]
coverageSkipTestFiles = true  # Exclude test files from coverage reports
```

### [​](https://bun.com/docs/test/configuration#coverage-thresholds) Coverage Thresholds

The coverage threshold can be specified either as a number or as an object with specific thresholds:

bunfig.toml

Copy

```
[test]
# Simple threshold - applies to lines, functions, and statements
coverageThreshold = 0.8

# Detailed thresholds
coverageThreshold = { lines = 0.9, functions = 0.8, statements = 0.85 }
```

Setting any of these enables `fail_on_low_coverage`, causing the test run to fail if coverage is below the threshold.

#### [​](https://bun.com/docs/test/configuration#threshold-examples) Threshold Examples

bunfig.toml

Copy

```
[test]
# Require 90% coverage across the board
coverageThreshold = 0.9

# Different requirements for different metrics
coverageThreshold = {
  lines = 0.85,      # 85% line coverage
  functions = 0.90,  # 90% function coverage
  statements = 0.80  # 80% statement coverage
}
```

### [​](https://bun.com/docs/test/configuration#coverage-path-ignore-patterns) Coverage Path Ignore Patterns

Exclude specific files or file patterns from coverage reports using glob patterns:

bunfig.toml

Copy

```
[test]
# Single pattern
coveragePathIgnorePatterns = "**/*.spec.ts"

# Multiple patterns
coveragePathIgnorePatterns = [
  "**/*.spec.ts",
  "**/*.test.ts",
  "src/utils/**",
  "*.config.js",
  "generated/**",
  "vendor/**"
]
```

Files matching any of these patterns will be excluded from coverage calculation and reporting. See the [coverage documentation](https://bun.com/docs/test/code-coverage) for more details and examples.

#### [​](https://bun.com/docs/test/configuration#common-ignore-patterns) Common Ignore Patterns

bunfig.toml

Copy

```
[test]
coveragePathIgnorePatterns = [
  # Test files
  "**/*.test.ts",
  "**/*.spec.ts",
  "**/*.e2e.ts",

  # Configuration files
  "*.config.js",
  "*.config.ts",
  "webpack.config.*",
  "vite.config.*",

  # Build output
  "dist/**",
  "build/**",
  ".next/**",

  # Generated code
  "generated/**",
  "**/*.generated.ts",

  # Vendor/third-party
  "vendor/**",
  "third-party/**",

  # Utilities that don't need testing
  "src/utils/constants.ts",
  "src/types/**"
]
```

### [​](https://bun.com/docs/test/configuration#sourcemap-handling) Sourcemap Handling

Internally, Bun transpiles every file. That means code coverage must also go through sourcemaps before they can be reported. We expose this as a flag to allow you to opt out of this behavior, but it will be confusing because during the transpilation process, Bun may move code around and change variable names. This option is mostly useful for debugging coverage issues.

bunfig.toml

Copy

```
[test]
coverageIgnoreSourcemaps = true  # Don't use sourcemaps for coverage analysis
```

When using this option, you probably want to stick a `// @bun` comment at the top of the source file to opt out of the
transpilation process.

## [​](https://bun.com/docs/test/configuration#install-settings-inheritance) Install Settings Inheritance

The `bun test` command inherits relevant network and installation configuration (registry, cafile, prefer, exact, etc.) from the `[install]` section of `bunfig.toml`. This is important if tests need to interact with private registries or require specific install behaviors triggered during the test run.

bunfig.toml

Copy

```
[install]
# These settings are inherited by bun test
registry = "https://npm.company.com/"
exact = true
prefer = "offline"

[test]
# Test-specific configuration
coverage = true
timeout = 10000
```

## [​](https://bun.com/docs/test/configuration#environment-variables) Environment Variables

You can also set environment variables in your configuration that affect test behavior:

bunfig.toml

Copy

```
[env]
NODE_ENV = "test"
DATABASE_URL = "postgresql://localhost:5432/test_db"
LOG_LEVEL = "error"

[test]
coverage = true
```

## [​](https://bun.com/docs/test/configuration#complete-configuration-example) Complete Configuration Example

Here’s a comprehensive example showing all available test configuration options:

bunfig.toml

Copy

```
[install]
# Install settings inherited by tests
registry = "https://registry.npmjs.org/"
exact = true

[env]
# Environment variables for tests
NODE_ENV = "test"
DATABASE_URL = "postgresql://localhost:5432/test_db"
API_URL = "http://localhost:3001"
LOG_LEVEL = "error"

[test]
# Test discovery
root = "src"
preload = ["./test-setup.ts", "./global-mocks.ts"]

# Execution settings
timeout = 10000
smol = true

# Coverage configuration
coverage = true
coverageReporter = ["text", "lcov"]
coverageDir = "./coverage"
coverageThreshold = { lines = 0.85, functions = 0.90, statements = 0.80 }
coverageSkipTestFiles = true
coveragePathIgnorePatterns = [
  "**/*.spec.ts",
  "src/utils/**",
  "*.config.js",
  "generated/**"
]

# Advanced coverage settings
coverageIgnoreSourcemaps = false

# Reporter configuration
[test.reporter]
junit = "./reports/junit.xml"
```

## [​](https://bun.com/docs/test/configuration#cli-override-behavior) CLI Override Behavior

Command-line options always override configuration file settings:

bunfig.toml

Copy

```
[test]
timeout = 5000
coverage = false
```

terminal

Copy

```
# These CLI flags override the config file
bun test --timeout 10000 --coverage
# timeout will be 10000ms and coverage will be enabled
```

## [​](https://bun.com/docs/test/configuration#conditional-configuration) Conditional Configuration

You can use different configurations for different environments:

bunfig.toml

Copy

```
[test]
# Default test configuration
coverage = false
timeout = 5000

# Override for CI environment
[test.ci]
coverage = true
coverageThreshold = 0.8
timeout = 30000
```

Then in CI:

terminal

Copy

```
# Use CI-specific settings
bun test --config=ci
```

## [​](https://bun.com/docs/test/configuration#validation-and-troubleshooting) Validation and Troubleshooting

### [​](https://bun.com/docs/test/configuration#invalid-configuration) Invalid Configuration

Bun will warn about invalid configuration options:

bunfig.toml

Copy

```
[test]
invalidOption = true  # This will generate a warning
```

### [​](https://bun.com/docs/test/configuration#common-configuration-issues) Common Configuration Issues

1. **Path Resolution**: Relative paths in config are resolved relative to the config file location
2. **Pattern Matching**: Glob patterns use standard glob syntax
3. **Type Mismatches**: Ensure numeric values are not quoted unless they should be strings

bunfig.toml

Copy

```
[test]
# Correct
timeout = 10000

# Incorrect - will be treated as string
timeout = "10000"
```

### [​](https://bun.com/docs/test/configuration#debugging-configuration) Debugging Configuration

To see what configuration is being used:

terminal

Copy

```
# Show effective configuration
bun test --dry-run

# Verbose output to see configuration loading
bun test --verbose
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test/configuration.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test/configuration)

⌘I