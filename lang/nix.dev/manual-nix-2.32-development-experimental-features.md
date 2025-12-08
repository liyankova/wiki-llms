---
url: https://nix.dev/manual/nix/2.32/development/experimental-features
title: Experimental Features - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Experimental Features - Nix 2.32.2 Reference Manual

This section describes the notion of *experimental features*, and how it fits into the big picture of the development of Nix.

# [What are experimental features?](https://nix.dev/manual/nix/2.32/development/experimental-features#what-are-experimental-features)

Experimental features are considered unstable, which means that they can be changed or removed at any time.
Users must explicitly enable them by toggling the associated [experimental feature flags](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-experimental-features).
This allows accessing unstable functionality without unwittingly relying on it.

Experimental feature flags were first introduced in [Nix 2.4](https://nix.dev/manual/nix/2.32/release-notes/rl-2.4).
Before that, Nix did have experimental features, but they were not guarded by flags and were merely documented as unstable.
This was a source of confusion and controversy.

# [When should a new feature be marked experimental?](https://nix.dev/manual/nix/2.32/development/experimental-features#when-should-a-new-feature-be-marked-experimental)

A change in the Nix codebase should be guarded by an experimental feature flag if it is considered likely to be reverted or adapted in a backwards-incompatible manner after gathering more experience with it in practice.

Examples:

* Changes to the Nix language, such as new built-ins, syntactic or semantic changes, etc.
* Changes to the command-line interface

# [Lifecycle of an experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features#lifecycle-of-an-experimental-feature)

Experimental features have to be treated on a case-by-case basis.
However, the standard workflow for an experimental feature is as follows:

* A new feature is implemented in a *pull request*
  + It is guarded by an experimental feature flag that is disabled by default
* The pull request is merged, the *experimental* feature ends up in a release
  + Using the feature requires explicitly enabling it, signifying awareness of the potential risks
  + Being experimental, the feature can still be changed arbitrarily
* The feature can be *removed*
  + The associated experimental feature flag is also removed
* The feature can be declared *stable*
  + The associated experimental feature flag is removed
  + There should be enough evidence of users having tried the feature, such as feedback, fixed bugs, demonstrations of how it is put to use
  + Maintainers must feel confident that:
    - The feature is designed and implemented sensibly, that it is fit for purpose
    - Potential interactions are well-understood
    - Stabilising the feature will not incur an outsized maintenance burden in the future

The following diagram illustrates the process:

```
                  .------.
                  | idea |
                  '------'
                      |
       discussion, design, implementation
                      |
                      |     .-------.
                      |     |       |
                      v     v       |
               .--------------.  review
               | pull request |     |
               '--------------'     |
                   |     ^  |       |
                   |     |  '-------'
               .---'     '----.
               |              |
             merge       user feedback,
               |       (breaking) changes
               |              |
               '---.     .----'
                   |     |
                   v     |
               +--------------+
           .---| experimental |----.
           |   +--------------+    |
           |                       |
decision to stabilise      decision against
           |              keeping the feature
           |                       |
           v                       v
       +--------+             +---------+
       | stable |             | removed |
       +--------+             +---------+
```

# [Relation to the RFC process](https://nix.dev/manual/nix/2.32/development/experimental-features#relation-to-the-rfc-process)

Experimental features and [RFCs](https://github.com/NixOS/rfcs/) both allow approaching substantial changes while minimizing the risk.
However they serve different purposes:

* An experimental feature enables developers to iterate on and deliver a new idea without committing to it or requiring a costly long-running fork.
  It is primarily an issue of *implementation*, targeting Nix developers and early testers.
* The goal of an RFC is to make explicit all the implications of a change:
  Explain why it is wanted, which new use-cases it enables, which interface changes it requires, etc.
  It is primarily an issue of *design* and *communication*, targeting the broader community.

This means that experimental features and RFCs are orthogonal mechanisms, and can be used independently or together as needed.

# [Currently available experimental features](https://nix.dev/manual/nix/2.32/development/experimental-features#currently-available-experimental-features)

## [`auto-allocate-uids`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-auto-allocate-uids)

Allows Nix to automatically pick UIDs for builds, rather than creating
`nixbld*` user accounts. See the [`auto-allocate-uids`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-auto-allocate-uids) setting for details.

Refer to [auto-allocate-uids tracking issue](https://github.com/NixOS/nix/milestone/34) for feature tracking.

## [`blake3-hashes`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-blake3-hashes)

Enables support for BLAKE3 hashes.

Refer to [blake3-hashes tracking issue](https://nix.dev/manual/nix/2.32/development/experimental-features) for feature tracking.

## [`ca-derivations`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-ca-derivations)

Allow derivations to be content-addressed in order to prevent
rebuilds when changes to the derivation do not result in changes to
the derivation's output. See
[\_\_contentAddressed](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-__contentAddressed)
for details.

Refer to [ca-derivations tracking issue](https://github.com/NixOS/nix/milestone/35) for feature tracking.

## [`cgroups`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-cgroups)

Allows Nix to execute builds inside cgroups. See
the [`use-cgroups`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-cgroups) setting for details.

Refer to [cgroups tracking issue](https://github.com/NixOS/nix/milestone/36) for feature tracking.

## [`configurable-impure-env`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-configurable-impure-env)

Allow the use of the [impure-env](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-impure-env) setting.

Refer to [configurable-impure-env tracking issue](https://github.com/NixOS/nix/milestone/37) for feature tracking.

## [`daemon-trust-override`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-daemon-trust-override)

Allow forcing trusting or not trusting clients with
`nix-daemon`. This is useful for testing, but possibly also
useful for various experiments with `nix-daemon --stdio`
networking.

Refer to [daemon-trust-override tracking issue](https://github.com/NixOS/nix/milestone/38) for feature tracking.

## [`dynamic-derivations`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-dynamic-derivations)

Allow the use of a few things related to dynamic derivations:

* "text hashing" derivation outputs, so we can build .drv
  files.
* dependencies in derivations on the outputs of
  derivations that are themselves derivations outputs.

Refer to [dynamic-derivations tracking issue](https://github.com/NixOS/nix/milestone/39) for feature tracking.

## [`external-builders`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-external-builders)

Enables support for external builders / sandbox providers.

Refer to [external-builders tracking issue](https://nix.dev/manual/nix/2.32/development/experimental-features) for feature tracking.

## [`fetch-closure`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-fetch-closure)

Enable the use of the [`fetchClosure`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-fetchClosure) built-in function in the Nix language.

Refer to [fetch-closure tracking issue](https://github.com/NixOS/nix/milestone/40) for feature tracking.

## [`fetch-tree`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-fetch-tree)

Enable the use of the [`fetchTree`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-fetchTree) built-in function in the Nix language.

`fetchTree` exposes a generic interface for fetching remote file system trees from different types of remote sources.
The [`flakes`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-flakes) feature flag always enables `fetch-tree`.
This built-in was previously guarded by the `flakes` experimental feature because of that overlap.

Enabling just this feature serves as a "release candidate", allowing users to try it out in isolation.

Refer to [fetch-tree tracking issue](https://github.com/NixOS/nix/milestone/31) for feature tracking.

## [`flakes`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-flakes)

Enable flakes. See the manual entry for [`nix flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake) for details.

Refer to [flakes tracking issue](https://github.com/NixOS/nix/milestone/27) for feature tracking.

## [`git-hashing`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-git-hashing)

Allow creating (content-addressed) store objects which are hashed via Git's hashing algorithm.
These store objects aren't understandable by older versions of Nix.

Refer to [git-hashing tracking issue](https://github.com/NixOS/nix/milestone/41) for feature tracking.

## [`impure-derivations`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-impure-derivations)

Allow derivations to produce non-fixed outputs by setting the
`__impure` derivation attribute to `true`. An impure derivation can
have differing outputs each time it is built.

Example:

```
derivation {
  name = "impure";
  builder = /bin/sh;
  __impure = true; # mark this derivation as impure
  args = [ "-c" "read -n 10 random < /dev/random; echo $random > $out" ];
  system = builtins.currentSystem;
}
```

Each time this derivation is built, it can produce a different
output (as the builder outputs random bytes to `$out`). Impure
derivations also have access to the network, and only fixed-output
or other impure derivations can rely on impure derivations. Finally,
an impure derivation cannot also be
[content-addressed](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-ca-derivations).

This is a more explicit alternative to using [`builtins.currentTime`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-currentTime).

Refer to [impure-derivations tracking issue](https://github.com/NixOS/nix/milestone/42) for feature tracking.

## [`local-overlay-store`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-local-overlay-store)

Allow the use of [local overlay store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-overlay-store).

Refer to [local-overlay-store tracking issue](https://github.com/NixOS/nix/milestone/50) for feature tracking.

## [`mounted-ssh-store`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-mounted-ssh-store)

Allow the use of the [`mounted SSH store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#experimental-ssh-store-with-filesystem-mounted).

Refer to [mounted-ssh-store tracking issue](https://github.com/NixOS/nix/milestone/43) for feature tracking.

## [`nix-command`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)

Enable the new `nix` subcommands. See the manual on
[`nix`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix) for details.

Refer to [nix-command tracking issue](https://github.com/NixOS/nix/milestone/28) for feature tracking.

## [`no-url-literals`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-no-url-literals)

Disallow unquoted URLs as part of the Nix language syntax. The Nix
language allows for URL literals, like so:

```
$ nix repl
Welcome to Nix 2.15.0. Type :? for help.

nix-repl> http://foo
"http://foo"
```

But enabling this experimental feature will cause the Nix parser to
throw an error when encountering a URL literal:

```
$ nix repl --extra-experimental-features 'no-url-literals'
Welcome to Nix 2.15.0. Type :? for help.

nix-repl> http://foo
error: URL literals are disabled

at «string»:1:1:

1| http://foo
 | ^
```

While this is currently an experimental feature, unquoted URLs are
being deprecated and their usage is discouraged.

The reason is that, as opposed to path literals, URLs have no
special properties that distinguish them from regular strings, URLs
containing parameters have to be quoted anyway, and unquoted URLs
may confuse external tooling.

Refer to [no-url-literals tracking issue](https://github.com/NixOS/nix/milestone/44) for feature tracking.

## [`parse-toml-timestamps`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-parse-toml-timestamps)

Allow parsing of timestamps in builtins.fromTOML.

Refer to [parse-toml-timestamps tracking issue](https://github.com/NixOS/nix/milestone/45) for feature tracking.

## [`pipe-operators`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-pipe-operators)

Add `|>` and `<|` operators to the Nix language.

Refer to [pipe-operators tracking issue](https://github.com/NixOS/nix/milestone/55) for feature tracking.

## [`read-only-local-store`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-read-only-local-store)

Allow the use of the `read-only` parameter in [local store](https://nix.dev/manual/nix/2.32/store/types/local-store) URIs.

Refer to [read-only-local-store tracking issue](https://github.com/NixOS/nix/milestone/46) for feature tracking.

## [`recursive-nix`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-recursive-nix)

Allow derivation builders to call Nix, and thus build derivations
recursively.

Example:

```
with import <nixpkgs> {};

runCommand "foo"
  {
     # Optional: let Nix know "foo" requires the experimental feature
     requiredSystemFeatures = [ "recursive-nix" ];
     buildInputs = [ nix jq ];
     NIX_PATH = "nixpkgs=${<nixpkgs>}";
  }
  ''
    hello=$(nix-build -E '(import <nixpkgs> {}).hello.overrideDerivation (args: { name = "recursive-hello"; })')

    mkdir -p $out/bin
    ln -s $hello/bin/hello $out/bin/hello
  ''
```

An important restriction on recursive builders is disallowing
arbitrary substitutions. For example, running

```
nix-store -r /nix/store/kmwd1hq55akdb9sc7l3finr175dajlby-hello-2.10
```

in the above `runCommand` script would be disallowed, as this could
lead to derivations with hidden dependencies or breaking
reproducibility by relying on the current state of the Nix store. An
exception would be if
`/nix/store/kmwd1hq55akdb9sc7l3finr175dajlby-hello-2.10` were
already in the build inputs or built by a previous recursive Nix
call.

Refer to [recursive-nix tracking issue](https://github.com/NixOS/nix/milestone/47) for feature tracking.

## [`verified-fetches`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-verified-fetches)

Enables verification of git commit signatures through the [`fetchGit`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-fetchGit) built-in.

Refer to [verified-fetches tracking issue](https://github.com/NixOS/nix/milestone/48) for feature tracking.