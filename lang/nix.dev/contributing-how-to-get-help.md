---
url: https://nix.dev/contributing/how-to-get-help
title: How to get help — nix.dev  documentation
source_domain: nix.dev
---

# How to get help — nix.dev  documentation

[Skip to main content](https://nix.dev/contributing/how-to-get-help#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/contributing/how-to-get-help.md "Download source file")

# How to get help

# How to get help[#](https://nix.dev/contributing/how-to-get-help#how-to-get-help "Link to this heading")

If you need assistance with one of your contributions, there are a few places you
can go for help.

## How to find maintainers[#](https://nix.dev/contributing/how-to-get-help#how-to-find-maintainers "Link to this heading")

For better efficiency and a higher chance of success, you should try contacting individuals or groups with more specific knowledge first:

* If your contribution is for a package in Nixpkgs, look for its maintainers in the
  [`maintainers`](https://nixos.org/manual/nixpkgs/stable/#var-meta-maintainers)
  attribute.
* Check if any teams are responsible for the relevant subsystem:

  + On the [NixOS website](https://nixos.org/community/#governance-teams).
  + In the [list of Nixpkgs maintainer teams](https://github.com/NixOS/nixpkgs/blob/master/maintainers/team-list.nix).
  + In the `CODEOWNERS` files for [Nixpkgs](https://github.com/NixOS/nixpkgs/blob/master/ci/OWNERS) or
    [Nix](https://github.com/NixOS/nix/blob/master/.github/CODEOWNERS).
* Check the output of [`git blame`](https://git-scm.com/docs/git-blame) or [`git log`](https://www.git-scm.com/docs/git-log) for the files you need help with.
  Take note of the email addresses of people who committed relevant code.

## Which communication channels to use[#](https://nix.dev/contributing/how-to-get-help#which-communication-channels-to-use "Link to this heading")

Once you’ve found the people you’re looking for, you can contact them on one of the [community communication platforms](https://nixos.org/community):

* [GitHub](https://github.com/nixos)

  All the source code is maintained on GitHub.
  This is the right place to discuss implementation details.

  In issue comments or pull request descriptions, [mention the GitHub username](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#mentioning-people-and-teams) found in the [`maintainers-list.nix` file](https://github.com/NixOS/nixpkgs/blob/master/maintainers/maintainer-list.nix).
* [Discourse](https://discourse.nixos.org)

  Discourse is used for announcements, coordination, and open-ended questions.

  Try the GitHub username found in the [`maintainers-list.nix` file](https://github.com/NixOS/nixpkgs/blob/master/maintainers/maintainer-list.nix) to mention or directly contact a specific user.
  Note that some people use a different username on Discourse.
* [Matrix](https://matrix.to/#/#community:nixos.org)

  Matrix is used for short-lived, timely exchanges, and direct messages.

  To contact a maintainer, use their Matrix handle found in the [`maintainers-list.nix` file](https://github.com/NixOS/nixpkgs/blob/master/maintainers/maintainer-list.nix).
  If no Matrix handle is present for a specific maintainer, try searching for their GitHub username, as most people tend to use the same one across channels.

  Maintainer teams sometimes have their own public Matrix room.
* Email

  Use email addresses found with `git log`.
* Meetings and events

  Check the [official NixOS Calendar](https://calendar.google.com/calendar/u/0/embed?src=b9o52fobqjak8oq8lfkhg3t0qg@group.calendar.google.com) and the [Discourse community calendar](https://discourse.nixos.org/t/community-calendar/18589) for real-time or in-person events.
  Some community teams hold regular meetings and publish their meeting notes.

## Other venues[#](https://nix.dev/contributing/how-to-get-help#other-venues "Link to this heading")

If you haven’t found any specific users or groups that could help you with your contribution, you can resort to asking the community at large, using one of the following official communication channels:

* A room related to your question in the [NixOS Matrix space](https://matrix.to/#/#community:nixos.org).
* The [*Help* category](https://discourse.nixos.org/c/learn/9) on Discourse.
* The general [`#nix`](https://matrix.to/#/#nix:nixos.org) room on Matrix.

Contents