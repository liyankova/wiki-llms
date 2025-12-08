---
url: https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store
title: Experimental Local Overlay Store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Experimental Local Overlay Store - Nix 2.32.2 Reference Manual

# [Experimental Local Overlay Store](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#experimental-local-overlay-store)

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
To use this store, you will first need to configure an OverlayFS mountpoint [appropriately](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#example-filesystem-layout) as Nix will not do this for you (though it will verify the mountpoint is configured correctly).

### [Conceptual parts of a local overlay store](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#conceptual-parts-of-a-local-overlay-store)

*This is a more abstract/conceptual description of the parts of a layered store, an authoritative reference.
For more "practical" instructions, see the worked-out example in the next subsection.*

The parts of a local overlay store are as follows:

* **Lower store**:

  > Specified with the [`lower-store`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-lower-store) setting.

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

    > Specified with [`upper-layer`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-upper-layer) setting.

    This contains additional [store objects](https://nix.dev/manual/nix/2.32/store/store-object)
    (or, strictly speaking, their [file system objects](https://nix.dev/manual/nix/2.32/store/file-system-object) that the local overlay store will extend the lower store with).
  + **Upper store directory**:

    > Specified with the [`real`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-real) setting.
    > This the same as the base local store setting, and can also be indirectly specified with the [`root`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-root) setting.

    This contains all the store objects from each of the two directories.

    The lower store directory and upper layer directory are combined via OverlayFS to create this directory.
    Nix doesn't do this itself, because it typically wouldn't have the permissions to do so, so it is the responsibility of the user to set this up first.
    Nix can, however, optionally check that the OverlayFS mount settings appear as expected, matching Nix's own settings.
  + **Upper SQLite database**:

    > Not directly specified.
    > The location of the database instead depends on the [`state`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-state) setting.
    > It is always `${state}/db`.

    This contains the metadata of all of the upper layer [store objects](https://nix.dev/manual/nix/2.32/store/store-object) (everything beyond their file system objects), and also duplicate copies of some lower layer store object's metadata.
    The duplication is so the metadata for the [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure) of upper layer [store objects](https://nix.dev/manual/nix/2.32/store/store-object) can be found entirely within the upper layer.
    (This allows us to use the same SQL Schema as the [local store]'s SQLite database, as foreign keys in that schema enforce closure metadata to be self-contained in this way.)

### [Example filesystem layout](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#example-filesystem-layout)

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
You can override this behaviour by passing [`check-mount=false`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-check-mount) if you need to.

## [Settings](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#settings)

* [`build-dir`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-build-dir)

  The directory on the host, in which derivations' temporary build directories are created.

  If not set, Nix will use the `builds` subdirectory of its configured state directory.

  Note that builds are often performed by the Nix daemon, so its `build-dir` applies.

  Nix will create this directory automatically with suitable permissions if it does not exist.
  Otherwise its permissions must allow all users to traverse the directory (i.e. it must have `o+x` set, in unix parlance) for non-sandboxed builds to work correctly.

  This is also the location where [`--keep-failed`](https://nix.dev/manual/nix/2.32/command-ref/opt-common#opt-keep-failed) leaves its files.

  If Nix runs without sandbox, or if the platform does not support sandboxing with bind mounts (e.g. macOS), then the [`builder`](https://nix.dev/manual/nix/2.32/language/derivations#attr-builder)'s environment will contain this directory, instead of the virtual location [`sandbox-build-dir`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#conf-sandbox-build-dir).

  > **Warning**
  >
  > `build-dir` must not be set to a world-writable directory.
  > Placing temporary build directories in a world-writable place allows other users to access or modify build data that is currently in use.
  > This alone is merely an impurity, but combined with another factor this has allowed malicious derivations to escape the build sandbox.

  **Default:** ``
* [`check-mount`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-check-mount)

  Check that the overlay filesystem is correctly mounted.

  Nix does not manage the overlayfs mount point itself, but the correct
  functioning of the overlay store does depend on this mount point being set up
  correctly. Rather than just assume this is the case, check that the lowerdir
  and upperdir options are what we expect them to be. This check is on by
  default, but can be disabled if needed.

  **Default:** `true`
* [`log`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-log)

  directory where Nix stores log files.

  **Default:** `/nix/var/log/nix`
* [`lower-store`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-lower-store)

  [Store URL](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-help-stores#store-url-format)
  for the lower store. The default is `auto` (i.e. use the Nix daemon or `/nix/store` directly).

  Must be a store with a store dir on the file system.
  Must be used as OverlayFS lower layer for this store's store dir.

  **Default:** *empty*
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`read-only`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-read-only)

  Allow this store to be opened when its [database](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-database) is on a read-only filesystem.

  Normally Nix attempts to open the store database in read-write mode, even for querying (when write access is not needed), causing it to fail if the database is on a read-only filesystem.

  Enable read-only mode to disable locking and open the SQLite database with the [`immutable` parameter](https://www.sqlite.org/c3ref/open.html) set.

  > **Warning**
  > Do not use this unless the filesystem is read-only.
  >
  > Using it when the filesystem is writable can cause incorrect query results or corruption errors if the database is changed by another process.
  > While the filesystem the database resides on might appear to be read-only, consider whether another user or system might have write access to it.

  **Default:** `false`
* [`real`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-real)

  Physical path of the Nix store.

  **Default:** `/nix/store`
* [`remount-hook`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-remount-hook)

  Script or other executable to run when overlay filesystem needs remounting.

  This is occasionally necessary when deleting a store path that exists in both upper and lower layers.
  In such a situation, bypassing OverlayFS and deleting the path in the upper layer directly
  is the only way to perform the deletion without creating a "whiteout".
  However this causes the OverlayFS kernel data structures to get out-of-sync,
  and can lead to 'stale file handle' errors; remounting solves the problem.

  The store directory is passed as an argument to the invoked executable.

  **Default:** *empty*
* [`require-sigs`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-require-sigs)

  Whether store paths copied into this store should have a trusted signature.

  **Default:** `true`
* [`root`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-root)

  Directory prefixed to all other paths.

  **Default:** ``
* [`state`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-state)

  Directory where Nix stores state.

  **Default:** `/dummy`
* [`store`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`upper-layer`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-upper-layer)

  Directory containing the OverlayFS upper layer for this store's store dir.

  **Default:** *empty*
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/store/types/experimental-local-overlay-store#store-experimental-local-overlay-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`