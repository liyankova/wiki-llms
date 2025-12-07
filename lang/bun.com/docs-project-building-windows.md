---
url: https://bun.com/docs/project/building-windows
title: Building Windows - Bun
source_domain: bun.com
---

# Building Windows - Bun

This document describes the build process for Windows. If you run into problems, please join the [#contributing channel on our Discord](http://bun.com/discord) for help.
It is strongly recommended to use [PowerShell 7 (`pwsh.exe`)](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.4) instead of the default `powershell.exe`.

## [​](https://bun.com/docs/project/building-windows#prerequisites) Prerequisites

### [​](https://bun.com/docs/project/building-windows#enable-scripts) Enable Scripts

By default, running unverified scripts are blocked.

Copy

```
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted
```

### [​](https://bun.com/docs/project/building-windows#system-dependencies) System Dependencies

Bun v1.1 or later. We use Bun to run it’s own code generators.

Copy

```
> irm bun.sh/install.ps1 | iex
```

[Visual Studio](https://visualstudio.microsoft.com) with the “Desktop Development with C++” workload. While installing, make sure to install Git as well, if Git for Windows is not already installed.
Visual Studio can be installed graphically using the wizard or through WinGet:

Copy

```
> winget install "Visual Studio Community 2022" --override "--add Microsoft.VisualStudio.Workload.NativeDesktop Microsoft.VisualStudio.Component.Git " -s msstore
```

After Visual Studio, you need the following:

* LLVM 19.1.7
* Go
* Rust
* NASM
* Perl
* Ruby
* Node.js

The Zig compiler is automatically downloaded, installed, and updated by the building process.

[Scoop](https://scoop.sh) can be used to install these remaining tools easily.

Scoop

Copy

```
> irm https://get.scoop.sh | iex
> scoop install nodejs-lts go rust nasm ruby perl sccache
# scoop seems to be buggy if you install llvm and the rest at the same time
> scoop install [email protected]
```

Please do not use WinGet/other package manager for these, as you will likely install Strawberry Perl instead of a more
minimal installation of Perl. Strawberry Perl includes many other utilities that get installed into `$Env:PATH` that
will conflict with MSVC and break the build.

If you intend on building WebKit locally (optional), you should install these packages:

Scoop

Copy

```
> scoop install make cygwin python
```

From here on out, it is **expected you use a PowerShell Terminal with `.\scripts\vs-shell.ps1` sourced**. This script is available in the Bun repository and can be loaded by executing it:

Copy

```
> .\scripts\vs-shell.ps1
```

To verify, you can check for an MSVC-only command line such as `mt.exe`

Copy

```
> Get-Command mt
```

It is not recommended to install `ninja` / `cmake` into your global path, because you may run into a situation where
you try to build bun without .\scripts\vs-shell.ps1 sourced.

## [​](https://bun.com/docs/project/building-windows#building) Building

Copy

```
> bun run build

# after the initial `bun run build` you can use the following to build
> ninja -Cbuild/debug
```

If this was successful, you should have a `bun-debug.exe` in the `build/debug` folder.

Copy

```
> .\build\debug\bun-debug.exe --revision
```

You should add this to `$Env:PATH`. The simplest way to do so is to open the start menu, type “Path”, and then navigate the environment variables menu to add `C:\.....\bun\build\debug` to the user environment variable `PATH`. You should then restart your editor (if it does not update still, log out and log back in).

## [​](https://bun.com/docs/project/building-windows#extra-paths) Extra paths

* WebKit is extracted to `build/debug/cache/webkit/`
* Zig is extracted to `build/debug/cache/zig/bin/zig.exe`

## [​](https://bun.com/docs/project/building-windows#tests) Tests

You can run the test suite either using `bun test <path>` or by using the wrapper script `bun node:test <path>`. The `bun node:test` command runs every test file in a separate instance of bun.exe, to prevent a crash in the test runner from stopping the entire suite.

Copy

```
# Setup
> bun i --cwd packages\bun-internal-test

# Run the entire test suite with reporter
# the package.json script "test" uses "build/debug/bun-debug.exe" by default
> bun run test

# Run an individual test file:
> bun-debug test node\fs
> bun-debug test "C:\bun\test\js\bun\resolve\import-meta.test.js"
```

## [​](https://bun.com/docs/project/building-windows#troubleshooting) Troubleshooting

### [​](https://bun.com/docs/project/building-windows#rc-file-fails-to-build) .rc file fails to build

`llvm-rc.exe` is odd. don’t use it. use `rc.exe`, to do this make sure you are in a visual studio dev terminal, check `rc /?` to ensure it is `Microsoft Resource Compiler`

### [​](https://bun.com/docs/project/building-windows#failed-to-write-output-‘bun-debug-exe’:-permission-denied) failed to write output ‘bun-debug.exe’: permission denied

you cannot overwrite `bun-debug.exe` if it is already open. you likely have a running instance, maybe in the vscode debugger?

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/project/building-windows.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /project/building-windows)

⌘I