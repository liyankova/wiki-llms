---
url: https://bun.com/docs/pm/catalogs
title: Catalogs - Bun
source_domain: bun.com
---

# Catalogs - Bun

Catalogs in Bun provide a straightforward way to share common dependency versions across multiple packages in a monorepo. Rather than specifying the same versions repeatedly in each workspace package, you define them once in the root package.json and reference them consistently throughout your project.

## [​](https://bun.com/docs/pm/catalogs#overview) Overview

Unlike traditional dependency management where each workspace package needs to independently specify versions, catalogs let you:

1. Define version catalogs in the root package.json
2. Reference these versions with a simple `catalog:` protocol
3. Update all packages simultaneously by changing the version in just one place

This is especially useful in large monorepos where dozens of packages need to use the same version of key dependencies.

## [​](https://bun.com/docs/pm/catalogs#how-to-use-catalogs) How to Use Catalogs

### [​](https://bun.com/docs/pm/catalogs#directory-structure-example) Directory Structure Example

Consider a monorepo with the following structure:

Copy

```
my-monorepo/
├── package.json
├── bun.lock
└── packages/
    ├── app/
    │   └── package.json
    ├── ui/
    │   └── package.json
    └── utils/
        └── package.json
```

### [​](https://bun.com/docs/pm/catalogs#1-define-catalogs-in-root-package-json) 1. Define Catalogs in Root package.json

In your root-level `package.json`, add a `catalog` or `catalogs` field within the `workspaces` object:

package.json

Copy

```
{
  "name": "my-monorepo",
  "workspaces": {
    "packages": ["packages/*"],
    "catalog": {
      "react": "^19.0.0",
      "react-dom": "^19.0.0"
    },
    "catalogs": {
      "testing": {
        "jest": "30.0.0",
        "testing-library": "14.0.0"
      }
    }
  }
}
```

If you put `catalog` or `catalogs` at the top level of the `package.json` file, that will work too.

### [​](https://bun.com/docs/pm/catalogs#2-reference-catalog-versions-in-workspace-packages) 2. Reference Catalog Versions in Workspace Packages

In your workspace packages, use the `catalog:` protocol to reference versions:

packages/app/package.json

Copy

```
{
  "name": "app",
  "dependencies": {
    "react": "catalog:",
    "react-dom": "catalog:",
    "jest": "catalog:testing"
  }
}
```

packages/ui/package.json

Copy

```
{
  "name": "ui",
  "dependencies": {
    "react": "catalog:",
    "react-dom": "catalog:"
  },
  "devDependencies": {
    "jest": "catalog:testing",
    "testing-library": "catalog:testing"
  }
}
```

### [​](https://bun.com/docs/pm/catalogs#3-run-bun-install) 3. Run Bun Install

Run `bun install` to install all dependencies according to the catalog versions.

## [​](https://bun.com/docs/pm/catalogs#catalog-vs-catalogs) Catalog vs Catalogs

Bun supports two ways to define catalogs:

1. **`catalog`** (singular): A single default catalog for commonly used dependencies

   package.json

   Copy

   ```
   "catalog": {
     "react": "^19.0.0",
     "react-dom": "^19.0.0"
   }
   ```

   Reference with simply `catalog:`:

   packages/app/package.json

   Copy

   ```
   "dependencies": {
     "react": "catalog:"
   }
   ```
2. **`catalogs`** (plural): Multiple named catalogs for grouping dependencies

   package.json

   Copy

   ```
   "catalogs": {
     "testing": {
       "jest": "30.0.0"
     },
     "ui": {
       "tailwind": "4.0.0"
     }
   }
   ```

   Reference with `catalog:<name>`:

   packages/app/package.json

   Copy

   ```
   "dependencies": {
     "jest": "catalog:testing",
     "tailwind": "catalog:ui"
   }
   ```

## [​](https://bun.com/docs/pm/catalogs#benefits-of-using-catalogs) Benefits of Using Catalogs

