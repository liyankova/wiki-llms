---
url: https://bun.com/docs/runtime/templating/init
title: bun init - Bun
source_domain: bun.com
---

# bun init - Bun

Get started with Bun by scaffolding a new project with `bun init`.

terminal

Copy

```
bun init my-app
```

Copy

```
? Select a project template - Press return to submit.
❯ Blank
  React
  Library

✓ Select a project template: Blank

 + .gitignore
 + CLAUDE.md
 + .cursor/rules/use-bun-instead-of-node-vite-npm-pnpm.mdc -> CLAUDE.md
 + index.ts
 + tsconfig.json (for editor autocomplete)
 + README.md
```

Press `enter` to accept the default answer for each prompt, or pass the `-y` flag to auto-accept the defaults.

---

`bun init` is a quick way to start a blank project with Bun. It guesses with sane defaults and is non-destructive when run multiple times.

![Demo](https://user-images.githubusercontent.com/709451/183006613-271960a3-ff22-4f7c-83f5-5e18f684c836.gif)

It creates:

* a `package.json` file with a name that defaults to the current directory name
* a `tsconfig.json` file or a `jsconfig.json` file, depending if the entry point is a TypeScript file or not
* an entry point which defaults to `index.ts` unless any of `index.{tsx, jsx, js, mts, mjs}` exist or the `package.json` specifies a `module` or `main` field
* a `README.md` file

AI Agent rules (disable with `$BUN_AGENT_RULE_DISABLED=1`):

* a `CLAUDE.md` file when Claude CLI is detected (disable with `CLAUDE_CODE_AGENT_RULE_DISABLED` env var)
* a `.cursor/rules/*.mdc` file to guide [Cursor AI](https://cursor.sh) to use Bun instead of Node.js and npm when Cursor is detected

If you pass `-y` or `--yes`, it will assume you want to continue without asking questions.
At the end, it runs `bun install` to install `@types/bun`.

---

## [​](https://bun.com/docs/runtime/templating/init#cli-usage) CLI Usage

terminal

Copy

```
bun init <folder?>
```

### [​](https://bun.com/docs/runtime/templating/init#initialization-options) Initialization Options

[​](https://bun.com/docs/runtime/templating/init#param-yes)

--yes

boolean

Accept all default prompts without asking questions. Alias: `-y`

[​](https://bun.com/docs/runtime/templating/init#param-minimal)

--minimal

boolean

Only initialize type definitions (skip app scaffolding). Alias: `-m`

### [​](https://bun.com/docs/runtime/templating/init#project-templates) Project Templates

[​](https://bun.com/docs/runtime/templating/init#param-react)

--react

string|boolean

Scaffold a React project. When used without a value, creates a baseline React app.
  
 Accepts values for presets:

* `tailwind` – React app preconfigured with Tailwind CSS
* `shadcn` – React app with `@shadcn/ui` and Tailwind CSS

Examples:

```
bun init —react bun init —react=tailwind bun init —react=shadcn
```

### [​](https://bun.com/docs/runtime/templating/init#output-&-files) Output & Files

[​](https://bun.com/docs/runtime/templating/init#param-result)

(result)

info

Initializes project files and configuration for the chosen options (e.g., creating essential config files and a
starter directory structure). Exact files vary by template.

### [​](https://bun.com/docs/runtime/templating/init#global-configuration-&-context) Global Configuration & Context

[​](https://bun.com/docs/runtime/templating/init#param-cwd)

--cwd

string

Run `bun init` as if started in a different working directory (useful in scripts).

### [​](https://bun.com/docs/runtime/templating/init#help) Help

[​](https://bun.com/docs/runtime/templating/init#param-help)

--help

boolean

Print this help menu. Alias: `-h`

### [​](https://bun.com/docs/runtime/templating/init#examples) Examples

* Accept all defaults

  terminal

  Copy

  ```
  bun init -y
  ```
* React

  terminal

  Copy

  ```
  bun init --react
  ```
* React + Tailwind CSS

  terminal

  Copy

  ```
  bun init --react=tailwind
  ```
* React + @shadcn/ui

  terminal

  Copy

  ```
  bun init --react=shadcn
  ```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/templating/init.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/templating/init)

⌘I