---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon
title: nix daemon - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix daemon - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#name)

`nix daemon` - daemon to perform store operations on behalf of non-root clients

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#synopsis)

`nix daemon` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#examples)

* Run the daemon:

  ```
  # nix daemon
  ```
* Run the daemon and listen on standard I/O instead of binding to a UNIX socket:

  ```
  # nix daemon --stdio
  ```
* Run the daemon and force all connections to be trusted:

  ```
  # nix daemon --force-trusted
  ```
* Run the daemon and force all connections to be untrusted:

  ```
  # nix daemon --force-untrusted
  ```
* Run the daemon, listen on standard I/O, and force all connections to use Nix's default trust:

  ```
  # nix daemon --stdio --default-trust
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#description)

This command runs the Nix daemon, which is a required component in
multi-user Nix installations. It runs build tasks and other
operations on the Nix store on behalf of non-root users. Usually you
don't run the daemon directly; instead it's managed by a service
management framework such as `systemd` on Linux, or `launchctl` on Darwin.

Note that this daemon does not fork into the background.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#options)

* [`--default-trust`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-default-trust)

  Use Nix's default trust.
* [`--force-trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-force-trusted)

  Force the daemon to trust connecting clients.
* [`--force-untrusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-force-untrusted)

  Force the daemon to not trust connecting clients. The connection is processed by the receiving daemon before forwarding commands.
* [`--process-ops`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-process-ops)

  Forces the daemon to process received commands itself rather than forwarding the commands straight to the remote store.

  ```
          This is useful for the `mounted-ssh://` store where some actions need to be performed on the remote end but as connected user, and not as the user of the underlying daemon on the remote end.
  ```
* [`--stdio`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-stdio)

  Attach to standard I/O, instead of trying to bind to a UNIX socket.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-daemon#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.