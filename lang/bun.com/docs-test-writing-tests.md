---
url: https://bun.com/docs/test/writing-tests
title: Writing tests - Bun
source_domain: bun.com
---

# Writing tests - Bun

Define tests with a Jest-like API imported from the built-in `bun:test` module. Long term, Bun aims for complete Jest compatibility; at the moment, a limited set of expect matchers are supported.

## [​](https://bun.com/docs/test/writing-tests#basic-usage) Basic Usage

To define a simple test:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { expect, test } from "bun:test";

test("2 + 2", () => {
  expect(2 + 2).toBe(4);
});
```

### [​](https://bun.com/docs/test/writing-tests#grouping-tests) Grouping Tests

Tests can be grouped into suites with `describe`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { expect, test, describe } from "bun:test";

describe("arithmetic", () => {
  test("2 + 2", () => {
    expect(2 + 2).toBe(4);
  });

  test("2 * 2", () => {
    expect(2 * 2).toBe(4);
  });
});
```

### [​](https://bun.com/docs/test/writing-tests#async-tests) Async Tests

Tests can be async.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { expect, test } from "bun:test";

test("2 * 2", async () => {
  const result = await Promise.resolve(2 * 2);
  expect(result).toEqual(4);
});
```

Alternatively, use the `done` callback to signal completion. If you include the `done` callback as a parameter in your test definition, you must call it or the test will hang.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { expect, test } from "bun:test";

test("2 * 2", done => {
  Promise.resolve(2 * 2).then(result => {
    expect(result).toEqual(4);
    done();
  });
});
```

## [​](https://bun.com/docs/test/writing-tests#timeouts) Timeouts

Optionally specify a per-test timeout in milliseconds by passing a number as the third argument to `test`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { test } from "bun:test";

test("wat", async () => {
  const data = await slowOperation();
  expect(data).toBe(42);
}, 500); // test must run in <500ms
```

In `bun:test`, test timeouts throw an uncatchable exception to force the test to stop running and fail. We also kill any child processes that were spawned in the test to avoid leaving behind zombie processes lurking in the background.
The default timeout for each test is 5000ms (5 seconds) if not overridden by this timeout option or `jest.setDefaultTimeout()`.

## [​](https://bun.com/docs/test/writing-tests#retries-and-repeats) Retries and Repeats

### [​](https://bun.com/docs/test/writing-tests#test-retry) test.retry

Use the `retry` option to automatically retry a test if it fails. The test passes if it succeeds within the specified number of attempts. This is useful for flaky tests that may fail intermittently.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
import { test } from "bun:test";

test(
  "flaky network request",
  async () => {
    const response = await fetch("https://example.com/api");
    expect(response.ok).toBe(true);
  },
  { retry: 3 }, // Retry up to 3 times if the test fails
);
```

### [​](https://bun.com/docs/test/writing-tests#test-repeats) test.repeats

Use the `repeats` option to run a test multiple times regardless of pass/fail status. The test fails if any iteration fails. This is useful for detecting flaky tests or stress testing. Note that `repeats: N` runs the test N+1 times total (1 initial run + N repeats).

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
import { test } from "bun:test";

test(
  "ensure test is stable",
  () => {
    expect(Math.random()).toBeLessThan(1);
  },
  { repeats: 20 }, // Runs 21 times total (1 initial + 20 repeats)
);
```

You cannot use both `retry` and `repeats` on the same test.

### [​](https://bun.com/docs/test/writing-tests#🧟-zombie-process-killer) 🧟 Zombie Process Killer

When a test times out and processes spawned in the test via `Bun.spawn`, `Bun.spawnSync`, or `node:child_process` are not killed, they will be automatically killed and a message will be logged to the console. This prevents zombie processes from lingering in the background after timed-out tests.

## [​](https://bun.com/docs/test/writing-tests#test-modifiers) Test Modifiers

### [​](https://bun.com/docs/test/writing-tests#test-skip) test.skip

Skip individual tests with `test.skip`. These tests will not be run.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { expect, test } from "bun:test";

test.skip("wat", () => {
  // TODO: fix this
  expect(0.1 + 0.2).toEqual(0.3);
});
```

