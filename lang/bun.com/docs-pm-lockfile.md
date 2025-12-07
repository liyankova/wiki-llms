---
url: https://bun.com/docs/pm/lockfile
title: Lockfile - Bun
source_domain: bun.com
---

# Lockfile - Bun

Running `bun install` will create a lockfile called `bun.lock`.

#### [​](https://bun.com/docs/pm/lockfile#should-it-be-committed-to-git) Should it be committed to git?

Yes

#### [​](https://bun.com/docs/pm/lockfile#generate-a-lockfile-without-installing) Generate a lockfile without installing?

To generate a lockfile without installing to `node_modules` you can use the `--lockfile-only` flag. The lockfile will always be saved to disk, even if it is up-to-date with the `package.json`(s) for your project.

terminal

Copy

```
bun install --lockfile-only
```

Using `--lockfile-only` will still populate the global install cache with registry metadata and git/tarball
dependencies.

#### [​](https://bun.com/docs/pm/lockfile#can-i-opt-out) Can I opt out?

To install without creating a lockfile:

terminal

Copy

```
bun install --no-save
```

To install a Yarn lockfile *in addition* to `bun.lock`.

Copy

```
bun install --yarn
```

#### [​](https://bun.com/docs/pm/lockfile#text-based-lockfile) Text-based lockfile

Bun v1.2 changed the default lockfile format to the text-based `bun.lock`. Existing binary `bun.lockb` lockfiles can be migrated to the new format by running `bun install --save-text-lockfile --frozen-lockfile --lockfile-only` and deleting `bun.lockb`.
More information about the new lockfile format can be found on [our blogpost](https://bun.com/blog/bun-lock-text-lockfile).

#### [​](https://bun.com/docs/pm/lockfile#automatic-lockfile-migration) Automatic lockfile migration

When running `bun install` in a project without a `bun.lock`, Bun automatically migrates existing lockfiles:

* `yarn.lock` (v1)
* `package-lock.json` (npm)
* `pnpm-lock.yaml` (pnpm)

The original lockfile is preserved and can be removed manually after verification.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/lockfile.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/lockfile)

⌘I