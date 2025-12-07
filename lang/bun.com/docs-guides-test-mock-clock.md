---
url: https://bun.com/docs/guides/test/mock-clock
title: Set the system time in Bun's test runner - Bun
source_domain: bun.com
---

# Set the system time in Bun's test runner - Bun

Bun’s test runner supports setting the system time programmatically with the `setSystemTime` function.

Copy

```
import { test, expect, setSystemTime } from "bun:test";

test("party like it's 1999", () => {
  const date = new Date("1999-01-01T00:00:00.000Z");
  setSystemTime(date); // it's now January 1, 1999

  const now = new Date();
  expect(now.getFullYear()).toBe(1999);
  expect(now.getMonth()).toBe(0);
  expect(now.getDate()).toBe(1);
});
```

---

The `setSystemTime` function is commonly used on conjunction with [Lifecycle Hooks](https://bun.com/docs/test/lifecycle) to configure a testing environment with a deterministic “fake clock”.

Copy

```
import { test, expect, beforeAll, setSystemTime } from "bun:test";

beforeAll(() => {
  const date = new Date("1999-01-01T00:00:00.000Z");
  setSystemTime(date); // it's now January 1, 1999
});

// tests...
```

---

To reset the system clock to the actual time, call `setSystemTime` with no arguments.

Copy

```
import { test, expect, beforeAll, setSystemTime } from "bun:test";

setSystemTime(); // reset to actual time
```

---

See [Docs > Test Runner > Date and time](https://bun.com/docs/test/dates-times) for complete documentation on mocking with the Bun test runner.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/mock-clock.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/mock-clock)

⌘I