* **Consistency**: Ensures all packages use the same version of critical dependencies
* **Maintenance**: Update a dependency version in one place instead of across multiple package.json files
* **Clarity**: Makes it obvious which dependencies are standardized across your monorepo
* **Simplicity**: No need for complex version resolution strategies or external tools

## [​](https://bun.com/docs/pm/catalogs#real-world-example) Real-World Example

Here’s a more comprehensive example for a React application:
**Root package.json**

package.json

Copy

```
{
  "name": "react-monorepo",
  "workspaces": {
    "packages": ["packages/*"],
    "catalog": {
      "react": "^19.0.0",
      "react-dom": "^19.0.0",
      "react-router-dom": "^6.15.0"
    },
    "catalogs": {
      "build": {
        "webpack": "5.88.2",
        "babel": "7.22.10"
      },
      "testing": {
        "jest": "29.6.2",
        "react-testing-library": "14.0.0"
      }
    }
  },
  "devDependencies": {
    "typescript": "5.1.6"
  }
}
```

packages/app/package.json

Copy

```
{
  "name": "app",
  "dependencies": {
    "react": "catalog:",
    "react-dom": "catalog:",
    "react-router-dom": "catalog:",
    "@monorepo/ui": "workspace:*",
    "@monorepo/utils": "workspace:*"
  },
  "devDependencies": {
    "webpack": "catalog:build",
    "babel": "catalog:build",
    "jest": "catalog:testing",
    "react-testing-library": "catalog:testing"
  }
}
```

packages/ui/package.json

Copy

```
{
  "name": "@monorepo/ui",
  "dependencies": {
    "react": "catalog:",
    "react-dom": "catalog:"
  },
  "devDependencies": {
    "jest": "catalog:testing",
    "react-testing-library": "catalog:testing"
  }
}
```

packages/utils/package.json

Copy

```
{
  "name": "@monorepo/utils",
  "dependencies": {
    "react": "catalog:"
  },
  "devDependencies": {
    "jest": "catalog:testing"
  }
}
```

## [​](https://bun.com/docs/pm/catalogs#updating-versions) Updating Versions

To update versions across all packages, simply change the version in the root package.json:

package.json

Copy

```
"catalog": {
  "react": "^19.1.0",  // Updated from ^19.0.0
  "react-dom": "^19.1.0"  // Updated from ^19.0.0
}
```

Then run `bun install` to update all packages.

## [​](https://bun.com/docs/pm/catalogs#lockfile-integration) Lockfile Integration

Bun’s lockfile tracks catalog versions, making it easy to ensure consistent installations across different environments. The lockfile includes:

* The catalog definitions from your package.json
* The resolution of each cataloged dependency

bun.lock(excerpt)

Copy

```
{
  "lockfileVersion": 1,
  "workspaces": {
    "": {
      "name": "react-monorepo",
    },
    "packages/app": {
      "name": "app",
      "dependencies": {
        "react": "catalog:",
        "react-dom": "catalog:",
        ...
      },
    },
    ...
  },
  "catalog": {
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    ...
  },
  "catalogs": {
    "build": {
      "webpack": "5.88.2",
      ...
    },
    ...
  },
  "packages": {
    ...
  }
}
```

## [​](https://bun.com/docs/pm/catalogs#limitations-and-edge-cases) Limitations and Edge Cases

* Catalog references must match a dependency defined in either `catalog` or one of the named `catalogs`
* Empty strings and whitespace in catalog names are ignored (treated as default catalog)
* Invalid dependency versions in catalogs will fail to resolve during `bun install`
* Catalogs are only available within workspaces; they cannot be used outside the monorepo

Bun’s catalog system provides a powerful yet simple way to maintain consistency across your monorepo without introducing additional complexity to your workflow.

## [​](https://bun.com/docs/pm/catalogs#publishing) Publishing

When you run `bun publish` or `bun pm pack`, Bun automatically replaces
`catalog:` references in your `package.json` with the resolved version numbers.
The published package includes regular semver strings and no longer depends on
your catalog definitions.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/catalogs.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/catalogs)

⌘I