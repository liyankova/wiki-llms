---
url: https://bun.com/docs/guides/install/cicd
title: Install dependencies with Bun in GitHub Actions - Bun
source_domain: bun.com
---

# Install dependencies with Bun in GitHub Actions - Bun

Use the official [`setup-bun`](https://github.com/oven-sh/setup-bun) GitHub Action to install `bun` in your GitHub Actions runner.

workflow.yml

Copy

```
title: my-workflow
jobs:
  my-job:
    title: my-job
    runs-on: ubuntu-latest
    steps:
      # ...
      - uses: actions/checkout@v4
      - uses: oven-sh/setup-bun@v2 // [!code ++]

      # run any `bun` or `bunx` command
      - run: bun install // [!code ++]
```

---

To specify a version of Bun to install:

workflow.yml

Copy

```
title: my-workflow
jobs:
  my-job:
    title: my-job
    runs-on: ubuntu-latest
    steps:
      # ...
      - uses: oven-sh/setup-bun@v2
         with:
          version: "latest" # or "canary" #
```

---

Refer to the [README.md](https://github.com/oven-sh/setup-bun) for complete documentation of the `setup-bun` GitHub Action.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/cicd.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/cicd)

⌘I