### [​](https://bun.com/docs/test/writing-tests#test-todo) test.todo

Mark a test as a todo with `test.todo`. These tests will not be run.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
import { expect, test } from "bun:test";

test.todo("fix this", () => {
  myTestFunction();
});
```

To run todo tests and find any which are passing, use `bun test --todo`.

terminal

Copy

```
bun test --todo
```

Copy

```
my.test.ts:
✗ unimplemented feature
  ^ this test is marked as todo but passes. Remove `.todo` or check that test is correct.

 0 pass
 1 fail
 1 expect() calls
```

With this flag, failing todo tests will not cause an error, but todo tests which pass will be marked as failing so you can remove the todo mark or fix the test.

### [​](https://bun.com/docs/test/writing-tests#test-only) test.only

To run a particular test or suite of tests use `test.only()` or `describe.only()`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
import { test, describe } from "bun:test";

test("test #1", () => {
  // does not run
});

test.only("test #2", () => {
  // runs
});

describe.only("only", () => {
  test("test #3", () => {
    // runs
  });
});
```

The following command will only execute tests #2 and #3.

terminal

Copy

```
bun test --only
```

The following command will only execute tests #1, #2 and #3.

terminal

Copy

```
bun test
```

### [​](https://bun.com/docs/test/writing-tests#test-if) test.if

To run a test conditionally, use `test.if()`. The test will run if the condition is truthy. This is particularly useful for tests that should only run on specific architectures or operating systems.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
test.if(Math.random() > 0.5)("runs half the time", () => {
  // ...
});

const macOS = process.platform === "darwin";
test.if(macOS)("runs on macOS", () => {
  // runs if macOS
});
```

### [​](https://bun.com/docs/test/writing-tests#test-skipif) test.skipIf

To instead skip a test based on some condition, use `test.skipIf()` or `describe.skipIf()`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
const macOS = process.platform === "darwin";

test.skipIf(macOS)("runs on non-macOS", () => {
  // runs if *not* macOS
});
```

### [​](https://bun.com/docs/test/writing-tests#test-todoif) test.todoIf

If instead you want to mark the test as TODO, use `test.todoIf()` or `describe.todoIf()`. Carefully choosing `skipIf` or `todoIf` can show a difference between, for example, intent of “invalid for this target” and “planned but not implemented yet.”

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
const macOS = process.platform === "darwin";

// TODO: we've only implemented this for Linux so far.
test.todoIf(macOS)("runs on posix", () => {
  // runs if *not* macOS
});
```

### [​](https://bun.com/docs/test/writing-tests#test-failing) test.failing

Use `test.failing()` when you know a test is currently failing but you want to track it and be notified when it starts passing. This inverts the test result:

* A failing test marked with `.failing()` will pass
* A passing test marked with `.failing()` will fail (with a message indicating it’s now passing and should be fixed)

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
// This will pass because the test is failing as expected
test.failing("math is broken", () => {
  expect(0.1 + 0.2).toBe(0.3); // fails due to floating point precision
});

// This will fail with a message that the test is now passing
test.failing("fixed bug", () => {
  expect(1 + 1).toBe(2); // passes, but we expected it to fail
});
```

This is useful for tracking known bugs that you plan to fix later, or for implementing test-driven development.

## [​](https://bun.com/docs/test/writing-tests#conditional-tests-for-describe-blocks) Conditional Tests for Describe Blocks

The conditional modifiers `.if()`, `.skipIf()`, and `.todoIf()` can also be applied to describe blocks, affecting all tests within the suite:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
const isMacOS = process.platform === "darwin";

// Only runs the entire suite on macOS
describe.if(isMacOS)("macOS-specific features", () => {
  test("feature A", () => {
    // only runs on macOS
  });

  test("feature B", () => {
    // only runs on macOS
  });
});

