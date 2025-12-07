---
url: https://bun.com/docs/pm/cli/audit
title: bun audit - Bun
source_domain: bun.com
---

# bun audit - Bun

Run the command in a project with a `bun.lock` file:

terminal

Copy

```
bun audit
```

Bun sends the list of installed packages and versions to NPM, and prints a report of any vulnerabilities that were found. Packages installed from registries other than the default registry are skipped.
If no vulnerabilities are found, the command prints:

Copy

```
No vulnerabilities found
```

When vulnerabilities are detected, each affected package is listed along with the severity, a short description and a link to the advisory. At the end of the report Bun prints a summary and hints for updating:

Copy

```
3 vulnerabilities (1 high, 2 moderate)
To update all dependencies to the latest compatible versions:
  bun update
To update all dependencies to the latest versions (including breaking changes):
  bun update --latest
```

### [​](https://bun.com/docs/pm/cli/audit#filtering-options) Filtering options

**`--audit-level=<low|moderate|high|critical>`** - Only show vulnerabilities at this severity level or higher:

terminal

Copy

```
bun audit --audit-level=high
```

**`--prod`** - Audit only production dependencies (excludes devDependencies):

terminal

Copy

```
bun audit --prod
```

**`--ignore <CVE>`** - Ignore specific CVEs (can be used multiple times):

terminal

Copy

```
bun audit --ignore CVE-2022-25883 --ignore CVE-2023-26136
```

### [​](https://bun.com/docs/pm/cli/audit#json) `--json`

Use the `--json` flag to print the raw JSON response from the registry instead of the formatted report:

terminal

Copy

```
bun audit --json
```

### [​](https://bun.com/docs/pm/cli/audit#exit-code) Exit code

`bun audit` will exit with code `0` if no vulnerabilities are found and `1` if the report lists any vulnerabilities. This will still happen even if `--json` is passed.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/audit.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/audit)

⌘I