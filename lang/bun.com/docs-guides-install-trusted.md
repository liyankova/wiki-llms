---
url: https://bun.com/docs/guides/install/trusted
title: Add a trusted dependency - Bun
source_domain: bun.com
---

# Add a trusted dependency - Bun

Unlike other npm clients, Bun does not execute arbitrary lifecycle scripts for installed dependencies, such as `postinstall` and `node-gyp` builds. These scripts represent a potential security risk, as they can execute arbitrary code on your machine.

Bun includes a default allowlist of popular packages containing `postinstall` scripts that are known to be safe. You
can see this list [here](https://github.com/oven-sh/bun/blob/main/src/install/default-trusted-dependencies.txt).

---

If you are seeing one of the following errors, you are probably trying to use a package that uses `postinstall` to work properly:

* `error: could not determine executable to run for package`
* `InvalidExe`

---

To allow Bun to execute lifecycle scripts for a specific package, add the package to `trustedDependencies` in your package.json file. You can do this automatically by running the command `bun pm trust <pkg>`.

Note that this only allows lifecycle scripts for the specific package listed in `trustedDependencies`, *not* the
dependencies of that dependency!

package.json

Copy

```
{
  "name": "my-app",
  "version": "1.0.0",
  "trustedDependencies": ["my-trusted-package"] 
}
```

---

Once this is added, run a fresh install. Bun will re-install your dependencies and properly install

terminal

Copy

```
rm -rf node_modules
rm bun.lock
bun install
```

---

See [Docs > Package manager > Trusted dependencies](https://bun.com/docs/pm/lifecycle) for complete documentation of trusted dependencies.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/trusted.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/trusted)

⌘I