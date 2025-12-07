---
url: https://bun.com/reference/node/test/reporters
title: Node.js node:test/reporters module | API Reference | Bun
source_domain: bun.com
---

# Node.js node:test/reporters module | API Reference | Bun

Node.js module

# [node:test/reporters](https://bun.com/reference/node/test/reporters)

The `'node:test/reporters'` module provides built-in reporter formats for `node:test`, such as `tap`, `json`, and `baseline`. Reporters format test results for human or machine consumption.

Use reporters to integrate with CI systems, test dashboards, or custom logging pipelines.

* const [lcov](https://bun.com/reference/node/test/reporters/lcov): ReporterConstructorWrapper<typeof LcovReporter>

  The `lcov` reporter outputs test coverage when used with the [`--experimental-test-coverage`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--experimental-test-coverage) flag.
* const [spec](https://bun.com/reference/node/test/reporters/spec): ReporterConstructorWrapper<typeof SpecReporter>

  The `spec` reporter outputs the test results in a human-readable format.
* function [dot](https://bun.com/reference/node/test/reporters/dot)(

  source: TestEventGenerator

  ): AsyncGenerator<'
  ' | '.' | 'X', void>;

  The `dot` reporter outputs the test results in a compact format, where each passing test is represented by a `.`, and each failing test is represented by a `X`.
* function [junit](https://bun.com/reference/node/test/reporters/junit)(

  source: TestEventGenerator

  ): AsyncGenerator<string, void>;

  The `junit` reporter outputs test results in a jUnit XML format.
* function [tap](https://bun.com/reference/node/test/reporters/tap)(

  source: TestEventGenerator

  ): AsyncGenerator<string, void>;

  The `tap` reporter outputs the test results in the [TAP](https://testanything.org/) format.

## Type definitions

* type [TestEvent](https://bun.com/reference/node/test/reporters/TestEvent) = { data: [EventData.TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage); type: 'test:coverage' } | { data: [EventData.TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete); type: 'test:complete' } | { data: [EventData.TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue); type: 'test:dequeue' } | { data: [EventData.TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic); type: 'test:diagnostic' } | { data: [EventData.TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue); type: 'test:enqueue' } | { data: [EventData.TestFail](https://bun.com/reference/node/test/default/EventData/TestFail); type: 'test:fail' } | { data: [EventData.TestPass](https://bun.com/reference/node/test/default/EventData/TestPass); type: 'test:pass' } | { data: [EventData.TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan); type: 'test:plan' } | { data: [EventData.TestStart](https://bun.com/reference/node/test/default/EventData/TestStart); type: 'test:start' } | { data: [EventData.TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr); type: 'test:stderr' } | { data: [EventData.TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout); type: 'test:stdout' } | { data: [EventData.TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary); type: 'test:summary' } | { data: undefined; type: 'test:watch:drained' } | { data: undefined; type: 'test:watch:restarted' }