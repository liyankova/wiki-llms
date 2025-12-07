---
url: https://bun.com/docs/project/contributing
title: Contributing - Bun
source_domain: bun.com
---

# Contributing - Bun

Configuring a development environment for Bun can take 10-30 minutes depending on your internet connection and computer speed. You will need ~10GB of free disk space for the repository and build artifacts.
If you are using Windows, please refer to [this guide](https://bun.com/docs/project/building-windows)

## [​](https://bun.com/docs/project/contributing#using-nix-alternative) Using Nix (Alternative)

A Nix flake is provided as an alternative to manual dependency installation:

Copy

```
nix develop
# or explicitly use the pure shell
# nix develop .#pure
export CMAKE_SYSTEM_PROCESSOR=$(uname -m)
bun bd
```

This provides all dependencies in an isolated, reproducible environment without requiring sudo.

## [​](https://bun.com/docs/project/contributing#install-dependencies-manual) Install Dependencies (Manual)

Using your system’s package manager, install Bun’s dependencies:

Copy

```
$ brew install automake cmake coreutils gnu-sed go icu4c libiconv libtool ninja pkg-config rust ruby sccache
```

> **Note**: The Zig compiler is automatically installed and updated by the build scripts. Manual installation is not required.

Before starting, you will need to already have a release build of Bun installed, as we use our bundler to transpile and minify our code, as well as for code generation scripts.

Copy

```
$ curl -fsSL https://bun.com/install | bash
```

### [​](https://bun.com/docs/project/contributing#optional:-install-sccache) Optional: Install `sccache`

sccache is used to cache compilation artifacts, significantly speeding up builds. It must be installed with S3 support:

Copy

```
# For macOS
$ brew install sccache

# For Linux. Note that the version in your package manager may not have S3 support.
$ cargo install sccache --features=s3
```

This will install `sccache` with S3 support. Our build scripts will automatically detect and use `sccache` with our shared S3 cache. **Note**: Not all versions of `sccache` are compiled with S3 support, hence we recommend installing it via `cargo`.

#### [​](https://bun.com/docs/project/contributing#registering-aws-credentials-for-sccache-core-developers-only) Registering AWS Credentials for `sccache` (Core Developers Only)

Core developers have write access to the shared S3 cache. To enable write access, you must log in with AWS credentials. The easiest way to do this is to use the [`aws` CLI](https://aws.amazon.com/cli/) and invoke [`aws configure` to provide your AWS security info](https://docs.aws.amazon.com/cli/latest/reference/configure/).
The `cmake` scripts should automatically detect your AWS credentials from the environment or the `~/.aws/credentials` file.

## [​](https://bun.com/docs/project/contributing#install-llvm) Install LLVM

Bun requires LLVM 19 (`clang` is part of LLVM). This version requirement is to match WebKit (precompiled), as mismatching versions will cause memory allocation failures at runtime. In most cases, you can install LLVM through your system package manager:

Copy

```
$ brew install llvm@19
```

If none of the above solutions apply, you will have to install it [manually](https://github.com/llvm/llvm-project/releases/tag/llvmorg-19.1.7).
Make sure Clang/LLVM 19 is in your path:

Copy

```
$ which clang-19
```

If not, run this to manually add it:

Copy

```
# use fish_add_path if you're using fish
# use path+="$(brew --prefix llvm@19)/bin" if you are using zsh
$ export PATH="$(brew --prefix llvm@19)/bin:$PATH"
```

⚠️ Ubuntu distributions (<= 20.04) may require installation of the C++ standard library independently. See the [troubleshooting section](https://bun.com/docs/project/contributing#span-file-not-found-on-ubuntu) for more information.

## [​](https://bun.com/docs/project/contributing#building-bun) Building Bun

After cloning the repository, run the following command to build. This may take a while as it will clone submodules and build dependencies.

Copy

```
bun run build
```

The binary will be located at `./build/debug/bun-debug`. It is recommended to add this to your `$PATH`. To verify the build worked, let’s print the version number on the development build of Bun.

Copy

```
$ build/debug/bun-debug --version
x.y.z_debug
```

## [​](https://bun.com/docs/project/contributing#vscode) VSCode

VSCode is the recommended IDE for working on Bun, as it has been configured. Once opening, you can run `Extensions: Show Recommended Extensions` to install the recommended extensions for Zig and C++. ZLS is automatically configured.
If you use a different editor, make sure that you tell ZLS to use the automatically installed Zig compiler, which is located at `./vendor/zig/zig.exe`. The filename is `zig.exe` so that it works as expected on Windows, but it still works on macOS/Linux (it just has a surprising file extension).
We recommend adding `./build/debug` to your `$PATH` so that you can run `bun-debug` in your terminal:

Copy

```
bun-debug
```

## [​](https://bun.com/docs/project/contributing#running-debug-builds) Running debug builds

The `bd` package.json script compiles and runs a debug build of Bun, only printing the output of the build process if it fails.

Copy

```
bun bd <args>
bun bd test foo.test.ts
bun bd ./foo.ts
```

Bun generally takes about 2.5 minutes to compile a debug build when there are Zig changes. If your development workflow is “change one line, save, rebuild”, you will spend too much time waiting for the build to finish. Instead:

* Batch up your changes
* Ensure zls is running with incremental watching for LSP errors (if you use VSCode and install Zig and run `bun run build` once to download Zig, this should just work)
* Prefer using the debugger (“CodeLLDB” in VSCode) to step through the code.
* Use debug logs. `BUN_DEBUG_<scope>=1` will enable debug logging for the corresponding `Output.scoped(.<scope>, .hidden)` logs. You can also set `BUN_DEBUG_QUIET_LOGS=1` to disable all debug logging that isn’t explicitly enabled. To dump debug logs into a file, `BUN_DEBUG=<path-to-file>.log`. Debug logs are aggressively removed in release builds.
* src/js/\*\*.ts changes are pretty much instant to rebuild. C++ changes are a bit slower, but still much faster than the Zig code (Zig is one compilation unit, C++ is many).

## [​](https://bun.com/docs/project/contributing#code-generation-scripts) Code generation scripts

Several code generation scripts are used during Bun’s build process. These are run automatically when changes are made to certain files.
In particular, these are:

* `./src/codegen/generate-jssink.ts` — Generates `build/debug/codegen/JSSink.cpp`, `build/debug/codegen/JSSink.h` which implement various classes for interfacing with `ReadableStream`. This is internally how `FileSink`, `ArrayBufferSink`, `"type": "direct"` streams and other code related to streams works.
* `./src/codegen/generate-classes.ts` — Generates `build/debug/codegen/ZigGeneratedClasses*`, which generates Zig & C++ bindings for JavaScriptCore classes implemented in Zig. In `**/*.classes.ts` files, we define the interfaces for various classes, methods, prototypes, getters/setters etc which the code generator reads to generate boilerplate code implementing the JavaScript objects in C++ and wiring them up to Zig
* `./src/codegen/cppbind.ts` — Generates automatic Zig bindings for C++ functions marked with `[[ZIG_EXPORT]]` attributes.
* `./src/codegen/bundle-modules.ts` — Bundles built-in modules like `node:fs`, `bun:ffi` into files we can include in the final binary. In development, these can be reloaded without rebuilding Zig (you still need to run `bun run build`, but it re-reads the transpiled files from disk afterwards). In release builds, these are embedded into the binary.
* `./src/codegen/bundle-functions.ts` — Bundles globally-accessible functions implemented in JavaScript/TypeScript like `ReadableStream`, `WritableStream`, and a handful more. These are used similarly to the builtin modules, but the output more closely aligns with what WebKit/Safari does for Safari’s built-in functions so that we can copy-paste the implementations from WebKit as a starting point.

## [​](https://bun.com/docs/project/contributing#modifying-esm-modules) Modifying ESM modules

Certain modules like `node:fs`, `node:stream`, `bun:sqlite`, and `ws` are implemented in JavaScript. These live in `src/js/{node,bun,thirdparty}` files and are pre-bundled using Bun.

## [​](https://bun.com/docs/project/contributing#release-build) Release build

To compile a release build of Bun, run:

Copy

```
bun run build:release
```

The binary will be located at `./build/release/bun` and `./build/release/bun-profile`.

### [​](https://bun.com/docs/project/contributing#download-release-build-from-pull-requests) Download release build from pull requests

To save you time spent building a release build locally, we provide a way to run release builds from pull requests. This is useful for manually testing changes in a release build before they are merged.
To run a release build from a pull request, you can use the `bun-pr` npm package:

Copy

```
bunx bun-pr <pr-number>
bunx bun-pr <branch-name>
bunx bun-pr "https://github.com/oven-sh/bun/pull/1234566"
bunx bun-pr --asan <pr-number> # Linux x64 only
```

This will download the release build from the pull request and add it to `$PATH` as `bun-${pr-number}`. You can then run the build with `bun-${pr-number}`.

Copy

```
bun-1234566 --version
```

This works by downloading the release build from the GitHub Actions artifacts on the linked pull request. You may need the `gh` CLI installed to authenticate with GitHub.

## [​](https://bun.com/docs/project/contributing#addresssanitizer) AddressSanitizer

[AddressSanitizer](https://en.wikipedia.org/wiki/AddressSanitizer) helps find memory issues, and is enabled by default in debug builds of Bun on Linux and macOS. This includes the Zig code and all dependencies. It makes the Zig code take about 2x longer to build, if that’s stopping you from being productive you can disable it by setting `-Denable_asan=$<IF:$<BOOL:${ENABLE_ASAN}>,true,false>` to `-Denable_asan=false` in the `cmake/targets/BuildBun.cmake` file, but generally we recommend batching your changes up between builds.
To build a release build with Address Sanitizer, run:

Copy

```
bun run build:release:asan
```

In CI, we run our test suite with at least one target that is built with Address Sanitizer.

## [​](https://bun.com/docs/project/contributing#building-webkit-locally-+-debug-mode-of-jsc) Building WebKit locally + Debug mode of JSC

WebKit is not cloned by default (to save time and disk space). To clone and build WebKit locally, run:

Copy

```
# Clone WebKit into ./vendor/WebKit
$ git clone https://github.com/oven-sh/WebKit vendor/WebKit

# Check out the commit hash specified in `set(WEBKIT_VERSION <commit_hash>)` in cmake/tools/SetupWebKit.cmake
$ git -C vendor/WebKit checkout <commit_hash>

# Make a debug build of JSC. This will output build artifacts in ./vendor/WebKit/WebKitBuild/Debug
# Optionally, you can use `bun run jsc:build` for a release build
bun run jsc:build:debug && rm vendor/WebKit/WebKitBuild/Debug/JavaScriptCore/DerivedSources/inspector/InspectorProtocolObjects.h

# After an initial run of `make jsc-debug`, you can rebuild JSC with:
$ cmake --build vendor/WebKit/WebKitBuild/Debug --target jsc && rm vendor/WebKit/WebKitBuild/Debug/JavaScriptCore/DerivedSources/inspector/InspectorProtocolObjects.h

# Build bun with the local JSC build
bun run build:local
```

Using `bun run build:local` will build Bun in the `./build/debug-local` directory (instead of `./build/debug`), you’ll have to change a couple of places to use this new directory:

* The first line in `src/js/builtins.d.ts`
* The `CompilationDatabase` line in `.clangd` config should be `CompilationDatabase: build/debug-local`
* In `build.zig`, the `codegen_path` option should be `build/debug-local/codegen` (instead of `build/debug/codegen`)
* In `.vscode/launch.json`, many configurations use `./build/debug/`, change them as you see fit

Note that the WebKit folder, including build artifacts, is 8GB+ in size.
If you are using a JSC debug build and using VScode, make sure to run the `C/C++: Select a Configuration` command to configure intellisense to find the debug headers.
Note that if you change make changes to our [WebKit fork](https://github.com/oven-sh/WebKit), you will also have to change `SetupWebKit.cmake` to point to the commit hash.

## [​](https://bun.com/docs/project/contributing#troubleshooting) Troubleshooting

### [​](https://bun.com/docs/project/contributing#’span’-file-not-found-on-ubuntu) ’span’ file not found on Ubuntu

⚠️ Please note that the instructions below are specific to issues occurring on Ubuntu. It is unlikely that the same
issues will occur on other Linux distributions.

The Clang compiler typically uses the `libstdc++` C++ standard library by default. `libstdc++` is the default C++ Standard Library implementation provided by the GNU Compiler Collection (GCC). While Clang may link against the `libc++` library, this requires explicitly providing the `-stdlib` flag when running Clang.
Bun relies on C++20 features like `std::span`, which are not available in GCC versions lower than 11. GCC 10 doesn’t have all of the C++20 features implemented. As a result, running `make setup` may fail with the following error:

Copy

```
fatal error: 'span' file not found
#include <span>
         ^~~~~~
```

The issue may manifest when initially running `bun setup` as Clang being unable to compile a simple program:

Copy

```
The C++ compiler

  "/usr/bin/clang++-19"

is not able to compile a simple test program.
```

To fix the error, we need to update the GCC version to 11. To do this, we’ll need to check if the latest version is available in the distribution’s official repositories or use a third-party repository that provides GCC 11 packages. Here are general steps:

Copy

```
$ sudo apt update
$ sudo apt install gcc-11 g++-11
# If the above command fails with `Unable to locate package gcc-11` we need
# to add the APT repository
$ sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test
# Now run `apt install` again
$ sudo apt install gcc-11 g++-11
```

Now, we need to set GCC 11 as the default compiler:

Copy

```
$ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 100
$ sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 100
```

### [​](https://bun.com/docs/project/contributing#libarchive) libarchive

If you see an error on macOS when compiling `libarchive`, run:

Copy

```
$ brew install pkg-config
```

### [​](https://bun.com/docs/project/contributing#macos-library-not-found-for-lsystem) macOS `library not found for -lSystem`

If you see this error when compiling, run:

Copy

```
$ xcode-select --install
```

### [​](https://bun.com/docs/project/contributing#cannot-find-libatomic-a) Cannot find `libatomic.a`

Bun defaults to linking `libatomic` statically, as not all systems have it. If you are building on a distro that does not have a static libatomic available, you can run the following command to enable dynamic linking:

Copy

```
bun run build -DUSE_STATIC_LIBATOMIC=OFF
```

The built version of Bun may not work on other systems if compiled this way.

## [​](https://bun.com/docs/project/contributing#using-bun-debug) Using bun-debug

* Disable logging: `BUN_DEBUG_QUIET_LOGS=1 bun-debug ...` (to disable all debug logging)
* Enable logging for a specific zig scope: `BUN_DEBUG_EventLoop=1 bun-debug ...` (to allow `std.log.scoped(.EventLoop)`)
* Bun transpiles every file it runs, to see the actual executed source in a debug build find it in `/tmp/bun-debug-src/...path/to/file`, for example the transpiled version of `/home/bun/index.ts` would be in `/tmp/bun-debug-src/home/bun/index.ts`

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/project/contributing.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /project/contributing)

⌘I