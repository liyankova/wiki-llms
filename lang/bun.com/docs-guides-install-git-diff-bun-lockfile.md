---
url: https://bun.com/docs/guides/install/git-diff-bun-lockfile
title: Configure git to diff Bun's lockb lockfile - Bun
source_domain: bun.com
---

# Configure git to diff Bun's lockb lockfile - Bun

Bun v1.1.39 introduced `bun.lock`, a JSONC formatted lockfile. `bun.lock` is human-readable and git-diffable without
configuration, at no cost to performance. In 1.2.0+ it is the default format used for new projects. [**Learn
more.**](https://bun.com/docs/pm/lockfile#text-based-lockfile)

---

To teach `git` how to generate a human-readable diff of Bun’s binary lockfile format (`.lockb`), add the following to your local or global `.gitattributes` file:

gitattributes

Copy

```
*.lockb binary diff=lockb
```

---

Then add the following to you local git config with:

terminal

Copy

```
git config diff.lockb.textconv bun
git config diff.lockb.binary true
```

---

To globally configure git to diff Bun’s lockfile, add the following to your global git config with:

terminal

Copy

```
git config --global diff.lockb.textconv bun
git config --global diff.lockb.binary true
```

---

## [​](https://bun.com/docs/guides/install/git-diff-bun-lockfile#how-this-works) How this works

Why this works:

* `textconv` tells git to run bun on the file before diffing
* `binary` tells git to treat the file as binary (so it doesn’t try to diff it line-by-line)

In Bun, you can execute Bun’s lockfile (`bun ./bun.lockb`) to generate a human-readable version of the lockfile and `git diff` can then use that to generate a human-readable diff.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/git-diff-bun-lockfile.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/git-diff-bun-lockfile)

⌘I