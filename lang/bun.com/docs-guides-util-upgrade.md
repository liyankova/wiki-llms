---
url: https://bun.com/docs/guides/util/upgrade
title: Upgrade Bun to the latest version - Bun
source_domain: bun.com
---

# Upgrade Bun to the latest version - Bun

Bun can upgrade itself using the built-in `bun upgrade` command. This is the fastest way to get the latest features and bug fixes.

terminal

Copy

```
bun upgrade
```

This downloads and installs the latest stable version of Bun, replacing the currently installed version.

To see the current version of Bun, run `bun --version`.

---

## [​](https://bun.com/docs/guides/util/upgrade#verify-the-upgrade) Verify the upgrade

After upgrading, verify the new version:

terminal

Copy

```
bun --version
# Output: 1.x.y

# See the exact commit of the Bun binary
bun --revision
# Output: 1.x.y+abc123def
```

---

## [​](https://bun.com/docs/guides/util/upgrade#upgrade-to-canary-builds) Upgrade to canary builds

Canary builds are automatically released on every commit to the `main` branch. These are untested but useful for trying new features or verifying bug fixes before they’re released.

terminal

Copy

```
bun upgrade --canary
```

Canary builds are not recommended for production use. They may contain bugs or breaking changes.

---

## [​](https://bun.com/docs/guides/util/upgrade#switch-back-to-stable) Switch back to stable

If you’re on a canary build and want to return to the latest stable release:

terminal

Copy

```
bun upgrade --stable
```

---

## [​](https://bun.com/docs/guides/util/upgrade#install-a-specific-version) Install a specific version

To install a specific version of Bun, use the install script with a version tag:

* macOS & Linux
* Windows

terminal

Copy

```
curl -fsSL https://bun.sh/install | bash -s "bun-v1.3.3"
```

---

## [​](https://bun.com/docs/guides/util/upgrade#package-manager-users) Package manager users

If you installed Bun via a package manager, use that package manager to upgrade instead of `bun upgrade` to avoid conflicts.

**Homebrew users**   
To avoid conflicts with Homebrew, use `brew upgrade bun` instead.**Scoop users**   
To avoid conflicts with Scoop, use `scoop update bun` instead.

---

## [​](https://bun.com/docs/guides/util/upgrade#see-also) See also

* [Installation](https://bun.com/docs/installation) — Install Bun for the first time
* [Update packages](https://bun.com/docs/pm/cli/update) — Update dependencies to latest versions

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/upgrade.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/upgrade)

⌘I