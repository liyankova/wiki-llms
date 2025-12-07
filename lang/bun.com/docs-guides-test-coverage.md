---
url: https://bun.com/docs/guides/test/coverage
title: Generate code coverage reports with the Bun test runner - Bun
source_domain: bun.com
---

# Generate code coverage reports with the Bun test runner - Bun

Bun’s test runner supports built-in *code coverage reporting*. This makes it easy to see how much of the codebase is covered by tests and find areas that are not currently well-tested.

---

Pass the `--coverage` flag to `bun test` to enable this feature. This will print a coverage report after the test run.
The coverage report lists the source files that were executed during the test run, the percentage of functions and lines that were executed, and the line ranges that were not executed during the run.

terminal

Copy

```
bun test --coverage
```

Copy

```
test.test.ts:
✓ math > add [0.71ms]
✓ math > multiply [0.03ms]
✓ random [0.13ms]
-------------|---------|---------|-------------------
File         | % Funcs | % Lines | Uncovered Line #s
-------------|---------|---------|-------------------
All files    |   66.67 |   77.78 |
 math.ts     |   50.00 |   66.67 |
 random.ts   |   50.00 |   66.67 |
-------------|---------|---------|-------------------

 3 pass
 0 fail
 3 expect() calls
```

---

To always enable coverage reporting by default, add the following line to your `bunfig.toml`:

bunfig.toml

Copy

```
[test]
coverage = true # always enable coverage
```

---

Refer to [Docs > Test runner > Coverage](https://bun.com/docs/test/code-coverage) for complete documentation on code coverage reporting in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/coverage.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/coverage)

⌘I