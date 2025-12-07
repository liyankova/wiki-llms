---
url: https://bun.com/docs/guides/runtime/typescript
title: Install TypeScript declarations for Bun - Bun
source_domain: bun.com
---

# Install TypeScript declarations for Bun - Bun

To install TypeScript definitions for Bun’s built-in APIs in your project, install `@types/bun`.

terminal

Copy

```
bun add -d @types/bun # dev dependency
```

---

Below is the full set of recommended `compilerOptions` for a Bun project. With this `tsconfig.json`, you can use top-level await, extensioned or extensionless imports, and JSX.

tsconfig.json

Copy

```
{
  "compilerOptions": {
    // Environment setup & latest features
    "lib": ["ESNext"],
    "target": "ESNext",
    "module": "Preserve",
    "moduleDetection": "force",
    "jsx": "react-jsx",
    "allowJs": true,

    // Bundler mode
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "verbatimModuleSyntax": true,
    "noEmit": true,

    // Best practices
    "strict": true,
    "skipLibCheck": true,
    "noFallthroughCasesInSwitch": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitOverride": true,

    // Some stricter flags (disabled by default)
    "noUnusedLocals": false,
    "noUnusedParameters": false,
    "noPropertyAccessFromIndexSignature": false
  }
}
```

---

Refer to [Ecosystem > TypeScript](https://bun.com/docs/runtime/typescript) for a complete guide to TypeScript support in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/typescript.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/typescript)

⌘I