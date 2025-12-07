---
url: https://bun.com/docs/guides/install/jfrog-artifactory
title: Using bun install with Artifactory - Bun
source_domain: bun.com
---

# Using bun install with Artifactory - Bun

[JFrog Artifactory](https://jfrog.com/artifactory/) is a package management system for npm, Docker, Maven, NuGet, Ruby, Helm, and more. It allows you to host your own private npm registry, npm packages, and other types of packages as well.
To use it with `bun install`, add a `bunfig.toml` file to your project with the following contents:

---

### [​](https://bun.com/docs/guides/install/jfrog-artifactory#configure-with-bunfig-toml) Configure with bunfig.toml

Make sure to replace `MY_SUBDOMAIN` with your JFrog Artifactory subdomain, such as `jarred1234` and MY\_TOKEN with your JFrog Artifactory token.

bunfig.toml

Copy

```
[install.registry]
url = "https://MY_SUBDOMAIN.jfrog.io/artifactory/api/npm/npm/_auth=MY_TOKEN"
# You can use an environment variable here
# url = "$NPM_CONFIG_REGISTRY"
```

---

### [​](https://bun.com/docs/guides/install/jfrog-artifactory#configure-with-$npm-config-registry) Configure with `$NPM_CONFIG_REGISTRY`

Like with npm, you can use the `NPM_CONFIG_REGISTRY` environment variable to configure JFrog Artifactory with bun install.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/jfrog-artifactory.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/jfrog-artifactory)

⌘I