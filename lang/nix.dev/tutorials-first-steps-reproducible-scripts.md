---
url: https://nix.dev/tutorials/first-steps/reproducible-scripts
title: Reproducible interpreted scripts — nix.dev  documentation
source_domain: nix.dev
---

# Reproducible interpreted scripts — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/first-steps/reproducible-scripts#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/first-steps/reproducible-scripts.md "Download source file")

# Reproducible interpreted scripts

# Reproducible interpreted scripts[#](https://nix.dev/tutorials/first-steps/reproducible-scripts#reproducible-interpreted-scripts "Link to this heading")

In this tutorial, you will learn how to use Nix to create and run reproducible interpreted scripts, also known as [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) scripts.

## Requirements[#](https://nix.dev/tutorials/first-steps/reproducible-scripts#requirements "Link to this heading")

* A working [Nix installation](https://nix.dev/install-nix#install-nix)
* Familiarity with [Bash](https://www.gnu.org/software/bash/)

## A trivial script with non-trivial dependencies[#](https://nix.dev/tutorials/first-steps/reproducible-scripts#a-trivial-script-with-non-trivial-dependencies "Link to this heading")

Take the following script, which fetches the content XML of a URL, converts it to JSON, and formats it for better readability:

```
#! /bin/bash

curl https://github.com/NixOS/nixpkgs/releases.atom | xml2json | jq .
```

It requires the programs `curl`, `xml2json`, and `jq`.
It also requires the `bash` interpreter.
If any of these dependencies are not present on the system running the script, it will fail partially or altogether.

With Nix, we can declare all dependencies explicitly, and produce a script that will always run on any machine that supports Nix and the required packages taken from Nixpkgs.

## The script[#](https://nix.dev/tutorials/first-steps/reproducible-scripts#the-script "Link to this heading")

A [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) determines which program to use for running an interpreted script.

We will use the shebang line `#!/usr/bin/env nix-shell`.

[`env`](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/env.html) is a program available on most modern Unix-like operating systems at the file system path `/usr/bin/env`.
It takes a command name as argument and will run the first executable by that name it finds in the directories listed in the environment variable `$PATH`.

We use [`nix-shell` as a shebang interpreter](https://nix.dev/manual/nix/stable/command-ref/nix-shell.html#use-as-a--interpreter).
It takes the following parameters relevant for our use case:

* `-i` tells which program to use for interpreting the rest of the file
* `--pure` excludes most environment variables when the script is run
* `-p` lists packages that should be present in the interpreter’s environment
* `-I` explicitly sets [the search path](https://nix.dev/manual/nix/stable/command-ref/opt-common.html#opt-I) for packages

More details on the options can be found in the [`nix-shell` reference documentation](https://nix.dev/manual/nix/stable/command-ref/nix-shell.html#options).

Create a file named `nixpkgs-releases.sh` with the following content:

```
#!/usr/bin/env nix-shell
#! nix-shell -i bash --pure
#! nix-shell -p bash cacert curl jq python3Packages.xmljson
#! nix-shell -I nixpkgs=https://github.com/NixOS/nixpkgs/archive/2a601aafdc5605a5133a2ca506a34a3a73377247.tar.gz

curl https://github.com/NixOS/nixpkgs/releases.atom | xml2json | jq .
```

The first line is a standard shebang.
The additional shebang lines are a Nix-specific construct:

* With the `-i` option, `bash` is specified as the interpreter for the rest of the file.
* In this case, the `--pure` option is enabled to prevent the script from implicitly using programs that may already exist on the system on which the script is run.
* The `-p` option lists the packages required for the script to run.

  The command `xml2json` is provided by the package `python3Packages.xmljson`, while `bash`, `jq`, and `curl` are provided by packages of the same name.
  `cacert` must be present for SSL authentication to work.

  Tip

  Use [search.nixos.org](https://search.nixos.org/packages) to find packages providing the program you need.
* The parameter of `-I` refers to a specific Git commit of the Nixpkgs repository.

  This ensures that the script will always run with the exact same package versions, everywhere.

Make the script executable:

```
chmod +x nixpkgs-releases.sh
```

Run the script:

```
./nixpkgs-releases.sh
```

## Next steps[#](https://nix.dev/tutorials/first-steps/reproducible-scripts#next-steps "Link to this heading")

* [Nix language basics](https://nix.dev/tutorials/nix-language#reading-nix-language) to learn about the Nix language, which is used to declare packages and configurations.
* [Declarative shell environments with shell.nix](https://nix.dev/tutorials/first-steps/declarative-shell#declarative-reproducible-envs) to create reproducible shell environments with a declarative configuration file.
* [Garbage Collection](https://nix.dev/manual/nix/stable/package-management/garbage-collection.html) – free up storage used by the programs made available through Nix

Contents