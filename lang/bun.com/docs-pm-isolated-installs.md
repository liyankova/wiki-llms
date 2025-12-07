---
url: https://bun.com/docs/pm/isolated-installs
title: Isolated installs - Bun
source_domain: bun.com
---

# Isolated installs - Bun

Bun provides an alternative package installation strategy called **isolated installs** that creates strict dependency isolation similar to pnpm’s approach. This mode prevents phantom dependencies and ensures reproducible, deterministic builds.
This is the default installation strategy for **new** workspace/monorepo projects (with `configVersion = 1` in the lockfile). Existing projects continue using hoisted installs unless explicitly configured.

## [​](https://bun.com/docs/pm/isolated-installs#what-are-isolated-installs) What are isolated installs?

Isolated installs create a non-hoisted dependency structure where packages can only access their explicitly declared dependencies. This differs from the traditional “hoisted” installation strategy used by npm and Yarn, where dependencies are flattened into a shared `node_modules` directory.

### [​](https://bun.com/docs/pm/isolated-installs#key-benefits) Key benefits

* **Prevents phantom dependencies** — Packages cannot accidentally import dependencies they haven’t declared
* **Deterministic resolution** — Same dependency tree regardless of what else is installed
* **Better for monorepos** — Workspace isolation prevents cross-contamination between packages
* **Reproducible builds** — More predictable resolution behavior across environments

## [​](https://bun.com/docs/pm/isolated-installs#using-isolated-installs) Using isolated installs

### [​](https://bun.com/docs/pm/isolated-installs#command-line) Command line

Use the `--linker` flag to specify the installation strategy:

terminal

Copy

```
# Use isolated installs
bun install --linker isolated

# Use traditional hoisted installs
bun install --linker hoisted
```

### [​](https://bun.com/docs/pm/isolated-installs#configuration-file) Configuration file

Set the default linker strategy in your `bunfig.toml` or globally in `$HOME/.bunfig.toml`:

bunfig.toml

Copy

```
[install]
linker = "isolated"
```

### [​](https://bun.com/docs/pm/isolated-installs#default-behavior) Default behavior

The default linker strategy depends on your project’s lockfile `configVersion`:

| `configVersion` | Using workspaces? | Default Linker |
| --- | --- | --- |
| `1` | ✅ | `isolated` |
| `1` | ❌ | `hoisted` |
| `0` | ✅ | `hoisted` |
| `0` | ❌ | `hoisted` |

**New projects**: Default to `configVersion = 1`. In workspaces, v1 uses the isolated linker by default; otherwise it uses hoisted linking.
**Existing Bun projects (made pre-v1.3.2)**: If your existing lockfile doesn’t have a version yet, Bun sets `configVersion = 0` when you run `bun install`, preserving the previous hoisted linker default.
**Migrations from other package managers**:

* From pnpm: `configVersion = 1` (using isolated installs in workspaces)
* From npm or yarn: `configVersion = 0` (using hoisted installs)

You can override the default behavior by explicitly specifying the `--linker` flag or setting it in your configuration file.

## [​](https://bun.com/docs/pm/isolated-installs#how-isolated-installs-work) How isolated installs work

### [​](https://bun.com/docs/pm/isolated-installs#directory-structure) Directory structure

Instead of hoisting dependencies, isolated installs create a two-tier structure:

tree layout of node\_modules

Copy

```
node_modules/
├── .bun/                          # Central package store
│   ├── [email protected]/             # Versioned package installations
│   │   └── node_modules/
│   │       └── package/           # Actual package files
│   ├── @[email protected]/      # Scoped packages (+ replaces /)
│   │   └── node_modules/
│   │       └── @scope/
│   │           └── package/
│   └── ...
└── package-name -> .bun/[email protected]/node_modules/package  # Symlinks
```

### [​](https://bun.com/docs/pm/isolated-installs#resolution-algorithm) Resolution algorithm

1. **Central store** — All packages are installed in `node_modules/.bun/package@version/` directories
2. **Symlinks** — Top-level `node_modules` contains symlinks pointing to the central store
3. **Peer resolution** — Complex peer dependencies create specialized directory names
4. **Deduplication** — Packages with identical package IDs and peer dependency sets are shared

### [​](https://bun.com/docs/pm/isolated-installs#workspace-handling) Workspace handling

In monorepos, workspace dependencies are handled specially:

* **Workspace packages** — Symlinked directly to their source directories, not the store
* **Workspace dependencies** — Can access other workspace packages in the monorepo
* **External dependencies** — Installed in the isolated store with proper isolation

## [​](https://bun.com/docs/pm/isolated-installs#comparison-with-hoisted-installs) Comparison with hoisted installs