// Skips the entire suite on Windows
describe.skipIf(process.platform === "win32")("Unix features", () => {
  test("feature C", () => {
    // skipped on Windows
  });
});

// Marks the entire suite as TODO on Linux
describe.todoIf(process.platform === "linux")("Upcoming Linux support", () => {
  test("feature D", () => {
    // marked as TODO on Linux
  });
});
```

## [​](https://bun.com/docs/test/writing-tests#parametrized-tests) Parametrized Tests

### [​](https://bun.com/docs/test/writing-tests#test-each-and-describe-each) `test.each` and `describe.each`

To run the same test with multiple sets of data, use `test.each`. This creates a parametrized test that runs once for each test case provided.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
const cases = [
  [1, 2, 3],
  [3, 4, 7],
];

test.each(cases)("%p + %p should be %p", (a, b, expected) => {
  expect(a + b).toBe(expected);
});
```

You can also use `describe.each` to create a parametrized suite that runs once for each test case:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)sum.test.ts

Copy

```
describe.each([
  [1, 2, 3],
  [3, 4, 7],
])("add(%i, %i)", (a, b, expected) => {
  test(`returns ${expected}`, () => {
    expect(a + b).toBe(expected);
  });

  test(`sum is greater than each value`, () => {
    expect(a + b).toBeGreaterThan(a);
    expect(a + b).toBeGreaterThan(b);
  });
});
```

### [​](https://bun.com/docs/test/writing-tests#argument-passing) Argument Passing

How arguments are passed to your test function depends on the structure of your test cases:

* If a table row is an array (like `[1, 2, 3]`), each element is passed as an individual argument
* If a row is not an array (like an object), it’s passed as a single argument

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
// Array items passed as individual arguments
test.each([
  [1, 2, 3],
  [4, 5, 9],
])("add(%i, %i) = %i", (a, b, expected) => {
  expect(a + b).toBe(expected);
});

// Object items passed as a single argument
test.each([
  { a: 1, b: 2, expected: 3 },
  { a: 4, b: 5, expected: 9 },
])("add($a, $b) = $expected", data => {
  expect(data.a + data.b).toBe(data.expected);
});
```

### [​](https://bun.com/docs/test/writing-tests#format-specifiers) Format Specifiers

There are a number of options available for formatting the test title:

| Specifier | Description |
| --- | --- |
| `%p` | pretty-format |
| `%s` | String |
| `%d` | Number |
| `%i` | Integer |
| `%f` | Floating point |
| `%j` | JSON |
| `%o` | Object |
| `%#` | Index of the test case |
| `%%` | Single percent sign (%) |

#### [​](https://bun.com/docs/test/writing-tests#examples) Examples

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
// Basic specifiers
test.each([
  ["hello", 123],
  ["world", 456],
])("string: %s, number: %i", (str, num) => {
  // "string: hello, number: 123"
  // "string: world, number: 456"
});

// %p for pretty-format output
test.each([
  [{ name: "Alice" }, { a: 1, b: 2 }],
  [{ name: "Bob" }, { x: 5, y: 10 }],
])("user %p with data %p", (user, data) => {
  // "user { name: 'Alice' } with data { a: 1, b: 2 }"
  // "user { name: 'Bob' } with data { x: 5, y: 10 }"
});

// %# for index
test.each(["apple", "banana"])("fruit #%# is %s", fruit => {
  // "fruit #0 is apple"
  // "fruit #1 is banana"
});
```

## [​](https://bun.com/docs/test/writing-tests#assertion-counting) Assertion Counting

Bun supports verifying that a specific number of assertions were called during a test:

### [​](https://bun.com/docs/test/writing-tests#expect-hasassertions) expect.hasAssertions()

Use `expect.hasAssertions()` to verify that at least one assertion is called during a test:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
test("async work calls assertions", async () => {
  expect.hasAssertions(); // Will fail if no assertions are called

  const data = await fetchData();
  expect(data).toBeDefined();
});
```

