---
url: https://bun.com/docs/guides/test/spy-on
title: Spy on methods in `bun test` - Bun
source_domain: bun.com
---

# Spy on methods in `bun test` - Bun

Use the `spyOn` utility to track method calls with Bun’s test runner.

Copy

```
import { test, expect, spyOn } from "bun:test";

const leo = {
  name: "Leonardo",
  sayHi(thing: string) {
    console.log(`Sup I'm ${this.name} and I like ${thing}`);
  },
};

const spy = spyOn(leo, "sayHi");
```

---

Once the spy is created, it can be used to write `expect` assertions relating to method calls.

Copy

```
import { test, expect, spyOn } from "bun:test";

const leo = {
  name: "Leonardo",
  sayHi(thing: string) {
    console.log(`Sup I'm ${this.name} and I like ${thing}`);
  },
};

const spy = spyOn(leo, "sayHi");

test("turtles", () => { 
  expect(spy).toHaveBeenCalledTimes(0); 
  leo.sayHi("pizza"); 
  expect(spy).toHaveBeenCalledTimes(1); 
  expect(spy.mock.calls).toEqual([["pizza"]]); 
});
```

---

See [Docs > Test Runner > Mocks](https://bun.com/docs/test/mocks) for complete documentation on mocking with the Bun test runner.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/spy-on.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/spy-on)

⌘I