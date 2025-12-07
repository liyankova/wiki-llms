---
url: https://bun.com/reference/node/test
title: Node.js node:test module | API Reference | Bun
source_domain: bun.com
---

# Node.js node:test module | API Reference | Bun

Node.js module

# [node:test](https://bun.com/reference/node/test)

The `'node:test'` module is Node.js's built-in test runner that provides a zero-dependency testing framework. It supports `test()` functions, lifecycle hooks (`before`, `after`), and assertions.

Tests run in isolation with concurrent support, snapshot testing, and detailed reporting, making it a lightweight alternative to external test frameworks.

Works in Bun

Basic test runner structure exists but lacks key features like mocking, snapshot testing, and timer manipulation/mocking. Use `bun:test` for a more complete testing solution.

* [export default function test](https://bun.com/reference/node/test/default)(

  name?: string,

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param name

  The name of the test, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  [export default function test](https://bun.com/reference/node/test/default)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param name

  The name of the test, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param options

  Configuration options for the test.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  [export default function test](https://bun.com/reference/node/test/default)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param options

  Configuration options for the test.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  [export default function test](https://bun.com/reference/node/test/default)(

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  ### [export default namespace test](https://bun.com/reference/node/test/default)

  + ### namespace [assert](https://bun.com/reference/node/test/default/assert)

    An object whose methods are used to configure available assertions on the `TestContext` objects in the current process. The methods from `node:assert` and snapshot testing functions are available by default.

    It is possible to apply the same configuration to all files by placing common configuration code in a module preloaded with `--require` or `--import`.

    - function [register](https://bun.com/reference/node/test/default/assert/register)(

      name: string,

      fn: (this: [TestContext](https://bun.com/reference/node/test/default/TestContext), ...args: any[]) => void

      ): void;

      Defines a new assertion function with the provided name and function. If an assertion already exists with the same name, it is overwritten.
  + ### namespace [EventData](https://bun.com/reference/node/test/default/EventData)

    - ### interface [Error](https://bun.com/reference/node/test/default/EventData/Error)

      * [cause](https://bun.com/reference/node/test/default/EventData/Error/cause): [Error](https://bun.com/reference/globals/Error)

        The cause of the error.
      * [message](https://bun.com/reference/node/test/default/EventData/Error/message): string
      * [name](https://bun.com/reference/node/test/default/EventData/Error/name): string
      * [stack](https://bun.com/reference/node/test/default/EventData/Error/stack)?: string
    - ### interface [LocationInfo](https://bun.com/reference/node/test/default/EventData/LocationInfo)

      * [column](https://bun.com/reference/node/test/default/EventData/LocationInfo/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [file](https://bun.com/reference/node/test/default/EventData/LocationInfo/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/LocationInfo/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - ### interface [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)

      * [column](https://bun.com/reference/node/test/default/EventData/TestComplete/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [details](https://bun.com/reference/node/test/default/EventData/TestComplete/details): { duration\_ms: number; error: [Error](https://bun.com/reference/node/test/default/EventData/Error); passed: boolean; type: 'suite' | 'test' }

        Additional execution metadata.
      * [file](https://bun.com/reference/node/test/default/EventData/TestComplete/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/TestComplete/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [name](https://bun.com/reference/node/test/default/EventData/TestComplete/name): string

        The test name.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestComplete/nesting): number

        The nesting level of the test.
      * [skip](https://bun.com/reference/node/test/default/EventData/TestComplete/skip)?: string | boolean

        Present if `context.skip` is called.
      * [testNumber](https://bun.com/reference/node/test/default/EventData/TestComplete/testNumber): number

        The ordinal number of the test.
      * [todo](https://bun.com/reference/node/test/default/EventData/TestComplete/todo)?: string | boolean

        Present if `context.todo` is called.
    - ### interface [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)

      * [nesting](https://bun.com/reference/node/test/default/EventData/TestCoverage/nesting): number

        The nesting level of the test.
      * [summary](https://bun.com/reference/node/test/default/EventData/TestCoverage/summary): { files: { branches: { count: number; line: number }[]; coveredBranchCount: number; coveredBranchPercent: number; coveredFunctionCount: number; coveredFunctionPercent: number; coveredLineCount: number; coveredLinePercent: number; functions: { count: number; line: number; name: string }[]; lines: { count: number; line: number }[]; path: string; totalBranchCount: number; totalFunctionCount: number; totalLineCount: number }[]; thresholds: { branch: number; function: number; line: number }; totals: { coveredBranchCount: number; coveredBranchPercent: number; coveredFunctionCount: number; coveredFunctionPercent: number; coveredLineCount: number; coveredLinePercent: number; totalBranchCount: number; totalFunctionCount: number; totalLineCount: number }; workingDirectory: string }

        An object containing the coverage report.
    - ### interface [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)

      * [column](https://bun.com/reference/node/test/default/EventData/TestDequeue/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [file](https://bun.com/reference/node/test/default/EventData/TestDequeue/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/TestDequeue/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [name](https://bun.com/reference/node/test/default/EventData/TestDequeue/name): string

        The test name.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestDequeue/nesting): number

        The nesting level of the test.
      * [type](https://bun.com/reference/node/test/default/EventData/TestDequeue/type): 'suite' | 'test'

        The test type. Either `'suite'` or `'test'`.
    - ### interface [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)

      * [column](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [file](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [level](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/level): 'error' | 'info' | 'warn'

        The severity level of the diagnostic message. Possible values are:

        + `'info'`: Informational messages.
        + `'warn'`: Warnings.
        + `'error'`: Errors.
      * [line](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [message](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/message): string

        The diagnostic message.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/nesting): number

        The nesting level of the test.
    - ### interface [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)

      * [column](https://bun.com/reference/node/test/default/EventData/TestEnqueue/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [file](https://bun.com/reference/node/test/default/EventData/TestEnqueue/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/TestEnqueue/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [name](https://bun.com/reference/node/test/default/EventData/TestEnqueue/name): string

        The test name.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestEnqueue/nesting): number

        The nesting level of the test.
      * [type](https://bun.com/reference/node/test/default/EventData/TestEnqueue/type): 'suite' | 'test'

        The test type. Either `'suite'` or `'test'`.
    - ### interface [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)

      * [column](https://bun.com/reference/node/test/default/EventData/TestFail/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [details](https://bun.com/reference/node/test/default/EventData/TestFail/details): { attempt: number; duration\_ms: number; error: [Error](https://bun.com/reference/node/test/default/EventData/Error); type: 'suite' | 'test' }

        Additional execution metadata.
      * [file](https://bun.com/reference/node/test/default/EventData/TestFail/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/TestFail/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [name](https://bun.com/reference/node/test/default/EventData/TestFail/name): string

        The test name.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestFail/nesting): number

        The nesting level of the test.
      * [skip](https://bun.com/reference/node/test/default/EventData/TestFail/skip)?: string | boolean

        Present if `context.skip` is called.
      * [testNumber](https://bun.com/reference/node/test/default/EventData/TestFail/testNumber): number

        The ordinal number of the test.
      * [todo](https://bun.com/reference/node/test/default/EventData/TestFail/todo)?: string | boolean

        Present if `context.todo` is called.
    - ### interface [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)

      * [column](https://bun.com/reference/node/test/default/EventData/TestPass/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [details](https://bun.com/reference/node/test/default/EventData/TestPass/details): { attempt: number; duration\_ms: number; passed\_on\_attempt: number; type: 'suite' | 'test' }

        Additional execution metadata.
      * [file](https://bun.com/reference/node/test/default/EventData/TestPass/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/TestPass/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [name](https://bun.com/reference/node/test/default/EventData/TestPass/name): string

        The test name.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestPass/nesting): number

        The nesting level of the test.
      * [skip](https://bun.com/reference/node/test/default/EventData/TestPass/skip)?: string | boolean

        Present if `context.skip` is called.
      * [testNumber](https://bun.com/reference/node/test/default/EventData/TestPass/testNumber): number

        The ordinal number of the test.
      * [todo](https://bun.com/reference/node/test/default/EventData/TestPass/todo)?: string | boolean

        Present if `context.todo` is called.
    - ### interface [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)

      * [column](https://bun.com/reference/node/test/default/EventData/TestPlan/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [count](https://bun.com/reference/node/test/default/EventData/TestPlan/count): number

        The number of subtests that have ran.
      * [file](https://bun.com/reference/node/test/default/EventData/TestPlan/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/TestPlan/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestPlan/nesting): number

        The nesting level of the test.
    - ### interface [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)

      * [column](https://bun.com/reference/node/test/default/EventData/TestStart/column)?: number

        The column number where the test is defined, or `undefined` if the test was run through the REPL.
      * [file](https://bun.com/reference/node/test/default/EventData/TestStart/file)?: string

        The path of the test file, `undefined` if test was run through the REPL.
      * [line](https://bun.com/reference/node/test/default/EventData/TestStart/line)?: number

        The line number where the test is defined, or `undefined` if the test was run through the REPL.
      * [name](https://bun.com/reference/node/test/default/EventData/TestStart/name): string

        The test name.
      * [nesting](https://bun.com/reference/node/test/default/EventData/TestStart/nesting): number

        The nesting level of the test.
    - ### interface [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)

      * [file](https://bun.com/reference/node/test/default/EventData/TestStderr/file): string

        The path of the test file.
      * [message](https://bun.com/reference/node/test/default/EventData/TestStderr/message): string

        The message written to `stderr`.
    - ### interface [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)

      * [file](https://bun.com/reference/node/test/default/EventData/TestStdout/file): string

        The path of the test file.
      * [message](https://bun.com/reference/node/test/default/EventData/TestStdout/message): string

        The message written to `stdout`.
    - ### interface [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)

      * [counts](https://bun.com/reference/node/test/default/EventData/TestSummary/counts): { cancelled: number; passed: number; skipped: number; suites: number; tests: number; todo: number; topLevel: number }

        An object containing the counts of various test results.
      * [duration\_ms](https://bun.com/reference/node/test/default/EventData/TestSummary/duration_ms): number

        The duration of the test run in milliseconds.
      * [file](https://bun.com/reference/node/test/default/EventData/TestSummary/file): undefined | string

        The path of the test file that generated the summary. If the summary corresponds to multiple files, this value is `undefined`.
      * [success](https://bun.com/reference/node/test/default/EventData/TestSummary/success): boolean

        Indicates whether or not the test run is considered successful or not. If any error condition occurs, such as a failing test or unmet coverage threshold, this value will be set to `false`.
  + ### namespace [snapshot](https://bun.com/reference/node/test/default/snapshot)

    - function [setDefaultSnapshotSerializers](https://bun.com/reference/node/test/default/snapshot/setDefaultSnapshotSerializers)(

      serializers: readonly (value: any) => any[]

      ): void;

      This function is used to customize the default serialization mechanism used by the test runner.

      By default, the test runner performs serialization by calling `JSON.stringify(value, null, 2)` on the provided value. `JSON.stringify()` does have limitations regarding circular structures and supported data types. If a more robust serialization mechanism is required, this function should be used to specify a list of custom serializers.

      Serializers are called in order, with the output of the previous serializer passed as input to the next. The final result must be a string value.

      @param serializers

      An array of synchronous functions used as the default serializers for snapshot tests.
    - function [setResolveSnapshotPath](https://bun.com/reference/node/test/default/snapshot/setResolveSnapshotPath)(

      fn: (path: undefined | string) => string

      ): void;

      This function is used to set a custom resolver for the location of the snapshot file used for snapshot testing. By default, the snapshot filename is the same as the entry point filename with `.snapshot` appended.

      @param fn

      A function used to compute the location of the snapshot file. The function receives the path of the test file as its only argument. If the test is not associated with a file (for example in the REPL), the input is undefined. `fn()` must return a string specifying the location of the snapshot file.
  + function [suite](https://bun.com/reference/node/test/default/suite)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param name

    The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

    @param options

    Configuration options for the suite. This supports the same options as test.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    function [suite](https://bun.com/reference/node/test/default/suite)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param name

    The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    function [suite](https://bun.com/reference/node/test/default/suite)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param options

    Configuration options for the suite. This supports the same options as test.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    function [suite](https://bun.com/reference/node/test/default/suite)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    ### namespace [suite](https://bun.com/reference/node/test/default/suite)

    - function [only](https://bun.com/reference/node/test/default/suite/only)(

      name?: string,

      options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

      function [only](https://bun.com/reference/node/test/default/suite/only)(

      name?: string,

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

      function [only](https://bun.com/reference/node/test/default/suite/only)(

      options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

      function [only](https://bun.com/reference/node/test/default/suite/only)(

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.
    - function [skip](https://bun.com/reference/node/test/default/suite/skip)(

      name?: string,

      options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

      function [skip](https://bun.com/reference/node/test/default/suite/skip)(

      name?: string,

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

      function [skip](https://bun.com/reference/node/test/default/suite/skip)(

      options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

      function [skip](https://bun.com/reference/node/test/default/suite/skip)(

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.
    - function [todo](https://bun.com/reference/node/test/default/suite/todo)(

      name?: string,

      options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

      function [todo](https://bun.com/reference/node/test/default/suite/todo)(

      name?: string,

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

      function [todo](https://bun.com/reference/node/test/default/suite/todo)(

      options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

      function [todo](https://bun.com/reference/node/test/default/suite/todo)(

      fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

      ): Promise<void>;

      Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.
  + ### class [MockPropertyContext](https://bun.com/reference/node/test/default/MockPropertyContext)<PropertyType = any>

    - readonly [accesses](https://bun.com/reference/node/test/default/MockPropertyContext/accesses): { stack: [Error](https://bun.com/reference/globals/Error); type: 'get' | 'set'; value: PropertyType }[]

      A getter that returns a copy of the internal array used to track accesses (get/set) to the mocked property. Each entry in the array is an object with the following properties:
    - [accessCount](https://bun.com/reference/node/test/default/MockPropertyContext/accessCount)(): number;

      This function returns the number of times that the property was accessed. This function is more efficient than checking `ctx.accesses.length` because `ctx.accesses` is a getter that creates a copy of the internal access tracking array.

      @returns

      The number of times that the property was accessed (read or written).
    - [mockImplementation](https://bun.com/reference/node/test/default/MockPropertyContext/mockImplementation)(

      value: PropertyType

      ): void;

      This function is used to change the value returned by the mocked property getter.

      @param value

      The new value to be set as the mocked property value.
    - [mockImplementationOnce](https://bun.com/reference/node/test/default/MockPropertyContext/mockImplementationOnce)(

      value: PropertyType,

      onAccess?: number

      ): void;

      This function is used to change the behavior of an existing mock for a single invocation. Once invocation `onAccess` has occurred, the mock will revert to whatever behavior it would have used had `mockImplementationOnce()` not been called.

      The following example creates a mock function using `t.mock.property()`, calls the mock property, changes the mock implementation to a different value for the next invocation, and then resumes its previous behavior.

      ```
      test('changes a mock behavior once', (t) => {
        const obj = { foo: 1 };

        const prop = t.mock.property(obj, 'foo', 5);

        assert.strictEqual(obj.foo, 5);
        prop.mock.mockImplementationOnce(25);
        assert.strictEqual(obj.foo, 25);
        assert.strictEqual(obj.foo, 5);
      });
      ```

      @param value

      The value to be used as the mock's implementation for the invocation number specified by `onAccess`.

      @param onAccess

      The invocation number that will use `value`. If the specified invocation has already occurred then an exception is thrown. **Default:** The number of the next invocation.
    - [resetAccesses](https://bun.com/reference/node/test/default/MockPropertyContext/resetAccesses)(): void;

      Resets the access history of the mocked property.
    - [restore](https://bun.com/reference/node/test/default/MockPropertyContext/restore)(): void;

      Resets the implementation of the mock property to its original behavior. The mock can still be used after calling this function.
  + ### interface [AssertSnapshotOptions](https://bun.com/reference/node/test/default/AssertSnapshotOptions)

    - [serializers](https://bun.com/reference/node/test/default/AssertSnapshotOptions/serializers)?: readonly (value: any) => any[]

      An array of synchronous functions used to serialize `value` into a string. `value` is passed as the only argument to the first serializer function. The return value of each serializer is passed as input to the next serializer. Once all serializers have run, the resulting value is coerced to a string.

      If no serializers are provided, the test runner's default serializers are used.
  + ### interface [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    Configuration options for hooks.

    - [signal](https://bun.com/reference/node/test/default/HookOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      Allows aborting an in-progress hook.
    - [timeout](https://bun.com/reference/node/test/default/HookOptions/timeout)?: number

      A number of milliseconds the hook will fail after. If unspecified, subtests inherit this value from their parent.
  + ### interface [MockFunctionCall](https://bun.com/reference/node/test/default/MockFunctionCall)<F extends Function, ReturnType = F extends (...args: any) => infer T ? T : F extends new (...args: any) => infer T ? T : unknown, Args = F extends (...args: infer Y) => any ? Y : F extends new (...args: infer Y) => any ? Y : unknown[]>

    - [arguments](https://bun.com/reference/node/test/default/MockFunctionCall/arguments): Args

      An array of the arguments passed to the mock function.
    - [error](https://bun.com/reference/node/test/default/MockFunctionCall/error): unknown

      If the mocked function threw then this property contains the thrown value.
    - [result](https://bun.com/reference/node/test/default/MockFunctionCall/result): undefined | ReturnType

      The value returned by the mocked function.

      If the mocked function threw, it will be `undefined`.
    - [stack](https://bun.com/reference/node/test/default/MockFunctionCall/stack): [Error](https://bun.com/reference/globals/Error)

      An `Error` object whose stack can be used to determine the callsite of the mocked function invocation.
    - [target](https://bun.com/reference/node/test/default/MockFunctionCall/target): F extends new (...args: any) => any ? F<F> : undefined

      If the mocked function is a constructor, this field contains the class being constructed. Otherwise this will be `undefined`.
    - [this](https://bun.com/reference/node/test/default/MockFunctionCall/this): unknown

      The mocked function's `this` value.
  + ### interface [MockFunctionContext](https://bun.com/reference/node/test/default/MockFunctionContext)<F extends Function>

    The `MockFunctionContext` class is used to inspect or manipulate the behavior of mocks created via the `MockTracker` APIs.

    - readonly [calls](https://bun.com/reference/node/test/default/MockFunctionContext/calls): [MockFunctionCall](https://bun.com/reference/node/test/default/MockFunctionCall)<F, F extends (...args: any) => T ? T : F extends new (...args: any) => T ? T : unknown, F extends (...args: Y) => any ? Y : F extends new (...args: Y) => any ? Y : unknown[]>[]

      A getter that returns a copy of the internal array used to track calls to the mock. Each entry in the array is an object with the following properties.
    - [callCount](https://bun.com/reference/node/test/default/MockFunctionContext/callCount)(): number;

      This function returns the number of times that this mock has been invoked. This function is more efficient than checking `ctx.calls.length` because `ctx.calls` is a getter that creates a copy of the internal call tracking array.

      @returns

      The number of times that this mock has been invoked.
    - [mockImplementation](https://bun.com/reference/node/test/default/MockFunctionContext/mockImplementation)(

      implementation: F

      ): void;

      This function is used to change the behavior of an existing mock.

      The following example creates a mock function using `t.mock.fn()`, calls the mock function, and then changes the mock implementation to a different function.

      ```
      test('changes a mock behavior', (t) => {
        let cnt = 0;

        function addOne() {
          cnt++;
          return cnt;
        }

        function addTwo() {
          cnt += 2;
          return cnt;
        }

        const fn = t.mock.fn(addOne);

        assert.strictEqual(fn(), 1);
        fn.mock.mockImplementation(addTwo);
        assert.strictEqual(fn(), 3);
        assert.strictEqual(fn(), 5);
      });
      ```

      @param implementation

      The function to be used as the mock's new implementation.
    - [mockImplementationOnce](https://bun.com/reference/node/test/default/MockFunctionContext/mockImplementationOnce)(

      implementation: F,

      onCall?: number

      ): void;

      This function is used to change the behavior of an existing mock for a single invocation. Once invocation `onCall` has occurred, the mock will revert to whatever behavior it would have used had `mockImplementationOnce()` not been called.

      The following example creates a mock function using `t.mock.fn()`, calls the mock function, changes the mock implementation to a different function for the next invocation, and then resumes its previous behavior.

      ```
      test('changes a mock behavior once', (t) => {
        let cnt = 0;

        function addOne() {
          cnt++;
          return cnt;
        }

        function addTwo() {
          cnt += 2;
          return cnt;
        }

        const fn = t.mock.fn(addOne);

        assert.strictEqual(fn(), 1);
        fn.mock.mockImplementationOnce(addTwo);
        assert.strictEqual(fn(), 3);
        assert.strictEqual(fn(), 4);
      });
      ```

      @param implementation

      The function to be used as the mock's implementation for the invocation number specified by `onCall`.

      @param onCall

      The invocation number that will use `implementation`. If the specified invocation has already occurred then an exception is thrown.
    - [resetCalls](https://bun.com/reference/node/test/default/MockFunctionContext/resetCalls)(): void;

      Resets the call history of the mock function.
    - [restore](https://bun.com/reference/node/test/default/MockFunctionContext/restore)(): void;

      Resets the implementation of the mock function to its original behavior. The mock can still be used after calling this function.
  + ### interface [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    - [times](https://bun.com/reference/node/test/default/MockFunctionOptions/times)?: number

      The number of times that the mock will use the behavior of `implementation`. Once the mock function has been called `times` times, it will automatically restore the behavior of `original`. This value must be an integer greater than zero.
  + ### interface [MockMethodOptions](https://bun.com/reference/node/test/default/MockMethodOptions)

    - [getter](https://bun.com/reference/node/test/default/MockMethodOptions/getter)?: boolean

      If `true`, `object[methodName]` is treated as a getter. This option cannot be used with the `setter` option.
    - [setter](https://bun.com/reference/node/test/default/MockMethodOptions/setter)?: boolean

      If `true`, `object[methodName]` is treated as a setter. This option cannot be used with the `getter` option.
    - [times](https://bun.com/reference/node/test/default/MockMethodOptions/times)?: number

      The number of times that the mock will use the behavior of `implementation`. Once the mock function has been called `times` times, it will automatically restore the behavior of `original`. This value must be an integer greater than zero.
  + ### interface [MockModuleContext](https://bun.com/reference/node/test/default/MockModuleContext)

    - [restore](https://bun.com/reference/node/test/default/MockModuleContext/restore)(): void;

      Resets the implementation of the mock module.
  + ### interface [MockModuleOptions](https://bun.com/reference/node/test/default/MockModuleOptions)

    - [cache](https://bun.com/reference/node/test/default/MockModuleOptions/cache)?: boolean

      If false, each call to `require()` or `import()` generates a new mock module. If true, subsequent calls will return the same module mock, and the mock module is inserted into the CommonJS cache.
    - [defaultExport](https://bun.com/reference/node/test/default/MockModuleOptions/defaultExport)?: any

      The value to use as the mocked module's default export.

      If this value is not provided, ESM mocks do not include a default export. If the mock is a CommonJS or builtin module, this setting is used as the value of `module.exports`. If this value is not provided, CJS and builtin mocks use an empty object as the value of `module.exports`.
    - [namedExports](https://bun.com/reference/node/test/default/MockModuleOptions/namedExports)?: object

      An object whose keys and values are used to create the named exports of the mock module.

      If the mock is a CommonJS or builtin module, these values are copied onto `module.exports`. Therefore, if a mock is created with both named exports and a non-object default export, the mock will throw an exception when used as a CJS or builtin module.
  + ### interface [MockTimers](https://bun.com/reference/node/test/default/MockTimers)

    Mocking timers is a technique commonly used in software testing to simulate and control the behavior of timers, such as `setInterval` and `setTimeout`, without actually waiting for the specified time intervals.

    The MockTimers API also allows for mocking of the `Date` constructor and `setImmediate`/`clearImmediate` functions.

    The `MockTracker` provides a top-level `timers` export which is a `MockTimers` instance.

    - [[Symbol.dispose]](https://bun.com/reference/node/test/default/MockTimers/[dispose])(): void;

      Calls ().
    - [enable](https://bun.com/reference/node/test/default/MockTimers/enable)(

      options?: [MockTimersOptions](https://bun.com/reference/node/test/default/MockTimersOptions)

      ): void;

      Enables timer mocking for the specified timers.

      **Note:** When you enable mocking for a specific timer, its associated clear function will also be implicitly mocked.

      **Note:** Mocking `Date` will affect the behavior of the mocked timers as they use the same internal clock.

      Example usage without setting initial time:

      ```
      import { mock } from 'node:test';
      mock.timers.enable({ apis: ['setInterval', 'Date'], now: 1234 });
      ```

      The above example enables mocking for the `Date` constructor, `setInterval` timer and implicitly mocks the `clearInterval` function. Only the `Date` constructor from `globalThis`, `setInterval` and `clearInterval` functions from `node:timers`, `node:timers/promises`, and `globalThis` will be mocked.

      Example usage with initial time set

      ```
      import { mock } from 'node:test';
      mock.timers.enable({ apis: ['Date'], now: 1000 });
      ```

      Example usage with initial Date object as time set

      ```
      import { mock } from 'node:test';
      mock.timers.enable({ apis: ['Date'], now: new Date() });
      ```

      Alternatively, if you call `mock.timers.enable()` without any parameters:

      All timers (`'setInterval'`, `'clearInterval'`, `'Date'`, `'setImmediate'`, `'clearImmediate'`, `'setTimeout'`, and `'clearTimeout'`) will be mocked.

      The `setInterval`, `clearInterval`, `setTimeout`, and `clearTimeout` functions from `node:timers`, `node:timers/promises`, and `globalThis` will be mocked. The `Date` constructor from `globalThis` will be mocked.

      If there is no initial epoch set, the initial date will be based on 0 in the Unix epoch. This is `January 1st, 1970, 00:00:00 UTC`. You can set an initial date by passing a now property to the `.enable()` method. This value will be used as the initial date for the mocked Date object. It can either be a positive integer, or another Date object.
    - [reset](https://bun.com/reference/node/test/default/MockTimers/reset)(): void;

      This function restores the default behavior of all mocks that were previously created by this `MockTimers` instance and disassociates the mocks from the `MockTracker` instance.

      **Note:** After each test completes, this function is called on the test context's `MockTracker`.

      ```
      import { mock } from 'node:test';
      mock.timers.reset();
      ```
    - [runAll](https://bun.com/reference/node/test/default/MockTimers/runAll)(): void;

      Triggers all pending mocked timers immediately. If the `Date` object is also mocked, it will also advance the `Date` object to the furthest timer's time.

      The example below triggers all pending timers immediately, causing them to execute without any delay.

      ```
      import assert from 'node:assert';
      import { test } from 'node:test';

      test('runAll functions following the given order', (context) => {
        context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
        const results = [];
        setTimeout(() => results.push(1), 9999);

        // Notice that if both timers have the same timeout,
        // the order of execution is guaranteed
        setTimeout(() => results.push(3), 8888);
        setTimeout(() => results.push(2), 8888);

        assert.deepStrictEqual(results, []);

        context.mock.timers.runAll();
        assert.deepStrictEqual(results, [3, 2, 1]);
        // The Date object is also advanced to the furthest timer's time
        assert.strictEqual(Date.now(), 9999);
      });
      ```

      **Note:** The `runAll()` function is specifically designed for triggering timers in the context of timer mocking. It does not have any effect on real-time system clocks or actual timers outside of the mocking environment.
    - [setTime](https://bun.com/reference/node/test/default/MockTimers/setTime)(

      time: number

      ): void;

      You can use the `.setTime()` method to manually move the mocked date to another time. This method only accepts a positive integer. Note: This method will execute any mocked timers that are in the past from the new time. In the below example we are setting a new time for the mocked date.

      ```
      import assert from 'node:assert';
      import { test } from 'node:test';
      test('sets the time of a date object', (context) => {
        // Optionally choose what to mock
        context.mock.timers.enable({ apis: ['Date'], now: 100 });
        assert.strictEqual(Date.now(), 100);
        // Advance in time will also advance the date
        context.mock.timers.setTime(1000);
        context.mock.timers.tick(200);
        assert.strictEqual(Date.now(), 1200);
      });
      ```
    - [tick](https://bun.com/reference/node/test/default/MockTimers/tick)(

      milliseconds: number

      ): void;

      Advances time for all mocked timers.

      **Note:** This diverges from how `setTimeout` in Node.js behaves and accepts only positive numbers. In Node.js, `setTimeout` with negative numbers is only supported for web compatibility reasons.

      The following example mocks a `setTimeout` function and by using `.tick` advances in time triggering all pending timers.

      ```
      import assert from 'node:assert';
      import { test } from 'node:test';

      test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
        const fn = context.mock.fn();

        context.mock.timers.enable({ apis: ['setTimeout'] });

        setTimeout(fn, 9999);

        assert.strictEqual(fn.mock.callCount(), 0);

        // Advance in time
        context.mock.timers.tick(9999);

        assert.strictEqual(fn.mock.callCount(), 1);
      });
      ```

      Alternativelly, the `.tick` function can be called many times

      ```
      import assert from 'node:assert';
      import { test } from 'node:test';

      test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
        const fn = context.mock.fn();
        context.mock.timers.enable({ apis: ['setTimeout'] });
        const nineSecs = 9000;
        setTimeout(fn, nineSecs);

        const twoSeconds = 3000;
        context.mock.timers.tick(twoSeconds);
        context.mock.timers.tick(twoSeconds);
        context.mock.timers.tick(twoSeconds);

        assert.strictEqual(fn.mock.callCount(), 1);
      });
      ```

      Advancing time using `.tick` will also advance the time for any `Date` object created after the mock was enabled (if `Date` was also set to be mocked).

      ```
      import assert from 'node:assert';
      import { test } from 'node:test';

      test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
        const fn = context.mock.fn();

        context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
        setTimeout(fn, 9999);

        assert.strictEqual(fn.mock.callCount(), 0);
        assert.strictEqual(Date.now(), 0);

        // Advance in time
        context.mock.timers.tick(9999);
        assert.strictEqual(fn.mock.callCount(), 1);
        assert.strictEqual(Date.now(), 9999);
      });
      ```
  + ### interface [MockTimersOptions](https://bun.com/reference/node/test/default/MockTimersOptions)

    - [apis](https://bun.com/reference/node/test/default/MockTimersOptions/apis): readonly 'Date' | 'setInterval' | 'setTimeout' | 'setImmediate'[]
    - [now](https://bun.com/reference/node/test/default/MockTimersOptions/now)?: number | Date
  + ### interface [MockTracker](https://bun.com/reference/node/test/default/MockTracker)

    The `MockTracker` class is used to manage mocking functionality. The test runner module provides a top level `mock` export which is a `MockTracker` instance. Each test also provides its own `MockTracker` instance via the test context's `mock` property.

    - readonly [timers](https://bun.com/reference/node/test/default/MockTracker/timers): [MockTimers](https://bun.com/reference/node/test/default/MockTimers)
    - [fn](https://bun.com/reference/node/test/default/MockTracker/fn)<F extends Function = (...args: any[]) => undefined>(

      original?: F,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<F>;

      This function is used to create a mock function.

      The following example creates a mock function that increments a counter by one on each invocation. The `times` option is used to modify the mock behavior such that the first two invocations add two to the counter instead of one.

      ```
      test('mocks a counting function', (t) => {
        let cnt = 0;

        function addOne() {
          cnt++;
          return cnt;
        }

        function addTwo() {
          cnt += 2;
          return cnt;
        }

        const fn = t.mock.fn(addOne, addTwo, { times: 2 });

        assert.strictEqual(fn(), 2);
        assert.strictEqual(fn(), 4);
        assert.strictEqual(fn(), 5);
        assert.strictEqual(fn(), 6);
      });
      ```

      @param original

      An optional function to create a mock on.

      @param options

      Optional configuration options for the mock function.

      @returns

      The mocked function. The mocked function contains a special `mock` property, which is an instance of MockFunctionContext, and can be used for inspecting and changing the behavior of the mocked function.

      [fn](https://bun.com/reference/node/test/default/MockTracker/fn)<F extends Function = (...args: any[]) => undefined, Implementation extends Function = F>(

      original?: F,

      implementation?: Implementation,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<F | Implementation>;
    - [getter](https://bun.com/reference/node/test/default/MockTracker/getter)<MockedObject extends object, MethodName extends string | number | symbol>(

      object: MockedObject,

      methodName: MethodName,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<() => MockedObject[MethodName]>;

      This function is syntax sugar for `MockTracker.method` with `options.getter` set to `true`.

      [getter](https://bun.com/reference/node/test/default/MockTracker/getter)<MockedObject extends object, MethodName extends string | number | symbol, Implementation extends Function>(

      object: MockedObject,

      methodName: MethodName,

      implementation?: Implementation,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<Implementation | () => MockedObject[MethodName]>;
    - [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object, MethodName extends string | number | symbol>(

      object: MockedObject,

      methodName: MethodName,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): MockedObject[MethodName] extends Function ? [Mock](https://bun.com/reference/node/test/default/Mock)<any[any]> : never;

      This function is used to create a mock on an existing object method. The following example demonstrates how a mock is created on an existing object method.

      ```
      test('spies on an object method', (t) => {
        const number = {
          value: 5,
          subtract(a) {
            return this.value - a;
          },
        };

        t.mock.method(number, 'subtract');
        assert.strictEqual(number.subtract.mock.calls.length, 0);
        assert.strictEqual(number.subtract(3), 2);
        assert.strictEqual(number.subtract.mock.calls.length, 1);

        const call = number.subtract.mock.calls[0];

        assert.deepStrictEqual(call.arguments, [3]);
        assert.strictEqual(call.result, 2);
        assert.strictEqual(call.error, undefined);
        assert.strictEqual(call.target, undefined);
        assert.strictEqual(call.this, number);
      });
      ```

      @param object

      The object whose method is being mocked.

      @param methodName

      The identifier of the method on `object` to mock. If `object[methodName]` is not a function, an error is thrown.

      @param options

      Optional configuration options for the mock method.

      @returns

      The mocked method. The mocked method contains a special `mock` property, which is an instance of MockFunctionContext, and can be used for inspecting and changing the behavior of the mocked method.

      [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object, MethodName extends string | number | symbol, Implementation extends Function>(

      object: MockedObject,

      methodName: MethodName,

      implementation: Implementation,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): MockedObject[MethodName] extends Function ? [Mock](https://bun.com/reference/node/test/default/Mock)<Implementation | any[any]> : never;

      [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object>(

      object: MockedObject,

      methodName: keyof MockedObject,

      options: [MockMethodOptions](https://bun.com/reference/node/test/default/MockMethodOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<Function>;

      [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object>(

      object: MockedObject,

      methodName: keyof MockedObject,

      implementation: Function,

      options: [MockMethodOptions](https://bun.com/reference/node/test/default/MockMethodOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<Function>;
    - [module](https://bun.com/reference/node/test/default/MockTracker/module)(

      specifier: string,

      options?: [MockModuleOptions](https://bun.com/reference/node/test/default/MockModuleOptions)

      ): [MockModuleContext](https://bun.com/reference/node/test/default/MockModuleContext);

      This function is used to mock the exports of ECMAScript modules, CommonJS modules, JSON modules, and Node.js builtin modules. Any references to the original module prior to mocking are not impacted. In order to enable module mocking, Node.js must be started with the [`--experimental-test-module-mocks`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--experimental-test-module-mocks) command-line flag.

      The following example demonstrates how a mock is created for a module.

      ```
      test('mocks a builtin module in both module systems', async (t) => {
        // Create a mock of 'node:readline' with a named export named 'fn', which
        // does not exist in the original 'node:readline' module.
        const mock = t.mock.module('node:readline', {
          namedExports: { fn() { return 42; } },
        });

        let esmImpl = await import('node:readline');
        let cjsImpl = require('node:readline');

        // cursorTo() is an export of the original 'node:readline' module.
        assert.strictEqual(esmImpl.cursorTo, undefined);
        assert.strictEqual(cjsImpl.cursorTo, undefined);
        assert.strictEqual(esmImpl.fn(), 42);
        assert.strictEqual(cjsImpl.fn(), 42);

        mock.restore();

        // The mock is restored, so the original builtin module is returned.
        esmImpl = await import('node:readline');
        cjsImpl = require('node:readline');

        assert.strictEqual(typeof esmImpl.cursorTo, 'function');
        assert.strictEqual(typeof cjsImpl.cursorTo, 'function');
        assert.strictEqual(esmImpl.fn, undefined);
        assert.strictEqual(cjsImpl.fn, undefined);
      });
      ```

      @param specifier

      A string identifying the module to mock.

      @param options

      Optional configuration options for the mock module.
    - [property](https://bun.com/reference/node/test/default/MockTracker/property)<MockedObject extends object, PropertyName extends string | number | symbol>(

      object: MockedObject,

      property: PropertyName,

      value?: MockedObject[PropertyName]

      ): MockedObject & { mock: [MockPropertyContext](https://bun.com/reference/node/test/default/MockPropertyContext)<MockedObject[PropertyName]> };

      Creates a mock for a property value on an object. This allows you to track and control access to a specific property, including how many times it is read (getter) or written (setter), and to restore the original value after mocking.

      ```
      test('mocks a property value', (t) => {
        const obj = { foo: 42 };
        const prop = t.mock.property(obj, 'foo', 100);

        assert.strictEqual(obj.foo, 100);
        assert.strictEqual(prop.mock.accessCount(), 1);
        assert.strictEqual(prop.mock.accesses[0].type, 'get');
        assert.strictEqual(prop.mock.accesses[0].value, 100);

        obj.foo = 200;
        assert.strictEqual(prop.mock.accessCount(), 2);
        assert.strictEqual(prop.mock.accesses[1].type, 'set');
        assert.strictEqual(prop.mock.accesses[1].value, 200);

        prop.mock.restore();
        assert.strictEqual(obj.foo, 42);
      });
      ```

      @param object

      The object whose value is being mocked.

      @param value

      An optional value used as the mock value for `object[propertyName]`. **Default:** The original property value.

      @returns

      A proxy to the mocked object. The mocked object contains a special `mock` property, which is an instance of [`MockPropertyContext`][], and can be used for inspecting and changing the behavior of the mocked property.
    - [reset](https://bun.com/reference/node/test/default/MockTracker/reset)(): void;

      This function restores the default behavior of all mocks that were previously created by this `MockTracker` and disassociates the mocks from the `MockTracker` instance. Once disassociated, the mocks can still be used, but the `MockTracker` instance can no longer be used to reset their behavior or otherwise interact with them.

      After each test completes, this function is called on the test context's `MockTracker`. If the global `MockTracker` is used extensively, calling this function manually is recommended.
    - [restoreAll](https://bun.com/reference/node/test/default/MockTracker/restoreAll)(): void;

      This function restores the default behavior of all mocks that were previously created by this `MockTracker`. Unlike `mock.reset()`, `mock.restoreAll()` does not disassociate the mocks from the `MockTracker` instance.
    - [setter](https://bun.com/reference/node/test/default/MockTracker/setter)<MockedObject extends object, MethodName extends string | number | symbol>(

      object: MockedObject,

      methodName: MethodName,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<(value: MockedObject[MethodName]) => void>;

      This function is syntax sugar for `MockTracker.method` with `options.setter` set to `true`.

      [setter](https://bun.com/reference/node/test/default/MockTracker/setter)<MockedObject extends object, MethodName extends string | number | symbol, Implementation extends Function>(

      object: MockedObject,

      methodName: MethodName,

      implementation?: Implementation,

      options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

      ): [Mock](https://bun.com/reference/node/test/default/Mock)<Implementation | (value: MockedObject[MethodName]) => void>;
  + ### interface [RunOptions](https://bun.com/reference/node/test/default/RunOptions)

    - [argv](https://bun.com/reference/node/test/default/RunOptions/argv)?: readonly string[]

      An array of CLI flags to pass to each test file when spawning the subprocesses. This option has no effect when `isolation` is `'none'`.
    - [branchCoverage](https://bun.com/reference/node/test/default/RunOptions/branchCoverage)?: number

      Require a minimum percent of covered branches. If code coverage does not reach the threshold specified, the process will exit with code `1`.
    - [concurrency](https://bun.com/reference/node/test/default/RunOptions/concurrency)?: number | boolean

      If a number is provided, then that many test processes would run in parallel, where each process corresponds to one test file. If `true`, it would run `os.availableParallelism() - 1` test files in parallel. If `false`, it would only run one test file at a time.
    - [coverage](https://bun.com/reference/node/test/default/RunOptions/coverage)?: boolean

      enable [code coverage](https://nodejs.org/docs/latest-v24.x/api/test.html#collecting-code-coverage) collection.
    - [coverageExcludeGlobs](https://bun.com/reference/node/test/default/RunOptions/coverageExcludeGlobs)?: string | readonly string[]

      Excludes specific files from code coverage using a glob pattern, which can match both absolute and relative file paths. This property is only applicable when `coverage` was set to `true`. If both `coverageExcludeGlobs` and `coverageIncludeGlobs` are provided, files must meet **both** criteria to be included in the coverage report.
    - [coverageIncludeGlobs](https://bun.com/reference/node/test/default/RunOptions/coverageIncludeGlobs)?: string | readonly string[]

      Includes specific files in code coverage using a glob pattern, which can match both absolute and relative file paths. This property is only applicable when `coverage` was set to `true`. If both `coverageExcludeGlobs` and `coverageIncludeGlobs` are provided, files must meet **both** criteria to be included in the coverage report.
    - [cwd](https://bun.com/reference/node/test/default/RunOptions/cwd)?: string

      Specifies the current working directory to be used by the test runner. Serves as the base path for resolving files according to the [test runner execution model](https://nodejs.org/docs/latest-v24.x/api/test.html#test-runner-execution-model).
    - [execArgv](https://bun.com/reference/node/test/default/RunOptions/execArgv)?: readonly string[]

      An array of CLI flags to pass to the `node` executable when spawning the subprocesses. This option has no effect when `isolation` is `'none`'.
    - [files](https://bun.com/reference/node/test/default/RunOptions/files)?: readonly string[]

      An array containing the list of files to run. If omitted, files are run according to the [test runner execution model](https://nodejs.org/docs/latest-v24.x/api/test.html#test-runner-execution-model).
    - [forceExit](https://bun.com/reference/node/test/default/RunOptions/forceExit)?: boolean

      Configures the test runner to exit the process once all known tests have finished executing even if the event loop would otherwise remain active.
    - [functionCoverage](https://bun.com/reference/node/test/default/RunOptions/functionCoverage)?: number

      Require a minimum percent of covered functions. If code coverage does not reach the threshold specified, the process will exit with code `1`.
    - [globPatterns](https://bun.com/reference/node/test/default/RunOptions/globPatterns)?: readonly string[]

      An array containing the list of glob patterns to match test files. This option cannot be used together with `files`. If omitted, files are run according to the [test runner execution model](https://nodejs.org/docs/latest-v24.x/api/test.html#test-runner-execution-model).
    - [inspectPort](https://bun.com/reference/node/test/default/RunOptions/inspectPort)?: number | () => number

      Sets inspector port of test child process. This can be a number, or a function that takes no arguments and returns a number. If a nullish value is provided, each process gets its own port, incremented from the primary's `process.debugPort`. This option is ignored if the `isolation` option is set to `'none'` as no child processes are spawned.
    - [isolation](https://bun.com/reference/node/test/default/RunOptions/isolation)?: 'none' | 'process'

      Configures the type of test isolation. If set to `'process'`, each test file is run in a separate child process. If set to `'none'`, all test files run in the current process.
    - [lineCoverage](https://bun.com/reference/node/test/default/RunOptions/lineCoverage)?: number

      Require a minimum percent of covered lines. If code coverage does not reach the threshold specified, the process will exit with code `1`.
    - [only](https://bun.com/reference/node/test/default/RunOptions/only)?: boolean

      If truthy, the test context will only run tests that have the `only` option set
    - [rerunFailuresFilePath](https://bun.com/reference/node/test/default/RunOptions/rerunFailuresFilePath)?: string

      A file path where the test runner will store the state of the tests to allow rerunning only the failed tests on a next run.
    - [setup](https://bun.com/reference/node/test/default/RunOptions/setup)?: (reporter: [TestsStream](https://bun.com/reference/node/test/default/TestsStream)) => void | Promise<void>

      A function that accepts the `TestsStream` instance and can be used to setup listeners before any tests are run.
    - [shard](https://bun.com/reference/node/test/default/RunOptions/shard)?: [TestShard](https://bun.com/reference/node/test/default/TestShard)

      Running tests in a specific shard.
    - [signal](https://bun.com/reference/node/test/default/RunOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      Allows aborting an in-progress test execution.
    - [testNamePatterns](https://bun.com/reference/node/test/default/RunOptions/testNamePatterns)?: string | RegExp | readonly string | RegExp[]

      If provided, only run tests whose name matches the provided pattern. Strings are interpreted as JavaScript regular expressions.
    - [testSkipPatterns](https://bun.com/reference/node/test/default/RunOptions/testSkipPatterns)?: string | RegExp | readonly string | RegExp[]

      A String, RegExp or a RegExp Array, that can be used to exclude running tests whose name matches the provided pattern. Test name patterns are interpreted as JavaScript regular expressions. For each test that is executed, any corresponding test hooks, such as `beforeEach()`, are also run.
    - [timeout](https://bun.com/reference/node/test/default/RunOptions/timeout)?: number

      The number of milliseconds after which the test execution will fail. If unspecified, subtests inherit this value from their parent.
    - [watch](https://bun.com/reference/node/test/default/RunOptions/watch)?: boolean

      Whether to run in watch mode or not.
  + ### interface [SuiteContext](https://bun.com/reference/node/test/default/SuiteContext)

    An instance of `SuiteContext` is passed to each suite function in order to interact with the test runner. However, the `SuiteContext` constructor is not exposed as part of the API.

    - readonly [filePath](https://bun.com/reference/node/test/default/SuiteContext/filePath): undefined | string

      The absolute path of the test file that created the current suite. If a test file imports additional modules that generate suites, the imported suites will return the path of the root test file.
    - readonly [name](https://bun.com/reference/node/test/default/SuiteContext/name): string

      The name of the suite.
    - readonly [signal](https://bun.com/reference/node/test/default/SuiteContext/signal): [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      Can be used to abort test subtasks when the test has been aborted.
  + ### interface [TestContext](https://bun.com/reference/node/test/default/TestContext)

    An instance of `TestContext` is passed to each test function in order to interact with the test runner. However, the `TestContext` constructor is not exposed as part of the API.

    - readonly [assert](https://bun.com/reference/node/test/default/TestContext/assert): [TestContextAssert](https://bun.com/reference/node/test/default/TestContextAssert)

      An object containing assertion methods bound to the test context. The top-level functions from the `node:assert` module are exposed here for the purpose of creating test plans.

      **Note:** Some of the functions from `node:assert` contain type assertions. If these are called via the TestContext `assert` object, then the context parameter in the test's function signature **must be explicitly typed** (ie. the parameter must have a type annotation), otherwise an error will be raised by the TypeScript compiler:

      ```
      import { test, type TestContext } from 'node:test';

      // The test function's context parameter must have a type annotation.
      test('example', (t: TestContext) => {
        t.assert.deepStrictEqual(actual, expected);
      });

      // Omitting the type annotation will result in a compilation error.
      test('example', t => {
        t.assert.deepStrictEqual(actual, expected); // Error: 't' needs an explicit type annotation.
      });
      ```
    - readonly [attempt](https://bun.com/reference/node/test/default/TestContext/attempt): number
    - readonly [filePath](https://bun.com/reference/node/test/default/TestContext/filePath): undefined | string

      The absolute path of the test file that created the current test. If a test file imports additional modules that generate tests, the imported tests will return the path of the root test file.
    - readonly [fullName](https://bun.com/reference/node/test/default/TestContext/fullName): string

      The name of the test and each of its ancestors, separated by `>`.
    - readonly [mock](https://bun.com/reference/node/test/default/TestContext/mock): [MockTracker](https://bun.com/reference/node/test/default/MockTracker)

      Each test provides its own MockTracker instance.
    - readonly [name](https://bun.com/reference/node/test/default/TestContext/name): string

      The name of the test.
    - readonly [signal](https://bun.com/reference/node/test/default/TestContext/signal): [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      ```
      test('top level test', async (t) => {
        await fetch('some/uri', { signal: t.signal });
      });
      ```
    - [test](https://bun.com/reference/node/test/default/TestContext/test): typeof [test](https://bun.com/reference/node/test/default)

      This function is used to create subtests under the current test. This function behaves in the same fashion as the top level test function.
    - [after](https://bun.com/reference/node/test/default/TestContext/after)(

      fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

      options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

      ): void;

      This function is used to create a hook that runs after the current test finishes.

      @param fn

      The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

      @param options

      Configuration options for the hook.
    - [afterEach](https://bun.com/reference/node/test/default/TestContext/afterEach)(

      fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

      options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

      ): void;

      This function is used to create a hook running after each subtest of the current test.

      @param fn

      The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

      @param options

      Configuration options for the hook.
    - [before](https://bun.com/reference/node/test/default/TestContext/before)(

      fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

      options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

      ): void;

      This function is used to create a hook running before subtest of the current test.

      @param fn

      The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

      @param options

      Configuration options for the hook.
    - [beforeEach](https://bun.com/reference/node/test/default/TestContext/beforeEach)(

      fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

      options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

      ): void;

      This function is used to create a hook running before each subtest of the current test.

      @param fn

      The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

      @param options

      Configuration options for the hook.
    - [diagnostic](https://bun.com/reference/node/test/default/TestContext/diagnostic)(

      message: string

      ): void;

      This function is used to write diagnostics to the output. Any diagnostic information is included at the end of the test's results. This function does not return a value.

      ```
      test('top level test', (t) => {
        t.diagnostic('A diagnostic message');
      });
      ```

      @param message

      Message to be reported.
    - [plan](https://bun.com/reference/node/test/default/TestContext/plan)(

      count: number,

      options?: [TestContextPlanOptions](https://bun.com/reference/node/test/default/TestContextPlanOptions)

      ): void;

      This function is used to set the number of assertions and subtests that are expected to run within the test. If the number of assertions and subtests that run does not match the expected count, the test will fail.

      Note: To make sure assertions are tracked, `t.assert` must be used instead of `assert` directly.

      ```
      test('top level test', (t) => {
        t.plan(2);
        t.assert.ok('some relevant assertion here');
        t.test('subtest', () => {});
      });
      ```

      When working with asynchronous code, the `plan` function can be used to ensure that the correct number of assertions are run:

      ```
      test('planning with streams', (t, done) => {
        function* generate() {
          yield 'a';
          yield 'b';
          yield 'c';
        }
        const expected = ['a', 'b', 'c'];
        t.plan(expected.length);
        const stream = Readable.from(generate());
        stream.on('data', (chunk) => {
          t.assert.strictEqual(chunk, expected.shift());
        });

        stream.on('end', () => {
          done();
        });
      });
      ```

      When using the `wait` option, you can control how long the test will wait for the expected assertions. For example, setting a maximum wait time ensures that the test will wait for asynchronous assertions to complete within the specified timeframe:

      ```
      test('plan with wait: 2000 waits for async assertions', (t) => {
        t.plan(1, { wait: 2000 }); // Waits for up to 2 seconds for the assertion to complete.

        const asyncActivity = () => {
          setTimeout(() => {
               *       t.assert.ok(true, 'Async assertion completed within the wait time');
          }, 1000); // Completes after 1 second, within the 2-second wait time.
        };

        asyncActivity(); // The test will pass because the assertion is completed in time.
      });
      ```

      Note: If a `wait` timeout is specified, it begins counting down only after the test function finishes executing.
    - [runOnly](https://bun.com/reference/node/test/default/TestContext/runOnly)(

      shouldRunOnlyTests: boolean

      ): void;

      If `shouldRunOnlyTests` is truthy, the test context will only run tests that have the `only` option set. Otherwise, all tests are run. If Node.js was not started with the `--test-only` command-line option, this function is a no-op.

      ```
      test('top level test', (t) => {
        // The test context can be set to run subtests with the 'only' option.
        t.runOnly(true);
        return Promise.all([
          t.test('this subtest is now skipped'),
          t.test('this subtest is run', { only: true }),
        ]);
      });
      ```

      @param shouldRunOnlyTests

      Whether or not to run `only` tests.
    - [skip](https://bun.com/reference/node/test/default/TestContext/skip)(

      message?: string

      ): void;

      This function causes the test's output to indicate the test as skipped. If `message` is provided, it is included in the output. Calling `skip()` does not terminate execution of the test function. This function does not return a value.

      ```
      test('top level test', (t) => {
        // Make sure to return here as well if the test contains additional logic.
        t.skip('this is skipped');
      });
      ```

      @param message

      Optional skip message.
    - [todo](https://bun.com/reference/node/test/default/TestContext/todo)(

      message?: string

      ): void;

      This function adds a `TODO` directive to the test's output. If `message` is provided, it is included in the output. Calling `todo()` does not terminate execution of the test function. This function does not return a value.

      ```
      test('top level test', (t) => {
        // This test is marked as `TODO`
        t.todo('this is a todo');
      });
      ```

      @param message

      Optional `TODO` message.
    - [waitFor](https://bun.com/reference/node/test/default/TestContext/waitFor)<T>(

      condition: () => T,

      options?: [TestContextWaitForOptions](https://bun.com/reference/node/test/default/TestContextWaitForOptions)

      ): Promise<Awaited<T>>;

      This method polls a `condition` function until that function either returns successfully or the operation times out.

      @param condition

      An assertion function that is invoked periodically until it completes successfully or the defined polling timeout elapses. Successful completion is defined as not throwing or rejecting. This function does not accept any arguments, and is allowed to return any value.

      @param options

      An optional configuration object for the polling operation.

      @returns

      Fulfilled with the value returned by `condition`.
  + ### interface [TestContextAssert](https://bun.com/reference/node/test/default/TestContextAssert)

    - [deepEqual](https://bun.com/reference/node/test/default/TestContextAssert/deepEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [deepStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/deepStrictEqual): (actual: unknown, expected: T, message?: string | [Error](https://bun.com/reference/globals/Error)) => asserts actual is T
    - [doesNotMatch](https://bun.com/reference/node/test/default/TestContextAssert/doesNotMatch): (value: string, regExp: RegExp, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [doesNotReject](https://bun.com/reference/node/test/default/TestContextAssert/doesNotReject): {(block: Promise<unknown> | () => Promise<unknown>, message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>; (block: Promise<unknown> | () => Promise<unknown>, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>}
    - [doesNotThrow](https://bun.com/reference/node/test/default/TestContextAssert/doesNotThrow): {(block: () => unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void; (block: () => unknown, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => void}
    - [equal](https://bun.com/reference/node/test/default/TestContextAssert/equal): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [fail](https://bun.com/reference/node/test/default/TestContextAssert/fail): {}
    - [ifError](https://bun.com/reference/node/test/default/TestContextAssert/ifError): (value: unknown) => asserts value is undefined | null
    - [match](https://bun.com/reference/node/test/default/TestContextAssert/match): (value: string, regExp: RegExp, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [notDeepEqual](https://bun.com/reference/node/test/default/TestContextAssert/notDeepEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [notDeepStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/notDeepStrictEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [notEqual](https://bun.com/reference/node/test/default/TestContextAssert/notEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [notStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/notStrictEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [ok](https://bun.com/reference/node/test/default/TestContextAssert/ok): (value: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => asserts value
    - [partialDeepStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/partialDeepStrictEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
    - [rejects](https://bun.com/reference/node/test/default/TestContextAssert/rejects): {(block: Promise<unknown> | () => Promise<unknown>, message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>; (block: Promise<unknown> | () => Promise<unknown>, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>}
    - [strictEqual](https://bun.com/reference/node/test/default/TestContextAssert/strictEqual): (actual: unknown, expected: T, message?: string | [Error](https://bun.com/reference/globals/Error)) => asserts actual is T
    - [throws](https://bun.com/reference/node/test/default/TestContextAssert/throws): {(block: () => unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void; (block: () => unknown, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => void}
    - [fileSnapshot](https://bun.com/reference/node/test/default/TestContextAssert/fileSnapshot)(

      value: any,

      path: string,

      options?: [AssertSnapshotOptions](https://bun.com/reference/node/test/default/AssertSnapshotOptions)

      ): void;

      This function serializes `value` and writes it to the file specified by `path`.

      ```
      test('snapshot test with default serialization', (t) => {
        t.assert.fileSnapshot({ value1: 1, value2: 2 }, './snapshots/snapshot.json');
      });
      ```

      This function differs from `context.assert.snapshot()` in the following ways:

      * The snapshot file path is explicitly provided by the user.
      * Each snapshot file is limited to a single snapshot value.
      * No additional escaping is performed by the test runner.

      These differences allow snapshot files to better support features such as syntax highlighting.

      @param value

      A value to serialize to a string. If Node.js was started with the [`--test-update-snapshots`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--test-update-snapshots) flag, the serialized value is written to `path`. Otherwise, the serialized value is compared to the contents of the existing snapshot file.

      @param path

      The file where the serialized `value` is written.

      @param options

      Optional configuration options.
    - [snapshot](https://bun.com/reference/node/test/default/TestContextAssert/snapshot)(

      value: any,

      options?: [AssertSnapshotOptions](https://bun.com/reference/node/test/default/AssertSnapshotOptions)

      ): void;

      This function implements assertions for snapshot testing.

      ```
      test('snapshot test with default serialization', (t) => {
        t.assert.snapshot({ value1: 1, value2: 2 });
      });

      test('snapshot test with custom serialization', (t) => {
        t.assert.snapshot({ value3: 3, value4: 4 }, {
          serializers: [(value) => JSON.stringify(value)]
        });
      });
      ```

      @param value

      A value to serialize to a string. If Node.js was started with the [`--test-update-snapshots`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--test-update-snapshots) flag, the serialized value is written to the snapshot file. Otherwise, the serialized value is compared to the corresponding value in the existing snapshot file.
  + ### interface [TestContextPlanOptions](https://bun.com/reference/node/test/default/TestContextPlanOptions)

    - [wait](https://bun.com/reference/node/test/default/TestContextPlanOptions/wait)?: number | boolean

      The wait time for the plan:

      * If `true`, the plan waits indefinitely for all assertions and subtests to run.
      * If `false`, the plan performs an immediate check after the test function completes, without waiting for any pending assertions or subtests. Any assertions or subtests that complete after this check will not be counted towards the plan.
      * If a number, it specifies the maximum wait time in milliseconds before timing out while waiting for expected assertions and subtests to be matched. If the timeout is reached, the test will fail.
  + ### interface [TestContextWaitForOptions](https://bun.com/reference/node/test/default/TestContextWaitForOptions)

    - [interval](https://bun.com/reference/node/test/default/TestContextWaitForOptions/interval)?: number

      The number of milliseconds to wait after an unsuccessful invocation of `condition` before trying again.
    - [timeout](https://bun.com/reference/node/test/default/TestContextWaitForOptions/timeout)?: number

      The poll timeout in milliseconds. If `condition` has not succeeded by the time this elapses, an error occurs.
  + ### interface [TestOptions](https://bun.com/reference/node/test/default/TestOptions)

    - [concurrency](https://bun.com/reference/node/test/default/TestOptions/concurrency)?: number | boolean

      If a number is provided, then that many tests would run in parallel. If truthy, it would run (number of cpu cores - 1) tests in parallel. For subtests, it will be `Infinity` tests in parallel. If falsy, it would only run one test at a time. If unspecified, subtests inherit this value from their parent.
    - [only](https://bun.com/reference/node/test/default/TestOptions/only)?: boolean

      If truthy, and the test context is configured to run `only` tests, then this test will be run. Otherwise, the test is skipped.
    - [plan](https://bun.com/reference/node/test/default/TestOptions/plan)?: number

      The number of assertions and subtests expected to be run in the test. If the number of assertions run in the test does not match the number specified in the plan, the test will fail.
    - [signal](https://bun.com/reference/node/test/default/TestOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      Allows aborting an in-progress test.
    - [skip](https://bun.com/reference/node/test/default/TestOptions/skip)?: string | boolean

      If truthy, the test is skipped. If a string is provided, that string is displayed in the test results as the reason for skipping the test.
    - [timeout](https://bun.com/reference/node/test/default/TestOptions/timeout)?: number

      A number of milliseconds the test will fail after. If unspecified, subtests inherit this value from their parent.
    - [todo](https://bun.com/reference/node/test/default/TestOptions/todo)?: string | boolean

      If truthy, the test marked as `TODO`. If a string is provided, that string is displayed in the test results as the reason why the test is `TODO`.
  + ### interface [TestShard](https://bun.com/reference/node/test/default/TestShard)

    - [index](https://bun.com/reference/node/test/default/TestShard/index): number

      A positive integer between 1 and `total` that specifies the index of the shard to run.
    - [total](https://bun.com/reference/node/test/default/TestShard/total): number

      A positive integer that specifies the total number of shards to split the test files to.
  + ### interface [TestsStream](https://bun.com/reference/node/test/default/TestsStream)

    A successful call to `run()` will return a new `TestsStream` object, streaming a series of events representing the execution of the tests.

    Some of the events are guaranteed to be emitted in the same order as the tests are defined, while others are emitted in the order that the tests execute.

    - readonly [closed](https://bun.com/reference/node/test/default/TestsStream/closed): boolean

      Is `true` after `'close'` has been emitted.
    - [destroyed](https://bun.com/reference/node/test/default/TestsStream/destroyed): boolean

      Is `true` after `readable.destroy()` has been called.
    - readonly [errored](https://bun.com/reference/node/test/default/TestsStream/errored): null | [Error](https://bun.com/reference/globals/Error)

      Returns error if the stream has been destroyed with an error.
    - [readable](https://bun.com/reference/node/test/default/TestsStream/readable): boolean

      Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
    - readonly [readableAborted](https://bun.com/reference/node/test/default/TestsStream/readableAborted): boolean

      Returns whether the stream was destroyed or errored before emitting `'end'`.
    - readonly [readableDidRead](https://bun.com/reference/node/test/default/TestsStream/readableDidRead): boolean

      Returns whether `'data'` has been emitted.
    - readonly [readableEncoding](https://bun.com/reference/node/test/default/TestsStream/readableEncoding): null | BufferEncoding

      Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
    - readonly [readableEnded](https://bun.com/reference/node/test/default/TestsStream/readableEnded): boolean

      Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
    - readonly [readableFlowing](https://bun.com/reference/node/test/default/TestsStream/readableFlowing): null | boolean

      This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
    - readonly [readableHighWaterMark](https://bun.com/reference/node/test/default/TestsStream/readableHighWaterMark): number

      Returns the value of `highWaterMark` passed when creating this `Readable`.
    - readonly [readableLength](https://bun.com/reference/node/test/default/TestsStream/readableLength): number

      This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
    - readonly [readableObjectMode](https://bun.com/reference/node/test/default/TestsStream/readableObjectMode): boolean

      Getter for the property `objectMode` of a given `Readable` stream.
    - [\_construct](https://bun.com/reference/node/test/default/TestsStream/_construct)(

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_destroy](https://bun.com/reference/node/test/default/TestsStream/_destroy)(

      error: null | [Error](https://bun.com/reference/globals/Error),

      callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

      ): void;
    - [\_read](https://bun.com/reference/node/test/default/TestsStream/_read)(

      size: number

      ): void;
    - [[Symbol.asyncDispose]](https://bun.com/reference/node/test/default/TestsStream/[asyncDispose])(): Promise<void>;

      Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
    - [[Symbol.asyncIterator]](https://bun.com/reference/node/test/default/TestsStream/[asyncIterator])(): AsyncIterator<any>;

      @returns

      `AsyncIterator` to fully consume the stream.
    - [[events.captureRejectionSymbol]](https://bun.com/reference/node/test/default/TestsStream/[captureRejectionSymbol])<K>(

      error: [Error](https://bun.com/reference/globals/Error),

      event: string | symbol,

      ...args: AnyRest

      ): void;
    - [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:coverage',

      listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:complete',

      listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:dequeue',

      listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:diagnostic',

      listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:enqueue',

      listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:fail',

      listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:pass',

      listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:plan',

      listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:start',

      listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:stderr',

      listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:stdout',

      listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:summary',

      listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:watch:drained',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: 'test:watch:restarted',

      listener: () => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume

      [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

      event: string,

      listener: (...args: any[]) => void

      ): this;

      Event emitter The defined events on documents including:

      1. close
      2. data
      3. end
      4. error
      5. pause
      6. readable
      7. resume
    - [asIndexedPairs](https://bun.com/reference/node/test/default/TestsStream/asIndexedPairs)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

      @returns

      a stream of indexed pairs.
    - [compose](https://bun.com/reference/node/test/default/TestsStream/compose)<T extends ReadableStream>(

      stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

      options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

      ): T;
    - [destroy](https://bun.com/reference/node/test/default/TestsStream/destroy)(

      error?: [Error](https://bun.com/reference/globals/Error)

      ): this;

      Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

      Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

      Implementors should not override this method, but instead implement `readable._destroy()`.

      @param error

      Error which will be passed as payload in `'error'` event
    - [drop](https://bun.com/reference/node/test/default/TestsStream/drop)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks dropped from the start.

      @param limit

      the number of chunks to drop from the readable.

      @returns

      a stream with *limit* chunks dropped from the start.
    - [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:coverage',

      data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)

      ): boolean;

      Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

      Returns `true` if the event had listeners, `false` otherwise.

      ```
      import { EventEmitter } from 'node:events';
      const myEmitter = new EventEmitter();

      // First listener
      myEmitter.on('event', function firstListener() {
        console.log('Helloooo! first listener');
      });
      // Second listener
      myEmitter.on('event', function secondListener(arg1, arg2) {
        console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
      });
      // Third listener
      myEmitter.on('event', function thirdListener(...args) {
        const parameters = args.join(', ');
        console.log(`event with parameters ${parameters} in third listener`);
      });

      console.log(myEmitter.listeners('event'));

      myEmitter.emit('event', 1, 2, 3, 4, 5);

      // Prints:
      // [
      //   [Function: firstListener],
      //   [Function: secondListener],
      //   [Function: thirdListener]
      // ]
      // Helloooo! first listener
      // event with parameters 1, 2 in second listener
      // event with parameters 1, 2, 3, 4, 5 in third listener
      ```

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:complete',

      data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:dequeue',

      data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:diagnostic',

      data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:enqueue',

      data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:fail',

      data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:pass',

      data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:plan',

      data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:start',

      data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:stderr',

      data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:stdout',

      data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:summary',

      data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:watch:drained'

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: 'test:watch:restarted'

      ): boolean;

      [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

      event: string | symbol,

      ...args: any[]

      ): boolean;
    - [eventNames](https://bun.com/reference/node/test/default/TestsStream/eventNames)(): string | symbol[];

      Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

      ```
      import { EventEmitter } from 'node:events';

      const myEE = new EventEmitter();
      myEE.on('foo', () => {});
      myEE.on('bar', () => {});

      const sym = Symbol('symbol');
      myEE.on(sym, () => {});

      console.log(myEE.eventNames());
      // Prints: [ 'foo', 'bar', Symbol(symbol) ]
      ```
    - [every](https://bun.com/reference/node/test/default/TestsStream/every)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
    - [filter](https://bun.com/reference/node/test/default/TestsStream/filter)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

      @param fn

      a function to filter chunks from the stream. Async or not.

      @returns

      a stream filtered with the predicate *fn*.
    - [find](https://bun.com/reference/node/test/default/TestsStream/find)<T>(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<undefined | T>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

      [find](https://bun.com/reference/node/test/default/TestsStream/find)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<any>;

      This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
    - [flatMap](https://bun.com/reference/node/test/default/TestsStream/flatMap)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

      It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

      @param fn

      a function to map over every chunk in the stream. May be async. May be a stream or generator.

      @returns

      a stream flat-mapped with the function *fn*.
    - [forEach](https://bun.com/reference/node/test/default/TestsStream/forEach)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<void>;

      This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

      This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

      This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise for when the stream has finished.
    - [getMaxListeners](https://bun.com/reference/node/test/default/TestsStream/getMaxListeners)(): number;

      Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
    - [isPaused](https://bun.com/reference/node/test/default/TestsStream/isPaused)(): boolean;

      The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

      ```
      const readable = new stream.Readable();

      readable.isPaused(); // === false
      readable.pause();
      readable.isPaused(); // === true
      readable.resume();
      readable.isPaused(); // === false
      ```
    - [iterator](https://bun.com/reference/node/test/default/TestsStream/iterator)(

      options?: { destroyOnReturn: boolean }

      ): AsyncIterator<any>;

      The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
    - [listenerCount](https://bun.com/reference/node/test/default/TestsStream/listenerCount)<K>(

      eventName: string | symbol,

      listener?: Function

      ): number;

      Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

      @param eventName

      The name of the event being listened for

      @param listener

      The event handler function
    - [listeners](https://bun.com/reference/node/test/default/TestsStream/listeners)<K>(

      eventName: string | symbol

      ): Function[];

      Returns a copy of the array of listeners for the event named `eventName`.

      ```
      server.on('connection', (stream) => {
        console.log('someone connected!');
      });
      console.log(util.inspect(server.listeners('connection')));
      // Prints: [ [Function] ]
      ```
    - [map](https://bun.com/reference/node/test/default/TestsStream/map)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

      @param fn

      a function to map over every chunk in the stream. Async or not.

      @returns

      a stream mapped with the function *fn*.
    - [off](https://bun.com/reference/node/test/default/TestsStream/off)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.removeListener()`.
    - [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:coverage',

      listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

      ): this;

      Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

      ```
      server.on('connection', (stream) => {
        console.log('someone connected!');
      });
      ```

      Returns a reference to the `EventEmitter`, so that calls can be chained.

      By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

      ```
      import { EventEmitter } from 'node:events';
      const myEE = new EventEmitter();
      myEE.on('foo', () => console.log('a'));
      myEE.prependListener('foo', () => console.log('b'));
      myEE.emit('foo');
      // Prints:
      //   b
      //   a
      ```

      @param listener

      The callback function

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:complete',

      listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:dequeue',

      listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:diagnostic',

      listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:enqueue',

      listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:fail',

      listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:pass',

      listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:plan',

      listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:start',

      listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:stderr',

      listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:stdout',

      listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:summary',

      listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:watch:drained',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: 'test:watch:restarted',

      listener: () => void

      ): this;

      [on](https://bun.com/reference/node/test/default/TestsStream/on)(

      event: string,

      listener: (...args: any[]) => void

      ): this;
    - [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:coverage',

      listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

      ): this;

      Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

      ```
      server.once('connection', (stream) => {
        console.log('Ah, we have our first user!');
      });
      ```

      Returns a reference to the `EventEmitter`, so that calls can be chained.

      By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

      ```
      import { EventEmitter } from 'node:events';
      const myEE = new EventEmitter();
      myEE.once('foo', () => console.log('a'));
      myEE.prependOnceListener('foo', () => console.log('b'));
      myEE.emit('foo');
      // Prints:
      //   b
      //   a
      ```

      @param listener

      The callback function

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:complete',

      listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:dequeue',

      listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:diagnostic',

      listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:enqueue',

      listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:fail',

      listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:pass',

      listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:plan',

      listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:start',

      listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:stderr',

      listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:stdout',

      listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:summary',

      listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:watch:drained',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: 'test:watch:restarted',

      listener: () => void

      ): this;

      [once](https://bun.com/reference/node/test/default/TestsStream/once)(

      event: string,

      listener: (...args: any[]) => void

      ): this;
    - [pause](https://bun.com/reference/node/test/default/TestsStream/pause)(): this;

      The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

      ```
      const readable = getReadableStreamSomehow();
      readable.on('data', (chunk) => {
        console.log(`Received ${chunk.length} bytes of data.`);
        readable.pause();
        console.log('There will be no additional data for 1 second.');
        setTimeout(() => {
          console.log('Now data will start flowing again.');
          readable.resume();
        }, 1000);
      });
      ```

      The `readable.pause()` method has no effect if there is a `'readable'` event listener.
    - [pipe](https://bun.com/reference/node/test/default/TestsStream/pipe)<T extends WritableStream>(

      destination: T,

      options?: { end: boolean }

      ): T;
    - [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:coverage',

      listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

      ): this;

      Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

      ```
      server.prependListener('connection', (stream) => {
        console.log('someone connected!');
      });
      ```

      Returns a reference to the `EventEmitter`, so that calls can be chained.

      @param listener

      The callback function

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:complete',

      listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:dequeue',

      listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:diagnostic',

      listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:enqueue',

      listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:fail',

      listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:pass',

      listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:plan',

      listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:start',

      listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:stderr',

      listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:stdout',

      listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:summary',

      listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:watch:drained',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: 'test:watch:restarted',

      listener: () => void

      ): this;

      [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

      event: string,

      listener: (...args: any[]) => void

      ): this;
    - [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:coverage',

      listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

      ): this;

      Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

      ```
      server.prependOnceListener('connection', (stream) => {
        console.log('Ah, we have our first user!');
      });
      ```

      Returns a reference to the `EventEmitter`, so that calls can be chained.

      @param listener

      The callback function

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:complete',

      listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:dequeue',

      listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:diagnostic',

      listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:enqueue',

      listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:fail',

      listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:pass',

      listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:plan',

      listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:start',

      listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:stderr',

      listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:stdout',

      listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:summary',

      listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:watch:drained',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: 'test:watch:restarted',

      listener: () => void

      ): this;

      [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

      event: string,

      listener: (...args: any[]) => void

      ): this;
    - [push](https://bun.com/reference/node/test/default/TestsStream/push)(

      chunk: any,

      encoding?: BufferEncoding

      ): boolean;
    - [rawListeners](https://bun.com/reference/node/test/default/TestsStream/rawListeners)<K>(

      eventName: string | symbol

      ): Function[];

      Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

      ```
      import { EventEmitter } from 'node:events';
      const emitter = new EventEmitter();
      emitter.once('log', () => console.log('log once'));

      // Returns a new Array with a function `onceWrapper` which has a property
      // `listener` which contains the original listener bound above
      const listeners = emitter.rawListeners('log');
      const logFnWrapper = listeners[0];

      // Logs "log once" to the console and does not unbind the `once` event
      logFnWrapper.listener();

      // Logs "log once" to the console and removes the listener
      logFnWrapper();

      emitter.on('log', () => console.log('log persistently'));
      // Will return a new Array with a single function bound by `.on()` above
      const newListeners = emitter.rawListeners('log');

      // Logs "log persistently" twice
      newListeners[0]();
      emitter.emit('log');
      ```
    - [read](https://bun.com/reference/node/test/default/TestsStream/read)(

      size?: number

      ): any;

      The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

      The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

      If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

      The `size` argument must be less than or equal to 1 GiB.

      The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

      ```
      const readable = getReadableStreamSomehow();

      // 'readable' may be triggered multiple times as data is buffered in
      readable.on('readable', () => {
        let chunk;
        console.log('Stream is readable (new data received in buffer)');
        // Use a loop to make sure we read all currently available data
        while (null !== (chunk = readable.read())) {
          console.log(`Read ${chunk.length} bytes of data...`);
        }
      });

      // 'end' will be triggered once when there is no more data available
      readable.on('end', () => {
        console.log('Reached end of stream.');
      });
      ```

      Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

      Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

      ```
      const chunks = [];

      readable.on('readable', () => {
        let chunk;
        while (null !== (chunk = readable.read())) {
          chunks.push(chunk);
        }
      });

      readable.on('end', () => {
        const content = chunks.join('');
      });
      ```

      A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

      If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

      Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

      @param size

      Optional argument to specify how much data to read.
    - [reduce](https://bun.com/reference/node/test/default/TestsStream/reduce)<T = any>(

      fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial?: undefined,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.

      [reduce](https://bun.com/reference/node/test/default/TestsStream/reduce)<T = any>(

      fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

      initial: T,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<T>;

      This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

      If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

      The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

      @param fn

      a reducer function to call over every chunk in the stream. Async or not.

      @param initial

      the initial value to use in the reduction.

      @returns

      a promise for the final value of the reduction.
    - [removeAllListeners](https://bun.com/reference/node/test/default/TestsStream/removeAllListeners)(

      eventName?: string | symbol

      ): this;

      Removes all listeners, or those of the specified `eventName`.

      It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: 'close',

      listener: () => void

      ): this;

      Removes the specified `listener` from the listener array for the event named `eventName`.

      ```
      const callback = (stream) => {
        console.log('someone connected!');
      };
      server.on('connection', callback);
      // ...
      server.removeListener('connection', callback);
      ```

      `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

      Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

      ```
      import { EventEmitter } from 'node:events';
      class MyEmitter extends EventEmitter {}
      const myEmitter = new MyEmitter();

      const callbackA = () => {
        console.log('A');
        myEmitter.removeListener('event', callbackB);
      };

      const callbackB = () => {
        console.log('B');
      };

      myEmitter.on('event', callbackA);

      myEmitter.on('event', callbackB);

      // callbackA removes listener callbackB but it will still be called.
      // Internal listener array at time of emit [callbackA, callbackB]
      myEmitter.emit('event');
      // Prints:
      //   A
      //   B

      // callbackB is now removed.
      // Internal listener array [callbackA]
      myEmitter.emit('event');
      // Prints:
      //   A
      ```

      Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

      When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

      ```
      import { EventEmitter } from 'node:events';
      const ee = new EventEmitter();

      function pong() {
        console.log('pong');
      }

      ee.on('ping', pong);
      ee.once('ping', pong);
      ee.removeListener('ping', pong);

      ee.emit('ping');
      ee.emit('ping');
      ```

      Returns a reference to the `EventEmitter`, so that calls can be chained.

      [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: 'data',

      listener: (chunk: any) => void

      ): this;

      [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: 'end',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: 'error',

      listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

      ): this;

      [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: 'pause',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: 'readable',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: 'resume',

      listener: () => void

      ): this;

      [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

      event: string | symbol,

      listener: (...args: any[]) => void

      ): this;
    - [resume](https://bun.com/reference/node/test/default/TestsStream/resume)(): this;

      The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

      The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

      ```
      getReadableStreamSomehow()
        .resume()
        .on('end', () => {
          console.log('Reached the end, but did not read anything.');
        });
      ```

      The `readable.resume()` method has no effect if there is a `'readable'` event listener.
    - [setEncoding](https://bun.com/reference/node/test/default/TestsStream/setEncoding)(

      encoding: BufferEncoding

      ): this;

      The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

      By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

      The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

      ```
      const readable = getReadableStreamSomehow();
      readable.setEncoding('utf8');
      readable.on('data', (chunk) => {
        assert.equal(typeof chunk, 'string');
        console.log('Got %d characters of string data:', chunk.length);
      });
      ```

      @param encoding

      The encoding to use.
    - [setMaxListeners](https://bun.com/reference/node/test/default/TestsStream/setMaxListeners)(

      n: number

      ): this;

      By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [some](https://bun.com/reference/node/test/default/TestsStream/some)(

      fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

      options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

      ): Promise<boolean>;

      This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

      @param fn

      a function to call on each chunk of the stream. Async or not.

      @returns

      a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
    - [take](https://bun.com/reference/node/test/default/TestsStream/take)(

      limit: number,

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): [Readable](https://bun.com/reference/node/stream/default/Readable);

      This method returns a new stream with the first *limit* chunks.

      @param limit

      the number of chunks to take from the readable.

      @returns

      a stream with *limit* chunks taken.
    - [toArray](https://bun.com/reference/node/test/default/TestsStream/toArray)(

      options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

      ): Promise<any[]>;

      This method allows easily obtaining the contents of a stream.

      As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

      @returns

      a promise containing an array with the contents of the stream.
    - [unpipe](https://bun.com/reference/node/test/default/TestsStream/unpipe)(

      destination?: WritableStream

      ): this;

      The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

      If the `destination` is not specified, then *all* pipes are detached.

      If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

      ```
      import fs from 'node:fs';
      const readable = getReadableStreamSomehow();
      const writable = fs.createWriteStream('file.txt');
      // All the data from readable goes into 'file.txt',
      // but only for the first second.
      readable.pipe(writable);
      setTimeout(() => {
        console.log('Stop writing to file.txt.');
        readable.unpipe(writable);
        console.log('Manually close the file stream.');
        writable.end();
      }, 1000);
      ```

      @param destination

      Optional specific stream to unpipe
    - [unshift](https://bun.com/reference/node/test/default/TestsStream/unshift)(

      chunk: any,

      encoding?: BufferEncoding

      ): void;

      Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

      The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

      The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

      Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

      ```
      // Pull off a header delimited by \n\n.
      // Use unshift() if we get too much.
      // Call the callback with (error, header, stream).
      import { StringDecoder } from 'node:string_decoder';
      function parseHeader(stream, callback) {
        stream.on('error', callback);
        stream.on('readable', onReadable);
        const decoder = new StringDecoder('utf8');
        let header = '';
        function onReadable() {
          let chunk;
          while (null !== (chunk = stream.read())) {
            const str = decoder.write(chunk);
            if (str.includes('\n\n')) {
              // Found the header boundary.
              const split = str.split(/\n\n/);
              header += split.shift();
              const remaining = split.join('\n\n');
              const buf = Buffer.from(remaining, 'utf8');
              stream.removeListener('error', callback);
              // Remove the 'readable' listener before unshifting.
              stream.removeListener('readable', onReadable);
              if (buf.length)
                stream.unshift(buf);
              // Now the body of the message can be read from the stream.
              callback(null, header, stream);
              return;
            }
            // Still reading the header.
            header += str;
          }
        }
      }
      ```

      Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

      @param chunk

      Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

      @param encoding

      Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
    - [wrap](https://bun.com/reference/node/test/default/TestsStream/wrap)(

      stream: ReadableStream

      ): this;

      Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

      When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

      It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

      ```
      import { OldReader } from './old-api-module.js';
      import { Readable } from 'node:stream';
      const oreader = new OldReader();
      const myReader = new Readable().wrap(oreader);

      myReader.on('readable', () => {
        myReader.read(); // etc.
      });
      ```

      @param stream

      An "old style" readable stream
  + type [HookFn](https://bun.com/reference/node/test/default/HookFn) = (c: [TestContext](https://bun.com/reference/node/test/default/TestContext) | [SuiteContext](https://bun.com/reference/node/test/default/SuiteContext), done: (result?: any) => void) => any

    The hook function. The first argument is the context in which the hook is called. If the hook uses callbacks, the callback function is passed as the second argument.
  + type [Mock](https://bun.com/reference/node/test/default/Mock)<F extends Function> = F & { mock: [MockFunctionContext](https://bun.com/reference/node/test/default/MockFunctionContext)<F> }
  + type [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn) = (s: [SuiteContext](https://bun.com/reference/node/test/default/SuiteContext)) => void | Promise<void>

    The type of a suite test function. The argument to this function is a SuiteContext object.
  + type [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn) = (t: [TestContext](https://bun.com/reference/node/test/default/TestContext), done: (result?: any) => void) => any

    The hook function. The first argument is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.
  + type [TestFn](https://bun.com/reference/node/test/default/TestFn) = (t: [TestContext](https://bun.com/reference/node/test/default/TestContext), done: (result?: any) => void) => void | Promise<void>

    The type of a function passed to test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.
  + const [mock](https://bun.com/reference/node/test/default/mock): [MockTracker](https://bun.com/reference/node/test/default/MockTracker)
  + function [after](https://bun.com/reference/node/test/default/after)(

    fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function creates a hook that runs after executing a suite.

    ```
    describe('tests', async () => {
      after(() => console.log('finished running tests'));
      it('is a subtest', () => {
        assert.ok('some relevant assertion here');
      });
    });
    ```

    @param fn

    The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + function [afterEach](https://bun.com/reference/node/test/default/afterEach)(

    fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function creates a hook that runs after each test in the current suite. The `afterEach()` hook is run even if the test fails.

    ```
    describe('tests', async () => {
      afterEach(() => console.log('finished running a test'));
      it('is a subtest', () => {
        assert.ok('some relevant assertion here');
      });
    });
    ```

    @param fn

    The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + function [before](https://bun.com/reference/node/test/default/before)(

    fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function creates a hook that runs before executing a suite.

    ```
    describe('tests', async () => {
      before(() => console.log('about to run some test'));
      it('is a subtest', () => {
        assert.ok('some relevant assertion here');
      });
    });
    ```

    @param fn

    The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + function [beforeEach](https://bun.com/reference/node/test/default/beforeEach)(

    fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function creates a hook that runs before each test in the current suite.

    ```
    describe('tests', async () => {
      beforeEach(() => console.log('about to run a test'));
      it('is a subtest', () => {
        assert.ok('some relevant assertion here');
      });
    });
    ```

    @param fn

    The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + function [only](https://bun.com/reference/node/test/default/only)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/only)(

    name?: string,

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/only)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/only)(

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.
  + function [run](https://bun.com/reference/node/test/default/run)(

    options?: [RunOptions](https://bun.com/reference/node/test/default/RunOptions)

    ): [TestsStream](https://bun.com/reference/node/test/default/TestsStream);

    **Note:** `shard` is used to horizontally parallelize test running across machines or processes, ideal for large-scale executions across varied environments. It's incompatible with `watch` mode, tailored for rapid code iteration by automatically rerunning tests on file changes.

    ```
    import { tap } from 'node:test/reporters';
    import { run } from 'node:test';
    import process from 'node:process';
    import path from 'node:path';

    run({ files: [path.resolve('./tests/test.js')] })
      .compose(tap)
      .pipe(process.stdout);
    ```

    @param options

    Configuration options for running tests.
  + function [skip](https://bun.com/reference/node/test/default/skip)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/skip)(

    name?: string,

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/skip)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/skip)(

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.
  + function [suite](https://bun.com/reference/node/test/default/suite)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param name

    The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

    @param options

    Configuration options for the suite. This supports the same options as test.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    function [suite](https://bun.com/reference/node/test/default/suite)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param name

    The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    function [suite](https://bun.com/reference/node/test/default/suite)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param options

    Configuration options for the suite. This supports the same options as test.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    function [suite](https://bun.com/reference/node/test/default/suite)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    The `suite()` function is imported from the `node:test` module.

    @param fn

    The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

    @returns

    Immediately fulfilled with `undefined`.

    function [only](https://bun.com/reference/node/test/default/suite/only)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/suite/only)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/suite/only)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/suite/only)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.
  + function [todo](https://bun.com/reference/node/test/default/todo)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/todo)(

    name?: string,

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/todo)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/todo)(

    fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

    ): Promise<void>;

    Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.
* [export default function test](https://bun.com/reference/node/test/default)(

  name?: string,

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param name

  The name of the test, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  [export default function test](https://bun.com/reference/node/test/default)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param name

  The name of the test, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param options

  Configuration options for the test.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  [export default function test](https://bun.com/reference/node/test/default)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param options

  Configuration options for the test.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  [export default function test](https://bun.com/reference/node/test/default)(

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  The `test()` function is the value imported from the `test` module. Each invocation of this function results in reporting the test to the `TestsStream`.

  The `TestContext` object passed to the `fn` argument can be used to perform actions related to the current test. Examples include skipping the test, adding additional diagnostic information, or creating subtests.

  `test()` returns a `Promise` that fulfills once the test completes. if `test()` is called within a suite, it fulfills immediately. The return value can usually be discarded for top level tests. However, the return value from subtests should be used to prevent the parent test from finishing first and cancelling the subtest as shown in the following example.

  ```
  test('top level test', async (t) => {
    // The setTimeout() in the following subtest would cause it to outlive its
    // parent test if 'await' is removed on the next line. Once the parent test
    // completes, it will cancel any outstanding subtests.
    await t.test('longer running subtest', async (t) => {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, 1000);
      });
    });
  });
  ```

  The `timeout` option can be used to fail the test if it takes longer than `timeout` milliseconds to complete. However, it is not a reliable mechanism for canceling tests because a running test might block the application thread and thus prevent the scheduled cancellation.

  @param fn

  The function under test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  @returns

  Fulfilled with `undefined` once the test completes, or immediately if the test runs within a suite.

  ### namespace [assert](https://bun.com/reference/node/test/default/assert)

  An object whose methods are used to configure available assertions on the `TestContext` objects in the current process. The methods from `node:assert` and snapshot testing functions are available by default.

  It is possible to apply the same configuration to all files by placing common configuration code in a module preloaded with `--require` or `--import`.

  + function [register](https://bun.com/reference/node/test/default/assert/register)(

    name: string,

    fn: (this: [TestContext](https://bun.com/reference/node/test/default/TestContext), ...args: any[]) => void

    ): void;

    Defines a new assertion function with the provided name and function. If an assertion already exists with the same name, it is overwritten.

  ### namespace [EventData](https://bun.com/reference/node/test/default/EventData)

  + ### interface [Error](https://bun.com/reference/node/test/default/EventData/Error)

    - [cause](https://bun.com/reference/node/test/default/EventData/Error/cause): [Error](https://bun.com/reference/globals/Error)

      The cause of the error.
    - [message](https://bun.com/reference/node/test/default/EventData/Error/message): string
    - [name](https://bun.com/reference/node/test/default/EventData/Error/name): string
    - [stack](https://bun.com/reference/node/test/default/EventData/Error/stack)?: string
  + ### interface [LocationInfo](https://bun.com/reference/node/test/default/EventData/LocationInfo)

    - [column](https://bun.com/reference/node/test/default/EventData/LocationInfo/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [file](https://bun.com/reference/node/test/default/EventData/LocationInfo/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/LocationInfo/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
  + ### interface [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)

    - [column](https://bun.com/reference/node/test/default/EventData/TestComplete/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [details](https://bun.com/reference/node/test/default/EventData/TestComplete/details): { duration\_ms: number; error: [Error](https://bun.com/reference/node/test/default/EventData/Error); passed: boolean; type: 'suite' | 'test' }

      Additional execution metadata.
    - [file](https://bun.com/reference/node/test/default/EventData/TestComplete/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/TestComplete/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [name](https://bun.com/reference/node/test/default/EventData/TestComplete/name): string

      The test name.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestComplete/nesting): number

      The nesting level of the test.
    - [skip](https://bun.com/reference/node/test/default/EventData/TestComplete/skip)?: string | boolean

      Present if `context.skip` is called.
    - [testNumber](https://bun.com/reference/node/test/default/EventData/TestComplete/testNumber): number

      The ordinal number of the test.
    - [todo](https://bun.com/reference/node/test/default/EventData/TestComplete/todo)?: string | boolean

      Present if `context.todo` is called.
  + ### interface [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)

    - [nesting](https://bun.com/reference/node/test/default/EventData/TestCoverage/nesting): number

      The nesting level of the test.
    - [summary](https://bun.com/reference/node/test/default/EventData/TestCoverage/summary): { files: { branches: { count: number; line: number }[]; coveredBranchCount: number; coveredBranchPercent: number; coveredFunctionCount: number; coveredFunctionPercent: number; coveredLineCount: number; coveredLinePercent: number; functions: { count: number; line: number; name: string }[]; lines: { count: number; line: number }[]; path: string; totalBranchCount: number; totalFunctionCount: number; totalLineCount: number }[]; thresholds: { branch: number; function: number; line: number }; totals: { coveredBranchCount: number; coveredBranchPercent: number; coveredFunctionCount: number; coveredFunctionPercent: number; coveredLineCount: number; coveredLinePercent: number; totalBranchCount: number; totalFunctionCount: number; totalLineCount: number }; workingDirectory: string }

      An object containing the coverage report.
  + ### interface [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)

    - [column](https://bun.com/reference/node/test/default/EventData/TestDequeue/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [file](https://bun.com/reference/node/test/default/EventData/TestDequeue/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/TestDequeue/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [name](https://bun.com/reference/node/test/default/EventData/TestDequeue/name): string

      The test name.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestDequeue/nesting): number

      The nesting level of the test.
    - [type](https://bun.com/reference/node/test/default/EventData/TestDequeue/type): 'suite' | 'test'

      The test type. Either `'suite'` or `'test'`.
  + ### interface [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)

    - [column](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [file](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [level](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/level): 'error' | 'info' | 'warn'

      The severity level of the diagnostic message. Possible values are:

      * `'info'`: Informational messages.
      * `'warn'`: Warnings.
      * `'error'`: Errors.
    - [line](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [message](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/message): string

      The diagnostic message.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestDiagnostic/nesting): number

      The nesting level of the test.
  + ### interface [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)

    - [column](https://bun.com/reference/node/test/default/EventData/TestEnqueue/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [file](https://bun.com/reference/node/test/default/EventData/TestEnqueue/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/TestEnqueue/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [name](https://bun.com/reference/node/test/default/EventData/TestEnqueue/name): string

      The test name.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestEnqueue/nesting): number

      The nesting level of the test.
    - [type](https://bun.com/reference/node/test/default/EventData/TestEnqueue/type): 'suite' | 'test'

      The test type. Either `'suite'` or `'test'`.
  + ### interface [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)

    - [column](https://bun.com/reference/node/test/default/EventData/TestFail/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [details](https://bun.com/reference/node/test/default/EventData/TestFail/details): { attempt: number; duration\_ms: number; error: [Error](https://bun.com/reference/node/test/default/EventData/Error); type: 'suite' | 'test' }

      Additional execution metadata.
    - [file](https://bun.com/reference/node/test/default/EventData/TestFail/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/TestFail/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [name](https://bun.com/reference/node/test/default/EventData/TestFail/name): string

      The test name.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestFail/nesting): number

      The nesting level of the test.
    - [skip](https://bun.com/reference/node/test/default/EventData/TestFail/skip)?: string | boolean

      Present if `context.skip` is called.
    - [testNumber](https://bun.com/reference/node/test/default/EventData/TestFail/testNumber): number

      The ordinal number of the test.
    - [todo](https://bun.com/reference/node/test/default/EventData/TestFail/todo)?: string | boolean

      Present if `context.todo` is called.
  + ### interface [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)

    - [column](https://bun.com/reference/node/test/default/EventData/TestPass/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [details](https://bun.com/reference/node/test/default/EventData/TestPass/details): { attempt: number; duration\_ms: number; passed\_on\_attempt: number; type: 'suite' | 'test' }

      Additional execution metadata.
    - [file](https://bun.com/reference/node/test/default/EventData/TestPass/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/TestPass/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [name](https://bun.com/reference/node/test/default/EventData/TestPass/name): string

      The test name.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestPass/nesting): number

      The nesting level of the test.
    - [skip](https://bun.com/reference/node/test/default/EventData/TestPass/skip)?: string | boolean

      Present if `context.skip` is called.
    - [testNumber](https://bun.com/reference/node/test/default/EventData/TestPass/testNumber): number

      The ordinal number of the test.
    - [todo](https://bun.com/reference/node/test/default/EventData/TestPass/todo)?: string | boolean

      Present if `context.todo` is called.
  + ### interface [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)

    - [column](https://bun.com/reference/node/test/default/EventData/TestPlan/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [count](https://bun.com/reference/node/test/default/EventData/TestPlan/count): number

      The number of subtests that have ran.
    - [file](https://bun.com/reference/node/test/default/EventData/TestPlan/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/TestPlan/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestPlan/nesting): number

      The nesting level of the test.
  + ### interface [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)

    - [column](https://bun.com/reference/node/test/default/EventData/TestStart/column)?: number

      The column number where the test is defined, or `undefined` if the test was run through the REPL.
    - [file](https://bun.com/reference/node/test/default/EventData/TestStart/file)?: string

      The path of the test file, `undefined` if test was run through the REPL.
    - [line](https://bun.com/reference/node/test/default/EventData/TestStart/line)?: number

      The line number where the test is defined, or `undefined` if the test was run through the REPL.
    - [name](https://bun.com/reference/node/test/default/EventData/TestStart/name): string

      The test name.
    - [nesting](https://bun.com/reference/node/test/default/EventData/TestStart/nesting): number

      The nesting level of the test.
  + ### interface [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)

    - [file](https://bun.com/reference/node/test/default/EventData/TestStderr/file): string

      The path of the test file.
    - [message](https://bun.com/reference/node/test/default/EventData/TestStderr/message): string

      The message written to `stderr`.
  + ### interface [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)

    - [file](https://bun.com/reference/node/test/default/EventData/TestStdout/file): string

      The path of the test file.
    - [message](https://bun.com/reference/node/test/default/EventData/TestStdout/message): string

      The message written to `stdout`.
  + ### interface [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)

    - [counts](https://bun.com/reference/node/test/default/EventData/TestSummary/counts): { cancelled: number; passed: number; skipped: number; suites: number; tests: number; todo: number; topLevel: number }

      An object containing the counts of various test results.
    - [duration\_ms](https://bun.com/reference/node/test/default/EventData/TestSummary/duration_ms): number

      The duration of the test run in milliseconds.
    - [file](https://bun.com/reference/node/test/default/EventData/TestSummary/file): undefined | string

      The path of the test file that generated the summary. If the summary corresponds to multiple files, this value is `undefined`.
    - [success](https://bun.com/reference/node/test/default/EventData/TestSummary/success): boolean

      Indicates whether or not the test run is considered successful or not. If any error condition occurs, such as a failing test or unmet coverage threshold, this value will be set to `false`.

  ### namespace [snapshot](https://bun.com/reference/node/test/default/snapshot)

  + function [setDefaultSnapshotSerializers](https://bun.com/reference/node/test/default/snapshot/setDefaultSnapshotSerializers)(

    serializers: readonly (value: any) => any[]

    ): void;

    This function is used to customize the default serialization mechanism used by the test runner.

    By default, the test runner performs serialization by calling `JSON.stringify(value, null, 2)` on the provided value. `JSON.stringify()` does have limitations regarding circular structures and supported data types. If a more robust serialization mechanism is required, this function should be used to specify a list of custom serializers.

    Serializers are called in order, with the output of the previous serializer passed as input to the next. The final result must be a string value.

    @param serializers

    An array of synchronous functions used as the default serializers for snapshot tests.
  + function [setResolveSnapshotPath](https://bun.com/reference/node/test/default/snapshot/setResolveSnapshotPath)(

    fn: (path: undefined | string) => string

    ): void;

    This function is used to set a custom resolver for the location of the snapshot file used for snapshot testing. By default, the snapshot filename is the same as the entry point filename with `.snapshot` appended.

    @param fn

    A function used to compute the location of the snapshot file. The function receives the path of the test file as its only argument. If the test is not associated with a file (for example in the REPL), the input is undefined. `fn()` must return a string specifying the location of the snapshot file.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param name

  The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param options

  Configuration options for the suite. This supports the same options as test.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  name?: string,

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param name

  The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param options

  Configuration options for the suite. This supports the same options as test.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  ### namespace [suite](https://bun.com/reference/node/test/default/suite)

  + function [only](https://bun.com/reference/node/test/default/suite/only)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/suite/only)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/suite/only)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

    function [only](https://bun.com/reference/node/test/default/suite/only)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.
  + function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

    function [skip](https://bun.com/reference/node/test/default/suite/skip)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.
  + function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    name?: string,

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    name?: string,

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

    function [todo](https://bun.com/reference/node/test/default/suite/todo)(

    fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

    ): Promise<void>;

    Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

  ### class [MockPropertyContext](https://bun.com/reference/node/test/default/MockPropertyContext)<PropertyType = any>

  + readonly [accesses](https://bun.com/reference/node/test/default/MockPropertyContext/accesses): { stack: [Error](https://bun.com/reference/globals/Error); type: 'get' | 'set'; value: PropertyType }[]

    A getter that returns a copy of the internal array used to track accesses (get/set) to the mocked property. Each entry in the array is an object with the following properties:
  + [accessCount](https://bun.com/reference/node/test/default/MockPropertyContext/accessCount)(): number;

    This function returns the number of times that the property was accessed. This function is more efficient than checking `ctx.accesses.length` because `ctx.accesses` is a getter that creates a copy of the internal access tracking array.

    @returns

    The number of times that the property was accessed (read or written).
  + [mockImplementation](https://bun.com/reference/node/test/default/MockPropertyContext/mockImplementation)(

    value: PropertyType

    ): void;

    This function is used to change the value returned by the mocked property getter.

    @param value

    The new value to be set as the mocked property value.
  + [mockImplementationOnce](https://bun.com/reference/node/test/default/MockPropertyContext/mockImplementationOnce)(

    value: PropertyType,

    onAccess?: number

    ): void;

    This function is used to change the behavior of an existing mock for a single invocation. Once invocation `onAccess` has occurred, the mock will revert to whatever behavior it would have used had `mockImplementationOnce()` not been called.

    The following example creates a mock function using `t.mock.property()`, calls the mock property, changes the mock implementation to a different value for the next invocation, and then resumes its previous behavior.

    ```
    test('changes a mock behavior once', (t) => {
      const obj = { foo: 1 };

      const prop = t.mock.property(obj, 'foo', 5);

      assert.strictEqual(obj.foo, 5);
      prop.mock.mockImplementationOnce(25);
      assert.strictEqual(obj.foo, 25);
      assert.strictEqual(obj.foo, 5);
    });
    ```

    @param value

    The value to be used as the mock's implementation for the invocation number specified by `onAccess`.

    @param onAccess

    The invocation number that will use `value`. If the specified invocation has already occurred then an exception is thrown. **Default:** The number of the next invocation.
  + [resetAccesses](https://bun.com/reference/node/test/default/MockPropertyContext/resetAccesses)(): void;

    Resets the access history of the mocked property.
  + [restore](https://bun.com/reference/node/test/default/MockPropertyContext/restore)(): void;

    Resets the implementation of the mock property to its original behavior. The mock can still be used after calling this function.

  ### interface [AssertSnapshotOptions](https://bun.com/reference/node/test/default/AssertSnapshotOptions)

  + [serializers](https://bun.com/reference/node/test/default/AssertSnapshotOptions/serializers)?: readonly (value: any) => any[]

    An array of synchronous functions used to serialize `value` into a string. `value` is passed as the only argument to the first serializer function. The return value of each serializer is passed as input to the next serializer. Once all serializers have run, the resulting value is coerced to a string.

    If no serializers are provided, the test runner's default serializers are used.

  ### interface [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

  Configuration options for hooks.

  + [signal](https://bun.com/reference/node/test/default/HookOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    Allows aborting an in-progress hook.
  + [timeout](https://bun.com/reference/node/test/default/HookOptions/timeout)?: number

    A number of milliseconds the hook will fail after. If unspecified, subtests inherit this value from their parent.

  ### interface [MockFunctionCall](https://bun.com/reference/node/test/default/MockFunctionCall)<F extends Function, ReturnType = F extends (...args: any) => infer T ? T : F extends new (...args: any) => infer T ? T : unknown, Args = F extends (...args: infer Y) => any ? Y : F extends new (...args: infer Y) => any ? Y : unknown[]>

  + [arguments](https://bun.com/reference/node/test/default/MockFunctionCall/arguments): Args

    An array of the arguments passed to the mock function.
  + [error](https://bun.com/reference/node/test/default/MockFunctionCall/error): unknown

    If the mocked function threw then this property contains the thrown value.
  + [result](https://bun.com/reference/node/test/default/MockFunctionCall/result): undefined | ReturnType

    The value returned by the mocked function.

    If the mocked function threw, it will be `undefined`.
  + [stack](https://bun.com/reference/node/test/default/MockFunctionCall/stack): [Error](https://bun.com/reference/globals/Error)

    An `Error` object whose stack can be used to determine the callsite of the mocked function invocation.
  + [target](https://bun.com/reference/node/test/default/MockFunctionCall/target): F extends new (...args: any) => any ? F<F> : undefined

    If the mocked function is a constructor, this field contains the class being constructed. Otherwise this will be `undefined`.
  + [this](https://bun.com/reference/node/test/default/MockFunctionCall/this): unknown

    The mocked function's `this` value.

  ### interface [MockFunctionContext](https://bun.com/reference/node/test/default/MockFunctionContext)<F extends Function>

  The `MockFunctionContext` class is used to inspect or manipulate the behavior of mocks created via the `MockTracker` APIs.

  + readonly [calls](https://bun.com/reference/node/test/default/MockFunctionContext/calls): [MockFunctionCall](https://bun.com/reference/node/test/default/MockFunctionCall)<F, F extends (...args: any) => T ? T : F extends new (...args: any) => T ? T : unknown, F extends (...args: Y) => any ? Y : F extends new (...args: Y) => any ? Y : unknown[]>[]

    A getter that returns a copy of the internal array used to track calls to the mock. Each entry in the array is an object with the following properties.
  + [callCount](https://bun.com/reference/node/test/default/MockFunctionContext/callCount)(): number;

    This function returns the number of times that this mock has been invoked. This function is more efficient than checking `ctx.calls.length` because `ctx.calls` is a getter that creates a copy of the internal call tracking array.

    @returns

    The number of times that this mock has been invoked.
  + [mockImplementation](https://bun.com/reference/node/test/default/MockFunctionContext/mockImplementation)(

    implementation: F

    ): void;

    This function is used to change the behavior of an existing mock.

    The following example creates a mock function using `t.mock.fn()`, calls the mock function, and then changes the mock implementation to a different function.

    ```
    test('changes a mock behavior', (t) => {
      let cnt = 0;

      function addOne() {
        cnt++;
        return cnt;
      }

      function addTwo() {
        cnt += 2;
        return cnt;
      }

      const fn = t.mock.fn(addOne);

      assert.strictEqual(fn(), 1);
      fn.mock.mockImplementation(addTwo);
      assert.strictEqual(fn(), 3);
      assert.strictEqual(fn(), 5);
    });
    ```

    @param implementation

    The function to be used as the mock's new implementation.
  + [mockImplementationOnce](https://bun.com/reference/node/test/default/MockFunctionContext/mockImplementationOnce)(

    implementation: F,

    onCall?: number

    ): void;

    This function is used to change the behavior of an existing mock for a single invocation. Once invocation `onCall` has occurred, the mock will revert to whatever behavior it would have used had `mockImplementationOnce()` not been called.

    The following example creates a mock function using `t.mock.fn()`, calls the mock function, changes the mock implementation to a different function for the next invocation, and then resumes its previous behavior.

    ```
    test('changes a mock behavior once', (t) => {
      let cnt = 0;

      function addOne() {
        cnt++;
        return cnt;
      }

      function addTwo() {
        cnt += 2;
        return cnt;
      }

      const fn = t.mock.fn(addOne);

      assert.strictEqual(fn(), 1);
      fn.mock.mockImplementationOnce(addTwo);
      assert.strictEqual(fn(), 3);
      assert.strictEqual(fn(), 4);
    });
    ```

    @param implementation

    The function to be used as the mock's implementation for the invocation number specified by `onCall`.

    @param onCall

    The invocation number that will use `implementation`. If the specified invocation has already occurred then an exception is thrown.
  + [resetCalls](https://bun.com/reference/node/test/default/MockFunctionContext/resetCalls)(): void;

    Resets the call history of the mock function.
  + [restore](https://bun.com/reference/node/test/default/MockFunctionContext/restore)(): void;

    Resets the implementation of the mock function to its original behavior. The mock can still be used after calling this function.

  ### interface [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

  + [times](https://bun.com/reference/node/test/default/MockFunctionOptions/times)?: number

    The number of times that the mock will use the behavior of `implementation`. Once the mock function has been called `times` times, it will automatically restore the behavior of `original`. This value must be an integer greater than zero.

  ### interface [MockMethodOptions](https://bun.com/reference/node/test/default/MockMethodOptions)

  + [getter](https://bun.com/reference/node/test/default/MockMethodOptions/getter)?: boolean

    If `true`, `object[methodName]` is treated as a getter. This option cannot be used with the `setter` option.
  + [setter](https://bun.com/reference/node/test/default/MockMethodOptions/setter)?: boolean

    If `true`, `object[methodName]` is treated as a setter. This option cannot be used with the `getter` option.
  + [times](https://bun.com/reference/node/test/default/MockMethodOptions/times)?: number

    The number of times that the mock will use the behavior of `implementation`. Once the mock function has been called `times` times, it will automatically restore the behavior of `original`. This value must be an integer greater than zero.

  ### interface [MockModuleContext](https://bun.com/reference/node/test/default/MockModuleContext)

  + [restore](https://bun.com/reference/node/test/default/MockModuleContext/restore)(): void;

    Resets the implementation of the mock module.

  ### interface [MockModuleOptions](https://bun.com/reference/node/test/default/MockModuleOptions)

  + [cache](https://bun.com/reference/node/test/default/MockModuleOptions/cache)?: boolean

    If false, each call to `require()` or `import()` generates a new mock module. If true, subsequent calls will return the same module mock, and the mock module is inserted into the CommonJS cache.
  + [defaultExport](https://bun.com/reference/node/test/default/MockModuleOptions/defaultExport)?: any

    The value to use as the mocked module's default export.

    If this value is not provided, ESM mocks do not include a default export. If the mock is a CommonJS or builtin module, this setting is used as the value of `module.exports`. If this value is not provided, CJS and builtin mocks use an empty object as the value of `module.exports`.
  + [namedExports](https://bun.com/reference/node/test/default/MockModuleOptions/namedExports)?: object

    An object whose keys and values are used to create the named exports of the mock module.

    If the mock is a CommonJS or builtin module, these values are copied onto `module.exports`. Therefore, if a mock is created with both named exports and a non-object default export, the mock will throw an exception when used as a CJS or builtin module.

  ### interface [MockTimers](https://bun.com/reference/node/test/default/MockTimers)

  Mocking timers is a technique commonly used in software testing to simulate and control the behavior of timers, such as `setInterval` and `setTimeout`, without actually waiting for the specified time intervals.

  The MockTimers API also allows for mocking of the `Date` constructor and `setImmediate`/`clearImmediate` functions.

  The `MockTracker` provides a top-level `timers` export which is a `MockTimers` instance.

  + [[Symbol.dispose]](https://bun.com/reference/node/test/default/MockTimers/[dispose])(): void;

    Calls ().
  + [enable](https://bun.com/reference/node/test/default/MockTimers/enable)(

    options?: [MockTimersOptions](https://bun.com/reference/node/test/default/MockTimersOptions)

    ): void;

    Enables timer mocking for the specified timers.

    **Note:** When you enable mocking for a specific timer, its associated clear function will also be implicitly mocked.

    **Note:** Mocking `Date` will affect the behavior of the mocked timers as they use the same internal clock.

    Example usage without setting initial time:

    ```
    import { mock } from 'node:test';
    mock.timers.enable({ apis: ['setInterval', 'Date'], now: 1234 });
    ```

    The above example enables mocking for the `Date` constructor, `setInterval` timer and implicitly mocks the `clearInterval` function. Only the `Date` constructor from `globalThis`, `setInterval` and `clearInterval` functions from `node:timers`, `node:timers/promises`, and `globalThis` will be mocked.

    Example usage with initial time set

    ```
    import { mock } from 'node:test';
    mock.timers.enable({ apis: ['Date'], now: 1000 });
    ```

    Example usage with initial Date object as time set

    ```
    import { mock } from 'node:test';
    mock.timers.enable({ apis: ['Date'], now: new Date() });
    ```

    Alternatively, if you call `mock.timers.enable()` without any parameters:

    All timers (`'setInterval'`, `'clearInterval'`, `'Date'`, `'setImmediate'`, `'clearImmediate'`, `'setTimeout'`, and `'clearTimeout'`) will be mocked.

    The `setInterval`, `clearInterval`, `setTimeout`, and `clearTimeout` functions from `node:timers`, `node:timers/promises`, and `globalThis` will be mocked. The `Date` constructor from `globalThis` will be mocked.

    If there is no initial epoch set, the initial date will be based on 0 in the Unix epoch. This is `January 1st, 1970, 00:00:00 UTC`. You can set an initial date by passing a now property to the `.enable()` method. This value will be used as the initial date for the mocked Date object. It can either be a positive integer, or another Date object.
  + [reset](https://bun.com/reference/node/test/default/MockTimers/reset)(): void;

    This function restores the default behavior of all mocks that were previously created by this `MockTimers` instance and disassociates the mocks from the `MockTracker` instance.

    **Note:** After each test completes, this function is called on the test context's `MockTracker`.

    ```
    import { mock } from 'node:test';
    mock.timers.reset();
    ```
  + [runAll](https://bun.com/reference/node/test/default/MockTimers/runAll)(): void;

    Triggers all pending mocked timers immediately. If the `Date` object is also mocked, it will also advance the `Date` object to the furthest timer's time.

    The example below triggers all pending timers immediately, causing them to execute without any delay.

    ```
    import assert from 'node:assert';
    import { test } from 'node:test';

    test('runAll functions following the given order', (context) => {
      context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
      const results = [];
      setTimeout(() => results.push(1), 9999);

      // Notice that if both timers have the same timeout,
      // the order of execution is guaranteed
      setTimeout(() => results.push(3), 8888);
      setTimeout(() => results.push(2), 8888);

      assert.deepStrictEqual(results, []);

      context.mock.timers.runAll();
      assert.deepStrictEqual(results, [3, 2, 1]);
      // The Date object is also advanced to the furthest timer's time
      assert.strictEqual(Date.now(), 9999);
    });
    ```

    **Note:** The `runAll()` function is specifically designed for triggering timers in the context of timer mocking. It does not have any effect on real-time system clocks or actual timers outside of the mocking environment.
  + [setTime](https://bun.com/reference/node/test/default/MockTimers/setTime)(

    time: number

    ): void;

    You can use the `.setTime()` method to manually move the mocked date to another time. This method only accepts a positive integer. Note: This method will execute any mocked timers that are in the past from the new time. In the below example we are setting a new time for the mocked date.

    ```
    import assert from 'node:assert';
    import { test } from 'node:test';
    test('sets the time of a date object', (context) => {
      // Optionally choose what to mock
      context.mock.timers.enable({ apis: ['Date'], now: 100 });
      assert.strictEqual(Date.now(), 100);
      // Advance in time will also advance the date
      context.mock.timers.setTime(1000);
      context.mock.timers.tick(200);
      assert.strictEqual(Date.now(), 1200);
    });
    ```
  + [tick](https://bun.com/reference/node/test/default/MockTimers/tick)(

    milliseconds: number

    ): void;

    Advances time for all mocked timers.

    **Note:** This diverges from how `setTimeout` in Node.js behaves and accepts only positive numbers. In Node.js, `setTimeout` with negative numbers is only supported for web compatibility reasons.

    The following example mocks a `setTimeout` function and by using `.tick` advances in time triggering all pending timers.

    ```
    import assert from 'node:assert';
    import { test } from 'node:test';

    test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
      const fn = context.mock.fn();

      context.mock.timers.enable({ apis: ['setTimeout'] });

      setTimeout(fn, 9999);

      assert.strictEqual(fn.mock.callCount(), 0);

      // Advance in time
      context.mock.timers.tick(9999);

      assert.strictEqual(fn.mock.callCount(), 1);
    });
    ```

    Alternativelly, the `.tick` function can be called many times

    ```
    import assert from 'node:assert';
    import { test } from 'node:test';

    test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
      const fn = context.mock.fn();
      context.mock.timers.enable({ apis: ['setTimeout'] });
      const nineSecs = 9000;
      setTimeout(fn, nineSecs);

      const twoSeconds = 3000;
      context.mock.timers.tick(twoSeconds);
      context.mock.timers.tick(twoSeconds);
      context.mock.timers.tick(twoSeconds);

      assert.strictEqual(fn.mock.callCount(), 1);
    });
    ```

    Advancing time using `.tick` will also advance the time for any `Date` object created after the mock was enabled (if `Date` was also set to be mocked).

    ```
    import assert from 'node:assert';
    import { test } from 'node:test';

    test('mocks setTimeout to be executed synchronously without having to actually wait for it', (context) => {
      const fn = context.mock.fn();

      context.mock.timers.enable({ apis: ['setTimeout', 'Date'] });
      setTimeout(fn, 9999);

      assert.strictEqual(fn.mock.callCount(), 0);
      assert.strictEqual(Date.now(), 0);

      // Advance in time
      context.mock.timers.tick(9999);
      assert.strictEqual(fn.mock.callCount(), 1);
      assert.strictEqual(Date.now(), 9999);
    });
    ```

  ### interface [MockTimersOptions](https://bun.com/reference/node/test/default/MockTimersOptions)

  + [apis](https://bun.com/reference/node/test/default/MockTimersOptions/apis): readonly 'Date' | 'setInterval' | 'setTimeout' | 'setImmediate'[]
  + [now](https://bun.com/reference/node/test/default/MockTimersOptions/now)?: number | Date

  ### interface [MockTracker](https://bun.com/reference/node/test/default/MockTracker)

  The `MockTracker` class is used to manage mocking functionality. The test runner module provides a top level `mock` export which is a `MockTracker` instance. Each test also provides its own `MockTracker` instance via the test context's `mock` property.

  + readonly [timers](https://bun.com/reference/node/test/default/MockTracker/timers): [MockTimers](https://bun.com/reference/node/test/default/MockTimers)
  + [fn](https://bun.com/reference/node/test/default/MockTracker/fn)<F extends Function = (...args: any[]) => undefined>(

    original?: F,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<F>;

    This function is used to create a mock function.

    The following example creates a mock function that increments a counter by one on each invocation. The `times` option is used to modify the mock behavior such that the first two invocations add two to the counter instead of one.

    ```
    test('mocks a counting function', (t) => {
      let cnt = 0;

      function addOne() {
        cnt++;
        return cnt;
      }

      function addTwo() {
        cnt += 2;
        return cnt;
      }

      const fn = t.mock.fn(addOne, addTwo, { times: 2 });

      assert.strictEqual(fn(), 2);
      assert.strictEqual(fn(), 4);
      assert.strictEqual(fn(), 5);
      assert.strictEqual(fn(), 6);
    });
    ```

    @param original

    An optional function to create a mock on.

    @param options

    Optional configuration options for the mock function.

    @returns

    The mocked function. The mocked function contains a special `mock` property, which is an instance of MockFunctionContext, and can be used for inspecting and changing the behavior of the mocked function.

    [fn](https://bun.com/reference/node/test/default/MockTracker/fn)<F extends Function = (...args: any[]) => undefined, Implementation extends Function = F>(

    original?: F,

    implementation?: Implementation,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<F | Implementation>;
  + [getter](https://bun.com/reference/node/test/default/MockTracker/getter)<MockedObject extends object, MethodName extends string | number | symbol>(

    object: MockedObject,

    methodName: MethodName,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<() => MockedObject[MethodName]>;

    This function is syntax sugar for `MockTracker.method` with `options.getter` set to `true`.

    [getter](https://bun.com/reference/node/test/default/MockTracker/getter)<MockedObject extends object, MethodName extends string | number | symbol, Implementation extends Function>(

    object: MockedObject,

    methodName: MethodName,

    implementation?: Implementation,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<Implementation | () => MockedObject[MethodName]>;
  + [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object, MethodName extends string | number | symbol>(

    object: MockedObject,

    methodName: MethodName,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): MockedObject[MethodName] extends Function ? [Mock](https://bun.com/reference/node/test/default/Mock)<any[any]> : never;

    This function is used to create a mock on an existing object method. The following example demonstrates how a mock is created on an existing object method.

    ```
    test('spies on an object method', (t) => {
      const number = {
        value: 5,
        subtract(a) {
          return this.value - a;
        },
      };

      t.mock.method(number, 'subtract');
      assert.strictEqual(number.subtract.mock.calls.length, 0);
      assert.strictEqual(number.subtract(3), 2);
      assert.strictEqual(number.subtract.mock.calls.length, 1);

      const call = number.subtract.mock.calls[0];

      assert.deepStrictEqual(call.arguments, [3]);
      assert.strictEqual(call.result, 2);
      assert.strictEqual(call.error, undefined);
      assert.strictEqual(call.target, undefined);
      assert.strictEqual(call.this, number);
    });
    ```

    @param object

    The object whose method is being mocked.

    @param methodName

    The identifier of the method on `object` to mock. If `object[methodName]` is not a function, an error is thrown.

    @param options

    Optional configuration options for the mock method.

    @returns

    The mocked method. The mocked method contains a special `mock` property, which is an instance of MockFunctionContext, and can be used for inspecting and changing the behavior of the mocked method.

    [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object, MethodName extends string | number | symbol, Implementation extends Function>(

    object: MockedObject,

    methodName: MethodName,

    implementation: Implementation,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): MockedObject[MethodName] extends Function ? [Mock](https://bun.com/reference/node/test/default/Mock)<Implementation | any[any]> : never;

    [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object>(

    object: MockedObject,

    methodName: keyof MockedObject,

    options: [MockMethodOptions](https://bun.com/reference/node/test/default/MockMethodOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<Function>;

    [method](https://bun.com/reference/node/test/default/MockTracker/method)<MockedObject extends object>(

    object: MockedObject,

    methodName: keyof MockedObject,

    implementation: Function,

    options: [MockMethodOptions](https://bun.com/reference/node/test/default/MockMethodOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<Function>;
  + [module](https://bun.com/reference/node/test/default/MockTracker/module)(

    specifier: string,

    options?: [MockModuleOptions](https://bun.com/reference/node/test/default/MockModuleOptions)

    ): [MockModuleContext](https://bun.com/reference/node/test/default/MockModuleContext);

    This function is used to mock the exports of ECMAScript modules, CommonJS modules, JSON modules, and Node.js builtin modules. Any references to the original module prior to mocking are not impacted. In order to enable module mocking, Node.js must be started with the [`--experimental-test-module-mocks`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--experimental-test-module-mocks) command-line flag.

    The following example demonstrates how a mock is created for a module.

    ```
    test('mocks a builtin module in both module systems', async (t) => {
      // Create a mock of 'node:readline' with a named export named 'fn', which
      // does not exist in the original 'node:readline' module.
      const mock = t.mock.module('node:readline', {
        namedExports: { fn() { return 42; } },
      });

      let esmImpl = await import('node:readline');
      let cjsImpl = require('node:readline');

      // cursorTo() is an export of the original 'node:readline' module.
      assert.strictEqual(esmImpl.cursorTo, undefined);
      assert.strictEqual(cjsImpl.cursorTo, undefined);
      assert.strictEqual(esmImpl.fn(), 42);
      assert.strictEqual(cjsImpl.fn(), 42);

      mock.restore();

      // The mock is restored, so the original builtin module is returned.
      esmImpl = await import('node:readline');
      cjsImpl = require('node:readline');

      assert.strictEqual(typeof esmImpl.cursorTo, 'function');
      assert.strictEqual(typeof cjsImpl.cursorTo, 'function');
      assert.strictEqual(esmImpl.fn, undefined);
      assert.strictEqual(cjsImpl.fn, undefined);
    });
    ```

    @param specifier

    A string identifying the module to mock.

    @param options

    Optional configuration options for the mock module.
  + [property](https://bun.com/reference/node/test/default/MockTracker/property)<MockedObject extends object, PropertyName extends string | number | symbol>(

    object: MockedObject,

    property: PropertyName,

    value?: MockedObject[PropertyName]

    ): MockedObject & { mock: [MockPropertyContext](https://bun.com/reference/node/test/default/MockPropertyContext)<MockedObject[PropertyName]> };

    Creates a mock for a property value on an object. This allows you to track and control access to a specific property, including how many times it is read (getter) or written (setter), and to restore the original value after mocking.

    ```
    test('mocks a property value', (t) => {
      const obj = { foo: 42 };
      const prop = t.mock.property(obj, 'foo', 100);

      assert.strictEqual(obj.foo, 100);
      assert.strictEqual(prop.mock.accessCount(), 1);
      assert.strictEqual(prop.mock.accesses[0].type, 'get');
      assert.strictEqual(prop.mock.accesses[0].value, 100);

      obj.foo = 200;
      assert.strictEqual(prop.mock.accessCount(), 2);
      assert.strictEqual(prop.mock.accesses[1].type, 'set');
      assert.strictEqual(prop.mock.accesses[1].value, 200);

      prop.mock.restore();
      assert.strictEqual(obj.foo, 42);
    });
    ```

    @param object

    The object whose value is being mocked.

    @param value

    An optional value used as the mock value for `object[propertyName]`. **Default:** The original property value.

    @returns

    A proxy to the mocked object. The mocked object contains a special `mock` property, which is an instance of [`MockPropertyContext`][], and can be used for inspecting and changing the behavior of the mocked property.
  + [reset](https://bun.com/reference/node/test/default/MockTracker/reset)(): void;

    This function restores the default behavior of all mocks that were previously created by this `MockTracker` and disassociates the mocks from the `MockTracker` instance. Once disassociated, the mocks can still be used, but the `MockTracker` instance can no longer be used to reset their behavior or otherwise interact with them.

    After each test completes, this function is called on the test context's `MockTracker`. If the global `MockTracker` is used extensively, calling this function manually is recommended.
  + [restoreAll](https://bun.com/reference/node/test/default/MockTracker/restoreAll)(): void;

    This function restores the default behavior of all mocks that were previously created by this `MockTracker`. Unlike `mock.reset()`, `mock.restoreAll()` does not disassociate the mocks from the `MockTracker` instance.
  + [setter](https://bun.com/reference/node/test/default/MockTracker/setter)<MockedObject extends object, MethodName extends string | number | symbol>(

    object: MockedObject,

    methodName: MethodName,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<(value: MockedObject[MethodName]) => void>;

    This function is syntax sugar for `MockTracker.method` with `options.setter` set to `true`.

    [setter](https://bun.com/reference/node/test/default/MockTracker/setter)<MockedObject extends object, MethodName extends string | number | symbol, Implementation extends Function>(

    object: MockedObject,

    methodName: MethodName,

    implementation?: Implementation,

    options?: [MockFunctionOptions](https://bun.com/reference/node/test/default/MockFunctionOptions)

    ): [Mock](https://bun.com/reference/node/test/default/Mock)<Implementation | (value: MockedObject[MethodName]) => void>;

  ### interface [RunOptions](https://bun.com/reference/node/test/default/RunOptions)

  + [argv](https://bun.com/reference/node/test/default/RunOptions/argv)?: readonly string[]

    An array of CLI flags to pass to each test file when spawning the subprocesses. This option has no effect when `isolation` is `'none'`.
  + [branchCoverage](https://bun.com/reference/node/test/default/RunOptions/branchCoverage)?: number

    Require a minimum percent of covered branches. If code coverage does not reach the threshold specified, the process will exit with code `1`.
  + [concurrency](https://bun.com/reference/node/test/default/RunOptions/concurrency)?: number | boolean

    If a number is provided, then that many test processes would run in parallel, where each process corresponds to one test file. If `true`, it would run `os.availableParallelism() - 1` test files in parallel. If `false`, it would only run one test file at a time.
  + [coverage](https://bun.com/reference/node/test/default/RunOptions/coverage)?: boolean

    enable [code coverage](https://nodejs.org/docs/latest-v24.x/api/test.html#collecting-code-coverage) collection.
  + [coverageExcludeGlobs](https://bun.com/reference/node/test/default/RunOptions/coverageExcludeGlobs)?: string | readonly string[]

    Excludes specific files from code coverage using a glob pattern, which can match both absolute and relative file paths. This property is only applicable when `coverage` was set to `true`. If both `coverageExcludeGlobs` and `coverageIncludeGlobs` are provided, files must meet **both** criteria to be included in the coverage report.
  + [coverageIncludeGlobs](https://bun.com/reference/node/test/default/RunOptions/coverageIncludeGlobs)?: string | readonly string[]

    Includes specific files in code coverage using a glob pattern, which can match both absolute and relative file paths. This property is only applicable when `coverage` was set to `true`. If both `coverageExcludeGlobs` and `coverageIncludeGlobs` are provided, files must meet **both** criteria to be included in the coverage report.
  + [cwd](https://bun.com/reference/node/test/default/RunOptions/cwd)?: string

    Specifies the current working directory to be used by the test runner. Serves as the base path for resolving files according to the [test runner execution model](https://nodejs.org/docs/latest-v24.x/api/test.html#test-runner-execution-model).
  + [execArgv](https://bun.com/reference/node/test/default/RunOptions/execArgv)?: readonly string[]

    An array of CLI flags to pass to the `node` executable when spawning the subprocesses. This option has no effect when `isolation` is `'none`'.
  + [files](https://bun.com/reference/node/test/default/RunOptions/files)?: readonly string[]

    An array containing the list of files to run. If omitted, files are run according to the [test runner execution model](https://nodejs.org/docs/latest-v24.x/api/test.html#test-runner-execution-model).
  + [forceExit](https://bun.com/reference/node/test/default/RunOptions/forceExit)?: boolean

    Configures the test runner to exit the process once all known tests have finished executing even if the event loop would otherwise remain active.
  + [functionCoverage](https://bun.com/reference/node/test/default/RunOptions/functionCoverage)?: number

    Require a minimum percent of covered functions. If code coverage does not reach the threshold specified, the process will exit with code `1`.
  + [globPatterns](https://bun.com/reference/node/test/default/RunOptions/globPatterns)?: readonly string[]

    An array containing the list of glob patterns to match test files. This option cannot be used together with `files`. If omitted, files are run according to the [test runner execution model](https://nodejs.org/docs/latest-v24.x/api/test.html#test-runner-execution-model).
  + [inspectPort](https://bun.com/reference/node/test/default/RunOptions/inspectPort)?: number | () => number

    Sets inspector port of test child process. This can be a number, or a function that takes no arguments and returns a number. If a nullish value is provided, each process gets its own port, incremented from the primary's `process.debugPort`. This option is ignored if the `isolation` option is set to `'none'` as no child processes are spawned.
  + [isolation](https://bun.com/reference/node/test/default/RunOptions/isolation)?: 'none' | 'process'

    Configures the type of test isolation. If set to `'process'`, each test file is run in a separate child process. If set to `'none'`, all test files run in the current process.
  + [lineCoverage](https://bun.com/reference/node/test/default/RunOptions/lineCoverage)?: number

    Require a minimum percent of covered lines. If code coverage does not reach the threshold specified, the process will exit with code `1`.
  + [only](https://bun.com/reference/node/test/default/RunOptions/only)?: boolean

    If truthy, the test context will only run tests that have the `only` option set
  + [rerunFailuresFilePath](https://bun.com/reference/node/test/default/RunOptions/rerunFailuresFilePath)?: string

    A file path where the test runner will store the state of the tests to allow rerunning only the failed tests on a next run.
  + [setup](https://bun.com/reference/node/test/default/RunOptions/setup)?: (reporter: [TestsStream](https://bun.com/reference/node/test/default/TestsStream)) => void | Promise<void>

    A function that accepts the `TestsStream` instance and can be used to setup listeners before any tests are run.
  + [shard](https://bun.com/reference/node/test/default/RunOptions/shard)?: [TestShard](https://bun.com/reference/node/test/default/TestShard)

    Running tests in a specific shard.
  + [signal](https://bun.com/reference/node/test/default/RunOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    Allows aborting an in-progress test execution.
  + [testNamePatterns](https://bun.com/reference/node/test/default/RunOptions/testNamePatterns)?: string | RegExp | readonly string | RegExp[]

    If provided, only run tests whose name matches the provided pattern. Strings are interpreted as JavaScript regular expressions.
  + [testSkipPatterns](https://bun.com/reference/node/test/default/RunOptions/testSkipPatterns)?: string | RegExp | readonly string | RegExp[]

    A String, RegExp or a RegExp Array, that can be used to exclude running tests whose name matches the provided pattern. Test name patterns are interpreted as JavaScript regular expressions. For each test that is executed, any corresponding test hooks, such as `beforeEach()`, are also run.
  + [timeout](https://bun.com/reference/node/test/default/RunOptions/timeout)?: number

    The number of milliseconds after which the test execution will fail. If unspecified, subtests inherit this value from their parent.
  + [watch](https://bun.com/reference/node/test/default/RunOptions/watch)?: boolean

    Whether to run in watch mode or not.

  ### interface [SuiteContext](https://bun.com/reference/node/test/default/SuiteContext)

  An instance of `SuiteContext` is passed to each suite function in order to interact with the test runner. However, the `SuiteContext` constructor is not exposed as part of the API.

  + readonly [filePath](https://bun.com/reference/node/test/default/SuiteContext/filePath): undefined | string

    The absolute path of the test file that created the current suite. If a test file imports additional modules that generate suites, the imported suites will return the path of the root test file.
  + readonly [name](https://bun.com/reference/node/test/default/SuiteContext/name): string

    The name of the suite.
  + readonly [signal](https://bun.com/reference/node/test/default/SuiteContext/signal): [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    Can be used to abort test subtasks when the test has been aborted.

  ### interface [TestContext](https://bun.com/reference/node/test/default/TestContext)

  An instance of `TestContext` is passed to each test function in order to interact with the test runner. However, the `TestContext` constructor is not exposed as part of the API.

  + readonly [assert](https://bun.com/reference/node/test/default/TestContext/assert): [TestContextAssert](https://bun.com/reference/node/test/default/TestContextAssert)

    An object containing assertion methods bound to the test context. The top-level functions from the `node:assert` module are exposed here for the purpose of creating test plans.

    **Note:** Some of the functions from `node:assert` contain type assertions. If these are called via the TestContext `assert` object, then the context parameter in the test's function signature **must be explicitly typed** (ie. the parameter must have a type annotation), otherwise an error will be raised by the TypeScript compiler:

    ```
    import { test, type TestContext } from 'node:test';

    // The test function's context parameter must have a type annotation.
    test('example', (t: TestContext) => {
      t.assert.deepStrictEqual(actual, expected);
    });

    // Omitting the type annotation will result in a compilation error.
    test('example', t => {
      t.assert.deepStrictEqual(actual, expected); // Error: 't' needs an explicit type annotation.
    });
    ```
  + readonly [attempt](https://bun.com/reference/node/test/default/TestContext/attempt): number
  + readonly [filePath](https://bun.com/reference/node/test/default/TestContext/filePath): undefined | string

    The absolute path of the test file that created the current test. If a test file imports additional modules that generate tests, the imported tests will return the path of the root test file.
  + readonly [fullName](https://bun.com/reference/node/test/default/TestContext/fullName): string

    The name of the test and each of its ancestors, separated by `>`.
  + readonly [mock](https://bun.com/reference/node/test/default/TestContext/mock): [MockTracker](https://bun.com/reference/node/test/default/MockTracker)

    Each test provides its own MockTracker instance.
  + readonly [name](https://bun.com/reference/node/test/default/TestContext/name): string

    The name of the test.
  + readonly [signal](https://bun.com/reference/node/test/default/TestContext/signal): [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    ```
    test('top level test', async (t) => {
      await fetch('some/uri', { signal: t.signal });
    });
    ```
  + [test](https://bun.com/reference/node/test/default/TestContext/test): typeof [test](https://bun.com/reference/node/test/default)

    This function is used to create subtests under the current test. This function behaves in the same fashion as the top level test function.
  + [after](https://bun.com/reference/node/test/default/TestContext/after)(

    fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function is used to create a hook that runs after the current test finishes.

    @param fn

    The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + [afterEach](https://bun.com/reference/node/test/default/TestContext/afterEach)(

    fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function is used to create a hook running after each subtest of the current test.

    @param fn

    The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + [before](https://bun.com/reference/node/test/default/TestContext/before)(

    fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function is used to create a hook running before subtest of the current test.

    @param fn

    The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + [beforeEach](https://bun.com/reference/node/test/default/TestContext/beforeEach)(

    fn?: [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn),

    options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

    ): void;

    This function is used to create a hook running before each subtest of the current test.

    @param fn

    The hook function. The first argument to this function is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

    @param options

    Configuration options for the hook.
  + [diagnostic](https://bun.com/reference/node/test/default/TestContext/diagnostic)(

    message: string

    ): void;

    This function is used to write diagnostics to the output. Any diagnostic information is included at the end of the test's results. This function does not return a value.

    ```
    test('top level test', (t) => {
      t.diagnostic('A diagnostic message');
    });
    ```

    @param message

    Message to be reported.
  + [plan](https://bun.com/reference/node/test/default/TestContext/plan)(

    count: number,

    options?: [TestContextPlanOptions](https://bun.com/reference/node/test/default/TestContextPlanOptions)

    ): void;

    This function is used to set the number of assertions and subtests that are expected to run within the test. If the number of assertions and subtests that run does not match the expected count, the test will fail.

    Note: To make sure assertions are tracked, `t.assert` must be used instead of `assert` directly.

    ```
    test('top level test', (t) => {
      t.plan(2);
      t.assert.ok('some relevant assertion here');
      t.test('subtest', () => {});
    });
    ```

    When working with asynchronous code, the `plan` function can be used to ensure that the correct number of assertions are run:

    ```
    test('planning with streams', (t, done) => {
      function* generate() {
        yield 'a';
        yield 'b';
        yield 'c';
      }
      const expected = ['a', 'b', 'c'];
      t.plan(expected.length);
      const stream = Readable.from(generate());
      stream.on('data', (chunk) => {
        t.assert.strictEqual(chunk, expected.shift());
      });

      stream.on('end', () => {
        done();
      });
    });
    ```

    When using the `wait` option, you can control how long the test will wait for the expected assertions. For example, setting a maximum wait time ensures that the test will wait for asynchronous assertions to complete within the specified timeframe:

    ```
    test('plan with wait: 2000 waits for async assertions', (t) => {
      t.plan(1, { wait: 2000 }); // Waits for up to 2 seconds for the assertion to complete.

      const asyncActivity = () => {
        setTimeout(() => {
             *       t.assert.ok(true, 'Async assertion completed within the wait time');
        }, 1000); // Completes after 1 second, within the 2-second wait time.
      };

      asyncActivity(); // The test will pass because the assertion is completed in time.
    });
    ```

    Note: If a `wait` timeout is specified, it begins counting down only after the test function finishes executing.
  + [runOnly](https://bun.com/reference/node/test/default/TestContext/runOnly)(

    shouldRunOnlyTests: boolean

    ): void;

    If `shouldRunOnlyTests` is truthy, the test context will only run tests that have the `only` option set. Otherwise, all tests are run. If Node.js was not started with the `--test-only` command-line option, this function is a no-op.

    ```
    test('top level test', (t) => {
      // The test context can be set to run subtests with the 'only' option.
      t.runOnly(true);
      return Promise.all([
        t.test('this subtest is now skipped'),
        t.test('this subtest is run', { only: true }),
      ]);
    });
    ```

    @param shouldRunOnlyTests

    Whether or not to run `only` tests.
  + [skip](https://bun.com/reference/node/test/default/TestContext/skip)(

    message?: string

    ): void;

    This function causes the test's output to indicate the test as skipped. If `message` is provided, it is included in the output. Calling `skip()` does not terminate execution of the test function. This function does not return a value.

    ```
    test('top level test', (t) => {
      // Make sure to return here as well if the test contains additional logic.
      t.skip('this is skipped');
    });
    ```

    @param message

    Optional skip message.
  + [todo](https://bun.com/reference/node/test/default/TestContext/todo)(

    message?: string

    ): void;

    This function adds a `TODO` directive to the test's output. If `message` is provided, it is included in the output. Calling `todo()` does not terminate execution of the test function. This function does not return a value.

    ```
    test('top level test', (t) => {
      // This test is marked as `TODO`
      t.todo('this is a todo');
    });
    ```

    @param message

    Optional `TODO` message.
  + [waitFor](https://bun.com/reference/node/test/default/TestContext/waitFor)<T>(

    condition: () => T,

    options?: [TestContextWaitForOptions](https://bun.com/reference/node/test/default/TestContextWaitForOptions)

    ): Promise<Awaited<T>>;

    This method polls a `condition` function until that function either returns successfully or the operation times out.

    @param condition

    An assertion function that is invoked periodically until it completes successfully or the defined polling timeout elapses. Successful completion is defined as not throwing or rejecting. This function does not accept any arguments, and is allowed to return any value.

    @param options

    An optional configuration object for the polling operation.

    @returns

    Fulfilled with the value returned by `condition`.

  ### interface [TestContextAssert](https://bun.com/reference/node/test/default/TestContextAssert)

  + [deepEqual](https://bun.com/reference/node/test/default/TestContextAssert/deepEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [deepStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/deepStrictEqual): (actual: unknown, expected: T, message?: string | [Error](https://bun.com/reference/globals/Error)) => asserts actual is T
  + [doesNotMatch](https://bun.com/reference/node/test/default/TestContextAssert/doesNotMatch): (value: string, regExp: RegExp, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [doesNotReject](https://bun.com/reference/node/test/default/TestContextAssert/doesNotReject): {(block: Promise<unknown> | () => Promise<unknown>, message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>; (block: Promise<unknown> | () => Promise<unknown>, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>}
  + [doesNotThrow](https://bun.com/reference/node/test/default/TestContextAssert/doesNotThrow): {(block: () => unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void; (block: () => unknown, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => void}
  + [equal](https://bun.com/reference/node/test/default/TestContextAssert/equal): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [fail](https://bun.com/reference/node/test/default/TestContextAssert/fail): {}
  + [ifError](https://bun.com/reference/node/test/default/TestContextAssert/ifError): (value: unknown) => asserts value is undefined | null
  + [match](https://bun.com/reference/node/test/default/TestContextAssert/match): (value: string, regExp: RegExp, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [notDeepEqual](https://bun.com/reference/node/test/default/TestContextAssert/notDeepEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [notDeepStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/notDeepStrictEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [notEqual](https://bun.com/reference/node/test/default/TestContextAssert/notEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [notStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/notStrictEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [ok](https://bun.com/reference/node/test/default/TestContextAssert/ok): (value: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => asserts value
  + [partialDeepStrictEqual](https://bun.com/reference/node/test/default/TestContextAssert/partialDeepStrictEqual): (actual: unknown, expected: unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void
  + [rejects](https://bun.com/reference/node/test/default/TestContextAssert/rejects): {(block: Promise<unknown> | () => Promise<unknown>, message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>; (block: Promise<unknown> | () => Promise<unknown>, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => Promise<void>}
  + [strictEqual](https://bun.com/reference/node/test/default/TestContextAssert/strictEqual): (actual: unknown, expected: T, message?: string | [Error](https://bun.com/reference/globals/Error)) => asserts actual is T
  + [throws](https://bun.com/reference/node/test/default/TestContextAssert/throws): {(block: () => unknown, message?: string | [Error](https://bun.com/reference/globals/Error)) => void; (block: () => unknown, error: [AssertPredicate](https://bun.com/reference/node/assert/default/AssertPredicate), message?: string | [Error](https://bun.com/reference/globals/Error)) => void}
  + [fileSnapshot](https://bun.com/reference/node/test/default/TestContextAssert/fileSnapshot)(

    value: any,

    path: string,

    options?: [AssertSnapshotOptions](https://bun.com/reference/node/test/default/AssertSnapshotOptions)

    ): void;

    This function serializes `value` and writes it to the file specified by `path`.

    ```
    test('snapshot test with default serialization', (t) => {
      t.assert.fileSnapshot({ value1: 1, value2: 2 }, './snapshots/snapshot.json');
    });
    ```

    This function differs from `context.assert.snapshot()` in the following ways:

    - The snapshot file path is explicitly provided by the user.
    - Each snapshot file is limited to a single snapshot value.
    - No additional escaping is performed by the test runner.

    These differences allow snapshot files to better support features such as syntax highlighting.

    @param value

    A value to serialize to a string. If Node.js was started with the [`--test-update-snapshots`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--test-update-snapshots) flag, the serialized value is written to `path`. Otherwise, the serialized value is compared to the contents of the existing snapshot file.

    @param path

    The file where the serialized `value` is written.

    @param options

    Optional configuration options.
  + [snapshot](https://bun.com/reference/node/test/default/TestContextAssert/snapshot)(

    value: any,

    options?: [AssertSnapshotOptions](https://bun.com/reference/node/test/default/AssertSnapshotOptions)

    ): void;

    This function implements assertions for snapshot testing.

    ```
    test('snapshot test with default serialization', (t) => {
      t.assert.snapshot({ value1: 1, value2: 2 });
    });

    test('snapshot test with custom serialization', (t) => {
      t.assert.snapshot({ value3: 3, value4: 4 }, {
        serializers: [(value) => JSON.stringify(value)]
      });
    });
    ```

    @param value

    A value to serialize to a string. If Node.js was started with the [`--test-update-snapshots`](https://nodejs.org/docs/latest-v24.x/api/cli.html#--test-update-snapshots) flag, the serialized value is written to the snapshot file. Otherwise, the serialized value is compared to the corresponding value in the existing snapshot file.

  ### interface [TestContextPlanOptions](https://bun.com/reference/node/test/default/TestContextPlanOptions)

  + [wait](https://bun.com/reference/node/test/default/TestContextPlanOptions/wait)?: number | boolean

    The wait time for the plan:

    - If `true`, the plan waits indefinitely for all assertions and subtests to run.
    - If `false`, the plan performs an immediate check after the test function completes, without waiting for any pending assertions or subtests. Any assertions or subtests that complete after this check will not be counted towards the plan.
    - If a number, it specifies the maximum wait time in milliseconds before timing out while waiting for expected assertions and subtests to be matched. If the timeout is reached, the test will fail.

  ### interface [TestContextWaitForOptions](https://bun.com/reference/node/test/default/TestContextWaitForOptions)

  + [interval](https://bun.com/reference/node/test/default/TestContextWaitForOptions/interval)?: number

    The number of milliseconds to wait after an unsuccessful invocation of `condition` before trying again.
  + [timeout](https://bun.com/reference/node/test/default/TestContextWaitForOptions/timeout)?: number

    The poll timeout in milliseconds. If `condition` has not succeeded by the time this elapses, an error occurs.

  ### interface [TestOptions](https://bun.com/reference/node/test/default/TestOptions)

  + [concurrency](https://bun.com/reference/node/test/default/TestOptions/concurrency)?: number | boolean

    If a number is provided, then that many tests would run in parallel. If truthy, it would run (number of cpu cores - 1) tests in parallel. For subtests, it will be `Infinity` tests in parallel. If falsy, it would only run one test at a time. If unspecified, subtests inherit this value from their parent.
  + [only](https://bun.com/reference/node/test/default/TestOptions/only)?: boolean

    If truthy, and the test context is configured to run `only` tests, then this test will be run. Otherwise, the test is skipped.
  + [plan](https://bun.com/reference/node/test/default/TestOptions/plan)?: number

    The number of assertions and subtests expected to be run in the test. If the number of assertions run in the test does not match the number specified in the plan, the test will fail.
  + [signal](https://bun.com/reference/node/test/default/TestOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    Allows aborting an in-progress test.
  + [skip](https://bun.com/reference/node/test/default/TestOptions/skip)?: string | boolean

    If truthy, the test is skipped. If a string is provided, that string is displayed in the test results as the reason for skipping the test.
  + [timeout](https://bun.com/reference/node/test/default/TestOptions/timeout)?: number

    A number of milliseconds the test will fail after. If unspecified, subtests inherit this value from their parent.
  + [todo](https://bun.com/reference/node/test/default/TestOptions/todo)?: string | boolean

    If truthy, the test marked as `TODO`. If a string is provided, that string is displayed in the test results as the reason why the test is `TODO`.

  ### interface [TestShard](https://bun.com/reference/node/test/default/TestShard)

  + [index](https://bun.com/reference/node/test/default/TestShard/index): number

    A positive integer between 1 and `total` that specifies the index of the shard to run.
  + [total](https://bun.com/reference/node/test/default/TestShard/total): number

    A positive integer that specifies the total number of shards to split the test files to.

  ### interface [TestsStream](https://bun.com/reference/node/test/default/TestsStream)

  A successful call to `run()` will return a new `TestsStream` object, streaming a series of events representing the execution of the tests.

  Some of the events are guaranteed to be emitted in the same order as the tests are defined, while others are emitted in the order that the tests execute.

  + readonly [closed](https://bun.com/reference/node/test/default/TestsStream/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/test/default/TestsStream/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/test/default/TestsStream/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/test/default/TestsStream/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/test/default/TestsStream/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/test/default/TestsStream/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/test/default/TestsStream/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/test/default/TestsStream/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/test/default/TestsStream/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/test/default/TestsStream/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/test/default/TestsStream/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/test/default/TestsStream/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [\_construct](https://bun.com/reference/node/test/default/TestsStream/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/test/default/TestsStream/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/test/default/TestsStream/_read)(

    size: number

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/test/default/TestsStream/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/test/default/TestsStream/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/test/default/TestsStream/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:coverage',

    listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:complete',

    listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:dequeue',

    listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:diagnostic',

    listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:enqueue',

    listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:fail',

    listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:pass',

    listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:plan',

    listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:start',

    listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:stderr',

    listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:stdout',

    listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:summary',

    listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:watch:drained',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: 'test:watch:restarted',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/test/default/TestsStream/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume
  + [asIndexedPairs](https://bun.com/reference/node/test/default/TestsStream/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [compose](https://bun.com/reference/node/test/default/TestsStream/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [destroy](https://bun.com/reference/node/test/default/TestsStream/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/test/default/TestsStream/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:coverage',

    data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:complete',

    data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:dequeue',

    data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:diagnostic',

    data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:enqueue',

    data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:fail',

    data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:pass',

    data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:plan',

    data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:start',

    data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:stderr',

    data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:stdout',

    data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:summary',

    data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:watch:drained'

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: 'test:watch:restarted'

    ): boolean;

    [emit](https://bun.com/reference/node/test/default/TestsStream/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/test/default/TestsStream/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/test/default/TestsStream/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/test/default/TestsStream/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/test/default/TestsStream/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/test/default/TestsStream/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/test/default/TestsStream/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/test/default/TestsStream/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/test/default/TestsStream/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/test/default/TestsStream/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/test/default/TestsStream/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/test/default/TestsStream/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/test/default/TestsStream/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/test/default/TestsStream/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/test/default/TestsStream/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:coverage',

    listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:complete',

    listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:dequeue',

    listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:diagnostic',

    listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:enqueue',

    listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:fail',

    listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:pass',

    listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:plan',

    listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:start',

    listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:stderr',

    listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:stdout',

    listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:summary',

    listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:watch:drained',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: 'test:watch:restarted',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/test/default/TestsStream/on)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:coverage',

    listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:complete',

    listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:dequeue',

    listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:diagnostic',

    listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:enqueue',

    listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:fail',

    listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:pass',

    listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:plan',

    listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:start',

    listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:stderr',

    listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:stdout',

    listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:summary',

    listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:watch:drained',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: 'test:watch:restarted',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/test/default/TestsStream/once)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/test/default/TestsStream/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/test/default/TestsStream/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:coverage',

    listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:complete',

    listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:dequeue',

    listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:diagnostic',

    listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:enqueue',

    listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:fail',

    listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:pass',

    listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:plan',

    listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:start',

    listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:stderr',

    listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:stdout',

    listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:summary',

    listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:watch:drained',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: 'test:watch:restarted',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/test/default/TestsStream/prependListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:coverage',

    listener: (data: [TestCoverage](https://bun.com/reference/node/test/default/EventData/TestCoverage)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:complete',

    listener: (data: [TestComplete](https://bun.com/reference/node/test/default/EventData/TestComplete)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:dequeue',

    listener: (data: [TestDequeue](https://bun.com/reference/node/test/default/EventData/TestDequeue)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:diagnostic',

    listener: (data: [TestDiagnostic](https://bun.com/reference/node/test/default/EventData/TestDiagnostic)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:enqueue',

    listener: (data: [TestEnqueue](https://bun.com/reference/node/test/default/EventData/TestEnqueue)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:fail',

    listener: (data: [TestFail](https://bun.com/reference/node/test/default/EventData/TestFail)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:pass',

    listener: (data: [TestPass](https://bun.com/reference/node/test/default/EventData/TestPass)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:plan',

    listener: (data: [TestPlan](https://bun.com/reference/node/test/default/EventData/TestPlan)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:start',

    listener: (data: [TestStart](https://bun.com/reference/node/test/default/EventData/TestStart)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:stderr',

    listener: (data: [TestStderr](https://bun.com/reference/node/test/default/EventData/TestStderr)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:stdout',

    listener: (data: [TestStdout](https://bun.com/reference/node/test/default/EventData/TestStdout)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:summary',

    listener: (data: [TestSummary](https://bun.com/reference/node/test/default/EventData/TestSummary)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:watch:drained',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: 'test:watch:restarted',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/test/default/TestsStream/prependOnceListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/test/default/TestsStream/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/test/default/TestsStream/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/test/default/TestsStream/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/test/default/TestsStream/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/test/default/TestsStream/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/test/default/TestsStream/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/test/default/TestsStream/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/test/default/TestsStream/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setEncoding](https://bun.com/reference/node/test/default/TestsStream/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/test/default/TestsStream/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/test/default/TestsStream/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/test/default/TestsStream/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/test/default/TestsStream/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [unpipe](https://bun.com/reference/node/test/default/TestsStream/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/test/default/TestsStream/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/test/default/TestsStream/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream

  type [HookFn](https://bun.com/reference/node/test/default/HookFn) = (c: [TestContext](https://bun.com/reference/node/test/default/TestContext) | [SuiteContext](https://bun.com/reference/node/test/default/SuiteContext), done: (result?: any) => void) => any

  The hook function. The first argument is the context in which the hook is called. If the hook uses callbacks, the callback function is passed as the second argument.

  type [Mock](https://bun.com/reference/node/test/default/Mock)<F extends Function> = F & { mock: [MockFunctionContext](https://bun.com/reference/node/test/default/MockFunctionContext)<F> }

  type [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn) = (s: [SuiteContext](https://bun.com/reference/node/test/default/SuiteContext)) => void | Promise<void>

  The type of a suite test function. The argument to this function is a SuiteContext object.

  type [TestContextHookFn](https://bun.com/reference/node/test/default/TestContextHookFn) = (t: [TestContext](https://bun.com/reference/node/test/default/TestContext), done: (result?: any) => void) => any

  The hook function. The first argument is a `TestContext` object. If the hook uses callbacks, the callback function is passed as the second argument.

  type [TestFn](https://bun.com/reference/node/test/default/TestFn) = (t: [TestContext](https://bun.com/reference/node/test/default/TestContext), done: (result?: any) => void) => void | Promise<void>

  The type of a function passed to test. The first argument to this function is a TestContext object. If the test uses callbacks, the callback function is passed as the second argument.

  const [mock](https://bun.com/reference/node/test/default/mock): [MockTracker](https://bun.com/reference/node/test/default/MockTracker)

  function [after](https://bun.com/reference/node/test/default/after)(

  fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

  options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

  ): void;

  This function creates a hook that runs after executing a suite.

  ```
  describe('tests', async () => {
    after(() => console.log('finished running tests'));
    it('is a subtest', () => {
      assert.ok('some relevant assertion here');
    });
  });
  ```

  @param fn

  The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

  @param options

  Configuration options for the hook.

  function [afterEach](https://bun.com/reference/node/test/default/afterEach)(

  fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

  options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

  ): void;

  This function creates a hook that runs after each test in the current suite. The `afterEach()` hook is run even if the test fails.

  ```
  describe('tests', async () => {
    afterEach(() => console.log('finished running a test'));
    it('is a subtest', () => {
      assert.ok('some relevant assertion here');
    });
  });
  ```

  @param fn

  The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

  @param options

  Configuration options for the hook.

  function [before](https://bun.com/reference/node/test/default/before)(

  fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

  options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

  ): void;

  This function creates a hook that runs before executing a suite.

  ```
  describe('tests', async () => {
    before(() => console.log('about to run some test'));
    it('is a subtest', () => {
      assert.ok('some relevant assertion here');
    });
  });
  ```

  @param fn

  The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

  @param options

  Configuration options for the hook.

  function [beforeEach](https://bun.com/reference/node/test/default/beforeEach)(

  fn?: [HookFn](https://bun.com/reference/node/test/default/HookFn),

  options?: [HookOptions](https://bun.com/reference/node/test/default/HookOptions)

  ): void;

  This function creates a hook that runs before each test in the current suite.

  ```
  describe('tests', async () => {
    beforeEach(() => console.log('about to run a test'));
    it('is a subtest', () => {
      assert.ok('some relevant assertion here');
    });
  });
  ```

  @param fn

  The hook function. If the hook uses callbacks, the callback function is passed as the second argument.

  @param options

  Configuration options for the hook.

  function [only](https://bun.com/reference/node/test/default/only)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.

  function [only](https://bun.com/reference/node/test/default/only)(

  name?: string,

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.

  function [only](https://bun.com/reference/node/test/default/only)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.

  function [only](https://bun.com/reference/node/test/default/only)(

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `only`. This is the same as calling test with `options.only` set to `true`.

  function [run](https://bun.com/reference/node/test/default/run)(

  options?: [RunOptions](https://bun.com/reference/node/test/default/RunOptions)

  ): [TestsStream](https://bun.com/reference/node/test/default/TestsStream);

  **Note:** `shard` is used to horizontally parallelize test running across machines or processes, ideal for large-scale executions across varied environments. It's incompatible with `watch` mode, tailored for rapid code iteration by automatically rerunning tests on file changes.

  ```
  import { tap } from 'node:test/reporters';
  import { run } from 'node:test';
  import process from 'node:process';
  import path from 'node:path';

  run({ files: [path.resolve('./tests/test.js')] })
    .compose(tap)
    .pipe(process.stdout);
  ```

  @param options

  Configuration options for running tests.

  function [skip](https://bun.com/reference/node/test/default/skip)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.

  function [skip](https://bun.com/reference/node/test/default/skip)(

  name?: string,

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.

  function [skip](https://bun.com/reference/node/test/default/skip)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.

  function [skip](https://bun.com/reference/node/test/default/skip)(

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for skipping a test. This is the same as calling test with `options.skip` set to `true`.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param name

  The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param options

  Configuration options for the suite. This supports the same options as test.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  name?: string,

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param name

  The name of the suite, which is displayed when reporting test results. Defaults to the `name` property of `fn`, or `'<anonymous>'` if `fn` does not have a name.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param options

  Configuration options for the suite. This supports the same options as test.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  function [suite](https://bun.com/reference/node/test/default/suite)(

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  The `suite()` function is imported from the `node:test` module.

  @param fn

  The suite function declaring nested tests and suites. The first argument to this function is a SuiteContext object.

  @returns

  Immediately fulfilled with `undefined`.

  function [only](https://bun.com/reference/node/test/default/suite/only)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

  function [only](https://bun.com/reference/node/test/default/suite/only)(

  name?: string,

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

  function [only](https://bun.com/reference/node/test/default/suite/only)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

  function [only](https://bun.com/reference/node/test/default/suite/only)(

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `only`. This is the same as calling suite with `options.only` set to `true`.

  function [skip](https://bun.com/reference/node/test/default/suite/skip)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

  function [skip](https://bun.com/reference/node/test/default/suite/skip)(

  name?: string,

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

  function [skip](https://bun.com/reference/node/test/default/suite/skip)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

  function [skip](https://bun.com/reference/node/test/default/suite/skip)(

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for skipping a suite. This is the same as calling suite with `options.skip` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/suite/todo)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/suite/todo)(

  name?: string,

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/suite/todo)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/suite/todo)(

  fn?: [SuiteFn](https://bun.com/reference/node/test/default/SuiteFn)

  ): Promise<void>;

  Shorthand for marking a suite as `TODO`. This is the same as calling suite with `options.todo` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/todo)(

  name?: string,

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/todo)(

  name?: string,

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/todo)(

  options?: [TestOptions](https://bun.com/reference/node/test/default/TestOptions),

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.

  function [todo](https://bun.com/reference/node/test/default/todo)(

  fn?: [TestFn](https://bun.com/reference/node/test/default/TestFn)

  ): Promise<void>;

  Shorthand for marking a test as `TODO`. This is the same as calling test with `options.todo` set to `true`.