This is especially useful for async tests to ensure your assertions actually run.

### [​](https://bun.com/docs/test/writing-tests#expect-assertions-count) expect.assertions(count)

Use `expect.assertions(count)` to verify that a specific number of assertions are called during a test:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
test("exactly two assertions", () => {
  expect.assertions(2); // Will fail if not exactly 2 assertions are called

  expect(1 + 1).toBe(2);
  expect("hello").toContain("ell");
});
```

This helps ensure all your assertions run, especially in complex async code with multiple code paths.

## [​](https://bun.com/docs/test/writing-tests#type-testing) Type Testing

Bun includes `expectTypeOf` for testing TypeScript types, compatible with Vitest.

### [​](https://bun.com/docs/test/writing-tests#expecttypeof) expectTypeOf

These functions are no-ops at runtime - you need to run TypeScript separately to verify the type checks.

The `expectTypeOf` function provides type-level assertions that are checked by TypeScript’s type checker. To test your types:

1. Write your type assertions using `expectTypeOf`
2. Run `bunx tsc --noEmit` to check that your types are correct

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
import { expectTypeOf } from "bun:test";

// Basic type assertions
expectTypeOf<string>().toEqualTypeOf<string>();
expectTypeOf(123).toBeNumber();
expectTypeOf("hello").toBeString();

// Object type matching
expectTypeOf({ a: 1, b: "hello" }).toMatchObjectType<{ a: number }>();

// Function types
function greet(name: string): string {
  return `Hello ${name}`;
}

expectTypeOf(greet).toBeFunction();
expectTypeOf(greet).parameters.toEqualTypeOf<[string]>();
expectTypeOf(greet).returns.toEqualTypeOf<string>();

// Array types
expectTypeOf([1, 2, 3]).items.toBeNumber();

// Promise types
expectTypeOf(Promise.resolve(42)).resolves.toBeNumber();
```

