---
url: https://bun.com/docs/guides/test/skip-tests
title: Skip tests with the Bun test runner - Bun
source_domain: bun.com
---

# Skip tests with the Bun test runner - Bun

To skip a test with the Bun test runner, use the `test.skip` function.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test } from "bun:test";

test.skip("unimplemented feature", () => {
  expect(Bun.isAwesome()).toBe(true);
});
```

---

Running `bun test` will not execute this test. It will be marked as skipped in the terminal output.

terminal

Copy

```
bun test
```

Copy

```
test.test.ts:
✓ add [0.03ms]
✓ multiply [0.02ms]
» unimplemented feature

 2 pass
 1 skip
 0 fail
 2 expect() calls
Ran 3 tests across 1 files. [74.00ms]
```

---

See also:

* [Mark a test as a todo](https://bun.com/docs/guides/test/todo-tests)
* [Docs > Test runner > Writing tests](https://bun.com/docs/test/writing-tests)

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/skip-tests.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/skip-tests)

⌘I