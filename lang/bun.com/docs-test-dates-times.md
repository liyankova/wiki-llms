---
url: https://bun.com/docs/test/dates-times
title: Dates and times - Bun
source_domain: bun.com
---

# Dates and times - Bun

`bun:test` lets you change what time it is in your tests.
This works with any of the following:

* `Date.now`
* `new Date()`
* `new Intl.DateTimeFormat().format()`

Timers are not impacted yet, but may be in a future release of Bun.

## [​](https://bun.com/docs/test/dates-times#setsystemtime) setSystemTime

To change the system time, use `setSystemTime`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { setSystemTime, beforeAll, test, expect } from "bun:test";

beforeAll(() => {
  setSystemTime(new Date("2020-01-01T00:00:00.000Z"));
});

test("it is 2020", () => {
  expect(new Date().getFullYear()).toBe(2020);
});
```

To support existing tests that use Jest’s `useFakeTimers` and `useRealTimers`, you can use `useFakeTimers` and `useRealTimers`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
test("just like in jest", () => {
  jest.useFakeTimers();
  jest.setSystemTime(new Date("2020-01-01T00:00:00.000Z"));
  expect(new Date().getFullYear()).toBe(2020);
  jest.useRealTimers();
  expect(new Date().getFullYear()).toBeGreaterThan(2020);
});

test("unlike in jest", () => {
  const OriginalDate = Date;
  jest.useFakeTimers();
  if (typeof Bun === "undefined") {
    // In Jest, the Date constructor changes
    // That can cause all sorts of bugs because suddenly Date !== Date before the test.
    expect(Date).not.toBe(OriginalDate);
    expect(Date.now).not.toBe(OriginalDate.now);
  } else {
    // In bun:test, Date constructor does not change when you useFakeTimers
    expect(Date).toBe(OriginalDate);
    expect(Date.now).toBe(OriginalDate.now);
  }
});
```

**Timers** — Note that we have not implemented builtin support for mocking timers yet, but this is on the roadmap.

## [​](https://bun.com/docs/test/dates-times#reset-the-system-time) Reset the system time

To reset the system time, pass no arguments to `setSystemTime`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { setSystemTime, expect, test } from "bun:test";

test("it was 2020, for a moment.", () => {
  // Set it to something!
  setSystemTime(new Date("2020-01-01T00:00:00.000Z"));
  expect(new Date().getFullYear()).toBe(2020);

  // reset it!
  setSystemTime();

  expect(new Date().getFullYear()).toBeGreaterThan(2020);
});
```

## [​](https://bun.com/docs/test/dates-times#get-mocked-time-with-jest-now) Get mocked time with jest.now()

When you’re using mocked time (with `setSystemTime` or `useFakeTimers`), you can use `jest.now()` to get the current mocked timestamp:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect, jest } from "bun:test";

test("get the current mocked time", () => {
  jest.useFakeTimers();
  jest.setSystemTime(new Date("2020-01-01T00:00:00.000Z"));

  expect(Date.now()).toBe(1577836800000); // Jan 1, 2020 timestamp
  expect(jest.now()).toBe(1577836800000); // Same value

  jest.useRealTimers();
});
```

This is useful when you need to access the mocked time directly without creating a new Date object.

## [​](https://bun.com/docs/test/dates-times#set-the-time-zone) Set the time zone

By default, the time zone for all `bun test` runs is set to UTC (`Etc/UTC`) unless overridden. To change the time zone, either pass the `$TZ` environment variable to `bun test`:

terminal

Copy

```
TZ=America/Los_Angeles bun test
```

Or set `process.env.TZ` at runtime:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("Welcome to California!", () => {
  process.env.TZ = "America/Los_Angeles";
  expect(new Date().getTimezoneOffset()).toBe(420);
  expect(new Intl.DateTimeFormat().resolvedOptions().timeZone).toBe("America/Los_Angeles");
});

test("Welcome to New York!", () => {
  // Unlike in Jest, you can set the timezone multiple times at runtime and it will work.
  process.env.TZ = "America/New_York";
  expect(new Date().getTimezoneOffset()).toBe(240);
  expect(new Intl.DateTimeFormat().resolvedOptions().timeZone).toBe("America/New_York");
});
```

Unlike in Jest, you can set the timezone multiple times at runtime and it will work.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test/dates-times.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test/dates-times)

⌘I