---
url: https://bun.com/docs/test/code-coverage
title: Code coverage - Bun
source_domain: bun.com
---

# Code coverage - Bun

Bun’s test runner now supports built-in code coverage reporting. This makes it easy to see how much of the codebase is covered by tests, and find areas that are not currently well-tested.

## [​](https://bun.com/docs/test/code-coverage#enabling-coverage) Enabling Coverage

`bun:test` supports seeing which lines of code are covered by tests. To use this feature, pass `--coverage` to the CLI. It will print out a coverage report to the console:

terminal

Copy

```
bun test --coverage

-------------|---------|---------|-------------------
File         | % Funcs | % Lines | Uncovered Line #s
-------------|---------|---------|-------------------
All files    |   38.89 |   42.11 |
 index-0.ts  |   33.33 |   36.84 | 10-15,19-24
 index-1.ts  |   33.33 |   36.84 | 10-15,19-24
 index-10.ts |   33.33 |   36.84 | 10-15,19-24
 index-2.ts  |   33.33 |   36.84 | 10-15,19-24
 index-3.ts  |   33.33 |   36.84 | 10-15,19-24
 index-4.ts  |   33.33 |   36.84 | 10-15,19-24
 index-5.ts  |   33.33 |   36.84 | 10-15,19-24
 index-6.ts  |   33.33 |   36.84 | 10-15,19-24
 index-7.ts  |   33.33 |   36.84 | 10-15,19-24
 index-8.ts  |   33.33 |   36.84 | 10-15,19-24
 index-9.ts  |   33.33 |   36.84 | 10-15,19-24
 index.ts    |  100.00 |  100.00 |
-------------|---------|---------|-------------------
```

### [​](https://bun.com/docs/test/code-coverage#enable-by-default) Enable by Default

To always enable coverage reporting by default, add the following line to your `bunfig.toml`:

bunfig.toml

Copy

```
[test]
# Always enable coverage
coverage = true
```

By default coverage reports will include test files and exclude sourcemaps. This is usually what you want, but it can be configured otherwise in `bunfig.toml`.

bunfig.toml

Copy

```
[test]
coverageSkipTestFiles = true  # default false
```

## [​](https://bun.com/docs/test/code-coverage#coverage-thresholds) Coverage Thresholds

It is possible to specify a coverage threshold in `bunfig.toml`. If your test suite does not meet or exceed this threshold, `bun test` will exit with a non-zero exit code to indicate the failure.

### [​](https://bun.com/docs/test/code-coverage#simple-threshold) Simple Threshold

bunfig.toml

Copy

```
[test]
# To require 90% line-level and function-level coverage
coverageThreshold = 0.9
```

### [​](https://bun.com/docs/test/code-coverage#detailed-thresholds) Detailed Thresholds

bunfig.toml

Copy

```
[test]
# To set different thresholds for lines and functions
coverageThreshold = { lines = 0.9, functions = 0.9, statements = 0.9 }
```

Setting any of these thresholds enables `fail_on_low_coverage`, causing the test run to fail if coverage is below the threshold.

## [​](https://bun.com/docs/test/code-coverage#coverage-reporters) Coverage Reporters

By default, coverage reports will be printed to the console.
For persistent code coverage reports in CI environments and for other tools, you can pass a `--coverage-reporter=lcov` CLI option or `coverageReporter` option in `bunfig.toml`.

bunfig.toml

Copy

```
[test]
coverageReporter = ["text", "lcov"]  # default ["text"]
coverageDir = "path/to/somewhere"    # default "coverage"
```

### [​](https://bun.com/docs/test/code-coverage#available-reporters) Available Reporters

| Reporter | Description |
| --- | --- |
| `text` | Prints a text summary of the coverage to the console |
| `lcov` | Save coverage in lcov format |

### [​](https://bun.com/docs/test/code-coverage#lcov-coverage-reporter) LCOV Coverage Reporter

To generate an lcov report, you can use the lcov reporter. This will generate an `lcov.info` file in the coverage directory.

bunfig.toml

Copy

```
[test]
coverageReporter = "lcov"
```

terminal

Copy

```
# Or via CLI
bun test --coverage --coverage-reporter=lcov
```

The LCOV format is widely supported by various tools and services:

* **Code editors**: VS Code extensions can show coverage inline
* **CI/CD services**: GitHub Actions, GitLab CI, CircleCI
* **Coverage services**: Codecov, Coveralls
* **IDEs**: WebStorm, IntelliJ IDEA

