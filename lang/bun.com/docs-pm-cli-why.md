---
url: https://bun.com/docs/pm/cli/why
title: bun why - Bun
source_domain: bun.com
---

# bun why - Bun

The `bun why` command explains why a package is installed in your project by showing the dependency chain that led to its installation.

## [​](https://bun.com/docs/pm/cli/why#usage) Usage

terminal

Copy

```
bun why <package>
```

## [​](https://bun.com/docs/pm/cli/why#arguments) Arguments

* `<package>`: The name of the package to explain. Supports glob patterns like `@org/*` or `*-lodash`.

## [​](https://bun.com/docs/pm/cli/why#options) Options

* `--top`: Show only the top-level dependencies instead of the complete dependency tree.
* `--depth <number>`: Maximum depth of the dependency tree to display.

## [​](https://bun.com/docs/pm/cli/why#examples) Examples

Check why a specific package is installed:

terminal

Copy

```
bun why react
```

Copy

```
[email protected]
  └─ [email protected] (requires ^18.0.0)
```

Check why all packages with a specific pattern are installed:

terminal

Copy

```
bun why "@types/*"
```

Copy

```
@types/[email protected]
  └─ dev [email protected] (requires ^18.0.0)

@types/[email protected]
  └─ dev [email protected] (requires ^18.0.0)
```

Show only top-level dependencies:

terminal

Copy

```
bun why express --top
```

Copy

```
[email protected]
  └─ [email protected] (requires ^4.18.2)
```

Limit the dependency tree depth:

terminal

Copy

```
bun why express --depth 2
```

Copy

```
[email protected]
  └─ [email protected] (requires ^4.18.2)
     └─ [email protected] (requires ^1.20.1)
     └─ [email protected] (requires ^1.3.8)
        └─ (deeper dependencies hidden)
```

## [​](https://bun.com/docs/pm/cli/why#understanding-the-output) Understanding the Output

The output shows:

* The package name and version being queried
* The dependency chain that led to its installation
* The type of dependency (dev, peer, optional, or production)
* The version requirement specified in each package’s dependencies

For nested dependencies, the command shows the complete dependency tree by default, with indentation indicating the relationship hierarchy.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/why.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/why)

⌘I