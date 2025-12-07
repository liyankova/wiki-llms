---
url: https://bun.com/docs/runtime/glob
title: Glob - Bun
source_domain: bun.com
---

# Glob - Bun

## [​](https://bun.com/docs/runtime/glob#quickstart) Quickstart

**Scan a directory for files matching `*.ts`**:

Copy

```
import { Glob } from "bun";

const glob = new Glob("**/*.ts");

// Scans the current working directory and each of its sub-directories recursively
for await (const file of glob.scan(".")) {
  console.log(file); // => "index.ts"
}
```

**Match a string against a glob pattern**:

Copy

```
import { Glob } from "bun";

const glob = new Glob("*.ts");

glob.match("index.ts"); // => true
glob.match("index.js"); // => false
```

`Glob` is a class which implements the following interface:

Copy

```
class Glob {
  scan(root: string | ScanOptions): AsyncIterable<string>;
  scanSync(root: string | ScanOptions): Iterable<string>;

  match(path: string): boolean;
}

interface ScanOptions {
  /**
   * The root directory to start matching from. Defaults to `process.cwd()`
   */
  cwd?: string;

  /**
   * Allow patterns to match entries that begin with a period (`.`).
   *
   * @default false
   */
  dot?: boolean;

  /**
   * Return the absolute path for entries.
   *
   * @default false
   */
  absolute?: boolean;

  /**
   * Indicates whether to traverse descendants of symbolic link directories.
   *
   * @default false
   */
  followSymlinks?: boolean;

  /**
   * Throw an error when symbolic link is broken
   *
   * @default false
   */
  throwErrorOnBrokenSymlink?: boolean;

  /**
   * Return only files.
   *
   * @default true
   */
  onlyFiles?: boolean;
}
```

## [​](https://bun.com/docs/runtime/glob#supported-glob-patterns) Supported Glob Patterns

Bun supports the following glob patterns:

### [​](https://bun.com/docs/runtime/glob#-match-any-single-character) `?` - Match any single character

Copy

```
const glob = new Glob("???.ts");
glob.match("foo.ts"); // => true
glob.match("foobar.ts"); // => false
```

### [​](https://bun.com/docs/runtime/glob#matches-zero-or-more-characters,-except-for-path-separators-/-or-\) `*` - Matches zero or more characters, except for path separators (`/` or `\`)

Copy

```
const glob = new Glob("*.ts");
glob.match("index.ts"); // => true
glob.match("src/index.ts"); // => false
```

### [​](https://bun.com/docs/runtime/glob#match-any-number-of-characters-including-/) `**` - Match any number of characters including `/`

Copy

```
const glob = new Glob("**/*.ts");
glob.match("index.ts"); // => true
glob.match("src/index.ts"); // => true
glob.match("src/index.js"); // => false
```

### [​](https://bun.com/docs/runtime/glob#[ab]-matches-one-of-the-characters-contained-in-the-brackets,-as-well-as-character-ranges) `[ab]` - Matches one of the characters contained in the brackets, as well as character ranges

Copy

```
const glob = new Glob("ba[rz].ts");
glob.match("bar.ts"); // => true
glob.match("baz.ts"); // => true
glob.match("bat.ts"); // => false
```

You can use character ranges (e.g `[0-9]`, `[a-z]`) as well as the negation operators `^` or `!` to match anything *except* the characters contained within the braces (e.g `[^ab]`, `[!a-z]`)

Copy

```
const glob = new Glob("ba[a-z][0-9][^4-9].ts");
glob.match("bar01.ts"); // => true
glob.match("baz83.ts"); // => true
glob.match("bat22.ts"); // => true
glob.match("bat24.ts"); // => false
glob.match("ba0a8.ts"); // => false
```

### [​](https://bun.com/docs/runtime/glob#{a,b,c}-match-any-of-the-given-patterns) `{a,b,c}` - Match any of the given patterns

Copy

```
const glob = new Glob("{a,b,c}.ts");
glob.match("a.ts"); // => true
glob.match("b.ts"); // => true
glob.match("c.ts"); // => true
glob.match("d.ts"); // => false
```

These match patterns can be deeply nested (up to 10 levels), and contain any of the wildcards from above.

### [​](https://bun.com/docs/runtime/glob#negates-the-result-at-the-start-of-a-pattern) `!` - Negates the result at the start of a pattern

Copy

```
const glob = new Glob("!index.ts");
glob.match("index.ts"); // => false
glob.match("foo.ts"); // => true
```

### [​](https://bun.com/docs/runtime/glob#\-escapes-any-of-the-special-characters-above) `\` - Escapes any of the special characters above

Copy

```
const glob = new Glob("\\!index.ts");
glob.match("!index.ts"); // => true
glob.match("index.ts"); // => false
```

## [​](https://bun.com/docs/runtime/glob#node-js-fs-glob-compatibility) Node.js `fs.glob()` compatibility

Bun also implements Node.js’s `fs.glob()` functions with additional features:

Copy

```
import { glob, globSync, promises } from "node:fs";

// Array of patterns
const files = await promises.glob(["**/*.ts", "**/*.js"]);

// Exclude patterns
const filtered = await promises.glob("**/*", {
  exclude: ["node_modules/**", "*.test.*"],
});
```

All three functions (`fs.glob()`, `fs.globSync()`, `fs.promises.glob()`) support:

* Array of patterns as the first argument
* `exclude` option to filter results

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/glob.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/glob)

⌘I