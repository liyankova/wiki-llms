---
url: https://bun.com/docs/typescript
title: TypeScript - Bun
source_domain: bun.com
---

# TypeScript - Bun

To install the TypeScript definitions for Bun’s built-in APIs, install `@types/bun`.

terminal

Copy

```
bun add -d @types/bun # dev dependency
```

At this point, you should be able to reference the `Bun` global in your TypeScript files without seeing errors in your editor.

## [​](https://bun.com/docs/typescript#suggested-compileroptions) Suggested `compilerOptions`

Bun supports things like top-level await, JSX, and extensioned `.ts` imports, which TypeScript doesn’t allow by default. Below is a set of recommended `compilerOptions` for a Bun project, so you can use these features without seeing compiler warnings from TypeScript.

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

If you run `bun init` in a new directory, this `tsconfig.json` will be generated for you. (The stricter flags are disabled by default.)

terminal

Copy

```
bun init
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/typescript.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /typescript)

⌘I