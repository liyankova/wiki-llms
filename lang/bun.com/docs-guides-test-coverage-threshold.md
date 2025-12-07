---
url: https://bun.com/docs/guides/test/coverage-threshold
title: Set a code coverage threshold with the Bun test runner - Bun
source_domain: bun.com
---

# Set a code coverage threshold with the Bun test runner - Bun

Bun’s test runner supports built-in code coverage reporting via the `--coverage` flag.

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

To set a minimum coverage threshold, add the following line to your `bunfig.toml`. This requires that 90% of your codebase is covered by tests.

bunfig.toml

Copy

```
[test]
# to require 90% line-level and function-level coverage
coverageThreshold = 0.9
```

---

If your test suite does not meet this threshold, `bun test` will exit with a non-zero exit code to signal a failure.

terminal

Copy

```
bun test --coverage
```

Copy

```
<test output>
$ echo $?
1 # this is the exit code of the previous command
```

---

Different thresholds can be set for line-level and function-level coverage.

bunfig.toml

Copy

```
[test]
# to set different thresholds for lines and functions
coverageThreshold = { lines = 0.5, functions = 0.7 }
```

---

See [Docs > Test runner > Coverage](https://bun.com/docs/test/code-coverage) for complete documentation on code coverage reporting in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/coverage-threshold.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/coverage-threshold)

⌘I