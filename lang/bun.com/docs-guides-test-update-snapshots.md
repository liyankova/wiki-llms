---
url: https://bun.com/docs/guides/test/update-snapshots
title: Update snapshots in `bun test` - Bun
source_domain: bun.com
---

# Update snapshots in `bun test` - Bun

Bun’s test runner supports Jest-style snapshot testing via `.toMatchSnapshot()`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)snap.test.ts

Copy

```
import { test, expect } from "bun:test";

test("snapshot", () => {
  expect({ foo: "bar" }).toMatchSnapshot();
});
```

---

The first time this test is executed, Bun will write a snapshot file to disk in a directory called `__snapshots__` that lives alongside the test file.

File Tree

Copy

```
test
├── __snapshots__
│   └── snap.test.ts.snap
└── snap.test.ts
```

---

To regenerate snapshots, use the `--update-snapshots` flag.

terminal

Copy

```
bun test --update-snapshots
```

Copy

```
test/snap.test.ts:
✓ snapshot [0.86ms]

 1 pass
 0 fail
 snapshots: +1 added # the snapshot was regenerated
 1 expect() calls
Ran 1 tests across 1 files. [102.00ms]
```

---

See [Docs > Test Runner > Snapshots](https://bun.com/docs/test/snapshots) for complete documentation on snapshots with the Bun test runner.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/update-snapshots.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/update-snapshots)

⌘I