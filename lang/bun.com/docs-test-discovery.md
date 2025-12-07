---
url: https://bun.com/docs/test/discovery
title: Finding tests - Bun
source_domain: bun.com
---

# Finding tests - Bun

bun test’s file discovery mechanism determines which files to run as tests. Understanding how it works helps you structure your test files effectively.

## [​](https://bun.com/docs/test/discovery#default-discovery-logic) Default Discovery Logic

By default, `bun test` recursively searches the project directory for files that match specific patterns:

* `*.test.{js|jsx|ts|tsx}` - Files ending with `.test.js`, `.test.jsx`, `.test.ts`, or `.test.tsx`
* `*_test.{js|jsx|ts|tsx}` - Files ending with `_test.js`, `_test.jsx`, `_test.ts`, or `_test.tsx`
* `*.spec.{js|jsx|ts|tsx}` - Files ending with `.spec.js`, `.spec.jsx`, `.spec.ts`, or `.spec.tsx`
* `*_spec.{js|jsx|ts|tsx}` - Files ending with `_spec.js`, `_spec.jsx`, `_spec.ts`, or `_spec.tsx`

## [​](https://bun.com/docs/test/discovery#exclusions) Exclusions

By default, Bun test ignores:

* `node_modules` directories
* Hidden directories (those starting with a period `.`)
* Files that don’t have JavaScript-like extensions (based on available loaders)

## [​](https://bun.com/docs/test/discovery#customizing-test-discovery) Customizing Test Discovery

### [​](https://bun.com/docs/test/discovery#position-arguments-as-filters) Position Arguments as Filters

You can filter which test files run by passing additional positional arguments to `bun test`:

terminal

Copy

```
bun test <filter> <filter> ...
```

Any test file with a path that contains one of the filters will run. These filters are simple substring matches, not glob patterns.
For example, to run all tests in a `utils` directory:

terminal

Copy

```
bun test utils
```

This would match files like `src/utils/string.test.ts` and `lib/utils/array_test.js`.

### [​](https://bun.com/docs/test/discovery#specifying-exact-file-paths) Specifying Exact File Paths

To run a specific file in the test runner, make sure the path starts with `./` or `/` to distinguish it from a filter name:

terminal

Copy

```
bun test ./test/specific-file.test.ts
```

### [​](https://bun.com/docs/test/discovery#filter-by-test-name) Filter by Test Name

To filter tests by name rather than file path, use the `-t`/`--test-name-pattern` flag with a regex pattern:

terminal

Copy

```
# run all tests with "addition" in the name
bun test --test-name-pattern addition
```

The pattern is matched against a concatenated string of the test name prepended with the labels of all its parent describe blocks, separated by spaces. For example, a test defined as:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)math.test.ts

Copy

```
describe("Math", () => {
  describe("operations", () => {
    test("should add correctly", () => {
      // ...
    });
  });
});
```

Would be matched against the string “Math operations should add correctly”.

### [​](https://bun.com/docs/test/discovery#changing-the-root-directory) Changing the Root Directory

By default, Bun looks for test files starting from the current working directory. You can change this with the `root` option in your `bunfig.toml`:

bunfig.toml

Copy

```
[test]
root = "src"  # Only scan for tests in the src directory
```

## [​](https://bun.com/docs/test/discovery#execution-order) Execution Order

Tests are run in the following order:

1. Test files are executed sequentially (not in parallel)
2. Within each file, tests run sequentially based on their definition order

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test/discovery.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test/discovery)

⌘I