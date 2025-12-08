---
url: https://nix.dev/tutorials/packaging-existing-software
title: Packaging existing software with Nix — nix.dev  documentation
source_domain: nix.dev
---

# Packaging existing software with Nix — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/packaging-existing-software#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/packaging-existing-software.md "Download source file")

# Packaging existing software with Nix

# Packaging existing software with Nix[#](https://nix.dev/tutorials/packaging-existing-software#packaging-existing-software-with-nix "Link to this heading")

One of Nix’s primary use-cases is in addressing common difficulties encountered with packaging software, such as specifying and obtaining dependencies.

In the long term, Nix helps tremendously with alleviating such problems.
But when *first* packaging existing software with Nix, it’s common to encounter errors that seem inscrutable.

## Introduction[#](https://nix.dev/tutorials/packaging-existing-software#introduction "Link to this heading")

In this tutorial, you’ll create your first [Nix derivations](https://nix.dev/manual/nix/stable/language/derivations) to package C/C++ software, taking advantage of the [Nixpkgs Standard Environment](https://nixos.org/manual/nixpkgs/stable/#part-stdenv) (`stdenv`), which automates much of the work involved.

### What will you learn?[#](https://nix.dev/tutorials/packaging-existing-software#what-will-you-learn "Link to this heading")

The tutorial begins with `hello`, an implementation of “hello world” which only requires dependencies already provided by `stdenv`.
Next, you will build more complex packages with their own dependencies, leading you to use additional derivation features.

You’ll encounter and address Nix error messages, build failures, and a host of other issues, developing your iterative debugging techniques along the way.

### What do you need?[#](https://nix.dev/tutorials/packaging-existing-software#what-do-you-need "Link to this heading")

* Familiarity with the Unix shell and plain text editors
* You should be confident with [reading the Nix language](https://nix.dev/tutorials/nix-language#reading-nix-language). Feel free to go back and work through the tutorial first.

### How long does it take?[#](https://nix.dev/tutorials/packaging-existing-software#how-long-does-it-take "Link to this heading")

Going through all the steps carefully will take around 60 minutes.

## Your first package[#](https://nix.dev/tutorials/packaging-existing-software#your-first-package "Link to this heading")

Note

A *package* is a loosely defined concept that refers to either a collection of files and other data, or a [Nix expression](https://nix.dev/reference/glossary#term-Nix-expression) representing such a collection before it comes into being.
Packages in Nixpkgs have a conventional structure, allowing them to be discovered in searches and composed in environments alongside other packages.

For the purposes of this tutorial, a “package” is a Nix language function that will evaluate to a derivation.
It will enable you or others to produce an artifact for practical use, as a consequence of having “packaged existing software with Nix”.

To start, consider this skeleton derivation:

```
1{ stdenv }:
2
3stdenv.mkDerivation {	}
```

This is a function which takes an attribute set containing `stdenv`, and produces a derivation (which currently does nothing).

### A package function[#](https://nix.dev/tutorials/packaging-existing-software#a-package-function "Link to this heading")

GNU Hello is an implementation of the “hello world” program, with source code accessible [from the GNU Project’s FTP server](https://ftp.gnu.org/gnu/hello/).

To begin, add a `pname` attribute to the set passed to `mkDerivation`.
Every package needs a name and a version, and Nix will throw `error: derivation name missing` without one.

```
stdenv.mkDerivation {
+ pname = "hello";
+ version = "2.12.1";
```

Next, you will declare a dependency on the latest version of `hello`, and instruct Nix to use `fetchzip` to download the [source code archive](https://ftp.gnu.org/gnu/hello/hello-2.12.1.tar.gz).

Note

`fetchzip` can fetch [more archives](https://nixos.org/manual/nixpkgs/stable/#fetchurl) than just zip files!

The hash cannot be known until after the archive has been downloaded and unpacked.
Nix will complain if the hash supplied to `fetchzip` is incorrect.
Set the `hash` attribute to an empty string and then use the resulting error message to determine the correct hash:

```
 1# hello.nix
 2{
 3  stdenv,
 4  fetchzip,
 5}:
 6
 7stdenv.mkDerivation {
 8  pname = "hello";
 9  version = "2.12.1";
10
11  src = fetchzip {
12    url = "https://ftp.gnu.org/gnu/hello/hello-2.12.1.tar.gz";
13    sha256 = "";
14  };
15}
```

Save this file to `hello.nix` and run `nix-build` to observe your first build failure:

```
$ nix-build hello.nix
error: cannot evaluate a function that has an argument without a value ('stdenv')
       Nix attempted to evaluate a function as a top level expression; in
       this case it must have its arguments supplied either by default
       values, or passed explicitly with '--arg' or '--argstr'. See
       https://nix.dev/manual/nix/stable/language/constructs.html#functions.

       at /home/nix-user/hello.nix:3:3:

            2| {
            3|   stdenv,
             |   ^
            4|   fetchzip,
```

Problem: the expression in `hello.nix` is a *function*, which only produces its intended output if it is passed the correct *arguments*.

### Building with `nix-build`[#](https://nix.dev/tutorials/packaging-existing-software#building-with-nix-build "Link to this heading")

`stdenv` is available from [`nixpkgs`](https://github.com/NixOS/nixpkgs/), which must be imported with another Nix expression in order to pass it as an argument to this derivation.

The recommended way to do this is to create a `default.nix` file in the same directory as `hello.nix`, with the following contents:

```
1# default.nix
2let
3  nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-24.05";
4  pkgs = import nixpkgs { config = {}; overlays = []; };
5in
6{
7  hello = pkgs.callPackage ./hello.nix { };
8}
```

This allows you to run `nix-build -A hello` to realize the derivation in `hello.nix`, similar to the current convention used in Nixpkgs.

Note

`callPackage` automatically passes attributes from `pkgs` to the given function, if they match attributes required by that function’s argument attribute set.
In this case, `callPackage` will supply `stdenv` and `fetchzip` to the function defined in `hello.nix`.

The tutorial [Package parameters and overrides with callPackage](https://nix.dev/tutorials/callpackage) goes into detail on how this works.

Now run the `nix-build` command with the new argument:

```
$ nix-build -A hello
error: hash mismatch in fixed-output derivation '/nix/store/pd2kiyfa0c06giparlhd1k31bvllypbb-source.drv':
         specified: sha256-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=
            got:    sha256-1kJjhtlsAkpNB7f6tZEs+dbKd8z7KoNHyDHEJ0tmhnc=
error: 1 dependencies of derivation '/nix/store/b4mjwlv73nmiqgkdabsdjc4zq9gnma1l-hello-2.12.1.drv' failed to build
```

### Finding the file hash[#](https://nix.dev/tutorials/packaging-existing-software#finding-the-file-hash "Link to this heading")

As expected, the incorrect file hash caused an error, and Nix helpfully provided the correct one.
In `hello.nix`, replace the empty string with the correct hash:

```
 1# hello.nix
 2{
 3  stdenv,
 4  fetchzip,
 5}:
 6
 7stdenv.mkDerivation {
 8  pname = "hello";
 9  version = "2.12.1";
10
11  src = fetchzip {
12    url = "https://ftp.gnu.org/gnu/hello/hello-2.12.1.tar.gz";
13    sha256 = "sha256-1kJjhtlsAkpNB7f6tZEs+dbKd8z7KoNHyDHEJ0tmhnc=";
14  };
15}
```

Now run the previous command again:

```
$ nix-build -A hello
this derivation will be built:
  /nix/store/rbq37s3r76rr77c7d8x8px7z04kw2mk7-hello.drv
building '/nix/store/rbq37s3r76rr77c7d8x8px7z04kw2mk7-hello.drv'...
...
configuring
...
configure: creating ./config.status
config.status: creating Makefile
...
building
... <many more lines omitted>
```

Great news: the derivation built successfully!

The console output shows that `configure` was called, which produced a `Makefile` that was then used to build the project.
It wasn’t necessary to write any build instructions in this case because the `stdenv` build system is based on [GNU Autoconf](https://www.gnu.org/software/autoconf/), which automatically detected the structure of the project directory.

### Build result[#](https://nix.dev/tutorials/packaging-existing-software#build-result "Link to this heading")

Check your working directory for the result:

```
$ ls
default.nix hello.nix  result
```

This `result` is a [symbolic link](https://en.wikipedia.org/wiki/Symbolic_link) to a Nix store location containing the built binary; you can call `./result/bin/hello` to execute this program:

```
$ ./result/bin/hello
Hello, world!
```

Congratulations, you have successfully packaged your first program with Nix!

Next, you’ll package another piece of software with external-to-`stdenv` dependencies that present new challenges, requiring you to make use of more `mkDerivation` features.

## A package with dependencies[#](https://nix.dev/tutorials/packaging-existing-software#a-package-with-dependencies "Link to this heading")

Now you will package a somewhat more complicated program, [`icat`](https://github.com/atextor/icat), which allows you to render images in your terminal.

Change the `default.nix` from the previous section by adding a new attribute for `icat`:

```
1# default.nix
2let
3  nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-24.05";
4  pkgs = import nixpkgs { config = {}; overlays = []; };
5in
6{
7  hello = pkgs.callPackage ./hello.nix { };
8  icat = pkgs.callPackage ./icat.nix { };
9}
```

Copy `hello.nix` to a new file `icat.nix`, and update the `pname` and `version` attributes in that file:

```
 1# icat.nix
 2{
 3  stdenv,
 4  fetchzip,
 5}:
 6
 7stdenv.mkDerivation {
 8  pname = "icat";
 9  version = "v0.5";
10
11  src = fetchzip {
12    # ...
13  };
14}
```

Now to download the source code.
`icat`’s upstream repository is hosted on [GitHub](https://github.com/atextor/icat), so you should replace the previous [source fetcher](https://nixos.org/manual/nixpkgs/stable/#chap-pkgs-fetchers).
This time you will use [`fetchFromGitHub`](https://nixos.org/manual/nixpkgs/stable/#fetchfromgithub) instead of `fetchzip`, by updating the argument attribute set to the function accordingly:

```
 1# icat.nix
 2{
 3  stdenv,
 4  fetchFromGitHub,
 5}:
 6
 7stdenv.mkDerivation {
 8  pname = "icat";
 9  version = "v0.5";
10
11  src = fetchFromGitHub {
12    # ...
13  };
14}
```

### Fetching source from GitHub[#](https://nix.dev/tutorials/packaging-existing-software#fetching-source-from-github "Link to this heading")

While `fetchzip` required `url` and `sha256` arguments, more are needed for [`fetchFromGitHub`](https://nixos.org/manual/nixpkgs/stable/#fetchfromgithub).

The source URL is `https://github.com/atextor/icat`, which already gives the first two arguments:

* `owner`: the name of the account controlling the repository

  ```
  owner = "atextor";
  ```
* `repo`: the name of the repository to fetch

  ```
  repo = "icat";
  ```

Navigate to the project’s [Tags page](https://github.com/atextor/icat/tags) to find a suitable [Git revision](https://git-scm.com/docs/revisions) (`rev`), such as the Git commit hash or tag (e.g. `v1.0`) corresponding to the release you want to fetch.

In this case, the latest release tag is `v0.5`.

As in the `hello` example, a hash must also be supplied.
This time, instead of using the empty string and letting `nix-build` report the correct one in an error, you can fetch the correct hash in the first place with the `nix-prefetch-url` command.

You need the SHA256 hash of the *contents* of the tarball (as opposed to the hash of the tarball file itself).
Therefore pass the `--unpack` and `--type sha256` arguments:

```
$ nix-prefetch-url --unpack https://github.com/atextor/icat/archive/refs/tags/v0.5.tar.gz --type sha256
path is '/nix/store/p8jl1jlqxcsc7ryiazbpm7c1mqb6848b-v0.5.tar.gz'
0wyy2ksxp95vnh71ybj1bbmqd5ggp13x3mk37pzr99ljs9awy8ka
```

Set the correct hash for `fetchFromGitHub`:

```
 1# icat.nix
 2{
 3  stdenv,
 4  fetchFromGitHub,
 5}:
 6
 7stdenv.mkDerivation {
 8  pname = "icat";
 9  version = "v0.5";
10
11  src = fetchFromGitHub {
12    owner = "atextor";
13    repo = "icat";
14    rev = "v0.5";
15    sha256 = "0wyy2ksxp95vnh71ybj1bbmqd5ggp13x3mk37pzr99ljs9awy8ka";
16  };
17}
```

### Missing dependencies[#](https://nix.dev/tutorials/packaging-existing-software#missing-dependencies "Link to this heading")

Running `nix-build` with the new `icat` attribute, an entirely new issue is reported:

```
$ nix-build -A icat
these 2 derivations will be built:
  /nix/store/86q9x927hsyyzfr4lcqirmsbimysi6mb-source.drv
  /nix/store/l5wz9inkvkf0qhl8kpl39vpg2xfm2qpy-icat.drv
...
error: builder for '/nix/store/l5wz9inkvkf0qhl8kpl39vpg2xfm2qpy-icat.drv' failed with exit code 2;
       last 10 log lines:
       >                  from /nix/store/hkj250rjsvxcbr31fr1v81cv88cdfp4l-glibc-2.37-8-dev/include/stdio.h:27,
       >                  from icat.c:31:
       > /nix/store/hkj250rjsvxcbr31fr1v81cv88cdfp4l-glibc-2.37-8-dev/include/features.h:195:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [8;;https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wcpp-Wcpp8;;]
       >   195 | # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
       >       |   ^~~~~~~
       > icat.c:39:10: fatal error: Imlib2.h: No such file or directory
       >    39 | #include <Imlib2.h>
       >       |          ^~~~~~~~~~
       > compilation terminated.
       > make: *** [Makefile:16: icat.o] Error 1
       For full logs, run 'nix log /nix/store/l5wz9inkvkf0qhl8kpl39vpg2xfm2qpy-icat.drv'.
```

A compiler error!
The `icat` source was pulled from GitHub, and Nix tried to build what it found, but compilation failed due to a missing dependency: the `imlib2` header.

If you [search for `imlib2` on search.nixos.org](https://search.nixos.org/packages?query=imlib2), you’ll find that `imlib2` is already in Nixpkgs.

Add this package to your build environment by adding `imlib2` to the arguments of the function in `icat.nix`.
Then add the argument’s value `imlib2` to the list of `buildInputs` in `stdenv.mkDerivation`:

```
 1# icat.nix
 2{
 3  stdenv,
 4  fetchFromGitHub,
 5  imlib2,
 6}:
 7
 8stdenv.mkDerivation {
 9  pname = "icat";
10  version = "v0.5";
11
12  src = fetchFromGitHub {
13    owner = "atextor";
14    repo = "icat";
15    rev = "v0.5";
16    sha256 = "0wyy2ksxp95vnh71ybj1bbmqd5ggp13x3mk37pzr99ljs9awy8ka";
17  };
18
19  buildInputs = [ imlib2 ];
20}
```

Run `nix-build -A icat` again and you’ll encounter another error, but compilation proceeds further this time:

```
$ nix-build -A icat
this derivation will be built:
  /nix/store/bw2d4rp2k1l5rg49hds199ma2mz36x47-icat.drv
...
error: builder for '/nix/store/bw2d4rp2k1l5rg49hds199ma2mz36x47-icat.drv' failed with exit code 2;
       last 10 log lines:
       >                  from icat.c:31:
       > /nix/store/hkj250rjsvxcbr31fr1v81cv88cdfp4l-glibc-2.37-8-dev/include/features.h:195:3: warning: #warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE" [8;;https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wcpp-Wcpp8;;]
       >   195 | # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
       >       |   ^~~~~~~
       > In file included from icat.c:39:
       > /nix/store/4fvrh0sjc8sbkbqda7dfsh7q0gxmnh9p-imlib2-1.11.1-dev/include/Imlib2.h:45:10: fatal error: X11/Xlib.h: No such file or directory
       >    45 | #include <X11/Xlib.h>
       >       |          ^~~~~~~~~~~~
       > compilation terminated.
       > make: *** [Makefile:16: icat.o] Error 1
       For full logs, run 'nix log /nix/store/bw2d4rp2k1l5rg49hds199ma2mz36x47-icat.drv'.
```

You can see a few warnings which should be corrected in the upstream code.
But the important bit for this tutorial is `fatal error: X11/Xlib.h: No such file or directory`: another dependency is missing.

## Finding packages[#](https://nix.dev/tutorials/packaging-existing-software#finding-packages "Link to this heading")

Determining from where to source a dependency is currently somewhat involved, because package names don’t always correspond to library or program names.

You will need the `Xlib.h` headers from the `X11` C package, the Nixpkgs derivation for which is `libX11`, available in the `xorg` package set.
There are multiple ways to figure this out:

### `search.nixos.org`[#](https://nix.dev/tutorials/packaging-existing-software#search-nixos-org "Link to this heading")

Tip

The easiest way to find what you need is on [search.nixos.org/packages](http://search.nixos.org/packages).

Unfortunately in this case, [searching for `x11`](https://search.nixos.org/packages?query=x11) produces too many irrelevant results because X11 is ubiquitous.
On the left side bar there is a list package sets, and [selecting `xorg`](https://search.nixos.org/packages?buckets=%7B%22package_attr_set%22%3A%5B%22xorg%22%5D%2C%22package_license_set%22%3A%5B%5D%2C%22package_maintainers_set%22%3A%5B%5D%2C%22package_platforms%22%3A%5B%5D%7D&amp;query=x11) shows something promising.

In case all else fails, it helps to become familiar with searching the [Nixpkgs source code](https://github.com/nixos/nixpkgs) for keywords.

### Local code search[#](https://nix.dev/tutorials/packaging-existing-software#local-code-search "Link to this heading")

To find name assignments in the source, search for `"<keyword> ="`.
For example, these are the search results for [`"x11 = "`](https://github.com/search?q=repo%3ANixOS%2Fnixpkgs+%22x11+%3D%22&amp;type=code) or [`"libx11 ="`](https://github.com/search?q=repo%3ANixOS%2Fnixpkgs+%22libx11+%3D%22&amp;type=code) on Github.

Or fetch a clone of the [Nixpkgs repository](https://github.com/nixos/nixpkgs) and search the code locally.

Start a shell that makes the required tools available – `git` for version control, and `rg` for code search (provided by the [`ripgrep` package](https://search.nixos.org/packages?show=ripgrep)):

```
$ nix-shell -p git ripgrep
[nix-shell:~]$
```

The Nixpkgs repository is huge.
Only clone the latest revision to avoid waiting a long time for a full clone:

```
[nix-shell:~]$ git clone https://github.com/NixOS/nixpkgs --depth 1
...
[nix-shell:~]$ cd nixpkgs/
```

To narrow down results, only search the `pkgs` subdirectory, which holds all the package recipes:

```
[nix-shell:~]$ rg "x11 =" pkgs
pkgs/tools/X11/primus/default.nix
21:  primus = if useNvidia then primusLib_ else primusLib_.override { nvidia_x11 = null; };
22:  primus_i686 = if useNvidia then primusLib_i686_ else primusLib_i686_.override { nvidia_x11 = null; };

pkgs/applications/graphics/imv/default.nix
38:    x11 = [ libGLU xorg.libxcb xorg.libX11 ];

pkgs/tools/X11/primus/lib.nix
14:    if nvidia_x11 == null then libGL

pkgs/top-level/linux-kernels.nix
573:    ati_drivers_x11 = throw "ati drivers are no longer supported by any kernel >=4.1"; # added 2021-05-18;
... <a lot more results>
```

Since `rg` is case sensitive by default,
Add `-i` to make sure you don’t miss anything:

```
[nix-shell:~]$ rg -i "libx11 =" pkgs
pkgs/applications/version-management/monotone-viz/graphviz-2.0.nix
55:    ++ lib.optional (libX11 == null) "--without-x";

pkgs/top-level/all-packages.nix
14191:    libX11 = xorg.libX11;

pkgs/servers/x11/xorg/default.nix
1119:  libX11 = callPackage ({ stdenv, pkg-config, fetchurl, xorgproto, libpthreadstubs, libxcb, xtrans, testers }: stdenv.mkDerivation (finalAttrs: {

pkgs/servers/x11/xorg/overrides.nix
147:  libX11 = super.libX11.overrideAttrs (attrs: {
```

### Local derivation search[#](https://nix.dev/tutorials/packaging-existing-software#local-derivation-search "Link to this heading")

To search derivations on the command line, use `nix-locate` from the [`nix-index`](https://github.com/nix-community/nix-index).

### Adding package sets as dependencies[#](https://nix.dev/tutorials/packaging-existing-software#adding-package-sets-as-dependencies "Link to this heading")

Add `xorg` to your derivation’s input attribute set and use `xorg.libX11` in `buildInputs`:

```
 1# icat.nix
 2{
 3  stdenv,
 4  fetchFromGitHub,
 5  imlib2,
 6  xorg,
 7}:
 8
 9stdenv.mkDerivation {
10  pname = "icat";
11  version = "v0.5";
12
13  src = fetchFromGitHub {
14    owner = "atextor";
15    repo = "icat";
16    rev = "v0.5";
17    sha256 = "0wyy2ksxp95vnh71ybj1bbmqd5ggp13x3mk37pzr99ljs9awy8ka";
18  };
19
20  buildInputs = [ imlib2 xorg.libX11 ];
21}
```

Note

Because the Nix language is lazily evaluated, accessing only `xorg.libX11` means that the remaining contents of the `xorg` attribute set are never processed.

## Fixing build failures[#](https://nix.dev/tutorials/packaging-existing-software#fixing-build-failures "Link to this heading")

Run the last command again:

```
$ nix-build -A icat
this derivation will be built:
  /nix/store/x1d79ld8jxqdla5zw2b47d2sl87mf56k-icat.drv
...
error: builder for '/nix/store/x1d79ld8jxqdla5zw2b47d2sl87mf56k-icat.drv' failed with exit code 2;
       last 10 log lines:
       >   195 | # warning "_BSD_SOURCE and _SVID_SOURCE are deprecated, use _DEFAULT_SOURCE"
       >       |   ^~~~~~~
       > icat.c: In function 'main':
       > icat.c:319:33: warning: ignoring return value of 'write' declared with attribute 'warn_unused_result' [8;;https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wunused-result-Wunused-result8;;]
       >   319 |                                 write(tempfile, &buf, 1);
       >       |                                 ^~~~~~~~~~~~~~~~~~~~~~~~
       > gcc -o icat icat.o -lImlib2
       > installing
       > install flags: SHELL=/nix/store/8fv91097mbh5049i9rglc73dx6kjg3qk-bash-5.2-p15/bin/bash install
       > make: *** No rule to make target 'install'.  Stop.
       For full logs, run 'nix log /nix/store/x1d79ld8jxqdla5zw2b47d2sl87mf56k-icat.drv'.
```

The missing dependency error is solved, but there is now another problem: `make: *** No rule to make target 'install'.  Stop.`

### `installPhase`[#](https://nix.dev/tutorials/packaging-existing-software#installphase "Link to this heading")

`stdenv` is automatically working with the `Makefile` that comes with `icat`.
The console output shows that `configure` and `make` are executed without issue, so the `icat` binary is compiling successfully.

The failure occurs when the `stdenv` attempts to run `make install`.
The `Makefile` included in the project happens to lack an `install` target.
The `README` in the `icat` repository only mentions using `make` to build the tool, leaving the installation step up to users.

To add this step to your derivation, use the [`installPhase` attribute](https://nixos.org/manual/nixpkgs/stable/#ssec-install-phase).
It contains a list of command strings that are executed to perform the installation.

Because `make` finishes successfully, the `icat` executable is available in the build directory.
You only need to copy it from there to the output directory.

In Nix, the output directory is stored in the `$out` variable.
That variable is accessible in the derivation’s [`builder` execution environment](https://nix.dev/manual/nix/2.19/language/derivations#builder-execution).
Create a `bin` directory within the `$out` directory and copy the `icat` binary there:

```
 1# icat.nix
 2{
 3  stdenv,
 4  fetchFromGitHub,
 5  imlib2,
 6  xorg,
 7}:
 8
 9stdenv.mkDerivation {
10  pname = "icat";
11  version = "v0.5";
12
13  src = fetchFromGitHub {
14    owner = "atextor";
15    repo = "icat";
16    rev = "v0.5";
17    sha256 = "0wyy2ksxp95vnh71ybj1bbmqd5ggp13x3mk37pzr99ljs9awy8ka";
18  };
19
20  buildInputs = [ imlib2 xorg.libX11 ];
21
22  installPhase = ''
23    mkdir -p $out/bin
24    cp icat $out/bin
25  '';
26}
```

### Phases and hooks[#](https://nix.dev/tutorials/packaging-existing-software#phases-and-hooks "Link to this heading")

Nixpkgs `stdenv.mkDerivation` derivations are separated into [phases](https://nixos.org/manual/nixpkgs/stable/#sec-stdenv-phases).
Each is intended to control some aspect of the build process.

Earlier you observed how `stdenv.mkDerivation` expected the project’s `Makefile` to have an `install` target, and failed when it didn’t.
To fix this, you defined a custom `installPhase` containing instructions for copying the `icat` binary to the correct output location, in effect installing it.
Up to that point, the `stdenv.mkDerivation` automatically determined the `buildPhase` information for the `icat` package.

During derivation realisation, there are a number of shell functions (“hooks”, in Nixpkgs) which may execute in each derivation phase.
Hooks do things like set variables, source files, create directories, and so on.

These are specific to each phase, and run both before and after that phase’s execution.
They modify the build environment for common operations during the build.

It’s good practice when packaging software with Nix to include calls to these hooks in the derivation phases you define, even when you don’t make direct use of them.
This facilitates easy [overriding](https://nixos.org/manual/nixpkgs/stable/#chap-overrides) of specific parts of the derivation later.
And it keeps the code tidy and makes it easier to read.

Adjust your `installPhase` to call the appropriate hooks:

```
 1# icat.nix
 2
 3# ...
 4
 5  installPhase = ''
 6    runHook preInstall
 7    mkdir -p $out/bin
 8    cp icat $out/bin
 9    runHook postInstall
10  '';
11
12# ...
```

## A successful build[#](https://nix.dev/tutorials/packaging-existing-software#a-successful-build "Link to this heading")

Running the `nix-build` command once more will finally do what you want, repeatably.
Call `ls` in the local directory to find a `result` symlink to a location in the Nix store:

```
$ ls
default.nix hello.nix icat.nix result
```

`result/bin/icat` is the executable built previously. Success!

## References[#](https://nix.dev/tutorials/packaging-existing-software#references "Link to this heading")

* [Nixpkgs Manual - Standard Environment](https://nixos.org/manual/nixpkgs/unstable/#part-stdenv)

## Next steps[#](https://nix.dev/tutorials/packaging-existing-software#next-steps "Link to this heading")

* [Package parameters and overrides with callPackage](https://nix.dev/tutorials/callpackage#callpackage-tutorial)
* [Dependencies in the development shell](https://nix.dev/guides/recipes/sharing-dependencies#sharing-dependencies)
* [Automatic environment activation with direnv](https://nix.dev/guides/recipes/direnv#automatic-direnv)
* [Setting up a Python development environment](https://nix.dev/guides/recipes/python-environment#python-dev-environment)
* [Add your own new packages to Nixpkgs](https://github.com/NixOS/nixpkgs/blob/master/CONTRIBUTING.md)

  + [How to contribute](https://nix.dev/contributing/how-to-contribute)
  + [How to get help](https://nix.dev/contributing/how-to-get-help)

Contents