#### [​](https://bun.com/docs/test/code-coverage#using-lcov-with-github-actions) Using LCOV with GitHub Actions

.github/workflows/test.yml

Copy

```
name: Test with Coverage
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: oven-sh/setup-bun@v2
      - run: bun install
      - run: bun test --coverage --coverage-reporter=lcov
      - name: Upload coverage to Codecov
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage/lcov.info
```

## [​](https://bun.com/docs/test/code-coverage#excluding-files-from-coverage) Excluding Files from Coverage

### [​](https://bun.com/docs/test/code-coverage#skip-test-files) Skip Test Files

By default, test files themselves are included in coverage reports. You can exclude them with:

bunfig.toml

Copy

```
[test]
coverageSkipTestFiles = true  # default false
```

This will exclude files matching test patterns (e.g., `*.test.ts`, `*.spec.js`) from the coverage report.

### [​](https://bun.com/docs/test/code-coverage#ignore-specific-paths-and-patterns) Ignore Specific Paths and Patterns

You can exclude specific files or file patterns from coverage reports using `coveragePathIgnorePatterns`:

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
  "*.config.js"
]
```

This option accepts glob patterns and works similarly to Jest’s `collectCoverageFrom` ignore patterns. Files matching any of these patterns will be excluded from coverage calculation and reporting in both text and LCOV outputs.

#### [​](https://bun.com/docs/test/code-coverage#common-use-cases) Common Use Cases

bunfig.toml

Copy

```
[test]
coveragePathIgnorePatterns = [
  # Exclude utility files
  "src/utils/**",

  # Exclude configuration files
  "*.config.js",
  "webpack.config.ts",
  "vite.config.ts",

  # Exclude specific test patterns
  "**/*.spec.ts",
  "**/*.e2e.ts",

  # Exclude build artifacts
  "dist/**",
  "build/**",

  # Exclude generated files
  "src/generated/**",
  "**/*.generated.ts",

  # Exclude vendor/third-party code
  "vendor/**",
  "third-party/**"
]
```

## [​](https://bun.com/docs/test/code-coverage#sourcemaps) Sourcemaps

Internally, Bun transpiles all files by default, so Bun automatically generates an internal source map that maps lines of your original source code onto Bun’s internal representation. If for any reason you want to disable this, set `test.coverageIgnoreSourcemaps` to `true`; this will rarely be desirable outside of advanced use cases.

bunfig.toml

Copy

```
[test]
coverageIgnoreSourcemaps = true  # default false
```

When using this option, you probably want to stick a `// @bun` comment at the top of the source file to opt out of the
transpilation process.

## [​](https://bun.com/docs/test/code-coverage#coverage-defaults) Coverage Defaults

By default, coverage reports:

* **Exclude** `node_modules` directories
* **Exclude** files loaded via non-JS/TS loaders (e.g., `.css`, `.txt`) unless a custom JS loader is specified
* **Include** test files themselves (can be disabled with `coverageSkipTestFiles = true`)
* Can exclude additional files with `coveragePathIgnorePatterns`

## [​](https://bun.com/docs/test/code-coverage#advanced-configuration) Advanced Configuration

### [​](https://bun.com/docs/test/code-coverage#custom-coverage-directory) Custom Coverage Directory

bunfig.toml

Copy

```
[test]
coverageDir = "coverage-reports"  # default "coverage"
```

### [​](https://bun.com/docs/test/code-coverage#multiple-reporters) Multiple Reporters

bunfig.toml

Copy

```
[test]
coverageReporter = ["text", "lcov"]
```

### [​](https://bun.com/docs/test/code-coverage#coverage-with-specific-test-patterns) Coverage with Specific Test Patterns

terminal

Copy

```
# Run coverage only on specific test files
bun test --coverage src/components/*.test.ts

# Run coverage with name pattern
bun test --coverage --test-name-pattern="API"
```

## [​](https://bun.com/docs/test/code-coverage#ci/cd-integration) CI/CD Integration

### [​](https://bun.com/docs/test/code-coverage#github-actions-example) GitHub Actions Example

.github/workflows/coverage.yml

Copy

```
name: Coverage Report
on: [push, pull_request]

jobs:
  coverage:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Bun
        uses: oven-sh/setup-bun@v2

      - name: Install dependencies
        run: bun install

      - name: Run tests with coverage
        run: bun test --coverage --coverage-reporter=lcov

      - name: Upload to Codecov
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage/lcov.info
          fail_ci_if_error: true
```

