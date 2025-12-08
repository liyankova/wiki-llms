---
url: https://nix.dev/manual/nix/2.32/development/building
title: Building - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Building - Nix 2.32.2 Reference Manual

# [Building Nix](https://nix.dev/manual/nix/2.32/development/building#building-nix)

This section provides some notes on how to start hacking on Nix.
To get the latest version of Nix from GitHub:

```
$ git clone https://github.com/NixOS/nix.git
$ cd nix
```

> **Note**
>
> The following instructions assume you already have some version of Nix installed locally, so that you can use it to set up the development environment.
> If you don't have it installed, follow the [installation instructions](https://nix.dev/manual/nix/2.32/installation/).

To build all dependencies and start a shell in which all environment variables are set up so that those dependencies can be found:

```
$ nix-shell
```

To get a shell with one of the other [supported compilation environments](https://nix.dev/manual/nix/2.32/development/building#compilation-environments):

```
$ nix-shell --attr devShells.x86_64-linux.native-clangStdenv
```

> **Note**
>
> You can use `native-ccacheStdenv` to drastically improve rebuild time.
> By default, [ccache](https://ccache.dev) keeps artifacts in `~/.cache/ccache/`.

To build Nix itself in this shell:

```
[nix-shell]$ out="$(pwd)/outputs/out" dev=$out debug=$out mesonFlags+=" --prefix=${out}"
[nix-shell]$ dontAddPrefix=1 configurePhase
[nix-shell]$ buildPhase
```

To test it:

```
[nix-shell]$ checkPhase
```

To install it in `$(pwd)/outputs`:

```
[nix-shell]$ installPhase
[nix-shell]$ ./outputs/out/bin/nix --version
nix (Nix) 2.12
```

To build a release version of Nix for the current operating system and CPU architecture:

```
$ nix-build
```

You can also build Nix for one of the [supported platforms](https://nix.dev/manual/nix/2.32/development/building#platforms).

## [Building Nix with flakes](https://nix.dev/manual/nix/2.32/development/building#building-nix-with-flakes)

This section assumes you are using Nix with the [`flakes`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-flakes) and [`nix-command`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-nix-command) experimental features enabled.

To build all dependencies and start a shell in which all environment variables are set up so that those dependencies can be found:

```
$ nix develop
```

This shell also adds `./outputs/bin/nix` to your `$PATH` so you can run `nix` immediately after building it.

To get a shell with one of the other [supported compilation environments](https://nix.dev/manual/nix/2.32/development/building#compilation-environments):

```
$ nix develop .#native-clangStdenv
```

> **Note**
>
> Use `ccacheStdenv` to drastically improve rebuild time.
> By default, [ccache](https://ccache.dev) keeps artifacts in `~/.cache/ccache/`.

To build Nix itself in this shell:

```
[nix-shell]$ configurePhase
[nix-shell]$ buildPhase
```

To test it:

```
[nix-shell]$ checkPhase
```

To install it in `$(pwd)/outputs`:

```
[nix-shell]$ installPhase
[nix-shell]$ nix --version
nix (Nix) 2.12
```

For more information on running and filtering tests, see
[`testing.md`](https://nix.dev/manual/nix/2.32/development/testing).

To build a release version of Nix for the current operating system and CPU architecture:

```
$ nix build
```

You can also build Nix for one of the [supported platforms](https://nix.dev/manual/nix/2.32/development/building#platforms).

## [Platforms](https://nix.dev/manual/nix/2.32/development/building#platforms)

Nix can be built for various platforms, as specified in [`flake.nix`](https://github.com/nixos/nix/blob/master/flake.nix):

* `x86_64-linux`
* `x86_64-darwin`
* `i686-linux`
* `aarch64-linux`
* `aarch64-darwin`
* `armv6l-linux`
* `armv7l-linux`
* `riscv64-linux`

In order to build Nix for a different platform than the one you're currently
on, you need a way for your current Nix installation to build code for that
platform. Common solutions include [remote build machines] and [binary format emulation](https://nixos.org/manual/nixos/stable/options.html#opt-boot.binfmt.emulatedSystems)
(only supported on NixOS).

Given such a setup, executing the build only requires selecting the respective attribute.
For example, to compile for `aarch64-linux`:

```
$ nix-build --attr packages.aarch64-linux.default
```

or for Nix with the [`flakes`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-flakes) and [`nix-command`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-nix-command) experimental features enabled:

```
$ nix build .#packages.aarch64-linux.default
```

Cross-compiled builds are available for:

* `armv6l-linux`
* `armv7l-linux`
* `riscv64-linux`
  Add more [system types](https://nix.dev/manual/nix/2.32/development/building#system-type) to `crossSystems` in `flake.nix` to bootstrap Nix on unsupported platforms.

### [Building for multiple platforms at once](https://nix.dev/manual/nix/2.32/development/building#building-for-multiple-platforms-at-once)

It is useful to perform multiple cross and native builds on the same source tree,
for example to ensure that better support for one platform doesn't break the build for another.
Meson thankfully makes this very easy by confining all build products to the build directory --- one simple shares the source directory between multiple build directories, each of which contains the build for Nix to a different platform.

Here's how to do that:

1. Instruct Nixpkgs's infra where we want Meson to put its build directory

   ```
   mesonBuildDir=build-my-variant-name
   ```
2. Configure as usual

   ```
   configurePhase
   ```
3. Build as usual

   ```
   buildPhase
   ```

## [System type](https://nix.dev/manual/nix/2.32/development/building#system-type)

Nix uses a string with the following format to identify the *system type* or *platform* it runs on:

```
<cpu>-<os>[-<abi>]
```

It is set when Nix is compiled for the given system, and based on the output of Meson's [`host_machine` information](https://mesonbuild.com/Reference-manual_builtin_host_machine.html)>

```
<cpu>-<vendor>-<os>[<version>][-<abi>]
```

When cross-compiling Nix with Meson for local development, you need to specify a [cross-file](https://mesonbuild.com/Cross-compilation.html) using the `--cross-file` option. Cross-files define the target architecture and toolchain. When cross-compiling Nix with Nix, Nixpkgs takes care of this for you.

In the nix flake we also have some cross-compilation targets available:

```
nix build .#nix-everything-riscv64-unknown-linux-gnu
nix build .#nix-everything-armv7l-unknown-linux-gnueabihf
nix build .#nix-everything-armv7l-unknown-linux-gnueabihf
nix build .#nix-everything-x86_64-unknown-freebsd
nix build .#nix-everything-x86_64-w64-mingw32
```

For historic reasons and backward-compatibility, some CPU and OS identifiers are translated as follows:

| `host_machine.cpu_family()` | `host_machine.endian()` | Nix |
| --- | --- | --- |
| `x86` |  | `i686` |
| `arm` |  | `host_machine.cpu()` |
| `ppc` | `little` | `powerpcle` |
| `ppc64` | `little` | `powerpc64le` |
| `ppc` | `big` | `powerpc` |
| `ppc64` | `big` | `powerpc64` |
| `mips` | `little` | `mipsel` |
| `mips64` | `little` | `mips64el` |
| `mips` | `big` | `mips` |
| `mips64` | `big` | `mips64` |

## [Compilation environments](https://nix.dev/manual/nix/2.32/development/building#compilation-environments)

Nix can be compiled using multiple environments:

* `stdenv`: default;
* `gccStdenv`: force the use of `gcc` compiler;
* `clangStdenv`: force the use of `clang` compiler;
* `ccacheStdenv`: enable [ccache], a compiler cache to speed up compilation.

To build with one of those environments, you can use

```
$ nix build .#nix-cli-ccacheStdenv
```

for flake-enabled Nix, or

```
$ nix-build --attr nix-cli-ccacheStdenv
```

for classic Nix.

You can use any of the other supported environments in place of `nix-cli-ccacheStdenv`.

## [Editor integration](https://nix.dev/manual/nix/2.32/development/building#editor-integration)

The `clangd` LSP server is installed by default on the `clang`-based `devShell`s.
See [supported compilation environments](https://nix.dev/manual/nix/2.32/development/building#compilation-environments) and instructions how to set up a shell [with flakes](https://nix.dev/manual/nix/2.32/development/building#nix-with-flakes) or in [classic Nix](https://nix.dev/manual/nix/2.32/development/building#classic-nix).

To use the LSP with your editor, you will want a `compile_commands.json` file telling `clangd` how we are compiling the code.
Meson's configure always produces this inside the build directory.

Configure your editor to use the `clangd` from the `.#native-clangStdenv` shell.
You can do that either by running it inside the development shell, or by using [nix-direnv](https://github.com/nix-community/nix-direnv) and [the appropriate editor plugin](https://github.com/direnv/direnv/wiki#editor-integration).

> **Note**
>
> For some editors (e.g. Visual Studio Code), you may need to install a [special extension](https://open-vsx.org/extension/llvm-vs-code-extensions/vscode-clangd) for the editor to interact with `clangd`.
> Some other editors (e.g. Emacs, Vim) need a plugin to support LSP servers in general (e.g. [lsp-mode](https://github.com/emacs-lsp/lsp-mode) for Emacs and [vim-lsp](https://github.com/prabirshrestha/vim-lsp) for vim).
> Editor-specific setup is typically opinionated, so we will not cover it here in more detail.

## [Formatting and pre-commit hooks](https://nix.dev/manual/nix/2.32/development/building#formatting-and-pre-commit-hooks)

You may run the formatters as a one-off using:

```
./maintainers/format.sh
```

### [Pre-commit hooks](https://nix.dev/manual/nix/2.32/development/building#pre-commit-hooks)

If you'd like to run the formatters before every commit, install the hooks:

```
pre-commit-hooks-install
```

This installs [pre-commit](https://pre-commit.com) using [cachix/git-hooks.nix](https://github.com/cachix/git-hooks.nix).

When making a commit, pay attention to the console output.
If it fails, run `git add --patch` to approve the suggestions *and commit again*.

To refresh pre-commit hook's config file, do the following:

1. Exit the development shell and start it again by running `nix develop`.
2. If you also use the pre-commit hook, also run `pre-commit-hooks-install` again.

### [VSCode](https://nix.dev/manual/nix/2.32/development/building#vscode)

Insert the following json into your `.vscode/settings.json` file to configure `nixfmt`.
This will be picked up by the *Format Document* command, `"editor.formatOnSave"`, etc.

```
{
  "nix.formatterPath": "nixfmt",
  "nix.serverSettings": {
    "nixd": {
      "formatting": {
        "command": [
          "nixfmt"
        ],
      },
    },
    "nil": {
      "formatting": {
        "command": [
          "nixfmt"
        ],
      },
    },
  },
}
```