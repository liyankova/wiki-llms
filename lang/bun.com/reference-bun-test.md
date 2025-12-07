---
url: https://bun.com/reference/bun/test
title: bun:test module | API Reference | Bun
source_domain: bun.com
---

# bun:test module | API Reference | Bun

module

# [bun:test](https://bun.com/reference/bun/test)

The `'bun:test'` module is a fast, built-in test runner that aims for Jest compatibility. Tests are executed with the Bun runtime, providing significantly improved performance over traditional test runners.

Key features include TypeScript and JSX support, lifecycle hooks (`beforeAll`, `beforeEach`, `afterEach`, `afterAll`), snapshot testing, UI & DOM testing, watch mode, and script pre-loading. The API supports test assertions with `expect`, test grouping with `describe`, mocks, and more.

While Bun aims for compatibility with Jest, not everything is implemented yet. Use `bun test` to automatically discover and run tests matching common patterns like `*.test.ts` or `*.spec.js`.

* ### namespace [jest](https://bun.com/reference/bun/test/jest)

  + type [Mock](https://bun.com/reference/bun/test/jest/Mock)<T extends (...args: any[]) => any = (...args: any[]) => any> = JestMock.Mock<T>

    Constructs the type of a mock function, e.g. the return type of `jest.fn()`.
  + type [Replaced](https://bun.com/reference/bun/test/jest/Replaced)<T> = JestMock.Replaced<T>

    Constructs the type of a replaced property.
  + type [Spied](https://bun.com/reference/bun/test/jest/Spied)<T extends JestMock.ClassLike | (...args: any[]) => any> = JestMock.Spied<T>

    Constructs the type of a spied class or function.
  + type [SpiedClass](https://bun.com/reference/bun/test/jest/SpiedClass)<T extends JestMock.ClassLike> = JestMock.SpiedClass<T>

    Constructs the type of a spied class.
  + type [SpiedFunction](https://bun.com/reference/bun/test/jest/SpiedFunction)<T extends (...args: any[]) => any> = JestMock.SpiedFunction<T>

    Constructs the type of a spied function.
  + type [SpiedGetter](https://bun.com/reference/bun/test/jest/SpiedGetter)<T> = JestMock.SpiedGetter<T>

    Constructs the type of a spied getter.
  + type [SpiedSetter](https://bun.com/reference/bun/test/jest/SpiedSetter)<T> = JestMock.SpiedSetter<T>

    Constructs the type of a spied setter.
  + function [advanceTimersByTime](https://bun.com/reference/bun/test/jest/advanceTimersByTime)(

    milliseconds: number

    ): { advanceTimersByTime: (milliseconds: number) => unknown; advanceTimersToNextTimer: () => unknown; clearAllMocks: () => void; clearAllTimers: () => void; fn: (func?: T) => [Mock](https://bun.com/reference/bun/test/jest/Mock)<T>; getTimerCount: () => number; isFakeTimers: () => boolean; mock: (id: string, factory: () => any) => void | Promise<void>; resetAllMocks: () => void; restoreAllMocks: () => void; runAllTimers: () => unknown; runOnlyPendingTimers: () => unknown; spyOn: (obj: T, methodOrPropertyValue: K) => [Mock](https://bun.com/reference/bun/test/Mock)<Extract<T[K], (...args: any[]) => any>>; useFakeTimers: (options?: { now: number | Date }) => unknown; useRealTimers: () => unknown };
  + function [advanceTimersToNextTimer](https://bun.com/reference/bun/test/jest/advanceTimersToNextTimer)(): { advanceTimersByTime: (milliseconds: number) => unknown; advanceTimersToNextTimer: () => unknown; clearAllMocks: () => void; clearAllTimers: () => void; fn: (func?: T) => [Mock](https://bun.com/reference/bun/test/jest/Mock)<T>; getTimerCount: () => number; isFakeTimers: () => boolean; mock: (id: string, factory: () => any) => void | Promise<void>; resetAllMocks: () => void; restoreAllMocks: () => void; runAllTimers: () => unknown; runOnlyPendingTimers: () => unknown; spyOn: (obj: T, methodOrPropertyValue: K) => [Mock](https://bun.com/reference/bun/test/Mock)<Extract<T[K], (...args: any[]) => any>>; useFakeTimers: (options?: { now: number | Date }) => unknown; useRealTimers: () => unknown };
  + function [clearAllMocks](https://bun.com/reference/bun/test/jest/clearAllMocks)(): void;
  + function [clearAllTimers](https://bun.com/reference/bun/test/jest/clearAllTimers)(): void;
  + function [fn](https://bun.com/reference/bun/test/jest/fn)<T extends (...args: any[]) => any>(

    func?: T

    ): [Mock](https://bun.com/reference/bun/test/jest/Mock)<T>;
  + function [getTimerCount](https://bun.com/reference/bun/test/jest/getTimerCount)(): number;
  + function [isFakeTimers](https://bun.com/reference/bun/test/jest/isFakeTimers)(): boolean;
  + function [resetAllMocks](https://bun.com/reference/bun/test/jest/resetAllMocks)(): void;
  + function [restoreAllMocks](https://bun.com/reference/bun/test/jest/restoreAllMocks)(): void;
  + function [runAllTimers](https://bun.com/reference/bun/test/jest/runAllTimers)(): { advanceTimersByTime: (milliseconds: number) => unknown; advanceTimersToNextTimer: () => unknown; clearAllMocks: () => void; clearAllTimers: () => void; fn: (func?: T) => [Mock](https://bun.com/reference/bun/test/jest/Mock)<T>; getTimerCount: () => number; isFakeTimers: () => boolean; mock: (id: string, factory: () => any) => void | Promise<void>; resetAllMocks: () => void; restoreAllMocks: () => void; runAllTimers: () => unknown; runOnlyPendingTimers: () => unknown; spyOn: (obj: T, methodOrPropertyValue: K) => [Mock](https://bun.com/reference/bun/test/Mock)<Extract<T[K], (...args: any[]) => any>>; useFakeTimers: (options?: { now: number | Date }) => unknown; useRealTimers: () => unknown };
  + function [runOnlyPendingTimers](https://bun.com/reference/bun/test/jest/runOnlyPendingTimers)(): { advanceTimersByTime: (milliseconds: number) => unknown; advanceTimersToNextTimer: () => unknown; clearAllMocks: () => void; clearAllTimers: () => void; fn: (func?: T) => [Mock](https://bun.com/reference/bun/test/jest/Mock)<T>; getTimerCount: () => number; isFakeTimers: () => boolean; mock: (id: string, factory: () => any) => void | Promise<void>; resetAllMocks: () => void; restoreAllMocks: () => void; runAllTimers: () => unknown; runOnlyPendingTimers: () => unknown; spyOn: (obj: T, methodOrPropertyValue: K) => [Mock](https://bun.com/reference/bun/test/Mock)<Extract<T[K], (...args: any[]) => any>>; useFakeTimers: (options?: { now: number | Date }) => unknown; useRealTimers: () => unknown };
  + function [setSystemTime](https://bun.com/reference/bun/test/jest/setSystemTime)(

    now?: number | Date

    ): void;
  + function [setTimeout](https://bun.com/reference/bun/test/jest/setTimeout)(

    milliseconds: number

    ): void;
  + function [spyOn](https://bun.com/reference/bun/test/jest/spyOn)<T extends object, K extends string | number | symbol>(

    obj: T,

    methodOrPropertyValue: K

    ): [Mock](https://bun.com/reference/bun/test/jest/Mock)<Extract<T[K], (...args: any[]) => any>>;
  + function [useFakeTimers](https://bun.com/reference/bun/test/jest/useFakeTimers)(

    options?: { now: number | Date }

    ): { advanceTimersByTime: (milliseconds: number) => unknown; advanceTimersToNextTimer: () => unknown; clearAllMocks: () => void; clearAllTimers: () => void; fn: (func?: T) => [Mock](https://bun.com/reference/bun/test/jest/Mock)<T>; getTimerCount: () => number; isFakeTimers: () => boolean; mock: (id: string, factory: () => any) => void | Promise<void>; resetAllMocks: () => void; restoreAllMocks: () => void; runAllTimers: () => unknown; runOnlyPendingTimers: () => unknown; spyOn: (obj: T, methodOrPropertyValue: K) => [Mock](https://bun.com/reference/bun/test/Mock)<Extract<T[K], (...args: any[]) => any>>; useFakeTimers: (options?: { now: number | Date }) => unknown; useRealTimers: () => unknown };
  + function [useRealTimers](https://bun.com/reference/bun/test/jest/useRealTimers)(): { advanceTimersByTime: (milliseconds: number) => unknown; advanceTimersToNextTimer: () => unknown; clearAllMocks: () => void; clearAllTimers: () => void; fn: (func?: T) => [Mock](https://bun.com/reference/bun/test/jest/Mock)<T>; getTimerCount: () => number; isFakeTimers: () => boolean; mock: (id: string, factory: () => any) => void | Promise<void>; resetAllMocks: () => void; restoreAllMocks: () => void; runAllTimers: () => unknown; runOnlyPendingTimers: () => unknown; spyOn: (obj: T, methodOrPropertyValue: K) => [Mock](https://bun.com/reference/bun/test/Mock)<Extract<T[K], (...args: any[]) => any>>; useFakeTimers: (options?: { now: number | Date }) => unknown; useRealTimers: () => unknown };
* const [describe](https://bun.com/reference/bun/test/describe): [Describe](https://bun.com/reference/bun/test/Describe)<[]>

  Describes a group of related tests.

  ```
  function sum(a, b) {
    return a + b;
  }
  describe("sum()", () => {
    test("can sum two values", () => {
      expect(sum(1, 1)).toBe(2);
    });
  });
  ```
* const [expect](https://bun.com/reference/bun/test/expect): [Expect](https://bun.com/reference/bun/test/Expect)

  Asserts that a value matches some criteria.

  ```
  expect(1 + 1).toBe(2);
  expect([1,2,3]).toContain(2);
  expect(null).toBeNull();
  ```
* const [expectTypeOf](https://bun.com/reference/bun/test/expectTypeOf): expectTypeOf
* const [mock](https://bun.com/reference/bun/test/mock): (Function?: T) => [Mock](https://bun.com/reference/bun/test/Mock)<T>
* const [test](https://bun.com/reference/bun/test/test): [Test](https://bun.com/reference/bun/test/Test)<[]>

  Runs a test.

  ```
  test("can check if using Bun", () => {
    expect(Bun).toBeDefined();
  });

  test("can make a fetch() request", async () => {
    const response = await fetch("https://example.com/");
    expect(response.ok).toBe(true);
  });
  ```
* const [vi](https://bun.com/reference/bun/test/vi): { advanceTimersByTime: typeof [jest.advanceTimersByTime](https://bun.com/reference/bun/test/jest/advanceTimersByTime); advanceTimersToNextTimer: typeof [jest.advanceTimersToNextTimer](https://bun.com/reference/bun/test/jest/advanceTimersToNextTimer); clearAllMocks: typeof [jest.clearAllMocks](https://bun.com/reference/bun/test/jest/clearAllMocks); clearAllTimers: typeof [jest.clearAllTimers](https://bun.com/reference/bun/test/jest/clearAllTimers); fn: typeof [jest.fn](https://bun.com/reference/bun/test/jest/fn); getTimerCount: typeof [jest.getTimerCount](https://bun.com/reference/bun/test/jest/getTimerCount); isFakeTimers: typeof [jest.isFakeTimers](https://bun.com/reference/bun/test/jest/isFakeTimers); mock: typeof mock.module; resetAllMocks: typeof [jest.resetAllMocks](https://bun.com/reference/bun/test/jest/resetAllMocks); restoreAllMocks: typeof [jest.restoreAllMocks](https://bun.com/reference/bun/test/jest/restoreAllMocks); runAllTimers: typeof [jest.runAllTimers](https://bun.com/reference/bun/test/jest/runAllTimers); runOnlyPendingTimers: typeof [jest.runOnlyPendingTimers](https://bun.com/reference/bun/test/jest/runOnlyPendingTimers); spyOn: typeof [spyOn](https://bun.com/reference/bun/test/spyOn); useFakeTimers: typeof [jest.useFakeTimers](https://bun.com/reference/bun/test/jest/useFakeTimers); useRealTimers: typeof [jest.useRealTimers](https://bun.com/reference/bun/test/jest/useRealTimers) }

  Vitest-compatible mocking utilities Provides Vitest-style mocking API for easier migration from Vitest to Bun
* const [xdescribe](https://bun.com/reference/bun/test/xdescribe): [Describe](https://bun.com/reference/bun/test/Describe)<[]>

  Skips a group of related tests.

  This is equivalent to calling `describe.skip()`.
* const [xtest](https://bun.com/reference/bun/test/xtest): [Test](https://bun.com/reference/bun/test/Test)<[]>

  Skips a test.

  This is equivalent to calling `test.skip()`.
* function [afterAll](https://bun.com/reference/bun/test/afterAll)(

  fn: () => void | Promise<unknown> | (done: (err?: unknown) => void) => void,

  options?: HookOptions

  ): void;

  Runs a function, once, after all the tests.

  This is useful for running clean up tasks, like closing a socket or deleting temporary files.

  @param fn

  the function to run

  ```
  let database;
  afterAll(async () => {
    if (database) {
      await database.close();
    }
  });
  ```
* function [afterEach](https://bun.com/reference/bun/test/afterEach)(

  fn: () => void | Promise<unknown> | (done: (err?: unknown) => void) => void,

  options?: HookOptions

  ): void;

  Runs a function after each test.

  This is useful for running clean up tasks, like closing a socket or deleting temporary files.

  @param fn

  the function to run
* function [beforeAll](https://bun.com/reference/bun/test/beforeAll)(

  fn: () => void | Promise<unknown> | (done: (err?: unknown) => void) => void,

  options?: HookOptions

  ): void;

  Runs a function, once, before all the tests.

  This is useful for running set up tasks, like initializing a global variable or connecting to a database.

  If this function throws, tests will not run in this file.

  @param fn

  the function to run

  ```
  let database;
  beforeAll(async () => {
    database = await connect("localhost");
  });
  ```
* function [beforeEach](https://bun.com/reference/bun/test/beforeEach)(

  fn: () => void | Promise<unknown> | (done: (err?: unknown) => void) => void,

  options?: HookOptions

  ): void;

  Runs a function before each test.

  This is useful for running set up tasks, like initializing a global variable or connecting to a database.

  If this function throws, the test will not run.

  @param fn

  the function to run
* function [onTestFinished](https://bun.com/reference/bun/test/onTestFinished)(

  fn: () => void | Promise<unknown> | (done: (err?: unknown) => void) => void,

  options?: HookOptions

  ): void;

  Runs a function after a test finishes, including after all afterEach hooks.

  This is useful for cleanup tasks that need to run at the very end of a test, after all other hooks have completed.

  Can only be called inside a test, not in describe blocks.

  @param fn

  the function to run

  ```
  test("my test", () => {
    onTestFinished(() => {
      // This runs after all afterEach hooks
      console.log("Test finished!");
    });
  });
  ```
* function [setDefaultTimeout](https://bun.com/reference/bun/test/setDefaultTimeout)(

  milliseconds: number

  ): void;

  Sets the default timeout for all tests in the current file. If a test specifies a timeout, it will override this value. The default timeout is 5000ms (5 seconds).

  @param milliseconds

  the number of milliseconds for the default timeout
* function [setSystemTime](https://bun.com/reference/bun/test/setSystemTime)(

  now?: number | Date

  ): ThisType<void>;

  Control the system time used by:

  + `Date.now()`
  + `new Date()`
  + `Intl.DateTimeFormat().format()`

  In the future, we may add support for more functions, but we haven't done that yet.

  @param now

  The time to set the system time to. If not provided, the system time will be reset.

  @returns

  `this`
* function [spyOn](https://bun.com/reference/bun/test/spyOn)<T extends object, K extends string | number | symbol>(

  obj: T,

  methodOrPropertyValue: K

  ): [Mock](https://bun.com/reference/bun/test/Mock)<Extract<T[K], (...args: any[]) => any>>;

  Create a spy on an object property or method

## Type definitions

* ### interface [AsymmetricMatchers](https://bun.com/reference/bun/test/AsymmetricMatchers)

  You can extend this interface with declaration merging, in order to add type support for custom asymmetric matchers.

  ```
  // my_modules.d.ts
  interface MyCustomMatchers {
    toBeWithinRange(floor: number, ceiling: number): any;
  }
  declare module "bun:test" {
    interface Matchers<T> extends MyCustomMatchers {}
    interface AsymmetricMatchers extends MyCustomMatchers {}
  }
  ```

  + [any](https://bun.com/reference/bun/test/AsymmetricMatchers/any)(

    constructor: (...args: any[]) => any | new (...args: any[]) => any

    ): any;

    Matches anything that was created with the given constructor. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value.

    ```
    function randocall(fn) {
      return fn(Math.floor(Math.random() * 6 + 1));
    }

    test('randocall calls its callback with a number', () => {
      const mock = jest.fn();
      randocall(mock);
      expect(mock).toBeCalledWith(expect.any(Number));
    });
    ```
  + [anything](https://bun.com/reference/bun/test/AsymmetricMatchers/anything)(): any;

    Matches anything but null or undefined. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value. For example, if you want to check that a mock function is called with a non-null argument:

    ```
    test('map calls its argument with a non-null argument', () => {
      const mock = jest.fn();
      [1].map(x => mock(x));
      expect(mock).toBeCalledWith(expect.anything());
    });
    ```
  + [arrayContaining](https://bun.com/reference/bun/test/AsymmetricMatchers/arrayContaining)<E = any>(

    arr: readonly E[]

    ): any;

    Matches any array made up entirely of elements in the provided array. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value.

    Optionally, you can provide a type for the elements via a generic.
  + [closeTo](https://bun.com/reference/bun/test/AsymmetricMatchers/closeTo)(

    num: number,

    numDigits?: number

    ): any;

    Useful when comparing floating point numbers in object properties or array item. If you need to compare a number, use `.toBeCloseTo` instead.

    The optional `numDigits` argument limits the number of digits to check after the decimal point. For the default value 2, the test criterion is `Math.abs(expected - received) < 0.005` (that is, `10 ** -2 / 2`).
  + [objectContaining](https://bun.com/reference/bun/test/AsymmetricMatchers/objectContaining)(

    obj: object

    ): any;

    Matches any object that recursively matches the provided keys. This is often handy in conjunction with other asymmetric matchers.

    Optionally, you can provide a type for the object via a generic. This ensures that the object contains the desired structure.
  + [stringContaining](https://bun.com/reference/bun/test/AsymmetricMatchers/stringContaining)(

    str: string | String

    ): any;

    Matches any received string that contains the exact expected string
  + [stringMatching](https://bun.com/reference/bun/test/AsymmetricMatchers/stringMatching)(

    regex: string | String | RegExp

    ): any;

    Matches any string that contains the exact provided string
* ### interface [AsymmetricMatchersBuiltin](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin)

  + [any](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin/any)(

    constructor: (...args: any[]) => any | new (...args: any[]) => any

    ): any;

    Matches anything that was created with the given constructor. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value.

    ```
    function randocall(fn) {
      return fn(Math.floor(Math.random() * 6 + 1));
    }

    test('randocall calls its callback with a number', () => {
      const mock = jest.fn();
      randocall(mock);
      expect(mock).toBeCalledWith(expect.any(Number));
    });
    ```
  + [anything](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin/anything)(): any;

    Matches anything but null or undefined. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value. For example, if you want to check that a mock function is called with a non-null argument:

    ```
    test('map calls its argument with a non-null argument', () => {
      const mock = jest.fn();
      [1].map(x => mock(x));
      expect(mock).toBeCalledWith(expect.anything());
    });
    ```
  + [arrayContaining](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin/arrayContaining)<E = any>(

    arr: readonly E[]

    ): any;

    Matches any array made up entirely of elements in the provided array. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value.

    Optionally, you can provide a type for the elements via a generic.
  + [closeTo](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin/closeTo)(

    num: number,

    numDigits?: number

    ): any;

    Useful when comparing floating point numbers in object properties or array item. If you need to compare a number, use `.toBeCloseTo` instead.

    The optional `numDigits` argument limits the number of digits to check after the decimal point. For the default value 2, the test criterion is `Math.abs(expected - received) < 0.005` (that is, `10 ** -2 / 2`).
  + [objectContaining](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin/objectContaining)(

    obj: object

    ): any;

    Matches any object that recursively matches the provided keys. This is often handy in conjunction with other asymmetric matchers.

    Optionally, you can provide a type for the object via a generic. This ensures that the object contains the desired structure.
  + [stringContaining](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin/stringContaining)(

    str: string | String

    ): any;

    Matches any received string that contains the exact expected string
  + [stringMatching](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin/stringMatching)(

    regex: string | String | RegExp

    ): any;

    Matches any string that contains the exact provided string
* ### interface [Describe](https://bun.com/reference/bun/test/Describe)<T extends Readonly<any[]>>

  Describes a group of related tests.

  ```
  function sum(a, b) {
    return a + b;
  }
  describe("sum()", () => {
    test("can sum two values", () => {
      expect(sum(1, 1)).toBe(2);
    });
  });
  ```

  + [concurrent](https://bun.com/reference/bun/test/Describe/concurrent): [Describe](https://bun.com/reference/bun/test/Describe)<T>

    Marks this group of tests to be executed concurrently.
  + [only](https://bun.com/reference/bun/test/Describe/only): [Describe](https://bun.com/reference/bun/test/Describe)<T>

    Skips all other tests, except this group of tests.
  + [serial](https://bun.com/reference/bun/test/Describe/serial): [Describe](https://bun.com/reference/bun/test/Describe)<T>

    Marks this group of tests to be executed serially (one after another), even when the --concurrent flag is used.
  + [skip](https://bun.com/reference/bun/test/Describe/skip): [Describe](https://bun.com/reference/bun/test/Describe)<T>

    Skips this group of tests.
  + [todo](https://bun.com/reference/bun/test/Describe/todo): [Describe](https://bun.com/reference/bun/test/Describe)<T>

    Marks this group of tests as to be written or to be fixed.
  + [each](https://bun.com/reference/bun/test/Describe/each)<T extends any[]>(

    table: readonly T[]

    ): [Describe](https://bun.com/reference/bun/test/Describe)<[...T[]]>;

    [each](https://bun.com/reference/bun/test/Describe/each)<T>(

    table: T[]

    ): [Describe](https://bun.com/reference/bun/test/Describe)<[T]>;
  + [if](https://bun.com/reference/bun/test/Describe/if)(

    condition: boolean

    ): [Describe](https://bun.com/reference/bun/test/Describe)<T>;

    Runs this group of tests, only if `condition` is true.

    This is the opposite of `describe.skipIf()`.

    @param condition

    if these tests should run
  + [skipIf](https://bun.com/reference/bun/test/Describe/skipIf)(

    condition: boolean

    ): [Describe](https://bun.com/reference/bun/test/Describe)<T>;

    Skips this group of tests, if `condition` is true.

    @param condition

    if these tests should be skipped
  + [todoIf](https://bun.com/reference/bun/test/Describe/todoIf)(

    condition: boolean

    ): [Describe](https://bun.com/reference/bun/test/Describe)<T>;

    Marks this group of tests as to be written or to be fixed, if `condition` is true.

    @param condition

    if these tests should be skipped
* ### interface [Expect](https://bun.com/reference/bun/test/Expect)

  You can extend this interface with declaration merging, in order to add type support for custom asymmetric matchers.

  ```
  // my_modules.d.ts
  interface MyCustomMatchers {
    toBeWithinRange(floor: number, ceiling: number): any;
  }
  declare module "bun:test" {
    interface Matchers<T> extends MyCustomMatchers {}
    interface AsymmetricMatchers extends MyCustomMatchers {}
  }
  ```

  + [not](https://bun.com/reference/bun/test/Expect/not): ExpectNot

    Access to negated asymmetric matchers.

    ```
    expect("abc").toEqual(expect.stringContaining("abc")); // will pass
    expect("abc").toEqual(expect.not.stringContaining("abc")); // will fail
    ```
  + [rejectsTo](https://bun.com/reference/bun/test/Expect/rejectsTo): [AsymmetricMatchers](https://bun.com/reference/bun/test/AsymmetricMatchers)

    Create an asymmetric matcher for a promise rejected value.

    ```
    expect(Promise.reject("error")).toEqual(expect.rejectsTo.stringContaining("error")); // will pass
    expect(Promise.resolve("error")).toEqual(expect.rejectsTo.stringContaining("error")); // will fail
    expect("error").toEqual(expect.rejectsTo.stringContaining("error")); // will fail
    ```
  + [resolvesTo](https://bun.com/reference/bun/test/Expect/resolvesTo): [AsymmetricMatchers](https://bun.com/reference/bun/test/AsymmetricMatchers)

    Create an asymmetric matcher for a promise resolved value.

    ```
    expect(Promise.resolve("value")).toEqual(expect.resolvesTo.stringContaining("value")); // will pass
    expect(Promise.reject("value")).toEqual(expect.resolvesTo.stringContaining("value")); // will fail
    expect("value").toEqual(expect.resolvesTo.stringContaining("value")); // will fail
    ```
  + [any](https://bun.com/reference/bun/test/Expect/any)(

    constructor: (...args: any[]) => any | new (...args: any[]) => any

    ): any;

    Matches anything that was created with the given constructor. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value.

    ```
    function randocall(fn) {
      return fn(Math.floor(Math.random() * 6 + 1));
    }

    test('randocall calls its callback with a number', () => {
      const mock = jest.fn();
      randocall(mock);
      expect(mock).toBeCalledWith(expect.any(Number));
    });
    ```
  + [anything](https://bun.com/reference/bun/test/Expect/anything)(): any;

    Matches anything but null or undefined. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value. For example, if you want to check that a mock function is called with a non-null argument:

    ```
    test('map calls its argument with a non-null argument', () => {
      const mock = jest.fn();
      [1].map(x => mock(x));
      expect(mock).toBeCalledWith(expect.anything());
    });
    ```
  + [arrayContaining](https://bun.com/reference/bun/test/Expect/arrayContaining)<E = any>(

    arr: readonly E[]

    ): any;

    Matches any array made up entirely of elements in the provided array. You can use it inside `toEqual` or `toBeCalledWith` instead of a literal value.

    Optionally, you can provide a type for the elements via a generic.
  + [assertions](https://bun.com/reference/bun/test/Expect/assertions)(

    neededAssertions: number

    ): void;

    Ensures that a specific number of assertions are made
  + [closeTo](https://bun.com/reference/bun/test/Expect/closeTo)(

    num: number,

    numDigits?: number

    ): any;

    Useful when comparing floating point numbers in object properties or array item. If you need to compare a number, use `.toBeCloseTo` instead.

    The optional `numDigits` argument limits the number of digits to check after the decimal point. For the default value 2, the test criterion is `Math.abs(expected - received) < 0.005` (that is, `10 ** -2 / 2`).
  + [extend](https://bun.com/reference/bun/test/Expect/extend)<M>(

    matchers: [ExpectExtendMatchers](https://bun.com/reference/bun/test/ExpectExtendMatchers)<M>

    ): void;

    Register new custom matchers.

    @param matchers

    An object containing the matchers to register, where each key is the matcher name, and its value the implementation function. The function must satisfy: `(actualValue, ...matcherInstantiationArguments) => { pass: true|false, message: () => string }`

    ```
    expect.extend({
        toBeWithinRange(actual, min, max) {
            if (typeof actual !== 'number' || typeof min !== 'number' || typeof max !== 'number')
                throw new Error('Invalid usage');
            const pass = actual >= min && actual <= max;
            return {
                pass: pass,
                message: () => `expected ${this.utils.printReceived(actual)} ` +
                    (pass ? `not to be`: `to be`) + ` within range ${this.utils.printExpected(`${min} .. ${max}`)}`,
            };
        },
    });

    test('some test', () => {
      expect(50).toBeWithinRange(0, 100); // will pass
      expect(50).toBeWithinRange(100, 200); // will fail
      expect(50).toBe(expect.toBeWithinRange(0, 100)); // will pass
      expect(50).toBe(expect.not.toBeWithinRange(100, 200)); // will pass
    });
    ```
  + [hasAssertions](https://bun.com/reference/bun/test/Expect/hasAssertions)(): void;

    Ensures that an assertion is made
  + [objectContaining](https://bun.com/reference/bun/test/Expect/objectContaining)(

    obj: object

    ): any;

    Matches any object that recursively matches the provided keys. This is often handy in conjunction with other asymmetric matchers.

    Optionally, you can provide a type for the object via a generic. This ensures that the object contains the desired structure.
  + [stringContaining](https://bun.com/reference/bun/test/Expect/stringContaining)(

    str: string | String

    ): any;

    Matches any received string that contains the exact expected string
  + [stringMatching](https://bun.com/reference/bun/test/Expect/stringMatching)(

    regex: string | String | RegExp

    ): any;

    Matches any string that contains the exact provided string
  + [unreachable](https://bun.com/reference/bun/test/Expect/unreachable)(

    msg?: string | [Error](https://bun.com/reference/globals/Error)

    ): never;

    Throw an error if this function is called.

    @param msg

    Optional message to display if the test fails

    @returns

    never

    ```
    import { expect, test } from "bun:test";

    test("!!abc!! is not a module", () => {
     try {
        require("!!abc!!");
        expect.unreachable();
     } catch(e) {
        expect(e.name).not.toBe("UnreachableError");
     }
    });
    ```
* ### interface [MatcherResult](https://bun.com/reference/bun/test/MatcherResult)

  + [message](https://bun.com/reference/bun/test/MatcherResult/message)?: string | () => string
  + [pass](https://bun.com/reference/bun/test/MatcherResult/pass): boolean
* ### interface [Matchers](https://bun.com/reference/bun/test/Matchers)<T = unknown>

  You can extend this interface with declaration merging, in order to add type support for custom matchers.

  ```
  // my_modules.d.ts
  interface MyCustomMatchers {
    toBeWithinRange(floor: number, ceiling: number): any;
  }
  declare module "bun:test" {
    interface Matchers<T> extends MyCustomMatchers {}
    interface AsymmetricMatchers extends MyCustomMatchers {}
  }
  ```

  + [fail](https://bun.com/reference/bun/test/Matchers/fail): (message?: string) => void

    Assertion which fails.

    ```
    expect().fail();
    expect().fail("message is optional");
    expect().not.fail();
    expect().not.fail("hi");
    ```
  + [not](https://bun.com/reference/bun/test/Matchers/not): [Matchers](https://bun.com/reference/bun/test/Matchers)<unknown>

    Negates the result of a subsequent assertion. If you know how to test something, `.not` lets you test its opposite.

    ```
    expect(1).not.toBe(0);
    expect(null).not.toBeNull();
    ```
  + [pass](https://bun.com/reference/bun/test/Matchers/pass): (message?: string) => void

    Assertion which passes.

    ```
    expect().pass();
    expect().pass("message is optional");
    expect().not.pass();
    expect().not.pass("hi");
    ```
  + [rejects](https://bun.com/reference/bun/test/Matchers/rejects): [Matchers](https://bun.com/reference/bun/test/Matchers)<unknown>

    Expects the value to be a promise that rejects.

    ```
    expect(Promise.reject("error")).rejects.toBe("error");
    ```
  + [resolves](https://bun.com/reference/bun/test/Matchers/resolves): [Matchers](https://bun.com/reference/bun/test/Matchers)<Awaited<T>>

    Expects the value to be a promise that resolves.

    ```
    expect(Promise.resolve(1)).resolves.toBe(1);
    ```
  + [lastCalledWith](https://bun.com/reference/bun/test/Matchers/lastCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the nth call.
  + [nthCalledWith](https://bun.com/reference/bun/test/Matchers/nthCalledWith)(

    n: number,

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the nth call.
  + [toBe](https://bun.com/reference/bun/test/Matchers/toBe)(

    expected: T

    ): void;

    Asserts that a value equals what is expected.

    - For non-primitive values, like objects and arrays, use `toEqual()` instead.
    - For floating-point numbers, use `toBeCloseTo()` instead.

    @param expected

    the expected value

    ```
    expect(100 + 23).toBe(123);
    expect("d" + "og").toBe("dog");
    expect([123]).toBe([123]); // fail, use toEqual()
    expect(3 + 0.14).toBe(3.14); // fail, use toBeCloseTo()

    // TypeScript errors:
    expect("hello").toBe(3.14); // typescript error + fail
    expect("hello").toBe<number>(3.14); // no typescript error, but still fails
    ```

    [toBe](https://bun.com/reference/bun/test/Matchers/toBe)<X = T>(

    expected: NoInfer<X>

    ): void;
  + [toBeArray](https://bun.com/reference/bun/test/Matchers/toBeArray)(): void;

    Asserts that a value is a `array`.

    ```
    expect([1]).toBeArray();
    expect(new Array(1)).toBeArray();
    expect({}).not.toBeArray();
    ```
  + [toBeArrayOfSize](https://bun.com/reference/bun/test/Matchers/toBeArrayOfSize)(

    size: number

    ): void;

    Asserts that a value is a `array` of a certain length.

    ```
    expect([]).toBeArrayOfSize(0);
    expect([1]).toBeArrayOfSize(1);
    expect(new Array(1)).toBeArrayOfSize(1);
    expect({}).not.toBeArrayOfSize(0);
    ```
  + [toBeBoolean](https://bun.com/reference/bun/test/Matchers/toBeBoolean)(): void;

    Asserts that a value is a `boolean`.

    ```
    expect(true).toBeBoolean();
    expect(false).toBeBoolean();
    expect(null).not.toBeBoolean();
    expect(0).not.toBeBoolean();
    ```
  + [toBeCalled](https://bun.com/reference/bun/test/Matchers/toBeCalled)(): void;

    Ensures that a mock function is called an exact number of times.
  + [toBeCalledTimes](https://bun.com/reference/bun/test/Matchers/toBeCalledTimes)(

    expected: number

    ): void;

    Ensure that a mock function is called with specific arguments.
  + [toBeCalledWith](https://bun.com/reference/bun/test/Matchers/toBeCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments.
  + [toBeCloseTo](https://bun.com/reference/bun/test/Matchers/toBeCloseTo)(

    expected: number,

    numDigits?: number

    ): void;

    Asserts that value is close to the expected by floating point precision.

    For example, the following fails because arithmetic on decimal (base 10) values often have rounding errors in limited precision binary (base 2) representation.

    @param expected

    the expected value

    @param numDigits

    the number of digits to check after the decimal point. Default is `2`

    ```
    expect(0.2 + 0.1).toBe(0.3); // fails

    Use `toBeCloseTo` to compare floating point numbers for approximate equality.
    ```
  + [toBeDate](https://bun.com/reference/bun/test/Matchers/toBeDate)(): void;

    Asserts that a value is a `Date` object.

    To check if a date is valid, use `toBeValidDate()` instead.

    ```
    expect(new Date()).toBeDate();
    expect(new Date(null)).toBeDate();
    expect("2020-03-01").not.toBeDate();
    ```
  + [toBeDefined](https://bun.com/reference/bun/test/Matchers/toBeDefined)(): void;

    Asserts that a value is defined. (e.g. is not `undefined`)

    ```
    expect(true).toBeDefined();
    expect(undefined).toBeDefined(); // fail
    ```
  + [toBeEmpty](https://bun.com/reference/bun/test/Matchers/toBeEmpty)(): void;

    Asserts that a value is empty.

    ```
    expect("").toBeEmpty();
    expect([]).toBeEmpty();
    expect({}).toBeEmpty();
    expect(new Set()).toBeEmpty();
    ```
  + [toBeEmptyObject](https://bun.com/reference/bun/test/Matchers/toBeEmptyObject)(): void;

    Asserts that a value is an empty `object`.

    ```
    expect({}).toBeEmptyObject();
    expect({ a: 'hello' }).not.toBeEmptyObject();
    ```
  + [toBeEven](https://bun.com/reference/bun/test/Matchers/toBeEven)(): void;

    Asserts that a number is even.

    ```
    expect(2).toBeEven();
    expect(1).not.toBeEven();
    ```
  + [toBeFalse](https://bun.com/reference/bun/test/Matchers/toBeFalse)(): void;

    Asserts that a value is `false`.

    ```
    expect(false).toBeFalse();
    expect(true).not.toBeFalse();
    expect(0).not.toBeFalse();
    ```
  + [toBeFalsy](https://bun.com/reference/bun/test/Matchers/toBeFalsy)(): void;

    Asserts that a value is "falsy".

    To assert that a value equals `false`, use `toBe(false)` instead.

    ```
    expect(true).toBeTruthy();
    expect(1).toBeTruthy();
    expect({}).toBeTruthy();
    ```
  + [toBeFinite](https://bun.com/reference/bun/test/Matchers/toBeFinite)(): void;

    Asserts that a value is a `number`, and is not `NaN` or `Infinity`.

    ```
    expect(1).toBeFinite();
    expect(3.14).toBeFinite();
    expect(NaN).not.toBeFinite();
    expect(Infinity).not.toBeFinite();
    ```
  + [toBeFunction](https://bun.com/reference/bun/test/Matchers/toBeFunction)(): void;

    Asserts that a value is a `function`.

    ```
    expect(() => {}).toBeFunction();
    ```
  + [toBeGreaterThan](https://bun.com/reference/bun/test/Matchers/toBeGreaterThan)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is greater than the expected value.

    @param expected

    the expected number

    ```
    expect(1).toBeGreaterThan(0);
    expect(3.14).toBeGreaterThan(3);
    expect(9).toBeGreaterThan(9); // fail
    ```
  + [toBeGreaterThanOrEqual](https://bun.com/reference/bun/test/Matchers/toBeGreaterThanOrEqual)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is greater than or equal to the expected value.

    @param expected

    the expected number

    ```
    expect(1).toBeGreaterThanOrEqual(0);
    expect(3.14).toBeGreaterThanOrEqual(3);
    expect(9).toBeGreaterThanOrEqual(9);
    ```
  + [toBeInstanceOf](https://bun.com/reference/bun/test/Matchers/toBeInstanceOf)(

    value: unknown

    ): void;

    Asserts that the expected value is an instance of value

    ```
    expect([]).toBeInstanceOf(Array);
    expect(null).toBeInstanceOf(Array); // fail
    ```
  + [toBeInteger](https://bun.com/reference/bun/test/Matchers/toBeInteger)(): void;

    Asserts that a value is a `number`, and is an integer.

    ```
    expect(1).toBeInteger();
    expect(3.14).not.toBeInteger();
    expect(NaN).not.toBeInteger();
    ```
  + [toBeLessThan](https://bun.com/reference/bun/test/Matchers/toBeLessThan)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is less than the expected value.

    @param expected

    the expected number

    ```
    expect(-1).toBeLessThan(0);
    expect(3).toBeLessThan(3.14);
    expect(9).toBeLessThan(9); // fail
    ```
  + [toBeLessThanOrEqual](https://bun.com/reference/bun/test/Matchers/toBeLessThanOrEqual)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is less than or equal to the expected value.

    @param expected

    the expected number

    ```
    expect(-1).toBeLessThanOrEqual(0);
    expect(3).toBeLessThanOrEqual(3.14);
    expect(9).toBeLessThanOrEqual(9);
    ```
  + [toBeNaN](https://bun.com/reference/bun/test/Matchers/toBeNaN)(): void;

    Asserts that a value is `NaN`.

    Same as using `Number.isNaN()`.

    ```
    expect(NaN).toBeNaN();
    expect(Infinity).toBeNaN(); // fail
    expect("notanumber").toBeNaN(); // fail
    ```
  + [toBeNegative](https://bun.com/reference/bun/test/Matchers/toBeNegative)(): void;

    Asserts that a value is a negative `number`.

    ```
    expect(-3.14).toBeNegative();
    expect(1).not.toBeNegative();
    expect(NaN).not.toBeNegative();
    ```
  + [toBeNil](https://bun.com/reference/bun/test/Matchers/toBeNil)(): void;

    Asserts that a value is `null` or `undefined`.

    ```
    expect(null).toBeNil();
    expect(undefined).toBeNil();
    ```
  + [toBeNull](https://bun.com/reference/bun/test/Matchers/toBeNull)(): void;

    Asserts that a value is `null`.

    ```
    expect(null).toBeNull();
    expect(undefined).toBeNull(); // fail
    ```
  + [toBeNumber](https://bun.com/reference/bun/test/Matchers/toBeNumber)(): void;

    Asserts that a value is a `number`.

    ```
    expect(1).toBeNumber();
    expect(3.14).toBeNumber();
    expect(NaN).toBeNumber();
    expect(BigInt(1)).not.toBeNumber();
    ```
  + [toBeObject](https://bun.com/reference/bun/test/Matchers/toBeObject)(): void;

    Asserts that a value is an `object`.

    ```
    expect({}).toBeObject();
    expect("notAnObject").not.toBeObject();
    expect(NaN).not.toBeObject();
    ```
  + [toBeOdd](https://bun.com/reference/bun/test/Matchers/toBeOdd)(): void;

    Asserts that a number is odd.

    ```
    expect(1).toBeOdd();
    expect(2).not.toBeOdd();
    ```
  + [toBeOneOf](https://bun.com/reference/bun/test/Matchers/toBeOneOf)(

    expected: Iterable<T>

    ): void;

    Asserts that the value is deep equal to an element in the expected array.

    The value must be an array or iterable, which includes strings.

    @param expected

    the expected value

    ```
    expect(1).toBeOneOf([1,2,3]);
    expect("foo").toBeOneOf(["foo", "bar"]);
    expect(true).toBeOneOf(new Set([true]));
    ```

    [toBeOneOf](https://bun.com/reference/bun/test/Matchers/toBeOneOf)<X = T>(

    expected: NoInfer<Iterable<X, any, any>>

    ): void;
  + [toBePositive](https://bun.com/reference/bun/test/Matchers/toBePositive)(): void;

    Asserts that a value is a positive `number`.

    ```
    expect(1).toBePositive();
    expect(-3.14).not.toBePositive();
    expect(NaN).not.toBePositive();
    ```
  + [toBeString](https://bun.com/reference/bun/test/Matchers/toBeString)(): void;

    Asserts that a value is a `string`.

    ```
    expect("foo").toBeString();
    expect(new String("bar")).toBeString();
    expect(123).not.toBeString();
    ```
  + [toBeSymbol](https://bun.com/reference/bun/test/Matchers/toBeSymbol)(): void;

    Asserts that a value is a `symbol`.

    ```
    expect(Symbol("foo")).toBeSymbol();
    expect("foo").not.toBeSymbol();
    ```
  + [toBeTrue](https://bun.com/reference/bun/test/Matchers/toBeTrue)(): void;

    Asserts that a value is `true`.

    ```
    expect(true).toBeTrue();
    expect(false).not.toBeTrue();
    expect(1).not.toBeTrue();
    ```
  + [toBeTruthy](https://bun.com/reference/bun/test/Matchers/toBeTruthy)(): void;

    Asserts that a value is "truthy".

    To assert that a value equals `true`, use `toBe(true)` instead.

    ```
    expect(true).toBeTruthy();
    expect(1).toBeTruthy();
    expect({}).toBeTruthy();
    ```
  + [toBeTypeOf](https://bun.com/reference/bun/test/Matchers/toBeTypeOf)(

    type: 'string' | 'number' | 'bigint' | 'boolean' | 'symbol' | 'undefined' | 'object' | 'function'

    ): void;

    Asserts that a value matches a specific type.

    ```
    expect(1).toBeTypeOf("number");
    expect("hello").toBeTypeOf("string");
    expect([]).not.toBeTypeOf("boolean");
    ```
  + [toBeUndefined](https://bun.com/reference/bun/test/Matchers/toBeUndefined)(): void;

    Asserts that a value is `undefined`.

    ```
    expect(undefined).toBeUndefined();
    expect(null).toBeUndefined(); // fail
    ```
  + [toBeValidDate](https://bun.com/reference/bun/test/Matchers/toBeValidDate)(): void;

    Asserts that a value is a valid `Date` object.

    ```
    expect(new Date()).toBeValidDate();
    expect(new Date(null)).not.toBeValidDate();
    expect("2020-03-01").not.toBeValidDate();
    ```
  + [toBeWithin](https://bun.com/reference/bun/test/Matchers/toBeWithin)(

    start: number,

    end: number

    ): void;

    Asserts that a value is a number between a start and end value.

    @param start

    the start number (inclusive)

    @param end

    the end number (exclusive)
  + [toContain](https://bun.com/reference/bun/test/Matchers/toContain)(

    expected: T extends Iterable<U, any, any> ? U : T

    ): void;

    Asserts that a value contains what is expected.

    The value must be an array or iterable, which includes strings.

    @param expected

    the expected value

    ```
    expect([1, 2, 3]).toContain(1);
    expect(new Set([true])).toContain(true);
    expect("hello").toContain("o");
    ```

    [toContain](https://bun.com/reference/bun/test/Matchers/toContain)<X = T>(

    expected: NoInfer<X extends Iterable<U, any, any> ? U : X>

    ): void;
  + [toContainAllKeys](https://bun.com/reference/bun/test/Matchers/toContainAllKeys)(

    expected: keyof T[]

    ): void;

    Asserts that an `object` contains all the provided keys.

    The value must be an object

    @param expected

    the expected value

    ```
    expect({ a: 'hello', b: 'world' }).toContainAllKeys(['a','b']);
    expect({ a: 'hello', b: 'world' }).toContainAllKeys(['b','a']);
    expect({ 1: 'hello', b: 'world' }).toContainAllKeys([1,'b']);
    expect({ a: 'hello', b: 'world' }).not.toContainAllKeys(['c']);
    expect({ a: 'hello', b: 'world' }).not.toContainAllKeys(['a']);
    ```

    [toContainAllKeys](https://bun.com/reference/bun/test/Matchers/toContainAllKeys)<X = T>(

    expected: NoInfer<keyof X[]>

    ): void;
  + [toContainAllValues](https://bun.com/reference/bun/test/Matchers/toContainAllValues)(

    expected: unknown[]

    ): void;

    Asserts that an `object` contain all the provided values.

    The value must be an object

    @param expected

    the expected value

    ```
    const o = { a: 'foo', b: 'bar', c: 'baz' };
    expect(o).toContainAllValues(['foo', 'bar', 'baz']);
    expect(o).toContainAllValues(['baz', 'bar', 'foo']);
    expect(o).not.toContainAllValues(['bar', 'foo']);
    ```
  + [toContainAnyKeys](https://bun.com/reference/bun/test/Matchers/toContainAnyKeys)(

    expected: keyof T[]

    ): void;

    Asserts that an `object` contains at least one of the provided keys. Asserts that an `object` contains all the provided keys.

    The value must be an object

    @param expected

    the expected value

    ```
    expect({ a: 'hello', b: 'world' }).toContainAnyKeys(['a']);
    expect({ a: 'hello', b: 'world' }).toContainAnyKeys(['b']);
    expect({ a: 'hello', b: 'world' }).toContainAnyKeys(['b', 'c']);
    expect({ a: 'hello', b: 'world' }).not.toContainAnyKeys(['c']);
    ```

    [toContainAnyKeys](https://bun.com/reference/bun/test/Matchers/toContainAnyKeys)<X = T>(

    expected: NoInfer<keyof X[]>

    ): void;
  + [toContainAnyValues](https://bun.com/reference/bun/test/Matchers/toContainAnyValues)(

    expected: unknown[]

    ): void;

    Asserts that an `object` contain any provided value.

    The value must be an object

    @param expected

    the expected value

    ```
    const o = { a: 'foo', b: 'bar', c: 'baz' };
    expect(o).toContainAnyValues(['qux', 'foo']);
    expect(o).toContainAnyValues(['qux', 'bar']);
    expect(o).toContainAnyValues(['qux', 'baz']);
    expect(o).not.toContainAnyValues(['qux']);
    ```
  + [toContainEqual](https://bun.com/reference/bun/test/Matchers/toContainEqual)(

    expected: T extends Iterable<U, any, any> ? U : T

    ): void;

    Asserts that a value contains and equals what is expected.

    This matcher will perform a deep equality check for members of arrays, rather than checking for object identity.

    @param expected

    the expected value

    ```
    expect([{ a: 1 }]).toContainEqual({ a: 1 });
    expect([{ a: 1 }]).not.toContainEqual({ a: 2 });
    ```

    [toContainEqual](https://bun.com/reference/bun/test/Matchers/toContainEqual)<X = T>(

    expected: NoInfer<X extends Iterable<U, any, any> ? U : X>

    ): void;
  + [toContainKey](https://bun.com/reference/bun/test/Matchers/toContainKey)(

    expected: keyof T

    ): void;

    Asserts that an `object` contains a key.

    The value must be an object

    @param expected

    the expected value

    ```
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKey('a');
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKey('b');
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKey('c');
    expect({ a: 'foo', b: 'bar', c: 'baz' }).not.toContainKey('d');
    ```

    [toContainKey](https://bun.com/reference/bun/test/Matchers/toContainKey)<X = T>(

    expected: NoInfer<keyof X>

    ): void;
  + [toContainKeys](https://bun.com/reference/bun/test/Matchers/toContainKeys)(

    expected: keyof T[]

    ): void;

    Asserts that an `object` contains all the provided keys.

    @param expected

    the expected value

    ```
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKeys(['a', 'b']);
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKeys(['a', 'b', 'c']);
    expect({ a: 'foo', b: 'bar', c: 'baz' }).not.toContainKeys(['a', 'b', 'e']);
    ```

    [toContainKeys](https://bun.com/reference/bun/test/Matchers/toContainKeys)<X = T>(

    expected: NoInfer<keyof X[]>

    ): void;
  + [toContainValue](https://bun.com/reference/bun/test/Matchers/toContainValue)(

    expected: unknown

    ): void;

    Asserts that an `object` contain the provided value.

    This method is deep and will look through child properties to find the expected value.

    The input value must be an object.

    @param expected

    the expected value

    ```
    const shallow = { hello: "world" };
    const deep = { message: shallow };
    const deepArray = { message: [shallow] };
    const o = { a: "foo", b: [1, "hello", true], c: "baz" };

    expect(shallow).toContainValue("world");
    expect({ foo: false }).toContainValue(false);
    expect(deep).toContainValue({ hello: "world" });
    expect(deepArray).toContainValue([{ hello: "world" }]);

    expect(o).toContainValue("foo", "barr");
    expect(o).toContainValue([1, "hello", true]);
    expect(o).not.toContainValue("qux");

    // NOT
    expect(shallow).not.toContainValue("foo");
    expect(deep).not.toContainValue({ foo: "bar" });
    expect(deepArray).not.toContainValue([{ foo: "bar" }]);
    ```
  + [toContainValues](https://bun.com/reference/bun/test/Matchers/toContainValues)(

    expected: unknown[]

    ): void;

    Asserts that an `object` contain the provided value.

    This is the same as toContainValue, but accepts an array of values instead.

    The value must be an object

    @param expected

    the expected value

    ```
    const o = { a: 'foo', b: 'bar', c: 'baz' };
    expect(o).toContainValues(['foo']);
    expect(o).toContainValues(['baz', 'bar']);
    expect(o).not.toContainValues(['qux', 'foo']);
    ```
  + [toEndWith](https://bun.com/reference/bun/test/Matchers/toEndWith)(

    expected: string

    ): void;

    Asserts that a value ends with a `string`.

    @param expected

    the string to end with
  + [toEqual](https://bun.com/reference/bun/test/Matchers/toEqual)(

    expected: T

    ): void;

    Asserts that a value is deeply equal to what is expected.

    @param expected

    the expected value

    ```
    expect(100 + 23).toBe(123);
    expect("d" + "og").toBe("dog");
    expect([456]).toEqual([456]);
    expect({ value: 1 }).toEqual({ value: 1 });
    ```

    [toEqual](https://bun.com/reference/bun/test/Matchers/toEqual)<X = T>(

    expected: NoInfer<X>

    ): void;
  + [toEqualIgnoringWhitespace](https://bun.com/reference/bun/test/Matchers/toEqualIgnoringWhitespace)(

    expected: string

    ): void;

    Asserts that a value is equal to the expected string, ignoring any whitespace.

    @param expected

    the expected string

    ```
    expect(" foo ").toEqualIgnoringWhitespace("foo");
    expect("bar").toEqualIgnoringWhitespace(" bar ");
    ```
  + [toHaveBeenCalled](https://bun.com/reference/bun/test/Matchers/toHaveBeenCalled)(): void;

    Ensures that a mock function is called.
  + [toHaveBeenCalledTimes](https://bun.com/reference/bun/test/Matchers/toHaveBeenCalledTimes)(

    expected: number

    ): void;

    Ensures that a mock function is called an exact number of times.
  + [toHaveBeenCalledWith](https://bun.com/reference/bun/test/Matchers/toHaveBeenCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments.
  + [toHaveBeenLastCalledWith](https://bun.com/reference/bun/test/Matchers/toHaveBeenLastCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the last call.
  + [toHaveBeenNthCalledWith](https://bun.com/reference/bun/test/Matchers/toHaveBeenNthCalledWith)(

    n: number,

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the nth call.
  + [toHaveLastReturnedWith](https://bun.com/reference/bun/test/Matchers/toHaveLastReturnedWith)(

    expected: unknown

    ): void;

    Ensures that a mock function has returned a specific value on its last invocation. This matcher uses deep equality, like toEqual(), and supports asymmetric matchers.
  + [toHaveLength](https://bun.com/reference/bun/test/Matchers/toHaveLength)(

    length: number

    ): void;

    Asserts that a value has a `.length` property that is equal to the expected length.

    @param length

    the expected length

    ```
    expect([]).toHaveLength(0);
    expect("hello").toHaveLength(4);
    ```
  + [toHaveNthReturnedWith](https://bun.com/reference/bun/test/Matchers/toHaveNthReturnedWith)(

    n: number,

    expected: unknown

    ): void;

    Ensures that a mock function has returned a specific value on the nth invocation. This matcher uses deep equality, like toEqual(), and supports asymmetric matchers.

    @param n

    The 1-based index of the function call

    @param expected

    The expected return value
  + [toHaveProperty](https://bun.com/reference/bun/test/Matchers/toHaveProperty)(

    keyPath: string | number | string | number[],

    value?: unknown

    ): void;

    Asserts that a value has a property with the expected name, and value if provided.

    @param keyPath

    the expected property name or path, or an index

    @param value

    the expected property value, if provided

    ```
    expect(new Set()).toHaveProperty("size");
    expect(new Uint8Array()).toHaveProperty("byteLength", 0);
    expect({ kitchen: { area: 20 }}).toHaveProperty("kitchen.area", 20);
    expect({ kitchen: { area: 20 }}).toHaveProperty(["kitchen", "area"], 20);
    ```
  + [toHaveReturned](https://bun.com/reference/bun/test/Matchers/toHaveReturned)(): void;

    Ensures that a mock function has returned successfully at least once.

    A promise that is unfulfilled will be considered a failure. If the function threw an error, it will be considered a failure.
  + [toHaveReturnedTimes](https://bun.com/reference/bun/test/Matchers/toHaveReturnedTimes)(

    times: number

    ): void;

    Ensures that a mock function has returned successfully at `times` times.

    A promise that is unfulfilled will be considered a failure. If the function threw an error, it will be considered a failure.
  + [toHaveReturnedWith](https://bun.com/reference/bun/test/Matchers/toHaveReturnedWith)(

    expected: unknown

    ): void;

    Ensures that a mock function has returned a specific value. This matcher uses deep equality, like toEqual(), and supports asymmetric matchers.
  + [toInclude](https://bun.com/reference/bun/test/Matchers/toInclude)(

    expected: string

    ): void;

    Asserts that a value includes a `string`.

    For non-string values, use `toContain()` instead.

    @param expected

    the expected substring
  + [toIncludeRepeated](https://bun.com/reference/bun/test/Matchers/toIncludeRepeated)(

    expected: string,

    times: number

    ): void;

    Asserts that a value includes a `string` {times} times.

    @param expected

    the expected substring

    @param times

    the number of times the substring should occur
  + [toMatch](https://bun.com/reference/bun/test/Matchers/toMatch)(

    expected: string | RegExp

    ): void;

    Asserts that a value matches a regular expression or includes a substring.

    @param expected

    the expected substring or pattern.

    ```
    expect("dog").toMatch(/dog/);
    expect("dog").toMatch("og");
    ```
  + [toMatchInlineSnapshot](https://bun.com/reference/bun/test/Matchers/toMatchInlineSnapshot)(

    value?: string

    ): void;

    Asserts that a value matches the most recent inline snapshot.

    @param value

    The latest automatically-updated snapshot value.

    ```
    expect("Hello").toMatchInlineSnapshot();
    expect("Hello").toMatchInlineSnapshot(`"Hello"`);
    ```

    [toMatchInlineSnapshot](https://bun.com/reference/bun/test/Matchers/toMatchInlineSnapshot)(

    propertyMatchers?: object,

    value?: string

    ): void;

    Asserts that a value matches the most recent inline snapshot.

    @param propertyMatchers

    Object containing properties to match against the value.

    @param value

    The latest automatically-updated snapshot value.

    ```
    expect({ c: new Date() }).toMatchInlineSnapshot({ c: expect.any(Date) });
    expect({ c: new Date() }).toMatchInlineSnapshot({ c: expect.any(Date) }, `
    {
      "v": Any<Date>,
    }
    `);
    ```
  + [toMatchObject](https://bun.com/reference/bun/test/Matchers/toMatchObject)(

    subset: object

    ): void;

    Asserts that an object matches a subset of properties.

    @param subset

    Subset of properties to match with.

    ```
    expect({ a: 1, b: 2 }).toMatchObject({ b: 2 });
    expect({ c: new Date(), d: 2 }).toMatchObject({ d: 2 });
    ```
  + [toMatchSnapshot](https://bun.com/reference/bun/test/Matchers/toMatchSnapshot)(

    hint?: string

    ): void;

    Asserts that a value matches the most recent snapshot.

    @param hint

    Hint used to identify the snapshot in the snapshot file.

    ```
    expect([1, 2, 3]).toMatchSnapshot('hint message');
    ```

    [toMatchSnapshot](https://bun.com/reference/bun/test/Matchers/toMatchSnapshot)(

    propertyMatchers?: object,

    hint?: string

    ): void;

    Asserts that a value matches the most recent snapshot.

    @param propertyMatchers

    Object containing properties to match against the value.

    @param hint

    Hint used to identify the snapshot in the snapshot file.

    ```
    expect([1, 2, 3]).toMatchSnapshot();
    expect({ a: 1, b: 2 }).toMatchSnapshot({ a: 1 });
    expect({ c: new Date() }).toMatchSnapshot({ c: expect.any(Date) });
    ```
  + [toSatisfy](https://bun.com/reference/bun/test/Matchers/toSatisfy)(

    predicate: (value: T) => boolean

    ): void;

    Checks whether a value satisfies a custom condition.

    @param predicate

    The custom condition to be satisfied. It should be a function that takes a value as an argument (in this case the value from expect) and returns a boolean.

    ```
    expect(1).toSatisfy((val) => val > 0);
    expect("foo").toSatisfy((val) => val === "foo");
    expect("bar").not.toSatisfy((val) => val === "bun");
    ```
  + [toStartWith](https://bun.com/reference/bun/test/Matchers/toStartWith)(

    expected: string

    ): void;

    Asserts that a value starts with a `string`.

    @param expected

    the string to start with
  + [toStrictEqual](https://bun.com/reference/bun/test/Matchers/toStrictEqual)(

    expected: T

    ): void;

    Asserts that a value is deeply and strictly equal to what is expected.

    There are two key differences from `toEqual()`:

    1. It checks that the class is the same.
    2. It checks that `undefined` values match as well.

    @param expected

    the expected value

    ```
    class Dog {
      type = "dog";
    }
    const actual = new Dog();
    expect(actual).toStrictEqual(new Dog());
    expect(actual).toStrictEqual({ type: "dog" }); // fail
    ```

    [toStrictEqual](https://bun.com/reference/bun/test/Matchers/toStrictEqual)<X = T>(

    expected: NoInfer<X>

    ): void;
  + [toThrow](https://bun.com/reference/bun/test/Matchers/toThrow)(

    expected?: unknown

    ): void;

    Asserts that a function throws an error.

    - If expected is a `string` or `RegExp`, it will check the `message` property.
    - If expected is an `Error` object, it will check the `name` and `message` properties.
    - If expected is an `Error` constructor, it will check the class of the `Error`.
    - If expected is not provided, it will check if anything has thrown.

    @param expected

    the expected error, error message, or error pattern

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrow("Oops!");
    expect(fail).toThrow(/oops/i);
    expect(fail).toThrow(Error);
    expect(fail).toThrow();
    ```
  + [toThrowError](https://bun.com/reference/bun/test/Matchers/toThrowError)(

    expected?: unknown

    ): void;

    Asserts that a function throws an error.

    - If expected is a `string` or `RegExp`, it will check the `message` property.
    - If expected is an `Error` object, it will check the `name` and `message` properties.
    - If expected is an `Error` constructor, it will check the class of the `Error`.
    - If expected is not provided, it will check if anything has thrown.

    @param expected

    the expected error, error message, or error pattern

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrowError("Oops!");
    expect(fail).toThrowError(/oops/i);
    expect(fail).toThrowError(Error);
    expect(fail).toThrowError();
    ```
  + [toThrowErrorMatchingInlineSnapshot](https://bun.com/reference/bun/test/Matchers/toThrowErrorMatchingInlineSnapshot)(

    value?: string

    ): void;

    Asserts that a function throws an error matching the most recent snapshot.

    @param value

    The latest automatically-updated snapshot value.

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrowErrorMatchingInlineSnapshot();
    expect(fail).toThrowErrorMatchingInlineSnapshot(`"Oops!"`);
    ```
  + [toThrowErrorMatchingSnapshot](https://bun.com/reference/bun/test/Matchers/toThrowErrorMatchingSnapshot)(

    hint?: string

    ): void;

    Asserts that a function throws an error matching the most recent snapshot.

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrowErrorMatchingSnapshot();
    expect(fail).toThrowErrorMatchingSnapshot("This one should say Oops!");
    ```
* ### interface [MatchersBuiltin](https://bun.com/reference/bun/test/MatchersBuiltin)<T = unknown>

  + [fail](https://bun.com/reference/bun/test/MatchersBuiltin/fail): (message?: string) => void

    Assertion which fails.

    ```
    expect().fail();
    expect().fail("message is optional");
    expect().not.fail();
    expect().not.fail("hi");
    ```
  + [not](https://bun.com/reference/bun/test/MatchersBuiltin/not): [Matchers](https://bun.com/reference/bun/test/Matchers)<unknown>

    Negates the result of a subsequent assertion. If you know how to test something, `.not` lets you test its opposite.

    ```
    expect(1).not.toBe(0);
    expect(null).not.toBeNull();
    ```
  + [pass](https://bun.com/reference/bun/test/MatchersBuiltin/pass): (message?: string) => void

    Assertion which passes.

    ```
    expect().pass();
    expect().pass("message is optional");
    expect().not.pass();
    expect().not.pass("hi");
    ```
  + [rejects](https://bun.com/reference/bun/test/MatchersBuiltin/rejects): [Matchers](https://bun.com/reference/bun/test/Matchers)<unknown>

    Expects the value to be a promise that rejects.

    ```
    expect(Promise.reject("error")).rejects.toBe("error");
    ```
  + [resolves](https://bun.com/reference/bun/test/MatchersBuiltin/resolves): [Matchers](https://bun.com/reference/bun/test/Matchers)<Awaited<T>>

    Expects the value to be a promise that resolves.

    ```
    expect(Promise.resolve(1)).resolves.toBe(1);
    ```
  + [lastCalledWith](https://bun.com/reference/bun/test/MatchersBuiltin/lastCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the nth call.
  + [nthCalledWith](https://bun.com/reference/bun/test/MatchersBuiltin/nthCalledWith)(

    n: number,

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the nth call.
  + [toBe](https://bun.com/reference/bun/test/MatchersBuiltin/toBe)(

    expected: T

    ): void;

    Asserts that a value equals what is expected.

    - For non-primitive values, like objects and arrays, use `toEqual()` instead.
    - For floating-point numbers, use `toBeCloseTo()` instead.

    @param expected

    the expected value

    ```
    expect(100 + 23).toBe(123);
    expect("d" + "og").toBe("dog");
    expect([123]).toBe([123]); // fail, use toEqual()
    expect(3 + 0.14).toBe(3.14); // fail, use toBeCloseTo()

    // TypeScript errors:
    expect("hello").toBe(3.14); // typescript error + fail
    expect("hello").toBe<number>(3.14); // no typescript error, but still fails
    ```

    [toBe](https://bun.com/reference/bun/test/MatchersBuiltin/toBe)<X = T>(

    expected: NoInfer<X>

    ): void;
  + [toBeArray](https://bun.com/reference/bun/test/MatchersBuiltin/toBeArray)(): void;

    Asserts that a value is a `array`.

    ```
    expect([1]).toBeArray();
    expect(new Array(1)).toBeArray();
    expect({}).not.toBeArray();
    ```
  + [toBeArrayOfSize](https://bun.com/reference/bun/test/MatchersBuiltin/toBeArrayOfSize)(

    size: number

    ): void;

    Asserts that a value is a `array` of a certain length.

    ```
    expect([]).toBeArrayOfSize(0);
    expect([1]).toBeArrayOfSize(1);
    expect(new Array(1)).toBeArrayOfSize(1);
    expect({}).not.toBeArrayOfSize(0);
    ```
  + [toBeBoolean](https://bun.com/reference/bun/test/MatchersBuiltin/toBeBoolean)(): void;

    Asserts that a value is a `boolean`.

    ```
    expect(true).toBeBoolean();
    expect(false).toBeBoolean();
    expect(null).not.toBeBoolean();
    expect(0).not.toBeBoolean();
    ```
  + [toBeCalled](https://bun.com/reference/bun/test/MatchersBuiltin/toBeCalled)(): void;

    Ensures that a mock function is called an exact number of times.
  + [toBeCalledTimes](https://bun.com/reference/bun/test/MatchersBuiltin/toBeCalledTimes)(

    expected: number

    ): void;

    Ensure that a mock function is called with specific arguments.
  + [toBeCalledWith](https://bun.com/reference/bun/test/MatchersBuiltin/toBeCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments.
  + [toBeCloseTo](https://bun.com/reference/bun/test/MatchersBuiltin/toBeCloseTo)(

    expected: number,

    numDigits?: number

    ): void;

    Asserts that value is close to the expected by floating point precision.

    For example, the following fails because arithmetic on decimal (base 10) values often have rounding errors in limited precision binary (base 2) representation.

    @param expected

    the expected value

    @param numDigits

    the number of digits to check after the decimal point. Default is `2`

    ```
    expect(0.2 + 0.1).toBe(0.3); // fails

    Use `toBeCloseTo` to compare floating point numbers for approximate equality.
    ```
  + [toBeDate](https://bun.com/reference/bun/test/MatchersBuiltin/toBeDate)(): void;

    Asserts that a value is a `Date` object.

    To check if a date is valid, use `toBeValidDate()` instead.

    ```
    expect(new Date()).toBeDate();
    expect(new Date(null)).toBeDate();
    expect("2020-03-01").not.toBeDate();
    ```
  + [toBeDefined](https://bun.com/reference/bun/test/MatchersBuiltin/toBeDefined)(): void;

    Asserts that a value is defined. (e.g. is not `undefined`)

    ```
    expect(true).toBeDefined();
    expect(undefined).toBeDefined(); // fail
    ```
  + [toBeEmpty](https://bun.com/reference/bun/test/MatchersBuiltin/toBeEmpty)(): void;

    Asserts that a value is empty.

    ```
    expect("").toBeEmpty();
    expect([]).toBeEmpty();
    expect({}).toBeEmpty();
    expect(new Set()).toBeEmpty();
    ```
  + [toBeEmptyObject](https://bun.com/reference/bun/test/MatchersBuiltin/toBeEmptyObject)(): void;

    Asserts that a value is an empty `object`.

    ```
    expect({}).toBeEmptyObject();
    expect({ a: 'hello' }).not.toBeEmptyObject();
    ```
  + [toBeEven](https://bun.com/reference/bun/test/MatchersBuiltin/toBeEven)(): void;

    Asserts that a number is even.

    ```
    expect(2).toBeEven();
    expect(1).not.toBeEven();
    ```
  + [toBeFalse](https://bun.com/reference/bun/test/MatchersBuiltin/toBeFalse)(): void;

    Asserts that a value is `false`.

    ```
    expect(false).toBeFalse();
    expect(true).not.toBeFalse();
    expect(0).not.toBeFalse();
    ```
  + [toBeFalsy](https://bun.com/reference/bun/test/MatchersBuiltin/toBeFalsy)(): void;

    Asserts that a value is "falsy".

    To assert that a value equals `false`, use `toBe(false)` instead.

    ```
    expect(true).toBeTruthy();
    expect(1).toBeTruthy();
    expect({}).toBeTruthy();
    ```
  + [toBeFinite](https://bun.com/reference/bun/test/MatchersBuiltin/toBeFinite)(): void;

    Asserts that a value is a `number`, and is not `NaN` or `Infinity`.

    ```
    expect(1).toBeFinite();
    expect(3.14).toBeFinite();
    expect(NaN).not.toBeFinite();
    expect(Infinity).not.toBeFinite();
    ```
  + [toBeFunction](https://bun.com/reference/bun/test/MatchersBuiltin/toBeFunction)(): void;

    Asserts that a value is a `function`.

    ```
    expect(() => {}).toBeFunction();
    ```
  + [toBeGreaterThan](https://bun.com/reference/bun/test/MatchersBuiltin/toBeGreaterThan)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is greater than the expected value.

    @param expected

    the expected number

    ```
    expect(1).toBeGreaterThan(0);
    expect(3.14).toBeGreaterThan(3);
    expect(9).toBeGreaterThan(9); // fail
    ```
  + [toBeGreaterThanOrEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toBeGreaterThanOrEqual)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is greater than or equal to the expected value.

    @param expected

    the expected number

    ```
    expect(1).toBeGreaterThanOrEqual(0);
    expect(3.14).toBeGreaterThanOrEqual(3);
    expect(9).toBeGreaterThanOrEqual(9);
    ```
  + [toBeInstanceOf](https://bun.com/reference/bun/test/MatchersBuiltin/toBeInstanceOf)(

    value: unknown

    ): void;

    Asserts that the expected value is an instance of value

    ```
    expect([]).toBeInstanceOf(Array);
    expect(null).toBeInstanceOf(Array); // fail
    ```
  + [toBeInteger](https://bun.com/reference/bun/test/MatchersBuiltin/toBeInteger)(): void;

    Asserts that a value is a `number`, and is an integer.

    ```
    expect(1).toBeInteger();
    expect(3.14).not.toBeInteger();
    expect(NaN).not.toBeInteger();
    ```
  + [toBeLessThan](https://bun.com/reference/bun/test/MatchersBuiltin/toBeLessThan)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is less than the expected value.

    @param expected

    the expected number

    ```
    expect(-1).toBeLessThan(0);
    expect(3).toBeLessThan(3.14);
    expect(9).toBeLessThan(9); // fail
    ```
  + [toBeLessThanOrEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toBeLessThanOrEqual)(

    expected: number | bigint

    ): void;

    Asserts that a value is a `number` and is less than or equal to the expected value.

    @param expected

    the expected number

    ```
    expect(-1).toBeLessThanOrEqual(0);
    expect(3).toBeLessThanOrEqual(3.14);
    expect(9).toBeLessThanOrEqual(9);
    ```
  + [toBeNaN](https://bun.com/reference/bun/test/MatchersBuiltin/toBeNaN)(): void;

    Asserts that a value is `NaN`.

    Same as using `Number.isNaN()`.

    ```
    expect(NaN).toBeNaN();
    expect(Infinity).toBeNaN(); // fail
    expect("notanumber").toBeNaN(); // fail
    ```
  + [toBeNegative](https://bun.com/reference/bun/test/MatchersBuiltin/toBeNegative)(): void;

    Asserts that a value is a negative `number`.

    ```
    expect(-3.14).toBeNegative();
    expect(1).not.toBeNegative();
    expect(NaN).not.toBeNegative();
    ```
  + [toBeNil](https://bun.com/reference/bun/test/MatchersBuiltin/toBeNil)(): void;

    Asserts that a value is `null` or `undefined`.

    ```
    expect(null).toBeNil();
    expect(undefined).toBeNil();
    ```
  + [toBeNull](https://bun.com/reference/bun/test/MatchersBuiltin/toBeNull)(): void;

    Asserts that a value is `null`.

    ```
    expect(null).toBeNull();
    expect(undefined).toBeNull(); // fail
    ```
  + [toBeNumber](https://bun.com/reference/bun/test/MatchersBuiltin/toBeNumber)(): void;

    Asserts that a value is a `number`.

    ```
    expect(1).toBeNumber();
    expect(3.14).toBeNumber();
    expect(NaN).toBeNumber();
    expect(BigInt(1)).not.toBeNumber();
    ```
  + [toBeObject](https://bun.com/reference/bun/test/MatchersBuiltin/toBeObject)(): void;

    Asserts that a value is an `object`.

    ```
    expect({}).toBeObject();
    expect("notAnObject").not.toBeObject();
    expect(NaN).not.toBeObject();
    ```
  + [toBeOdd](https://bun.com/reference/bun/test/MatchersBuiltin/toBeOdd)(): void;

    Asserts that a number is odd.

    ```
    expect(1).toBeOdd();
    expect(2).not.toBeOdd();
    ```
  + [toBeOneOf](https://bun.com/reference/bun/test/MatchersBuiltin/toBeOneOf)(

    expected: Iterable<T>

    ): void;

    Asserts that the value is deep equal to an element in the expected array.

    The value must be an array or iterable, which includes strings.

    @param expected

    the expected value

    ```
    expect(1).toBeOneOf([1,2,3]);
    expect("foo").toBeOneOf(["foo", "bar"]);
    expect(true).toBeOneOf(new Set([true]));
    ```

    [toBeOneOf](https://bun.com/reference/bun/test/MatchersBuiltin/toBeOneOf)<X = T>(

    expected: NoInfer<Iterable<X, any, any>>

    ): void;
  + [toBePositive](https://bun.com/reference/bun/test/MatchersBuiltin/toBePositive)(): void;

    Asserts that a value is a positive `number`.

    ```
    expect(1).toBePositive();
    expect(-3.14).not.toBePositive();
    expect(NaN).not.toBePositive();
    ```
  + [toBeString](https://bun.com/reference/bun/test/MatchersBuiltin/toBeString)(): void;

    Asserts that a value is a `string`.

    ```
    expect("foo").toBeString();
    expect(new String("bar")).toBeString();
    expect(123).not.toBeString();
    ```
  + [toBeSymbol](https://bun.com/reference/bun/test/MatchersBuiltin/toBeSymbol)(): void;

    Asserts that a value is a `symbol`.

    ```
    expect(Symbol("foo")).toBeSymbol();
    expect("foo").not.toBeSymbol();
    ```
  + [toBeTrue](https://bun.com/reference/bun/test/MatchersBuiltin/toBeTrue)(): void;

    Asserts that a value is `true`.

    ```
    expect(true).toBeTrue();
    expect(false).not.toBeTrue();
    expect(1).not.toBeTrue();
    ```
  + [toBeTruthy](https://bun.com/reference/bun/test/MatchersBuiltin/toBeTruthy)(): void;

    Asserts that a value is "truthy".

    To assert that a value equals `true`, use `toBe(true)` instead.

    ```
    expect(true).toBeTruthy();
    expect(1).toBeTruthy();
    expect({}).toBeTruthy();
    ```
  + [toBeTypeOf](https://bun.com/reference/bun/test/MatchersBuiltin/toBeTypeOf)(

    type: 'string' | 'number' | 'bigint' | 'boolean' | 'symbol' | 'undefined' | 'object' | 'function'

    ): void;

    Asserts that a value matches a specific type.

    ```
    expect(1).toBeTypeOf("number");
    expect("hello").toBeTypeOf("string");
    expect([]).not.toBeTypeOf("boolean");
    ```
  + [toBeUndefined](https://bun.com/reference/bun/test/MatchersBuiltin/toBeUndefined)(): void;

    Asserts that a value is `undefined`.

    ```
    expect(undefined).toBeUndefined();
    expect(null).toBeUndefined(); // fail
    ```
  + [toBeValidDate](https://bun.com/reference/bun/test/MatchersBuiltin/toBeValidDate)(): void;

    Asserts that a value is a valid `Date` object.

    ```
    expect(new Date()).toBeValidDate();
    expect(new Date(null)).not.toBeValidDate();
    expect("2020-03-01").not.toBeValidDate();
    ```
  + [toBeWithin](https://bun.com/reference/bun/test/MatchersBuiltin/toBeWithin)(

    start: number,

    end: number

    ): void;

    Asserts that a value is a number between a start and end value.

    @param start

    the start number (inclusive)

    @param end

    the end number (exclusive)
  + [toContain](https://bun.com/reference/bun/test/MatchersBuiltin/toContain)(

    expected: T extends Iterable<U, any, any> ? U : T

    ): void;

    Asserts that a value contains what is expected.

    The value must be an array or iterable, which includes strings.

    @param expected

    the expected value

    ```
    expect([1, 2, 3]).toContain(1);
    expect(new Set([true])).toContain(true);
    expect("hello").toContain("o");
    ```

    [toContain](https://bun.com/reference/bun/test/MatchersBuiltin/toContain)<X = T>(

    expected: NoInfer<X extends Iterable<U, any, any> ? U : X>

    ): void;
  + [toContainAllKeys](https://bun.com/reference/bun/test/MatchersBuiltin/toContainAllKeys)(

    expected: keyof T[]

    ): void;

    Asserts that an `object` contains all the provided keys.

    The value must be an object

    @param expected

    the expected value

    ```
    expect({ a: 'hello', b: 'world' }).toContainAllKeys(['a','b']);
    expect({ a: 'hello', b: 'world' }).toContainAllKeys(['b','a']);
    expect({ 1: 'hello', b: 'world' }).toContainAllKeys([1,'b']);
    expect({ a: 'hello', b: 'world' }).not.toContainAllKeys(['c']);
    expect({ a: 'hello', b: 'world' }).not.toContainAllKeys(['a']);
    ```

    [toContainAllKeys](https://bun.com/reference/bun/test/MatchersBuiltin/toContainAllKeys)<X = T>(

    expected: NoInfer<keyof X[]>

    ): void;
  + [toContainAllValues](https://bun.com/reference/bun/test/MatchersBuiltin/toContainAllValues)(

    expected: unknown[]

    ): void;

    Asserts that an `object` contain all the provided values.

    The value must be an object

    @param expected

    the expected value

    ```
    const o = { a: 'foo', b: 'bar', c: 'baz' };
    expect(o).toContainAllValues(['foo', 'bar', 'baz']);
    expect(o).toContainAllValues(['baz', 'bar', 'foo']);
    expect(o).not.toContainAllValues(['bar', 'foo']);
    ```
  + [toContainAnyKeys](https://bun.com/reference/bun/test/MatchersBuiltin/toContainAnyKeys)(

    expected: keyof T[]

    ): void;

    Asserts that an `object` contains at least one of the provided keys. Asserts that an `object` contains all the provided keys.

    The value must be an object

    @param expected

    the expected value

    ```
    expect({ a: 'hello', b: 'world' }).toContainAnyKeys(['a']);
    expect({ a: 'hello', b: 'world' }).toContainAnyKeys(['b']);
    expect({ a: 'hello', b: 'world' }).toContainAnyKeys(['b', 'c']);
    expect({ a: 'hello', b: 'world' }).not.toContainAnyKeys(['c']);
    ```

    [toContainAnyKeys](https://bun.com/reference/bun/test/MatchersBuiltin/toContainAnyKeys)<X = T>(

    expected: NoInfer<keyof X[]>

    ): void;
  + [toContainAnyValues](https://bun.com/reference/bun/test/MatchersBuiltin/toContainAnyValues)(

    expected: unknown[]

    ): void;

    Asserts that an `object` contain any provided value.

    The value must be an object

    @param expected

    the expected value

    ```
    const o = { a: 'foo', b: 'bar', c: 'baz' };
    expect(o).toContainAnyValues(['qux', 'foo']);
    expect(o).toContainAnyValues(['qux', 'bar']);
    expect(o).toContainAnyValues(['qux', 'baz']);
    expect(o).not.toContainAnyValues(['qux']);
    ```
  + [toContainEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toContainEqual)(

    expected: T extends Iterable<U, any, any> ? U : T

    ): void;

    Asserts that a value contains and equals what is expected.

    This matcher will perform a deep equality check for members of arrays, rather than checking for object identity.

    @param expected

    the expected value

    ```
    expect([{ a: 1 }]).toContainEqual({ a: 1 });
    expect([{ a: 1 }]).not.toContainEqual({ a: 2 });
    ```

    [toContainEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toContainEqual)<X = T>(

    expected: NoInfer<X extends Iterable<U, any, any> ? U : X>

    ): void;
  + [toContainKey](https://bun.com/reference/bun/test/MatchersBuiltin/toContainKey)(

    expected: keyof T

    ): void;

    Asserts that an `object` contains a key.

    The value must be an object

    @param expected

    the expected value

    ```
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKey('a');
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKey('b');
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKey('c');
    expect({ a: 'foo', b: 'bar', c: 'baz' }).not.toContainKey('d');
    ```

    [toContainKey](https://bun.com/reference/bun/test/MatchersBuiltin/toContainKey)<X = T>(

    expected: NoInfer<keyof X>

    ): void;
  + [toContainKeys](https://bun.com/reference/bun/test/MatchersBuiltin/toContainKeys)(

    expected: keyof T[]

    ): void;

    Asserts that an `object` contains all the provided keys.

    @param expected

    the expected value

    ```
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKeys(['a', 'b']);
    expect({ a: 'foo', b: 'bar', c: 'baz' }).toContainKeys(['a', 'b', 'c']);
    expect({ a: 'foo', b: 'bar', c: 'baz' }).not.toContainKeys(['a', 'b', 'e']);
    ```

    [toContainKeys](https://bun.com/reference/bun/test/MatchersBuiltin/toContainKeys)<X = T>(

    expected: NoInfer<keyof X[]>

    ): void;
  + [toContainValue](https://bun.com/reference/bun/test/MatchersBuiltin/toContainValue)(

    expected: unknown

    ): void;

    Asserts that an `object` contain the provided value.

    This method is deep and will look through child properties to find the expected value.

    The input value must be an object.

    @param expected

    the expected value

    ```
    const shallow = { hello: "world" };
    const deep = { message: shallow };
    const deepArray = { message: [shallow] };
    const o = { a: "foo", b: [1, "hello", true], c: "baz" };

    expect(shallow).toContainValue("world");
    expect({ foo: false }).toContainValue(false);
    expect(deep).toContainValue({ hello: "world" });
    expect(deepArray).toContainValue([{ hello: "world" }]);

    expect(o).toContainValue("foo", "barr");
    expect(o).toContainValue([1, "hello", true]);
    expect(o).not.toContainValue("qux");

    // NOT
    expect(shallow).not.toContainValue("foo");
    expect(deep).not.toContainValue({ foo: "bar" });
    expect(deepArray).not.toContainValue([{ foo: "bar" }]);
    ```
  + [toContainValues](https://bun.com/reference/bun/test/MatchersBuiltin/toContainValues)(

    expected: unknown[]

    ): void;

    Asserts that an `object` contain the provided value.

    This is the same as toContainValue, but accepts an array of values instead.

    The value must be an object

    @param expected

    the expected value

    ```
    const o = { a: 'foo', b: 'bar', c: 'baz' };
    expect(o).toContainValues(['foo']);
    expect(o).toContainValues(['baz', 'bar']);
    expect(o).not.toContainValues(['qux', 'foo']);
    ```
  + [toEndWith](https://bun.com/reference/bun/test/MatchersBuiltin/toEndWith)(

    expected: string

    ): void;

    Asserts that a value ends with a `string`.

    @param expected

    the string to end with
  + [toEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toEqual)(

    expected: T

    ): void;

    Asserts that a value is deeply equal to what is expected.

    @param expected

    the expected value

    ```
    expect(100 + 23).toBe(123);
    expect("d" + "og").toBe("dog");
    expect([456]).toEqual([456]);
    expect({ value: 1 }).toEqual({ value: 1 });
    ```

    [toEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toEqual)<X = T>(

    expected: NoInfer<X>

    ): void;
  + [toEqualIgnoringWhitespace](https://bun.com/reference/bun/test/MatchersBuiltin/toEqualIgnoringWhitespace)(

    expected: string

    ): void;

    Asserts that a value is equal to the expected string, ignoring any whitespace.

    @param expected

    the expected string

    ```
    expect(" foo ").toEqualIgnoringWhitespace("foo");
    expect("bar").toEqualIgnoringWhitespace(" bar ");
    ```
  + [toHaveBeenCalled](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveBeenCalled)(): void;

    Ensures that a mock function is called.
  + [toHaveBeenCalledTimes](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveBeenCalledTimes)(

    expected: number

    ): void;

    Ensures that a mock function is called an exact number of times.
  + [toHaveBeenCalledWith](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveBeenCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments.
  + [toHaveBeenLastCalledWith](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveBeenLastCalledWith)(

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the last call.
  + [toHaveBeenNthCalledWith](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveBeenNthCalledWith)(

    n: number,

    ...expected: unknown[]

    ): void;

    Ensure that a mock function is called with specific arguments for the nth call.
  + [toHaveLastReturnedWith](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveLastReturnedWith)(

    expected: unknown

    ): void;

    Ensures that a mock function has returned a specific value on its last invocation. This matcher uses deep equality, like toEqual(), and supports asymmetric matchers.
  + [toHaveLength](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveLength)(

    length: number

    ): void;

    Asserts that a value has a `.length` property that is equal to the expected length.

    @param length

    the expected length

    ```
    expect([]).toHaveLength(0);
    expect("hello").toHaveLength(4);
    ```
  + [toHaveNthReturnedWith](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveNthReturnedWith)(

    n: number,

    expected: unknown

    ): void;

    Ensures that a mock function has returned a specific value on the nth invocation. This matcher uses deep equality, like toEqual(), and supports asymmetric matchers.

    @param n

    The 1-based index of the function call

    @param expected

    The expected return value
  + [toHaveProperty](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveProperty)(

    keyPath: string | number | string | number[],

    value?: unknown

    ): void;

    Asserts that a value has a property with the expected name, and value if provided.

    @param keyPath

    the expected property name or path, or an index

    @param value

    the expected property value, if provided

    ```
    expect(new Set()).toHaveProperty("size");
    expect(new Uint8Array()).toHaveProperty("byteLength", 0);
    expect({ kitchen: { area: 20 }}).toHaveProperty("kitchen.area", 20);
    expect({ kitchen: { area: 20 }}).toHaveProperty(["kitchen", "area"], 20);
    ```
  + [toHaveReturned](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveReturned)(): void;

    Ensures that a mock function has returned successfully at least once.

    A promise that is unfulfilled will be considered a failure. If the function threw an error, it will be considered a failure.
  + [toHaveReturnedTimes](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveReturnedTimes)(

    times: number

    ): void;

    Ensures that a mock function has returned successfully at `times` times.

    A promise that is unfulfilled will be considered a failure. If the function threw an error, it will be considered a failure.
  + [toHaveReturnedWith](https://bun.com/reference/bun/test/MatchersBuiltin/toHaveReturnedWith)(

    expected: unknown

    ): void;

    Ensures that a mock function has returned a specific value. This matcher uses deep equality, like toEqual(), and supports asymmetric matchers.
  + [toInclude](https://bun.com/reference/bun/test/MatchersBuiltin/toInclude)(

    expected: string

    ): void;

    Asserts that a value includes a `string`.

    For non-string values, use `toContain()` instead.

    @param expected

    the expected substring
  + [toIncludeRepeated](https://bun.com/reference/bun/test/MatchersBuiltin/toIncludeRepeated)(

    expected: string,

    times: number

    ): void;

    Asserts that a value includes a `string` {times} times.

    @param expected

    the expected substring

    @param times

    the number of times the substring should occur
  + [toMatch](https://bun.com/reference/bun/test/MatchersBuiltin/toMatch)(

    expected: string | RegExp

    ): void;

    Asserts that a value matches a regular expression or includes a substring.

    @param expected

    the expected substring or pattern.

    ```
    expect("dog").toMatch(/dog/);
    expect("dog").toMatch("og");
    ```
  + [toMatchInlineSnapshot](https://bun.com/reference/bun/test/MatchersBuiltin/toMatchInlineSnapshot)(

    value?: string

    ): void;

    Asserts that a value matches the most recent inline snapshot.

    @param value

    The latest automatically-updated snapshot value.

    ```
    expect("Hello").toMatchInlineSnapshot();
    expect("Hello").toMatchInlineSnapshot(`"Hello"`);
    ```

    [toMatchInlineSnapshot](https://bun.com/reference/bun/test/MatchersBuiltin/toMatchInlineSnapshot)(

    propertyMatchers?: object,

    value?: string

    ): void;

    Asserts that a value matches the most recent inline snapshot.

    @param propertyMatchers

    Object containing properties to match against the value.

    @param value

    The latest automatically-updated snapshot value.

    ```
    expect({ c: new Date() }).toMatchInlineSnapshot({ c: expect.any(Date) });
    expect({ c: new Date() }).toMatchInlineSnapshot({ c: expect.any(Date) }, `
    {
      "v": Any<Date>,
    }
    `);
    ```
  + [toMatchObject](https://bun.com/reference/bun/test/MatchersBuiltin/toMatchObject)(

    subset: object

    ): void;

    Asserts that an object matches a subset of properties.

    @param subset

    Subset of properties to match with.

    ```
    expect({ a: 1, b: 2 }).toMatchObject({ b: 2 });
    expect({ c: new Date(), d: 2 }).toMatchObject({ d: 2 });
    ```
  + [toMatchSnapshot](https://bun.com/reference/bun/test/MatchersBuiltin/toMatchSnapshot)(

    hint?: string

    ): void;

    Asserts that a value matches the most recent snapshot.

    @param hint

    Hint used to identify the snapshot in the snapshot file.

    ```
    expect([1, 2, 3]).toMatchSnapshot('hint message');
    ```

    [toMatchSnapshot](https://bun.com/reference/bun/test/MatchersBuiltin/toMatchSnapshot)(

    propertyMatchers?: object,

    hint?: string

    ): void;

    Asserts that a value matches the most recent snapshot.

    @param propertyMatchers

    Object containing properties to match against the value.

    @param hint

    Hint used to identify the snapshot in the snapshot file.

    ```
    expect([1, 2, 3]).toMatchSnapshot();
    expect({ a: 1, b: 2 }).toMatchSnapshot({ a: 1 });
    expect({ c: new Date() }).toMatchSnapshot({ c: expect.any(Date) });
    ```
  + [toSatisfy](https://bun.com/reference/bun/test/MatchersBuiltin/toSatisfy)(

    predicate: (value: T) => boolean

    ): void;

    Checks whether a value satisfies a custom condition.

    @param predicate

    The custom condition to be satisfied. It should be a function that takes a value as an argument (in this case the value from expect) and returns a boolean.

    ```
    expect(1).toSatisfy((val) => val > 0);
    expect("foo").toSatisfy((val) => val === "foo");
    expect("bar").not.toSatisfy((val) => val === "bun");
    ```
  + [toStartWith](https://bun.com/reference/bun/test/MatchersBuiltin/toStartWith)(

    expected: string

    ): void;

    Asserts that a value starts with a `string`.

    @param expected

    the string to start with
  + [toStrictEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toStrictEqual)(

    expected: T

    ): void;

    Asserts that a value is deeply and strictly equal to what is expected.

    There are two key differences from `toEqual()`:

    1. It checks that the class is the same.
    2. It checks that `undefined` values match as well.

    @param expected

    the expected value

    ```
    class Dog {
      type = "dog";
    }
    const actual = new Dog();
    expect(actual).toStrictEqual(new Dog());
    expect(actual).toStrictEqual({ type: "dog" }); // fail
    ```

    [toStrictEqual](https://bun.com/reference/bun/test/MatchersBuiltin/toStrictEqual)<X = T>(

    expected: NoInfer<X>

    ): void;
  + [toThrow](https://bun.com/reference/bun/test/MatchersBuiltin/toThrow)(

    expected?: unknown

    ): void;

    Asserts that a function throws an error.

    - If expected is a `string` or `RegExp`, it will check the `message` property.
    - If expected is an `Error` object, it will check the `name` and `message` properties.
    - If expected is an `Error` constructor, it will check the class of the `Error`.
    - If expected is not provided, it will check if anything has thrown.

    @param expected

    the expected error, error message, or error pattern

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrow("Oops!");
    expect(fail).toThrow(/oops/i);
    expect(fail).toThrow(Error);
    expect(fail).toThrow();
    ```
  + [toThrowError](https://bun.com/reference/bun/test/MatchersBuiltin/toThrowError)(

    expected?: unknown

    ): void;

    Asserts that a function throws an error.

    - If expected is a `string` or `RegExp`, it will check the `message` property.
    - If expected is an `Error` object, it will check the `name` and `message` properties.
    - If expected is an `Error` constructor, it will check the class of the `Error`.
    - If expected is not provided, it will check if anything has thrown.

    @param expected

    the expected error, error message, or error pattern

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrowError("Oops!");
    expect(fail).toThrowError(/oops/i);
    expect(fail).toThrowError(Error);
    expect(fail).toThrowError();
    ```
  + [toThrowErrorMatchingInlineSnapshot](https://bun.com/reference/bun/test/MatchersBuiltin/toThrowErrorMatchingInlineSnapshot)(

    value?: string

    ): void;

    Asserts that a function throws an error matching the most recent snapshot.

    @param value

    The latest automatically-updated snapshot value.

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrowErrorMatchingInlineSnapshot();
    expect(fail).toThrowErrorMatchingInlineSnapshot(`"Oops!"`);
    ```
  + [toThrowErrorMatchingSnapshot](https://bun.com/reference/bun/test/MatchersBuiltin/toThrowErrorMatchingSnapshot)(

    hint?: string

    ): void;

    Asserts that a function throws an error matching the most recent snapshot.

    ```
    function fail() {
      throw new Error("Oops!");
    }
    expect(fail).toThrowErrorMatchingSnapshot();
    expect(fail).toThrowErrorMatchingSnapshot("This one should say Oops!");
    ```
* ### interface [Test](https://bun.com/reference/bun/test/Test)<T extends ReadonlyArray<unknown>>

  Runs a test.

  ```
  test("can check if using Bun", () => {
    expect(Bun).toBeDefined();
  });

  test("can make a fetch() request", async () => {
    const response = await fetch("https://example.com/");
    expect(response.ok).toBe(true);
  });

  test("can set a timeout", async () => {
    await Bun.sleep(100);
  }, 50); // or { timeout: 50 }
  ```

  + [concurrent](https://bun.com/reference/bun/test/Test/concurrent): [Test](https://bun.com/reference/bun/test/Test)<T>

    Runs the test concurrently with other concurrent tests.
  + [failing](https://bun.com/reference/bun/test/Test/failing): [Test](https://bun.com/reference/bun/test/Test)<T>

    Marks this test as failing.

    Use `test.failing` when you are writing a test and expecting it to fail. These tests will behave the other way normal tests do. If failing test will throw any errors then it will pass. If it does not throw it will fail.

    `test.failing` is very similar to test.todo except that it always runs, regardless of the `--todo` flag.
  + [only](https://bun.com/reference/bun/test/Test/only): [Test](https://bun.com/reference/bun/test/Test)<T>

    Skips all other tests, except this test.
  + [serial](https://bun.com/reference/bun/test/Test/serial): [Test](https://bun.com/reference/bun/test/Test)<T>

    Forces the test to run serially (not in parallel), even when the --concurrent flag is used.
  + [skip](https://bun.com/reference/bun/test/Test/skip): [Test](https://bun.com/reference/bun/test/Test)<T>

    Skips this test.
  + [todo](https://bun.com/reference/bun/test/Test/todo): [Test](https://bun.com/reference/bun/test/Test)<T>

    Marks this test as to be written or to be fixed.

    These tests will not be executed unless the `--todo` flag is passed. With the flag, if the test passes, the test will be marked as `fail` in the results; you will have to remove the `.todo` or check that your test is implemented correctly.
  + [concurrentIf](https://bun.com/reference/bun/test/Test/concurrentIf)(

    condition: boolean

    ): [Test](https://bun.com/reference/bun/test/Test)<T>;

    Runs the test concurrently with other concurrent tests, if `condition` is true.

    @param condition

    if the test should run concurrently
  + [each](https://bun.com/reference/bun/test/Test/each)<T extends unknown[]>(

    table: readonly T[]

    ): [Test](https://bun.com/reference/bun/test/Test)<T>;

    [each](https://bun.com/reference/bun/test/Test/each)<T>(

    table: T[]

    ): [Test](https://bun.com/reference/bun/test/Test)<[T]>;
  + [failingIf](https://bun.com/reference/bun/test/Test/failingIf)(

    condition: boolean

    ): [Test](https://bun.com/reference/bun/test/Test)<T>;

    Marks this test as failing, if `condition` is true.

    @param condition

    if the test should be marked as failing
  + [if](https://bun.com/reference/bun/test/Test/if)(

    condition: boolean

    ): [Test](https://bun.com/reference/bun/test/Test)<T>;

    Runs this test, if `condition` is true.

    This is the opposite of `test.skipIf()`.

    @param condition

    if the test should run
  + [serialIf](https://bun.com/reference/bun/test/Test/serialIf)(

    condition: boolean

    ): [Test](https://bun.com/reference/bun/test/Test)<T>;

    Forces the test to run serially (not in parallel), if `condition` is true. This applies even when the --concurrent flag is used.

    @param condition

    if the test should run serially
  + [skipIf](https://bun.com/reference/bun/test/Test/skipIf)(

    condition: boolean

    ): [Test](https://bun.com/reference/bun/test/Test)<T>;

    Skips this test, if `condition` is true.

    @param condition

    if the test should be skipped
  + [todoIf](https://bun.com/reference/bun/test/Test/todoIf)(

    condition: boolean

    ): [Test](https://bun.com/reference/bun/test/Test)<T>;

    Marks this test as to be written or to be fixed, if `condition` is true.

    @param condition

    if the test should be marked TODO
* ### interface [TesterContext](https://bun.com/reference/bun/test/TesterContext)

  + [equals](https://bun.com/reference/bun/test/TesterContext/equals): [EqualsFunction](https://bun.com/reference/bun/test/EqualsFunction)
* ### interface [TestOptions](https://bun.com/reference/bun/test/TestOptions)

  + [repeats](https://bun.com/reference/bun/test/TestOptions/repeats)?: number

    Sets the number of times to repeat the test, regardless of whether it passed or failed.
  + [retry](https://bun.com/reference/bun/test/TestOptions/retry)?: number

    Sets the number of times to retry the test if it fails.
  + [timeout](https://bun.com/reference/bun/test/TestOptions/timeout)?: number

    Sets the timeout for the test in milliseconds.

    If the test does not complete within this time, the test will fail with:

    ```
    'Timeout: test {name} timed out after 5000ms'
    ```
* type [AsymmetricMatcher](https://bun.com/reference/bun/test/AsymmetricMatcher) = any

  Object representing an asymmetric matcher obtained by an static call to expect like `expect.anything()`, `expect.stringContaining("...")`, etc.
* type [CustomMatcher](https://bun.com/reference/bun/test/CustomMatcher)<E, P extends any[]> = (this: MatcherContext, expected: E, ...matcherArguments: P) => [MatcherResult](https://bun.com/reference/bun/test/MatcherResult) | Promise<[MatcherResult](https://bun.com/reference/bun/test/MatcherResult)>
* type [CustomMatchersDetected](https://bun.com/reference/bun/test/CustomMatchersDetected) = Omit<[Matchers](https://bun.com/reference/bun/test/Matchers)<unknown>, keyof [MatchersBuiltin](https://bun.com/reference/bun/test/MatchersBuiltin)<unknown>> & Omit<[AsymmetricMatchers](https://bun.com/reference/bun/test/AsymmetricMatchers), keyof [AsymmetricMatchersBuiltin](https://bun.com/reference/bun/test/AsymmetricMatchersBuiltin)>

  All non-builtin matchers and asymmetric matchers that have been type-registered through declaration merging
* type [EqualsFunction](https://bun.com/reference/bun/test/EqualsFunction) = (a: unknown, b: unknown) => boolean
* type [ExpectExtendMatchers](https://bun.com/reference/bun/test/ExpectExtendMatchers)<M> = { [K in keyof M]: k extends keyof [CustomMatchersDetected](https://bun.com/reference/bun/test/CustomMatchersDetected) ? [CustomMatcher](https://bun.com/reference/bun/test/CustomMatcher)<unknown, Parameters<[CustomMatchersDetected](https://bun.com/reference/bun/test/CustomMatchersDetected)[k]>> : [CustomMatcher](https://bun.com/reference/bun/test/CustomMatcher)<unknown, any[]> }

  If the types has been defined through declaration merging, enforce it. Otherwise enforce the generic custom matcher signature.
* type [Mock](https://bun.com/reference/bun/test/Mock)<T extends (...args: any[]) => any> = JestMock.Mock<T>
* type [Tester](https://bun.com/reference/bun/test/Tester) = (this: [TesterContext](https://bun.com/reference/bun/test/TesterContext), a: any, b: any, customTesters: [Tester](https://bun.com/reference/bun/test/Tester)[]) => boolean | undefined

  Custom equality tester