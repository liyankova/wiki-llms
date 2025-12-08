---
url: https://nix.dev/manual/nix/2.32/quick-start
title: Quick Start - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Quick Start - Nix 2.32.2 Reference Manual

# [Quick Start](https://nix.dev/manual/nix/2.32/quick-start#quick-start)

This chapter is for impatient people who don't like reading documentation.
For more in-depth information you are kindly referred to subsequent chapters.

1. Install Nix:

   ```
   $ curl -L https://nixos.org/nix/install | sh
   ```

   The install script will use `sudo`, so make sure you have sufficient rights.

   For other installation methods, see the detailed [installation instructions](https://nix.dev/manual/nix/2.32/installation/).
2. Run software without installing it permanently:

   ```
   $ nix-shell --packages cowsay lolcat
   ```

   This downloads the specified packages with all their dependencies, and drops you into a Bash shell where the commands provided by those packages are present.
   This will not affect your normal environment:

   ```
   [nix-shell:~]$ cowsay Hello, Nix! | lolcat
   ```

   Exiting the shell will make the programs disappear again:

   ```
   [nix-shell:~]$ exit
   $ lolcat
   lolcat: command not found
   ```
3. Search for more packages on [search.nixos.org](https://search.nixos.org/) to try them out.
4. Free up storage space:

   ```
   $ nix-collect-garbage
   ```