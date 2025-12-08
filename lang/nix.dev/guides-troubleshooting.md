---
url: https://nix.dev/guides/troubleshooting
title: Troubleshooting — nix.dev  documentation
source_domain: nix.dev
---

# Troubleshooting — nix.dev  documentation

[Skip to main content](https://nix.dev/guides/troubleshooting#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/guides/troubleshooting.md "Download source file")

# Troubleshooting

# Troubleshooting[#](https://nix.dev/guides/troubleshooting#troubleshooting "Link to this heading")

This page is a collection of tips to solve problems you may encounter when using Nix.

## What to do if a binary cache is down or unreachable?[#](https://nix.dev/guides/troubleshooting#what-to-do-if-a-binary-cache-is-down-or-unreachable "Link to this heading")

Pass [`--option substitute false`](https://nix.dev/manual/nix/stable/command-ref/conf-file#conf-substitute) to Nix commands.

## How to force Nix to re-check if something exists in the binary cache?[#](https://nix.dev/guides/troubleshooting#how-to-force-nix-to-re-check-if-something-exists-in-the-binary-cache "Link to this heading")

Nix keeps track of what’s available in binary caches so it doesn’t have to query them on every command.
This includes negative answers, that is, if a given store path cannot be substituted.

Pass the [`--narinfo-cache-negative-ttl`](https://nix.dev/manual/nix/stable/command-ref/conf-file.html#conf-narinfo-cache-negative-ttl) option to set the cache timeout in seconds.

## How to fix: `error: querying path in database: database disk image is malformed`[#](https://nix.dev/guides/troubleshooting#how-to-fix-error-querying-path-in-database-database-disk-image-is-malformed "Link to this heading")

This is a [known issue](https://github.com/NixOS/nix/issues/1353).
Try:

```
$ sqlite3 /nix/var/nix/db/db.sqlite "pragma integrity_check"
```

Which will print the errors in the [database](https://nix.dev/manual/nix/stable/glossary#gloss-nix-database).
If the errors are due to missing references, the following may work:

```
$ mv /nix/var/nix/db/db.sqlite /nix/var/nix/db/db.sqlite-bkp
$ sqlite3 /nix/var/nix/db/db.sqlite-bkp ".dump" | sqlite3 /nix/var/nix/db/db.sqlite
```

## How to fix: `error: current Nix store schema is version 10, but I only support 7`[#](https://nix.dev/guides/troubleshooting#how-to-fix-error-current-nix-store-schema-is-version-10-but-i-only-support-7 "Link to this heading")

This is a [known issue](https://github.com/NixOS/nix/issues/1251).

It means that using a new version of Nix upgraded the SQLite schema of the [database](https://nix.dev/manual/nix/stable/glossary#gloss-nix-database), and then you tried to use an older version of Nix.

The solution is to dump the database, and use the old Nix version to re-import the data:

```
$ /path/to/nix/unstable/bin/nix-store --dump-db > /tmp/db.dump
$ mv /nix/var/nix/db /nix/var/nix/db.toonew
$ mkdir /nix/var/nix/db
$ nix-store --load-db < /tmp/db.dump
```

## How to fix: `writing to file: Connection reset by peer`[#](https://nix.dev/guides/troubleshooting#how-to-fix-writing-to-file-connection-reset-by-peer "Link to this heading")

This may mean you are trying to import too large a file or directory into the [Nix store](https://nix.dev/manual/nix/stable/glossary#gloss-store), or your machine is running out of resources, such as disk space or memory.

Try to reduce the size of the directory to import, or run [garbage collection](https://nix.dev/manual/nix/stable/command-ref/nix-collect-garbage).

## macOS update breaks Nix installation[#](https://nix.dev/guides/troubleshooting#macos-update-breaks-nix-installation "Link to this heading")

This is a [known issue](https://github.com/NixOS/nix/issues/3616).
The [Nix installer](https://nix.dev/manual/nix/latest/installation/installing-binary) modifies `/etc/zshrc`.
When macOS is updated, it will typically overwrite `/etc/zshrc` again.

As a workaround, add the following code snippet to the end of `/etc/zshrc` and restart the shell:

```
if [ -e '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh' ]; then
  . '/nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh'
fi
```

Contents