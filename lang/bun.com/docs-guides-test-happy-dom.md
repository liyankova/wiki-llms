---
url: https://bun.com/docs/guides/test/happy-dom
title: Write browser DOM tests with Bun and happy-dom - Bun
source_domain: bun.com
---

# Write browser DOM tests with Bun and happy-dom - Bun

You can write and run browser tests with Bun’s test runner in conjunction with [Happy DOM](https://github.com/capricorn86/happy-dom). Happy DOM implements mocked versions of browser APIs like `document` and `location`.

---

To get started, install `happy-dom`.

terminal

Copy

```
bun add -d @happy-dom/global-registrator
```

---

This module exports a “registrator” that injects the mocked browser APIs to the global scope.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)happydom.ts

Copy

```
import { GlobalRegistrator } from "@happy-dom/global-registrator";

GlobalRegistrator.register();
```

---

We need to make sure this file is executed before any of our test files. That’s a job for Bun’s built-in [*preload*](https://bun.com/docs/guides/test/happy-dom) functionality. Create a `bunfig.toml` file in the root of your project (if it doesn’t already exist) and add the following lines.
The `./happydom.ts` file should contain the registration code above.

bunfig.toml

Copy

```
[test]
preload = "./happydom.ts"
```

---

Now running `bun test` inside our project will automatically execute `happydom.ts` first. We can start writing tests that use browser APIs.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)dom.test.ts

Copy

```
import { test, expect } from "bun:test";

test("set button text", () => {
  document.body.innerHTML = `<button>My button</button>`;
  const button = document.querySelector("button");
  expect(button?.innerText).toEqual("My button");
});
```

---

With Happy DOM properly configured, this test runs as expected.

terminal

Copy

```
bun test
```

Copy

```
dom.test.ts:
✓ set button text [0.82ms]

 1 pass
 0 fail
 1 expect() calls
Ran 1 tests across 1 files. 1 total [125.00ms]
```

---

Refer to the [Happy DOM repo](https://github.com/capricorn86/happy-dom) and [Docs > Test runner > DOM](https://bun.com/docs/test/dom) for complete documentation on writing browser tests with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/happy-dom.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/happy-dom)

⌘I