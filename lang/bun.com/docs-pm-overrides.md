---
url: https://bun.com/docs/pm/overrides
title: Overrides and resolutions - Bun
source_domain: bun.com
---

# Overrides and resolutions - Bun

Bun supports npm’s `"overrides"` and Yarn’s `"resolutions"` in `package.json`. These are mechanisms for specifying a version range for *metadependencies*—the dependencies of your dependencies.

package.json

Copy

```
{
  "name": "my-app",
  "dependencies": {
    "foo": "^2.0.0"
  },
  "overrides": { 
    "bar": "~4.4.0"
  } 
}
```

By default, Bun will install the latest version of all dependencies and metadependencies, according to the ranges specified in each package’s `package.json`. Let’s say you have a project with one dependency, `foo`, which in turn has a dependency on `bar`. This means `bar` is a *metadependency* of our project.

package.json

Copy

```
{
  "name": "my-app",
  "dependencies": {
    "foo": "^2.0.0"
  }
}
```

When you run `bun install`, Bun will install the latest versions of each package.

tree layout of node\_modules

Copy

```
node_modules
├── [email protected]
└── [email protected]
```

But what if a security vulnerability was introduced in `[email protected]`? We may want a way to pin `bar` to an older version that doesn’t have the vulnerability. This is where `"overrides"`/`"resolutions"` come in.

---

## [​](https://bun.com/docs/pm/overrides#"overrides") `"overrides"`

Add `bar` to the `"overrides"` field in `package.json`. Bun will defer to the specified version range when determining which version of `bar` to install, whether it’s a dependency or a metadependency.

Bun currently only supports top-level `"overrides"`. [Nested
overrides](https://docs.npmjs.com/cli/v9/configuring-npm/package-json#overrides) are not supported.

package.json

Copy

```
{
  "name": "my-app",
  "dependencies": {
    "foo": "^2.0.0"
  },
  "overrides": { 
    "bar": "~4.4.0"
  } 
}
```

## [​](https://bun.com/docs/pm/overrides#"resolutions") `"resolutions"`

The syntax is similar for `"resolutions"`, which is Yarn’s alternative to `"overrides"`. Bun supports this feature to make migration from Yarn easier.
As with `"overrides"`, *nested resolutions* are not currently supported.

package.json

Copy

```
{
  "name": "my-app",
  "dependencies": {
    "foo": "^2.0.0"
  },
  "resolutions": { 
    "bar": "~4.4.0"
  } 
}
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/overrides.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/overrides)

⌘I