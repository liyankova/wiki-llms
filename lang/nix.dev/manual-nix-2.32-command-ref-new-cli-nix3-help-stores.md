---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores
title: nix help-stores - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix help-stores - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#name)

`nix help-stores` - show help about store types and their settings

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#synopsis)

`nix help-stores` [*option*...]

Nix supports different types of stores:

* [Dummy Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#dummy-store)
* [Experimental Local Overlay Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#experimental-local-overlay-store)
* [Experimental SSH Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#experimental-ssh-store)
* [Experimental SSH Store with filesystem mounted](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#experimental-ssh-store-with-filesystem-mounted)
* [HTTP Binary Cache Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#http-binary-cache-store)
* [Local Binary Cache Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-binary-cache-store)
* [Local Daemon Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-daemon-store)
* [Local Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-store)
* [S3 Binary Cache Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#s3-binary-cache-store)
* [SSH Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#ssh-store)

## [Store URL format](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-url-format)

Stores are specified using a URL-like syntax. For example, the command

```
# nix path-info --store https://cache.nixos.org/ --json \
  /nix/store/a7gvj343m05j2s32xcnwr35v31ynlypr-coreutils-9.1
```

fetches information about a store path in the HTTP binary cache
located at https://cache.nixos.org/, which is a type of store.

Store URLs can specify **store settings** using URL query strings,
i.e. by appending `?name1=value1&name2=value2&...` to the URL. For
instance,

```
--store ssh://machine.example.org?ssh-key=/path/to/my/key
```

tells Nix to access the store on a remote machine via the SSH
protocol, using `/path/to/my/key` as the SSH private key. The
supported settings for each store type are documented below.

The special store URL `auto` causes Nix to automatically select a
store as follows:

* Use the [local store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-store) `/nix/store` if `/nix/var/nix`
  is writable by the current user.
* Otherwise, if `/nix/var/nix/daemon-socket/socket` exists, [connect
  to the Nix daemon listening on that socket](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-daemon-store).
* Otherwise, on Linux only, use the [local chroot store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-store)
  `~/.local/share/nix/root`, which will be created automatically if it
  does not exist.
* Otherwise, use the [local store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-store) `/nix/store`.

# [Dummy Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#dummy-store)

**Store URL format**: `dummy://`

This store type represents a store in memory.
Store objects can be read and written, but only so long as the store is open.
Once the store is closed, all data will be discarded.

It's useful when you want to use the Nix evaluator when no actual Nix store exists, e.g.

```
# nix eval --store dummy:// --expr '1 + 2'
```

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings)

* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-dummy-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-dummy-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`read-only`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-dummy-store-read-only)

  Make any sort of write fail instead of succeeding.
  No additional memory will be used, because no information needs to be stored.

  **Default:** `true`
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-dummy-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-dummy-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-dummy-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-dummy-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`

# [Experimental Local Overlay Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#experimental-local-overlay-store)

> **Warning**
>
> This store is part of an
> [experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features).
>
> To use this store, make sure the
> [`local-overlay-store` experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-local-overlay-store)
> is enabled.
> For example, include the following in [`nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file):
>
> ```
> extra-experimental-features = local-overlay-store
> ```

**Store URL format**: `local-overlay`

This store type is a variation of the [local store] designed to leverage Linux's [Overlay Filesystem](https://docs.kernel.org/filesystems/overlayfs.html) (OverlayFS for short).
Just as OverlayFS combines a lower and upper filesystem by treating the upper one as a patch against the lower, the local overlay store combines a lower store with an upper almost-[local store].
("almost" because while the upper filesystems for OverlayFS is valid on its own, the upper almost-store is not a valid local store on its own because some references will dangle.)
To use this store, you will first need to configure an OverlayFS mountpoint [appropriately](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#example-filesystem-layout) as Nix will not do this for you (though it will verify the mountpoint is configured correctly).

### [Conceptual parts of a local overlay store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#conceptual-parts-of-a-local-overlay-store)

*This is a more abstract/conceptual description of the parts of a layered store, an authoritative reference.
For more "practical" instructions, see the worked-out example in the next subsection.*

The parts of a local overlay store are as follows:

* **Lower store**:

  > Specified with the [`lower-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-lower-store) setting.

  This is any store implementation that includes a store directory as part of the native operating system filesystem.
  For example, this could be a [local store], [local daemon store], or even another local overlay store.

  The local overlay store never tries to modify the lower store in any way.
  Something else could modify the lower store, but there are restrictions on this
  Nix itself requires that this store only grow, and not change in other ways.
  For example, new store objects can be added, but deleting or modifying store objects is not allowed in general, because that will confuse and corrupt any local overlay store using those objects.
  (In addition, the underlying filesystem overlay mechanism may impose additional restrictions, see below.)

  The lower store must not change while it is mounted as part of an overlay store.
  To ensure it does not, you might want to mount the store directory read-only (which then requires the [read-only] parameter to be set to `true`).

  + **Lower store directory**:

    > Specified with `lower-store.real` setting.

    This is the directory used/exposed by the lower store.

    As specified above, Nix requires the local store can only grow not change in other ways.
    Linux's OverlayFS in addition imposes the further requirement that this directory cannot change at all.
    That means that, while any local overlay store exists that is using this store as a lower store, this directory must not change.
  + **Lower metadata source**:

    > Not directly specified.
    > A consequence of the `lower-store` setting, depending on the type of lower store chosen.

    This is abstract, just some way to read the metadata of lower store [store objects](https://nix.dev/manual/nix/2.32/store/store-object).
    For example it could be a SQLite database (for the [local store]), or a socket connection (for the [local daemon store]).

    This need not be writable.
    As stated above a local overlay store never tries to modify its lower store.
    The lower store's metadata is considered part of the lower store, just as the store's [file system objects](https://nix.dev/manual/nix/2.32/store/file-system-object) that appear in the store directory are.
* **Upper almost-store**:

  > Not directly specified.
  > Instead the constituent parts are independently specified as described below.

  This is almost but not quite just a [local store].
  That is because taken in isolation, not as part of a local overlay store, by itself, it would appear corrupted.
  But combined with everything else as part of an overlay local store, it is valid.

  + **Upper layer directory**:

    > Specified with [`upper-layer`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-upper-layer) setting.

    This contains additional [store objects](https://nix.dev/manual/nix/2.32/store/store-object)
    (or, strictly speaking, their [file system objects](https://nix.dev/manual/nix/2.32/store/file-system-object) that the local overlay store will extend the lower store with).
  + **Upper store directory**:

    > Specified with the [`real`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-real) setting.
    > This the same as the base local store setting, and can also be indirectly specified with the [`root`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-root) setting.

    This contains all the store objects from each of the two directories.

    The lower store directory and upper layer directory are combined via OverlayFS to create this directory.
    Nix doesn't do this itself, because it typically wouldn't have the permissions to do so, so it is the responsibility of the user to set this up first.
    Nix can, however, optionally check that the OverlayFS mount settings appear as expected, matching Nix's own settings.
  + **Upper SQLite database**:

    > Not directly specified.
    > The location of the database instead depends on the [`state`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-state) setting.
    > It is always `${state}/db`.

    This contains the metadata of all of the upper layer [store objects](https://nix.dev/manual/nix/2.32/store/store-object) (everything beyond their file system objects), and also duplicate copies of some lower layer store object's metadata.
    The duplication is so the metadata for the [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure) of upper layer [store objects](https://nix.dev/manual/nix/2.32/store/store-object) can be found entirely within the upper layer.
    (This allows us to use the same SQL Schema as the [local store]'s SQLite database, as foreign keys in that schema enforce closure metadata to be self-contained in this way.)

### [Example filesystem layout](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#example-filesystem-layout)

Here is a worked out example of usage, following the concepts in the previous section.

Say we have the following paths:

* `/mnt/example/merged-store/nix/store`
* `/mnt/example/store-a/nix/store`
* `/mnt/example/store-b`

Then the following store URI can be used to access a local-overlay store at `/mnt/example/merged-store`:

```
local-overlay://?root=/mnt/example/merged-store&lower-store=/mnt/example/store-a&upper-layer=/mnt/example/store-b
```

The lower store directory is located at `/mnt/example/store-a/nix/store`, while the upper layer is at `/mnt/example/store-b`.

Before accessing the overlay store you will need to ensure the OverlayFS mount is set up correctly:

```
mount -t overlay overlay \
  -o lowerdir="/mnt/example/store-a/nix/store" \
  -o upperdir="/mnt/example/store-b" \
  -o workdir="/mnt/example/workdir" \
  "/mnt/example/merged-store/nix/store"
```

Note that OverlayFS requires `/mnt/example/workdir` to be on the same volume as the `upperdir`.

By default, Nix will check that the mountpoint as been set up correctly and fail with an error if it has not.
You can override this behaviour by passing [`check-mount=false`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-check-mount) if you need to.

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-1)

* [`build-dir`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-build-dir)

  The directory on the host, in which derivations' temporary build directories are created.

  If not set, Nix will use the `builds` subdirectory of its configured state directory.

  Note that builds are often performed by the Nix daemon, so its `build-dir` applies.

  Nix will create this directory automatically with suitable permissions if it does not exist.
  Otherwise its permissions must allow all users to traverse the directory (i.e. it must have `o+x` set, in unix parlance) for non-sandboxed builds to work correctly.

  This is also the location where [`--keep-failed`](https://nix.dev/manual/nix/2.32/command-ref/opt-common#opt-keep-failed) leaves its files.

  If Nix runs without sandbox, or if the platform does not support sandboxing with bind mounts (e.g. macOS), then the [`builder`](https://nix.dev/manual/nix/2.32/language/derivations#attr-builder)'s environment will contain this directory, instead of the virtual location [`sandbox-build-dir`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#conf-sandbox-build-dir).

  > **Warning**
  >
  > `build-dir` must not be set to a world-writable directory.
  > Placing temporary build directories in a world-writable place allows other users to access or modify build data that is currently in use.
  > This alone is merely an impurity, but combined with another factor this has allowed malicious derivations to escape the build sandbox.

  **Default:** ``
* [`check-mount`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-check-mount)

  Check that the overlay filesystem is correctly mounted.

  Nix does not manage the overlayfs mount point itself, but the correct
  functioning of the overlay store does depend on this mount point being set up
  correctly. Rather than just assume this is the case, check that the lowerdir
  and upperdir options are what we expect them to be. This check is on by
  default, but can be disabled if needed.

  **Default:** `true`
* [`log`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-log)

  directory where Nix stores log files.

  **Default:** `/nix/var/log/nix`
* [`lower-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-lower-store)

  [Store URL](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-url-format)
  for the lower store. The default is `auto` (i.e. use the Nix daemon or `/nix/store` directly).

  Must be a store with a store dir on the file system.
  Must be used as OverlayFS lower layer for this store's store dir.

  **Default:** *empty*
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`read-only`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-read-only)

  Allow this store to be opened when its [database](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-database) is on a read-only filesystem.

  Normally Nix attempts to open the store database in read-write mode, even for querying (when write access is not needed), causing it to fail if the database is on a read-only filesystem.

  Enable read-only mode to disable locking and open the SQLite database with the [`immutable` parameter](https://www.sqlite.org/c3ref/open.html) set.

  > **Warning**
  > Do not use this unless the filesystem is read-only.
  >
  > Using it when the filesystem is writable can cause incorrect query results or corruption errors if the database is changed by another process.
  > While the filesystem the database resides on might appear to be read-only, consider whether another user or system might have write access to it.

  **Default:** `false`
* [`real`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-real)

  Physical path of the Nix store.

  **Default:** `/nix/store`
* [`remount-hook`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-remount-hook)

  Script or other executable to run when overlay filesystem needs remounting.

  This is occasionally necessary when deleting a store path that exists in both upper and lower layers.
  In such a situation, bypassing OverlayFS and deleting the path in the upper layer directly
  is the only way to perform the deletion without creating a "whiteout".
  However this causes the OverlayFS kernel data structures to get out-of-sync,
  and can lead to 'stale file handle' errors; remounting solves the problem.

  The store directory is passed as an argument to the invoked executable.

  **Default:** *empty*
* [`require-sigs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-require-sigs)

  Whether store paths copied into this store should have a trusted signature.

  **Default:** `true`
* [`root`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-root)

  Directory prefixed to all other paths.

  **Default:** ``
* [`state`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-state)

  Directory where Nix stores state.

  **Default:** `/dummy`
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`upper-layer`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-upper-layer)

  Directory containing the OverlayFS upper layer for this store's store dir.

  **Default:** *empty*
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-local-overlay-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`

# [Experimental SSH Store with filesystem mounted](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#experimental-ssh-store-with-filesystem-mounted)

> **Warning**
>
> This store is part of an
> [experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features).
>
> To use this store, make sure the
> [`mounted-ssh-store` experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-mounted-ssh-store)
> is enabled.
> For example, include the following in [`nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file):
>
> ```
> extra-experimental-features = mounted-ssh-store
> ```

**Store URL format**: `mounted-ssh-ng://[username@]hostname`

Experimental store type that allows full access to a Nix store on a remote machine,
and additionally requires that store be mounted in the local file system.

The mounting of that store is not managed by Nix, and must by managed manually.
It could be accomplished with SSHFS or NFS, for example.

The local file system is used to optimize certain operations.
For example, rather than serializing Nix archives and sending over the Nix channel,
we can directly access the file system data via the mount-point.

The local file system is also used to make certain operations possible that wouldn't otherwise be.
For example, persistent GC roots can be created if they reside on the same file system as the remote store:
the remote side will create the symlinks necessary to avoid race conditions.

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-2)

* [`base64-ssh-public-host-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-base64-ssh-public-host-key)

  The public host key of the remote machine.

  **Default:** *empty*
* [`compress`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-compress)

  Whether to enable SSH compression.

  **Default:** `false`
* [`log`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-log)

  directory where Nix stores log files.

  **Default:** `/nix/var/log/nix`
* [`max-connection-age`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-max-connection-age)

  Maximum age of a connection before it is closed.

  **Default:** `4294967295`
* [`max-connections`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-max-connections)

  Maximum number of concurrent connections to the Nix daemon.

  **Default:** `1`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`real`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-real)

  Physical path of the Nix store.

  **Default:** `/nix/store`
* [`remote-program`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-remote-program)

  Path to the `nix-daemon` executable on the remote machine.

  **Default:** `nix-daemon`
* [`remote-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-remote-store)

  [Store URL](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to be used on the remote machine. The default is `auto`
  (i.e. use the Nix daemon or `/nix/store` directly).

  **Default:** *empty*
* [`root`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-root)

  Directory prefixed to all other paths.

  **Default:** ``
* [`ssh-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-ssh-key)

  Path to the SSH private key used to authenticate to the remote machine.

  **Default:** *empty*
* [`state`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-state)

  Directory where Nix stores state.

  **Default:** `/dummy`
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-with-filesystem-mounted-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`

# [Experimental SSH Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#experimental-ssh-store)

**Store URL format**: `ssh-ng://[username@]hostname[:port]`

Experimental store type that allows full access to a Nix store on a
remote machine.

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-3)

* [`base64-ssh-public-host-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-base64-ssh-public-host-key)

  The public host key of the remote machine.

  **Default:** *empty*
* [`compress`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-compress)

  Whether to enable SSH compression.

  **Default:** `false`
* [`max-connection-age`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-max-connection-age)

  Maximum age of a connection before it is closed.

  **Default:** `4294967295`
* [`max-connections`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-max-connections)

  Maximum number of concurrent connections to the Nix daemon.

  **Default:** `1`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`remote-program`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-remote-program)

  Path to the `nix-daemon` executable on the remote machine.

  **Default:** `nix-daemon`
* [`remote-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-remote-store)

  [Store URL](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to be used on the remote machine. The default is `auto`
  (i.e. use the Nix daemon or `/nix/store` directly).

  **Default:** *empty*
* [`ssh-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-ssh-key)

  Path to the SSH private key used to authenticate to the remote machine.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-experimental-ssh-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`

# [HTTP Binary Cache Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#http-binary-cache-store)

**Store URL format**: `http://...`, `https://...`

This store allows a binary cache to be accessed via the HTTP
protocol.

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-4)

* [`compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-compression)

  NAR compression method (`xz`, `bzip2`, `gzip`, `zstd`, or `none`).

  **Default:** `xz`
* [`compression-level`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-compression-level)

  The *preset level* to be used when compressing NARs.
  The meaning and accepted values depend on the compression method selected.
  `-1` specifies that the default compression level should be used.

  **Default:** `-1`
* [`index-debug-info`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-index-debug-info)

  Whether to index DWARF debug info files by build ID. This allows [`dwarffs`](https://github.com/edolstra/dwarffs) to
  fetch debug info on demand

  **Default:** `false`
* [`local-nar-cache`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-local-nar-cache)

  Path to a local cache of NARs fetched from this binary cache, used by commands such as `nix store cat`.

  **Default:** *empty*
* [`log-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-log-compression)

  Compression method for `log/*` files. It is recommended to
  use a compression method supported by most web browsers
  (e.g. `brotli`).

  **Default:** *empty*
* [`ls-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-ls-compression)

  Compression method for `.ls` files.

  **Default:** *empty*
* [`narinfo-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-narinfo-compression)

  Compression method for `.narinfo` files.

  **Default:** *empty*
* [`parallel-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-parallel-compression)

  Enable multi-threaded compression of NARs. This is currently only available for `xz` and `zstd`.

  **Default:** `false`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`secret-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-secret-key)

  Path to the secret key used to sign the binary cache.

  **Default:** *empty*
* [`secret-keys`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-secret-keys)

  List of comma-separated paths to the secret keys used to sign the binary cache.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`
* [`write-nar-listing`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-http-binary-cache-store-write-nar-listing)

  Whether to write a JSON file that lists the files in each NAR.

  **Default:** `false`

# [Local Binary Cache Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-binary-cache-store)

**Store URL format**: `file://`*path*

This store allows reading and writing a binary cache stored in *path*
in the local filesystem. If *path* does not exist, it will be created.

For example, the following builds or downloads `nixpkgs#hello` into
the local store and then copies it to the binary cache in
`/tmp/binary-cache`:

```
# nix copy --to file:///tmp/binary-cache nixpkgs#hello
```

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-5)

* [`compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-compression)

  NAR compression method (`xz`, `bzip2`, `gzip`, `zstd`, or `none`).

  **Default:** `xz`
* [`compression-level`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-compression-level)

  The *preset level* to be used when compressing NARs.
  The meaning and accepted values depend on the compression method selected.
  `-1` specifies that the default compression level should be used.

  **Default:** `-1`
* [`index-debug-info`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-index-debug-info)

  Whether to index DWARF debug info files by build ID. This allows [`dwarffs`](https://github.com/edolstra/dwarffs) to
  fetch debug info on demand

  **Default:** `false`
* [`local-nar-cache`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-local-nar-cache)

  Path to a local cache of NARs fetched from this binary cache, used by commands such as `nix store cat`.

  **Default:** *empty*
* [`parallel-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-parallel-compression)

  Enable multi-threaded compression of NARs. This is currently only available for `xz` and `zstd`.

  **Default:** `false`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`secret-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-secret-key)

  Path to the secret key used to sign the binary cache.

  **Default:** *empty*
* [`secret-keys`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-secret-keys)

  List of comma-separated paths to the secret keys used to sign the binary cache.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`
* [`write-nar-listing`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-binary-cache-store-write-nar-listing)

  Whether to write a JSON file that lists the files in each NAR.

  **Default:** `false`

# [Local Daemon Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-daemon-store)

**Store URL format**: `daemon`, `unix://`*path*

This store type accesses a Nix store by talking to a Nix daemon
listening on the Unix domain socket *path*. The store pseudo-URL
`daemon` is equivalent to `unix:///nix/var/nix/daemon-socket/socket`.

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-6)

* [`log`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-log)

  directory where Nix stores log files.

  **Default:** `/nix/var/log/nix`
* [`max-connection-age`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-max-connection-age)

  Maximum age of a connection before it is closed.

  **Default:** `4294967295`
* [`max-connections`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-max-connections)

  Maximum number of concurrent connections to the Nix daemon.

  **Default:** `1`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`real`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-real)

  Physical path of the Nix store.

  **Default:** `/nix/store`
* [`root`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-root)

  Directory prefixed to all other paths.

  **Default:** ``
* [`state`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-state)

  Directory where Nix stores state.

  **Default:** `/dummy`
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-daemon-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`

# [Local Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#local-store)

**Store URL format**: `local`, *root*

This store type accesses a Nix store in the local filesystem directly
(i.e. not via the Nix daemon). *root* is an absolute path that is
prefixed to other directories such as the Nix store directory. The
store pseudo-URL `local` denotes a store that uses `/` as its root
directory.

A store that uses a *root* other than `/` is called a *chroot
store*. With such stores, the store directory is "logically" still
`/nix/store`, so programs stored in them can only be built and
executed by `chroot`-ing into *root*. Chroot stores only support
building and running on Linux when [`mount namespaces`](https://man7.org/linux/man-pages/man7/mount_namespaces.7.html) and [`user namespaces`](https://man7.org/linux/man-pages/man7/user_namespaces.7.html) are
enabled.

For example, the following uses `/tmp/root` as the chroot environment
to build or download `nixpkgs#hello` and then execute it:

```
# nix run --store /tmp/root nixpkgs#hello
Hello, world!
```

Here, the "physical" store location is `/tmp/root/nix/store`, and
Nix's store metadata is in `/tmp/root/nix/var/nix/db`.

It is also possible, but not recommended, to change the "logical"
location of the Nix store from its default of `/nix/store`. This makes
it impossible to use default substituters such as
`https://cache.nixos.org/`, and thus you may have to build everything
locally. Here is an example:

```
# nix build --store 'local?store=/tmp/my-nix/store&state=/tmp/my-nix/state&log=/tmp/my-nix/log' nixpkgs#hello
```

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-7)

* [`build-dir`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-build-dir)

  The directory on the host, in which derivations' temporary build directories are created.

  If not set, Nix will use the `builds` subdirectory of its configured state directory.

  Note that builds are often performed by the Nix daemon, so its `build-dir` applies.

  Nix will create this directory automatically with suitable permissions if it does not exist.
  Otherwise its permissions must allow all users to traverse the directory (i.e. it must have `o+x` set, in unix parlance) for non-sandboxed builds to work correctly.

  This is also the location where [`--keep-failed`](https://nix.dev/manual/nix/2.32/command-ref/opt-common#opt-keep-failed) leaves its files.

  If Nix runs without sandbox, or if the platform does not support sandboxing with bind mounts (e.g. macOS), then the [`builder`](https://nix.dev/manual/nix/2.32/language/derivations#attr-builder)'s environment will contain this directory, instead of the virtual location [`sandbox-build-dir`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#conf-sandbox-build-dir).

  > **Warning**
  >
  > `build-dir` must not be set to a world-writable directory.
  > Placing temporary build directories in a world-writable place allows other users to access or modify build data that is currently in use.
  > This alone is merely an impurity, but combined with another factor this has allowed malicious derivations to escape the build sandbox.

  **Default:** ``
* [`log`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-log)

  directory where Nix stores log files.

  **Default:** `/nix/var/log/nix`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`read-only`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-read-only)

  Allow this store to be opened when its [database](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-database) is on a read-only filesystem.

  Normally Nix attempts to open the store database in read-write mode, even for querying (when write access is not needed), causing it to fail if the database is on a read-only filesystem.

  Enable read-only mode to disable locking and open the SQLite database with the [`immutable` parameter](https://www.sqlite.org/c3ref/open.html) set.

  > **Warning**
  > Do not use this unless the filesystem is read-only.
  >
  > Using it when the filesystem is writable can cause incorrect query results or corruption errors if the database is changed by another process.
  > While the filesystem the database resides on might appear to be read-only, consider whether another user or system might have write access to it.

  **Default:** `false`
* [`real`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-real)

  Physical path of the Nix store.

  **Default:** `/nix/store`
* [`require-sigs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-require-sigs)

  Whether store paths copied into this store should have a trusted signature.

  **Default:** `true`
* [`root`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-root)

  Directory prefixed to all other paths.

  **Default:** ``
* [`state`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-state)

  Directory where Nix stores state.

  **Default:** `/dummy`
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-local-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`

# [S3 Binary Cache Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#s3-binary-cache-store)

**Store URL format**: `s3://`*bucket-name*

This store allows reading and writing a binary cache stored in an AWS S3 (or S3-compatible service) bucket.
This store shares many idioms with the [HTTP Binary Cache Store](https://nix.dev/manual/nix/2.32/store/types/http-binary-cache-store).

For AWS S3, the binary cache URL for a bucket named `example-nix-cache` will be exactly <s3://example-nix-cache>.
For S3 compatible binary caches, consult that cache's documentation.

### [Anonymous reads to your S3-compatible binary cache](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#anonymous-reads-to-your-s3-compatible-binary-cache)

> If your binary cache is publicly accessible and does not require authentication,
> it is simplest to use the [HTTP Binary Cache Store] rather than S3 Binary Cache Store with
> <https://example-nix-cache.s3.amazonaws.com> instead of <s3://example-nix-cache>.

Your bucket will need a
[bucket policy](https://docs.aws.amazon.com/AmazonS3/v1/userguide/bucket-policies.html)
like the following to be accessible:

```
{
    "Id": "DirectReads",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowDirectReads",
            "Action": [
                "s3:GetObject",
                "s3:GetBucketLocation"
            ],
            "Effect": "Allow",
            "Resource": [
                "arn:aws:s3:::example-nix-cache",
                "arn:aws:s3:::example-nix-cache/*"
            ],
            "Principal": "*"
        }
    ]
}
```

### [Authentication](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#authentication)

Nix will use the
[default credential provider chain](https://docs.aws.amazon.com/sdk-for-cpp/v1/developer-guide/credentials.html)
for authenticating requests to Amazon S3.

Note that this means Nix will read environment variables and files with different idioms than with Nix's own settings, as implemented by the AWS SDK.
Consult the documentation linked above for further details.

### [Authenticated reads to your S3 binary cache](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#authenticated-reads-to-your-s3-binary-cache)

Your bucket will need a bucket policy allowing the desired users to perform the `s3:GetObject` and `s3:GetBucketLocation` action on all objects in the bucket.
The [anonymous policy given above](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#anonymous-reads-to-your-s3-compatible-binary-cache) can be updated to have a restricted `Principal` to support this.

### [Authenticated writes to your S3-compatible binary cache](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#authenticated-writes-to-your-s3-compatible-binary-cache)

Your account will need an IAM policy to support uploading to the bucket:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "UploadToCache",
      "Effect": "Allow",
      "Action": [
        "s3:AbortMultipartUpload",
        "s3:GetBucketLocation",
        "s3:GetObject",
        "s3:ListBucket",
        "s3:ListBucketMultipartUploads",
        "s3:ListMultipartUploadParts",
        "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:s3:::example-nix-cache",
        "arn:aws:s3:::example-nix-cache/*"
      ]
    }
  ]
}
```

### [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#examples)

With bucket policies and authentication set up as described above, uploading works via [`nix copy`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy) (experimental).

* To upload with a specific credential profile for Amazon S3:

  ```
  $ nix copy nixpkgs.hello \
    --to 's3://example-nix-cache?profile=cache-upload&region=eu-west-2'
  ```
* To upload to an S3-compatible binary cache:

  ```
  $ nix copy nixpkgs.hello --to \
    's3://example-nix-cache?profile=cache-upload&scheme=https&endpoint=minio.example.com'
  ```

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-8)

* [`buffer-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-buffer-size)

  Size (in bytes) of each part in multi-part uploads.

  **Default:** `5242880`
* [`compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-compression)

  NAR compression method (`xz`, `bzip2`, `gzip`, `zstd`, or `none`).

  **Default:** `xz`
* [`compression-level`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-compression-level)

  The *preset level* to be used when compressing NARs.
  The meaning and accepted values depend on the compression method selected.
  `-1` specifies that the default compression level should be used.

  **Default:** `-1`
* [`endpoint`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-endpoint)

  The URL of the endpoint of an S3-compatible service such as MinIO.
  Do not specify this setting if you're using Amazon S3.

  > **Note**
  >
  > This endpoint must support HTTPS and uses path-based
  > addressing instead of virtual host based addressing.

  **Default:** *empty*
* [`index-debug-info`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-index-debug-info)

  Whether to index DWARF debug info files by build ID. This allows [`dwarffs`](https://github.com/edolstra/dwarffs) to
  fetch debug info on demand

  **Default:** `false`
* [`local-nar-cache`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-local-nar-cache)

  Path to a local cache of NARs fetched from this binary cache, used by commands such as `nix store cat`.

  **Default:** *empty*
* [`log-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-log-compression)

  Compression method for `log/*` files. It is recommended to
  use a compression method supported by most web browsers
  (e.g. `brotli`).

  **Default:** *empty*
* [`ls-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-ls-compression)

  Compression method for `.ls` files.

  **Default:** *empty*
* [`multipart-upload`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-multipart-upload)

  Whether to use multi-part uploads.

  **Default:** `false`
* [`narinfo-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-narinfo-compression)

  Compression method for `.narinfo` files.

  **Default:** *empty*
* [`parallel-compression`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-parallel-compression)

  Enable multi-threaded compression of NARs. This is currently only available for `xz` and `zstd`.

  **Default:** `false`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-profile)

  The name of the AWS configuration profile to use. By default
  Nix uses the `default` profile.

  **Default:** *empty*
* [`region`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-region)

  The region of the S3 bucket. If your bucket is not in
  `us-east-1`, you should always explicitly specify the region
  parameter.

  **Default:** `us-east-1`
* [`scheme`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-scheme)

  The scheme used for S3 requests, `https` (default) or `http`. This
  option allows you to disable HTTPS for binary caches which don't
  support it.

  > **Note**
  >
  > HTTPS should be used if the cache might contain sensitive
  > information.

  **Default:** *empty*
* [`secret-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-secret-key)

  Path to the secret key used to sign the binary cache.

  **Default:** *empty*
* [`secret-keys`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-secret-keys)

  List of comma-separated paths to the secret keys used to sign the binary cache.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`
* [`write-nar-listing`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-s3-binary-cache-store-write-nar-listing)

  Whether to write a JSON file that lists the files in each NAR.

  **Default:** `false`

# [SSH Store](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#ssh-store)

**Store URL format**: `ssh://[username@]hostname[:port]`

This store type allows limited access to a remote store on another
machine via SSH.

## [Settings](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#settings-9)

* [`base64-ssh-public-host-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-base64-ssh-public-host-key)

  The public host key of the remote machine.

  **Default:** *empty*
* [`compress`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-compress)

  Whether to enable SSH compression.

  **Default:** `false`
* [`log-fd`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-log-fd)

  file descriptor to which SSH's stderr is connected

  **Default:** `-1`
* [`max-connections`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-max-connections)

  Maximum number of concurrent SSH connections.

  **Default:** `1`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`remote-program`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-remote-program)

  Path to the `nix-store` executable on the remote machine.

  **Default:** `nix-store`
* [`remote-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-remote-store)

  [Store URL](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to be used on the remote machine. The default is `auto`
  (i.e. use the Nix daemon or `/nix/store` directly).

  **Default:** *empty*
* [`ssh-key`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-ssh-key)

  Path to the SSH private key used to authenticate to the remote machine.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-ssh-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.