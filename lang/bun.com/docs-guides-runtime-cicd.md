---
url: https://bun.com/docs/guides/runtime/cicd
title: Install and run Bun in GitHub Actions - Bun
source_domain: bun.com
---

# Install and run Bun in GitHub Actions - Bun

Use the official [`setup-bun`](https://github.com/oven-sh/setup-bun) GitHub Action to install `bun` in your GitHub Actions runner.

workflow.yml

Copy

```
name: my-workflow
jobs:
  my-job:
    name: my-job
    runs-on: ubuntu-latest
    steps:
      # ...
      - uses: actions/checkout@v4
      - uses: oven-sh/setup-bun@v2

      # run any `bun` or `bunx` command
      - run: bun install
      - run: bun index.ts
      - run: bun run build
```

---

To specify a version of Bun to install:

workflow.yml

Copy

```
name: my-workflow
jobs:
  my-job:
    name: my-job
    runs-on: ubuntu-latest
    steps:
      # ...
      - uses: oven-sh/setup-bun@v2
        with:
          bun-version: 1.3.3 # or "latest", "canary", <sha> #
```

---

Refer to the [README.md](https://github.com/oven-sh/setup-bun) for complete documentation of the `setup-bun` GitHub Action.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/cicd.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/cicd)

⌘I