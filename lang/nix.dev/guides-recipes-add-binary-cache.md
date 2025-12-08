---
url: https://nix.dev/guides/recipes/add-binary-cache
title: Configure Nix to use a custom binary cache — nix.dev  documentation
source_domain: nix.dev
---

# Configure Nix to use a custom binary cache — nix.dev  documentation

[Skip to main content](https://nix.dev/guides/recipes/add-binary-cache#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/guides/recipes/add-binary-cache.md "Download source file")

# Configure Nix to use a custom binary cache

# Configure Nix to use a custom binary cache[#](https://nix.dev/guides/recipes/add-binary-cache#configure-nix-to-use-a-custom-binary-cache "Link to this heading")

Nix can be configured to use a binary cache with the [`substituters`](https://nix.dev/manual/nix/2.21/command-ref/conf-file#conf-substituters) and [`trusted-public-keys`](https://nix.dev/manual/nix/2.21/command-ref/conf-file#conf-trusted-public-keys) settings, either exclusively or in addition to [cache.nixos.org](http://cache.nixos.org).

Tip

Follow the tutorial to [set up an HTTP binary cache](https://nix.dev/tutorials/nixos/binary-cache-setup#setup-http-binary-cache) and create a key pair for signing store objects.

For example, given a binary cache at `https://example.org` with public key `My56...Q==%`, and some derivation in `default.nix`, make Nix exclusively use that cache once by passing [settings as command line flags](https://nix.dev/manual/nix/2.21/command-ref/conf-file#command-line-flags):

```
$ nix-build --substituters https://example.org --trusted-public-keys example.org:My56...Q==%
```

To permanently use the custom cache in addition to the public cache, add to the [Nix configuration file](https://nix.dev/manual/nix/2.21/command-ref/conf-file#configuration-file):

```
$ echo "extra-substituters = https://example.org" >> /etc/nix/nix.conf
$ echo "extra-trusted-public-keys = example.org:My56...Q==%" >> /etc/nix/nix.conf
```

To always use only the custom cache:

```
$ echo "substituters = https://example.org" >> /etc/nix/nix.conf
$ echo "trusted-public-keys = example.org:My56...Q==%" >> /etc/nix/nix.conf
```

NixOS

On NixOS, Nix is configured through the [`nix.settings`](https://search.nixos.org/options?show=nix.settings) option:

```
1{ ... }: {
2  nix.settings = {
3    substituters = [ "https://example.org" ];
4    trusted-public-keys = [ "example.org:My56...Q==%" ];
5  };
6}
```