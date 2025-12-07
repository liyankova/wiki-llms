---
url: https://bun.com/docs/test/snapshots
title: Snapshots - Bun
source_domain: bun.com
---

# Snapshots - Bun

Snapshot testing saves the output of a value and compares it against future test runs. This is particularly useful for UI components, complex objects, or any output that needs to remain consistent.

## [​](https://bun.com/docs/test/snapshots#basic-snapshots) Basic Snapshots

Snapshot tests are written using the `.toMatchSnapshot()` matcher:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("snap", () => {
  expect("foo").toMatchSnapshot();
});
```

The first time this test is run, the argument to `expect` will be serialized and written to a special snapshot file in a `__snapshots__` directory alongside the test file.

### [​](https://bun.com/docs/test/snapshots#snapshot-files) Snapshot Files

After running the test above, Bun will create:

directory structure

Copy

```
your-project/
├── snap.test.ts
└── __snapshots__/
    └── snap.test.ts.snap
```

The snapshot file contains:

\_\_snapshots\_\_/snap.test.ts.snap

Copy

```
// Bun Snapshot v1, https://bun.com/docs/test/snapshots

exports[`snap 1`] = `"foo"`;
```

On future runs, the argument is compared against the snapshot on disk.

## [​](https://bun.com/docs/test/snapshots#updating-snapshots) Updating Snapshots

Snapshots can be re-generated with the following command:

terminal

Copy

```
bun test --update-snapshots
```

This is useful when:

* You’ve intentionally changed the output
* You’re adding new snapshot tests
* The expected output has legitimately changed

## [​](https://bun.com/docs/test/snapshots#inline-snapshots) Inline Snapshots

For smaller values, you can use inline snapshots with `.toMatchInlineSnapshot()`. These snapshots are stored directly in your test file:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("inline snapshot", () => {
  // First run: snapshot will be inserted automatically
  expect({ hello: "world" }).toMatchInlineSnapshot();
});
```

After the first run, Bun automatically updates your test file:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("inline snapshot", () => {
  expect({ hello: "world" }).toMatchInlineSnapshot(`
{
  "hello": "world",
}
`);
});
```

### [​](https://bun.com/docs/test/snapshots#using-inline-snapshots) Using Inline Snapshots

1. Write your test with `.toMatchInlineSnapshot()`
2. Run the test once
3. Bun automatically updates your test file with the snapshot
4. On subsequent runs, the value will be compared against the inline snapshot

Inline snapshots are particularly useful for small, simple values where it’s helpful to see the expected output right in the test file.

## [​](https://bun.com/docs/test/snapshots#error-snapshots) Error Snapshots

You can also snapshot error messages using `.toThrowErrorMatchingSnapshot()` and `.toThrowErrorMatchingInlineSnapshot()`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("error snapshot", () => {
  expect(() => {
    throw new Error("Something went wrong");
  }).toThrowErrorMatchingSnapshot();

  expect(() => {
    throw new Error("Another error");
  }).toThrowErrorMatchingInlineSnapshot();
});
```

After running, the inline version becomes:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
test("error snapshot", () => {
  expect(() => {
    throw new Error("Something went wrong");
  }).toThrowErrorMatchingSnapshot();

  expect(() => {
    throw new Error("Another error");
  }).toThrowErrorMatchingInlineSnapshot(`"Another error"`);
});
```

## [​](https://bun.com/docs/test/snapshots#advanced-snapshot-usage) Advanced Snapshot Usage

### [​](https://bun.com/docs/test/snapshots#complex-objects) Complex Objects

Snapshots work well with complex nested objects:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("complex object snapshot", () => {
  const user = {
    id: 1,
    name: "John Doe",
    email: "[email protected]",
    profile: {
      age: 30,
      preferences: {
        theme: "dark",
        notifications: true,
      },
    },
    tags: ["developer", "javascript", "bun"],
  };

  expect(user).toMatchSnapshot();
});
```

### [​](https://bun.com/docs/test/snapshots#array-snapshots) Array Snapshots

Arrays are also well-suited for snapshot testing:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("array snapshot", () => {
  const numbers = [1, 2, 3, 4, 5].map(n => n * 2);
  expect(numbers).toMatchSnapshot();
});
```

### [​](https://bun.com/docs/test/snapshots#function-output-snapshots) Function Output Snapshots

Snapshot the output of functions:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

function generateReport(data: any[]) {
  return {
    total: data.length,
    summary: data.map(item => ({ id: item.id, name: item.name })),
    timestamp: "2024-01-01", // Fixed for testing
  };
}

test("report generation", () => {
  const data = [
    { id: 1, name: "Alice", age: 30 },
    { id: 2, name: "Bob", age: 25 },
  ];

  expect(generateReport(data)).toMatchSnapshot();
});
```

## [​](https://bun.com/docs/test/snapshots#react-component-snapshots) React Component Snapshots

Snapshots are particularly useful for React components:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";
import { render } from "@testing-library/react";

function Button({ children, variant = "primary" }) {
  return <button className={`btn btn-${variant}`}>{children}</button>;
}

test("Button component snapshots", () => {
  const { container: primary } = render(<Button>Click me</Button>);
  const { container: secondary } = render(<Button variant="secondary">Cancel</Button>);

  expect(primary.innerHTML).toMatchSnapshot();
  expect(secondary.innerHTML).toMatchSnapshot();
});
```

## [​](https://bun.com/docs/test/snapshots#property-matchers) Property Matchers

For values that change between test runs (like timestamps or IDs), use property matchers:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

test("snapshot with dynamic values", () => {
  const user = {
    id: Math.random(), // This changes every run
    name: "John",
    createdAt: new Date().toISOString(), // This also changes
  };

  expect(user).toMatchSnapshot({
    id: expect.any(Number),
    createdAt: expect.any(String),
  });
});
```

