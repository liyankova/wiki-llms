---
url: https://bun.com/docs/pm/cli/info
title: bun info - Bun
source_domain: bun.com
---

# bun info - Bun

`bun info` displays package metadata from the npm registry.

## [​](https://bun.com/docs/pm/cli/info#usage) Usage

terminal

Copy

```
bun info react
```

This will display information about the `react` package, including its latest version, description, homepage, dependencies, and more.

## [​](https://bun.com/docs/pm/cli/info#viewing-specific-versions) Viewing specific versions

To view information about a specific version:

terminal

Copy

```
bun info [email protected]
```

## [​](https://bun.com/docs/pm/cli/info#viewing-specific-properties) Viewing specific properties

You can also query specific properties from the package metadata:

terminal

Copy

```
bun info react version
bun info react dependencies
bun info react repository.url
```

## [​](https://bun.com/docs/pm/cli/info#json-output) JSON output

To get the output in JSON format, use the `--json` flag:

terminal

Copy

```
bun info react --json
```

## [​](https://bun.com/docs/pm/cli/info#alias) Alias

`bun pm view` is an alias for `bun info`:

terminal

Copy

```
bun pm view react  # equivalent to: bun info react
```

## [​](https://bun.com/docs/pm/cli/info#examples) Examples

terminal

Copy

```
# View basic package information
bun info is-number

# View a specific version
bun info [email protected]

# View all available versions
bun info is-number versions

# View package dependencies
bun info express dependencies

# View package homepage
bun info lodash homepage

# Get JSON output
bun info react --json
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/info.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/info)

⌘I