| Aspect | Hoisted (npm/Yarn) | Isolated (pnpm-like) |
| --- | --- | --- |
| **Dependency access** | Packages can access any hoisted dependency | Packages only see declared dependencies |
| **Phantom dependencies** | ❌ Possible | ✅ Prevented |
| **Disk usage** | ✅ Lower (shared installs) | ✅ Similar (uses symlinks) |
| **Determinism** | ❌ Less deterministic | ✅ More deterministic |
| **Node.js compatibility** | ✅ Standard behavior | ✅ Compatible via symlinks |
| **Best for** | Single projects, legacy code | Monorepos, strict dependency management |

## [​](https://bun.com/docs/pm/isolated-installs#advanced-features) Advanced features

### [​](https://bun.com/docs/pm/isolated-installs#peer-dependency-handling) Peer dependency handling

Isolated installs handle peer dependencies through sophisticated resolution:

tree layout of node\_modules

Copy

```
# Package with peer dependencies creates specialized paths
node_modules/.bun/[email protected][email protected]/
```

The directory name encodes both the package version and its peer dependency versions, ensuring each unique combination gets its own installation.

### [​](https://bun.com/docs/pm/isolated-installs#backend-strategies) Backend strategies

Bun uses different file operation strategies for performance:

* **Clonefile** (macOS) — Copy-on-write filesystem clones for maximum efficiency
* **Hardlink** (Linux/Windows) — Hardlinks to save disk space
* **Copyfile** (fallback) — Full file copies when other methods aren’t available

### [​](https://bun.com/docs/pm/isolated-installs#debugging-isolated-installs) Debugging isolated installs

Enable verbose logging to understand the installation process:

terminal

Copy

```
bun install --linker isolated --verbose
```

This shows:

* Store entry creation
* Symlink operations
* Peer dependency resolution
* Deduplication decisions

## [​](https://bun.com/docs/pm/isolated-installs#troubleshooting) Troubleshooting

### [​](https://bun.com/docs/pm/isolated-installs#compatibility-issues) Compatibility issues

Some packages may not work correctly with isolated installs due to:

* **Hardcoded paths** — Packages that assume a flat `node_modules` structure
* **Dynamic imports** — Runtime imports that don’t follow Node.js resolution
* **Build tools** — Tools that scan `node_modules` directly

If you encounter issues, you can:

1. **Switch to hoisted mode** for specific projects:

   terminal

   Copy

   ```
   bun install --linker hoisted
   ```
2. **Report compatibility issues** to help improve isolated install support

### [​](https://bun.com/docs/pm/isolated-installs#performance-considerations) Performance considerations

* **Install time** — May be slightly slower due to symlink operations
* **Disk usage** — Similar to hoisted (uses symlinks, not file copies)
* **Memory usage** — Higher during install due to complex peer resolution

## [​](https://bun.com/docs/pm/isolated-installs#migration-guide) Migration guide

### [​](https://bun.com/docs/pm/isolated-installs#from-npm/yarn) From npm/Yarn

terminal

Copy

```
# Remove existing node_modules and lockfiles
rm -rf node_modules package-lock.json yarn.lock

# Install with isolated linker
bun install --linker isolated
```

### [​](https://bun.com/docs/pm/isolated-installs#from-pnpm) From pnpm

Isolated installs are conceptually similar to pnpm, so migration should be straightforward:

terminal

Copy

```
# Remove pnpm files
$ rm -rf node_modules pnpm-lock.yaml

# Install with Bun's isolated linker
bun install --linker isolated
```

The main difference is that Bun uses symlinks in `node_modules` while pnpm uses a global store with symlinks.

## [​](https://bun.com/docs/pm/isolated-installs#when-to-use-isolated-installs) When to use isolated installs

**Use isolated installs when:**

* Working in monorepos with multiple packages
* Strict dependency management is required
* Preventing phantom dependencies is important
* Building libraries that need deterministic dependencies

**Use hoisted installs when:**

* Working with legacy code that assumes flat `node_modules`
* Compatibility with existing build tools is required
* Working in environments where symlinks aren’t well supported
* You prefer the simpler traditional npm behavior

## [​](https://bun.com/docs/pm/isolated-installs#related-documentation) Related documentation

* [Package manager > Workspaces](https://bun.com/docs/pm/workspaces) — Monorepo workspace management
* [Package manager > Lockfile](https://bun.com/docs/pm/lockfile) — Understanding Bun’s lockfile format
* [CLI > install](https://bun.com/docs/pm/cli/install) — Complete `bun install` command reference

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/isolated-installs.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/isolated-installs)

⌘I