For full documentation on expectTypeOf matchers, see the [API Reference](https://bun.com/reference/bun/test/expectTypeOf).

## [​](https://bun.com/docs/test/writing-tests#matchers) Matchers

Bun implements the following matchers. Full Jest compatibility is on the roadmap; [track progress here](https://github.com/oven-sh/bun/issues/1825).

### [​](https://bun.com/docs/test/writing-tests#basic-matchers) Basic Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.not` |
| ✅ | `.toBe()` |
| ✅ | `.toEqual()` |
| ✅ | `.toBeNull()` |
| ✅ | `.toBeUndefined()` |
| ✅ | `.toBeNaN()` |
| ✅ | `.toBeDefined()` |
| ✅ | `.toBeFalsy()` |
| ✅ | `.toBeTruthy()` |
| ✅ | `.toStrictEqual()` |

### [​](https://bun.com/docs/test/writing-tests#string-and-array-matchers) String and Array Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.toContain()` |
| ✅ | `.toHaveLength()` |
| ✅ | `.toMatch()` |
| ✅ | `.toContainEqual()` |
| ✅ | `.stringContaining()` |
| ✅ | `.stringMatching()` |
| ✅ | `.arrayContaining()` |

### [​](https://bun.com/docs/test/writing-tests#object-matchers) Object Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.toHaveProperty()` |
| ✅ | `.toMatchObject()` |
| ✅ | `.toContainAllKeys()` |
| ✅ | `.toContainValue()` |
| ✅ | `.toContainValues()` |
| ✅ | `.toContainAllValues()` |
| ✅ | `.toContainAnyValues()` |
| ✅ | `.objectContaining()` |

### [​](https://bun.com/docs/test/writing-tests#number-matchers) Number Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.toBeCloseTo()` |
| ✅ | `.closeTo()` |
| ✅ | `.toBeGreaterThan()` |
| ✅ | `.toBeGreaterThanOrEqual()` |
| ✅ | `.toBeLessThan()` |
| ✅ | `.toBeLessThanOrEqual()` |

### [​](https://bun.com/docs/test/writing-tests#function-and-class-matchers) Function and Class Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.toThrow()` |
| ✅ | `.toBeInstanceOf()` |

### [​](https://bun.com/docs/test/writing-tests#promise-matchers) Promise Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.resolves()` |
| ✅ | `.rejects()` |

### [​](https://bun.com/docs/test/writing-tests#mock-function-matchers) Mock Function Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.toHaveBeenCalled()` |
| ✅ | `.toHaveBeenCalledTimes()` |
| ✅ | `.toHaveBeenCalledWith()` |
| ✅ | `.toHaveBeenLastCalledWith()` |
| ✅ | `.toHaveBeenNthCalledWith()` |
| ✅ | `.toHaveReturned()` |
| ✅ | `.toHaveReturnedTimes()` |
| ✅ | `.toHaveReturnedWith()` |
| ✅ | `.toHaveLastReturnedWith()` |
| ✅ | `.toHaveNthReturnedWith()` |

### [​](https://bun.com/docs/test/writing-tests#snapshot-matchers) Snapshot Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.toMatchSnapshot()` |
| ✅ | `.toMatchInlineSnapshot()` |
| ✅ | `.toThrowErrorMatchingSnapshot()` |
| ✅ | `.toThrowErrorMatchingInlineSnapshot()` |

### [​](https://bun.com/docs/test/writing-tests#utility-matchers) Utility Matchers

| Status | Matcher |
| --- | --- |
| ✅ | `.extend` |
| ✅ | `.anything()` |
| ✅ | `.any()` |
| ✅ | `.assertions()` |
| ✅ | `.hasAssertions()` |

### [​](https://bun.com/docs/test/writing-tests#not-yet-implemented) Not Yet Implemented

| Status | Matcher |
| --- | --- |
| ❌ | `.addSnapshotSerializer()` |

## [​](https://bun.com/docs/test/writing-tests#best-practices) Best Practices

### [​](https://bun.com/docs/test/writing-tests#use-descriptive-test-names) Use Descriptive Test Names

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
// Good
test("should calculate total price including tax for multiple items", () => {
  // test implementation
});

// Avoid
test("price calculation", () => {
  // test implementation
});
```

### [​](https://bun.com/docs/test/writing-tests#group-related-tests) Group Related Tests

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)auth.test.ts

Copy

```
describe("User authentication", () => {
  describe("with valid credentials", () => {
    test("should return user data", () => {
      // test implementation
    });

    test("should set authentication token", () => {
      // test implementation
    });
  });

  describe("with invalid credentials", () => {
    test("should throw authentication error", () => {
      // test implementation
    });
  });
});
```

### [​](https://bun.com/docs/test/writing-tests#use-appropriate-matchers) Use Appropriate Matchers

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)auth.test.ts

Copy

```
// Good: Use specific matchers
expect(users).toHaveLength(3);
expect(user.email).toContain("@");
expect(response.status).toBeGreaterThanOrEqual(200);

// Avoid: Using toBe for everything
expect(users.length === 3).toBe(true);
expect(user.email.includes("@")).toBe(true);
expect(response.status >= 200).toBe(true);
```

### [​](https://bun.com/docs/test/writing-tests#test-error-conditions) Test Error Conditions

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
test("should throw error for invalid input", () => {
  expect(() => {
    validateEmail("not-an-email");
  }).toThrow("Invalid email format");
});

test("should handle async errors", async () => {
  await expect(async () => {
    await fetchUser("invalid-id");
  }).rejects.toThrow("User not found");
});
```

### [​](https://bun.com/docs/test/writing-tests#use-setup-and-teardown) Use Setup and Teardown

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)example.test.ts

Copy

```
import { beforeEach, afterEach, test } from "bun:test";

let testUser;

beforeEach(() => {
  testUser = createTestUser();
});

afterEach(() => {
  cleanupTestUser(testUser);
});

test("should update user profile", () => {
  // Use testUser in test
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test/writing-tests.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test/writing-tests)

⌘I