The snapshot will store:

snapshot file

Copy

```
exports[`snapshot with dynamic values 1`] = `
{
  "createdAt": Any<String>,
  "id": Any<Number>,
  "name": "John",
}
`;
```

## [​](https://bun.com/docs/test/snapshots#custom-serializers) Custom Serializers

You can customize how objects are serialized in snapshots:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { test, expect } from "bun:test";

// Custom serializer for Date objects
expect.addSnapshotSerializer({
  test: val => val instanceof Date,
  serialize: val => `"${val.toISOString()}"`,
});

test("custom serializer", () => {
  const event = {
    name: "Meeting",
    date: new Date("2024-01-01T10:00:00Z"),
  };

  expect(event).toMatchSnapshot();
});
```

## [​](https://bun.com/docs/test/snapshots#best-practices) Best Practices

### [​](https://bun.com/docs/test/snapshots#keep-snapshots-small) Keep Snapshots Small

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// Good: Focused snapshots
test("user name formatting", () => {
  const formatted = formatUserName("john", "doe");
  expect(formatted).toMatchInlineSnapshot(`"John Doe"`);
});

// Avoid: Huge snapshots that are hard to review
test("entire page render", () => {
  const page = renderEntirePage();
  expect(page).toMatchSnapshot(); // This could be thousands of lines
});
```

### [​](https://bun.com/docs/test/snapshots#use-descriptive-test-names) Use Descriptive Test Names

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// Good: Clear what the snapshot represents
test("formats currency with USD symbol", () => {
  expect(formatCurrency(99.99)).toMatchInlineSnapshot(`"$99.99"`);
});

// Avoid: Unclear what's being tested
test("format test", () => {
  expect(format(99.99)).toMatchInlineSnapshot(`"$99.99"`);
});
```

### [​](https://bun.com/docs/test/snapshots#group-related-snapshots) Group Related Snapshots

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
import { describe, test, expect } from "bun:test";

describe("Button component", () => {
  test("primary variant", () => {
    expect(render(<Button variant="primary">Click</Button>))
      .toMatchSnapshot();
  });

  test("secondary variant", () => {
    expect(render(<Button variant="secondary">Cancel</Button>))
      .toMatchSnapshot();
  });

  test("disabled state", () => {
    expect(render(<Button disabled>Disabled</Button>))
      .toMatchSnapshot();
  });
});
```

### [​](https://bun.com/docs/test/snapshots#handle-dynamic-data) Handle Dynamic Data

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// Good: Normalize dynamic data
test("API response format", () => {
  const response = {
    data: { id: 1, name: "Test" },
    timestamp: Date.now(),
    requestId: generateId(),
  };

  expect({
    ...response,
    timestamp: "TIMESTAMP",
    requestId: "REQUEST_ID",
  }).toMatchSnapshot();
});

// Or use property matchers
test("API response with matchers", () => {
  const response = getApiResponse();

  expect(response).toMatchSnapshot({
    timestamp: expect.any(Number),
    requestId: expect.any(String),
  });
});
```

## [​](https://bun.com/docs/test/snapshots#managing-snapshots) Managing Snapshots

### [​](https://bun.com/docs/test/snapshots#reviewing-snapshot-changes) Reviewing Snapshot Changes

When snapshots change, carefully review them:

terminal

Copy

```
# See what changed
git diff __snapshots__/

# Update if changes are intentional
bun test --update-snapshots

# Commit the updated snapshots
git add __snapshots__/
git commit -m "Update snapshots after UI changes"
```

### [​](https://bun.com/docs/test/snapshots#cleaning-up-unused-snapshots) Cleaning Up Unused Snapshots

Bun will warn about unused snapshots:

warning

Copy

```
Warning: 1 unused snapshot found:
  my-test.test.ts.snap: "old test that no longer exists 1"
```

Remove unused snapshots by deleting them from the snapshot files or by running tests with cleanup flags if available.

### [​](https://bun.com/docs/test/snapshots#organizing-large-snapshot-files) Organizing Large Snapshot Files

For large projects, consider organizing tests to keep snapshot files manageable:

directory structure

Copy

```
tests/
├── components/
│   ├── Button.test.tsx
│   └── __snapshots__/
│       └── Button.test.tsx.snap
├── utils/
│   ├── formatters.test.ts
│   └── __snapshots__/
│       └── formatters.test.ts.snap
```

## [​](https://bun.com/docs/test/snapshots#troubleshooting) Troubleshooting

### [​](https://bun.com/docs/test/snapshots#snapshot-failures) Snapshot Failures

When snapshots fail, you’ll see a diff:

diff

Copy

```
- Expected
+ Received

  Object {
-   "name": "John",
+   "name": "Jane",
  }
```

Common causes:

* Intentional changes (update with `--update-snapshots`)
* Unintentional changes (fix the code)
* Dynamic data (use property matchers)
* Environment differences (normalize the data)

### [​](https://bun.com/docs/test/snapshots#platform-differences) Platform Differences

Be aware of platform-specific differences:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)test.ts

Copy

```
// Paths might differ between Windows/Unix
test("file operations", () => {
  const result = processFile("./test.txt");

  expect({
    ...result,
    path: result.path.replace(/\\/g, "/"), // Normalize paths
  }).toMatchSnapshot();
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/test/snapshots.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /test/snapshots)

⌘I