### [​](https://bun.com/docs/test/code-coverage#gitlab-ci-example) GitLab CI Example

.gitlab-ci.yml

Copy

```
test:coverage:
  stage: test
  script:
    - bun install
    - bun test --coverage --coverage-reporter=lcov
  coverage: '/Lines\s*:\s*(\d+.\d+)%/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage/lcov.info
```

## [​](https://bun.com/docs/test/code-coverage#interpreting-coverage-reports) Interpreting Coverage Reports

### [​](https://bun.com/docs/test/code-coverage#text-output-explanation) Text Output Explanation

Copy

```
-------------|---------|---------|-------------------
File         | % Funcs | % Lines | Uncovered Line #s
-------------|---------|---------|-------------------
All files    |   85.71 |   90.48 |
 src/        |   85.71 |   90.48 |
  utils.ts   |  100.00 |  100.00 |
  api.ts     |   75.00 |   85.71 | 15-18,25
  main.ts    |   80.00 |   88.89 | 42,50-52
-------------|---------|---------|-------------------
```

* **% Funcs**: Percentage of functions that were called during tests
* **% Lines**: Percentage of executable lines that were run during tests
* **Uncovered Line #s**: Specific line numbers that were not executed

### [​](https://bun.com/docs/test/code-coverage#what-to-aim-for) What to Aim For

* **80%+ overall coverage**: Generally considered good
* **90%+ critical paths**: Important business logic should be well-tested
* **100% utility functions**: Pure functions and utilities are easy to test completely
* **Lower coverage for UI components**: Often acceptable as they may require integration tests

## [​](https://bun.com/docs/test/code-coverage#best-practices) Best Practices

### [​](https://bun.com/docs/test/code-coverage#focus-on-quality,-not-just-quantity) Focus on Quality, Not Just Quantity

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// Good: Test actual functionality
test("calculateTax should handle different tax rates", () => {
  expect(calculateTax(100, 0.08)).toBe(8);
  expect(calculateTax(100, 0.1)).toBe(10);
  expect(calculateTax(0, 0.08)).toBe(0);
});

// Avoid: Just hitting lines for coverage
test("calculateTax exists", () => {
  calculateTax(100, 0.08); // No assertions!
});
```

### [​](https://bun.com/docs/test/code-coverage#test-edge-cases) Test Edge Cases

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
test("user input validation", () => {
  // Test normal case
  expect(validateEmail("[email protected]")).toBe(true);

  // Test edge cases that improve coverage meaningfully
  expect(validateEmail("")).toBe(false);
  expect(validateEmail("invalid")).toBe(false);
  expect(validateEmail(null)).toBe(false);
});
```

### [​](https://bun.com/docs/test/code-coverage#use-coverage-to-find-missing-tests) Use Coverage to Find Missing Tests

terminal

Copy

```
# Run coverage to identify untested code
bun test --coverage

# Look at specific files that need attention
bun test --coverage src/critical-module.ts
```

### [​](https://bun.com/docs/test/code-coverage#combine-with-other-quality-metrics) Combine with Other Quality Metrics

Coverage is just one metric. Also consider:

* **Code review quality**
* **Integration test coverage**
* **Error handling tests**
* **Performance tests**
* **Type safety**

## [​](https://bun.com/docs/test/code-coverage#troubleshooting) Troubleshooting

### [​](https://bun.com/docs/test/code-coverage#coverage-not-showing-for-some-files) Coverage Not Showing for Some Files

If files aren’t appearing in coverage reports, they might not be imported by your tests. Coverage only tracks files that are actually loaded.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// Make sure to import the modules you want to test
import { myFunction } from "../src/my-module";

test("my function works", () => {
  expect(myFunction()).toBeDefined();
});
```

### [​](https://bun.com/docs/test/code-coverage#false-coverage-reports) False Coverage Reports

If you see coverage reports that don’t match your expectations:

1. Check if source maps are working correctly
2. Verify file patterns in `coveragePathIgnorePatterns`
3. Ensure test files are actually importing the code to test

### [​](https://bun.com/docs/test/code-coverage#performance-issues-with-large-codebases) Performance Issues with Large Codebases

For large projects, coverage collection can slow down tests:

bunfig.toml

Copy

```
[test]
# Exclude large directories you don't need coverage for
coveragePathIgnorePatterns = [
  "node_modules/**",
  "vendor/**",
  "generated/**"
]
```

Consider running coverage only on CI or specific branches rather than every test run during development.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test/code-coverage.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test/code-coverage)

⌘I