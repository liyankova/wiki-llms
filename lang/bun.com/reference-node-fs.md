---
url: https://bun.com/reference/node/fs
title: Node.js fs module | API Reference | Bun
source_domain: bun.com
---

# Node.js fs module | API Reference | Bun

Node.js module

# [fs](https://bun.com/reference/node/fs)

The `'node:fs'` module provides file system I/O operations, including reading, writing, renaming, and deleting files and directories. It offers both synchronous and asynchronous methods.

Works in Bun

Fully implemented. 92% of Node.js's test suite passes.

* ### namespace [constants](https://bun.com/reference/node/fs/constants)

  + const [COPYFILE\_EXCL](https://bun.com/reference/node/fs/constants/COPYFILE_EXCL): number

    Constant for fs.copyFile. Flag indicating the destination file should not be overwritten if it already exists.
  + const [COPYFILE\_FICLONE](https://bun.com/reference/node/fs/constants/COPYFILE_FICLONE): number

    Constant for fs.copyFile. copy operation will attempt to create a copy-on-write reflink. If the underlying platform does not support copy-on-write, then a fallback copy mechanism is used.
  + const [COPYFILE\_FICLONE\_FORCE](https://bun.com/reference/node/fs/constants/COPYFILE_FICLONE_FORCE): number

    Constant for fs.copyFile. Copy operation will attempt to create a copy-on-write reflink. If the underlying platform does not support copy-on-write, then the operation will fail with an error.
  + const [F\_OK](https://bun.com/reference/node/fs/constants/F_OK): number

    Constant for fs.access(). File is visible to the calling process.
  + const [O\_APPEND](https://bun.com/reference/node/fs/constants/O_APPEND): number

    Constant for fs.open(). Flag indicating that data will be appended to the end of the file.
  + const [O\_CREAT](https://bun.com/reference/node/fs/constants/O_CREAT): number

    Constant for fs.open(). Flag indicating to create the file if it does not already exist.
  + const [O\_DIRECT](https://bun.com/reference/node/fs/constants/O_DIRECT): number

    Constant for fs.open(). When set, an attempt will be made to minimize caching effects of file I/O.
  + const [O\_DIRECTORY](https://bun.com/reference/node/fs/constants/O_DIRECTORY): number

    Constant for fs.open(). Flag indicating that the open should fail if the path is not a directory.
  + const [O\_DSYNC](https://bun.com/reference/node/fs/constants/O_DSYNC): number

    Constant for fs.open(). Flag indicating that the file is opened for synchronous I/O with write operations waiting for data integrity.
  + const [O\_EXCL](https://bun.com/reference/node/fs/constants/O_EXCL): number

    Constant for fs.open(). Flag indicating that opening a file should fail if the O\_CREAT flag is set and the file already exists.
  + const [O\_NOATIME](https://bun.com/reference/node/fs/constants/O_NOATIME): number

    constant for fs.open(). Flag indicating reading accesses to the file system will no longer result in an update to the atime information associated with the file. This flag is available on Linux operating systems only.
  + const [O\_NOCTTY](https://bun.com/reference/node/fs/constants/O_NOCTTY): number

    Constant for fs.open(). Flag indicating that if path identifies a terminal device, opening the path shall not cause that terminal to become the controlling terminal for the process (if the process does not already have one).
  + const [O\_NOFOLLOW](https://bun.com/reference/node/fs/constants/O_NOFOLLOW): number

    Constant for fs.open(). Flag indicating that the open should fail if the path is a symbolic link.
  + const [O\_NONBLOCK](https://bun.com/reference/node/fs/constants/O_NONBLOCK): number

    Constant for fs.open(). Flag indicating to open the file in nonblocking mode when possible.
  + const [O\_RDONLY](https://bun.com/reference/node/fs/constants/O_RDONLY): number

    Constant for fs.open(). Flag indicating to open a file for read-only access.
  + const [O\_RDWR](https://bun.com/reference/node/fs/constants/O_RDWR): number

    Constant for fs.open(). Flag indicating to open a file for read-write access.
  + const [O\_SYMLINK](https://bun.com/reference/node/fs/constants/O_SYMLINK): number

    Constant for fs.open(). Flag indicating to open the symbolic link itself rather than the resource it is pointing to.
  + const [O\_SYNC](https://bun.com/reference/node/fs/constants/O_SYNC): number

    Constant for fs.open(). Flag indicating that the file is opened for synchronous I/O.
  + const [O\_TRUNC](https://bun.com/reference/node/fs/constants/O_TRUNC): number

    Constant for fs.open(). Flag indicating that if the file exists and is a regular file, and the file is opened successfully for write access, its length shall be truncated to zero.
  + const [O\_WRONLY](https://bun.com/reference/node/fs/constants/O_WRONLY): number

    Constant for fs.open(). Flag indicating to open a file for write-only access.
  + const [R\_OK](https://bun.com/reference/node/fs/constants/R_OK): number

    Constant for fs.access(). File can be read by the calling process.
  + const [S\_IFBLK](https://bun.com/reference/node/fs/constants/S_IFBLK): number

    Constant for fs.Stats mode property for determining a file's type. File type constant for a block-oriented device file.
  + const [S\_IFCHR](https://bun.com/reference/node/fs/constants/S_IFCHR): number

    Constant for fs.Stats mode property for determining a file's type. File type constant for a character-oriented device file.
  + const [S\_IFDIR](https://bun.com/reference/node/fs/constants/S_IFDIR): number

    Constant for fs.Stats mode property for determining a file's type. File type constant for a directory.
  + const [S\_IFIFO](https://bun.com/reference/node/fs/constants/S_IFIFO): number

    Constant for fs.Stats mode property for determining a file's type. File type constant for a FIFO/pipe.
  + const [S\_IFLNK](https://bun.com/reference/node/fs/constants/S_IFLNK): number

    Constant for fs.Stats mode property for determining a file's type. File type constant for a symbolic link.
  + const [S\_IFMT](https://bun.com/reference/node/fs/constants/S_IFMT): number

    Constant for fs.Stats mode property for determining a file's type. Bit mask used to extract the file type code.
  + const [S\_IFREG](https://bun.com/reference/node/fs/constants/S_IFREG): number

    Constant for fs.Stats mode property for determining a file's type. File type constant for a regular file.
  + const [S\_IFSOCK](https://bun.com/reference/node/fs/constants/S_IFSOCK): number

    Constant for fs.Stats mode property for determining a file's type. File type constant for a socket.
  + const [S\_IRGRP](https://bun.com/reference/node/fs/constants/S_IRGRP): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating readable by group.
  + const [S\_IROTH](https://bun.com/reference/node/fs/constants/S_IROTH): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating readable by others.
  + const [S\_IRUSR](https://bun.com/reference/node/fs/constants/S_IRUSR): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating readable by owner.
  + const [S\_IRWXG](https://bun.com/reference/node/fs/constants/S_IRWXG): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating readable, writable and executable by group.
  + const [S\_IRWXO](https://bun.com/reference/node/fs/constants/S_IRWXO): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating readable, writable and executable by others.
  + const [S\_IRWXU](https://bun.com/reference/node/fs/constants/S_IRWXU): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating readable, writable and executable by owner.
  + const [S\_IWGRP](https://bun.com/reference/node/fs/constants/S_IWGRP): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating writable by group.
  + const [S\_IWOTH](https://bun.com/reference/node/fs/constants/S_IWOTH): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating writable by others.
  + const [S\_IWUSR](https://bun.com/reference/node/fs/constants/S_IWUSR): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating writable by owner.
  + const [S\_IXGRP](https://bun.com/reference/node/fs/constants/S_IXGRP): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating executable by group.
  + const [S\_IXOTH](https://bun.com/reference/node/fs/constants/S_IXOTH): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating executable by others.
  + const [S\_IXUSR](https://bun.com/reference/node/fs/constants/S_IXUSR): number

    Constant for fs.Stats mode property for determining access permissions for a file. File mode indicating executable by owner.
  + const [UV\_FS\_O\_FILEMAP](https://bun.com/reference/node/fs/constants/UV_FS_O_FILEMAP): number

    When set, a memory file mapping is used to access the file. This flag is available on Windows operating systems only. On other operating systems, this flag is ignored.
  + const [W\_OK](https://bun.com/reference/node/fs/constants/W_OK): number

    Constant for fs.access(). File can be written by the calling process.
  + const [X\_OK](https://bun.com/reference/node/fs/constants/X_OK): number

    Constant for fs.access(). File can be executed by the calling process.
* function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: string) => void

  ): void;

  Asynchronously computes the canonical pathname by resolving `.`, `..`, and symbolic links.

  A canonical pathname is not necessarily unique. Hard links and bind mounts can expose a file system entity through many pathnames.

  This function behaves like [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html), with some exceptions:

  1. No case conversion is performed on case-insensitive file systems.
  2. The maximum number of symbolic links is platform-independent and generally (much) higher than what the native [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html) implementation supports.

  The `callback` gets two arguments `(err, resolvedPath)`. May use `process.cwd` to resolve relative paths.

  Only paths that can be converted to UTF8 strings are supported.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

  If `path` resolves to a socket or a pipe, the function will return a system dependent name for that object.

  function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: NonSharedBuffer) => void

  ): void;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: string | NonSharedBuffer) => void

  ): void;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, resolvedPath: string) => void

  ): void;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  ### namespace [realpath](https://bun.com/reference/node/fs/realpath)

  + function [native](https://bun.com/reference/node/fs/realpath/native)(

    path: [PathLike](https://bun.com/reference/node/fs/PathLike),

    options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

    callback: (err: null | ErrnoException, resolvedPath: string) => void

    ): void;

    Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

    The `callback` gets two arguments `(err, resolvedPath)`.

    Only paths that can be converted to UTF8 strings are supported.

    The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

    On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.

    function [native](https://bun.com/reference/node/fs/realpath/native)(

    path: [PathLike](https://bun.com/reference/node/fs/PathLike),

    options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

    callback: (err: null | ErrnoException, resolvedPath: NonSharedBuffer) => void

    ): void;

    Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

    The `callback` gets two arguments `(err, resolvedPath)`.

    Only paths that can be converted to UTF8 strings are supported.

    The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

    On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.

    function [native](https://bun.com/reference/node/fs/realpath/native)(

    path: [PathLike](https://bun.com/reference/node/fs/PathLike),

    options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

    callback: (err: null | ErrnoException, resolvedPath: string | NonSharedBuffer) => void

    ): void;

    Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

    The `callback` gets two arguments `(err, resolvedPath)`.

    Only paths that can be converted to UTF8 strings are supported.

    The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

    On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.

    function [native](https://bun.com/reference/node/fs/realpath/native)(

    path: [PathLike](https://bun.com/reference/node/fs/PathLike),

    callback: (err: null | ErrnoException, resolvedPath: string) => void

    ): void;

    Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

    The `callback` gets two arguments `(err, resolvedPath)`.

    Only paths that can be converted to UTF8 strings are supported.

    The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

    On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.
* function [realpathSync](https://bun.com/reference/node/fs/realpathSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string;

  Returns the resolved pathname.

  For detailed information, see the documentation of the asynchronous version of this API: realpath.

  function [realpathSync](https://bun.com/reference/node/fs/realpathSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): NonSharedBuffer;

  Synchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [realpathSync](https://bun.com/reference/node/fs/realpathSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string | NonSharedBuffer;

  Synchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  ### namespace [realpathSync](https://bun.com/reference/node/fs/realpathSync)

  + function [native](https://bun.com/reference/node/fs/realpathSync/native)(

    path: [PathLike](https://bun.com/reference/node/fs/PathLike),

    options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

    ): string;

    function [native](https://bun.com/reference/node/fs/realpathSync/native)(

    path: [PathLike](https://bun.com/reference/node/fs/PathLike),

    options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

    ): NonSharedBuffer;

    function [native](https://bun.com/reference/node/fs/realpathSync/native)(

    path: [PathLike](https://bun.com/reference/node/fs/PathLike),

    options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

    ): string | NonSharedBuffer;
* ### class [Dir](https://bun.com/reference/node/fs/Dir)

  A class representing a directory stream.

  Created by opendir, opendirSync, or `fsPromises.opendir()`.

  ```
  import { opendir } from 'node:fs/promises';

  try {
    const dir = await opendir('./');
    for await (const dirent of dir)
      console.log(dirent.name);
  } catch (err) {
    console.error(err);
  }
  ```

  When using the async iterator, the `fs.Dir` object will be automatically closed after the iterator exits.

  + readonly [path](https://bun.com/reference/node/fs/Dir/path): string

    The read-only path of this directory as was provided to opendir,opendirSync, or `fsPromises.opendir()`.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/fs/Dir/[asyncDispose])(): Promise<void>;

    Calls `dir.close()` if the directory handle is open, and returns a promise that fulfills when disposal is complete.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/fs/Dir/[asyncIterator])(): AsyncIterator<[Dirent](https://bun.com/reference/node/fs/Dirent)<string>>;

    Asynchronously iterates over the directory via `readdir(3)` until all entries have been read.
  + [[Symbol.dispose]](https://bun.com/reference/node/fs/Dir/[dispose])(): void;

    Calls `dir.closeSync()` if the directory handle is open, and returns `undefined`.
  + [close](https://bun.com/reference/node/fs/Dir/close)(): Promise<void>;

    Asynchronously close the directory's underlying resource handle. Subsequent reads will result in errors.

    A promise is returned that will be fulfilled after the resource has been closed.

    [close](https://bun.com/reference/node/fs/Dir/close)(

    cb: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

    ): void;

    Asynchronously close the directory's underlying resource handle. Subsequent reads will result in errors.

    A promise is returned that will be fulfilled after the resource has been closed.
  + [closeSync](https://bun.com/reference/node/fs/Dir/closeSync)(): void;

    Synchronously close the directory's underlying resource handle. Subsequent reads will result in errors.
  + [read](https://bun.com/reference/node/fs/Dir/read)(): Promise<null | [Dirent](https://bun.com/reference/node/fs/Dirent)<string>>;

    Asynchronously read the next directory entry via [`readdir(3)`](http://man7.org/linux/man-pages/man3/readdir.3.html) as an `fs.Dirent`.

    A promise is returned that will be fulfilled with an `fs.Dirent`, or `null` if there are no more directory entries to read.

    Directory entries returned by this function are in no particular order as provided by the operating system's underlying directory mechanisms. Entries added or removed while iterating over the directory might not be included in the iteration results.

    @returns

    containing {fs.Dirent|null}

    [read](https://bun.com/reference/node/fs/Dir/read)(

    cb: (err: null | ErrnoException, dirEnt: null | [Dirent](https://bun.com/reference/node/fs/Dirent)<string>) => void

    ): void;

    Asynchronously read the next directory entry via [`readdir(3)`](http://man7.org/linux/man-pages/man3/readdir.3.html) as an `fs.Dirent`.

    A promise is returned that will be fulfilled with an `fs.Dirent`, or `null` if there are no more directory entries to read.

    Directory entries returned by this function are in no particular order as provided by the operating system's underlying directory mechanisms. Entries added or removed while iterating over the directory might not be included in the iteration results.

    @returns

    containing {fs.Dirent|null}
  + [readSync](https://bun.com/reference/node/fs/Dir/readSync)(): null | [Dirent](https://bun.com/reference/node/fs/Dirent)<string>;

    Synchronously read the next directory entry as an `fs.Dirent`. See the POSIX [`readdir(3)`](http://man7.org/linux/man-pages/man3/readdir.3.html) documentation for more detail.

    If there are no more directory entries to read, `null` will be returned.

    Directory entries returned by this function are in no particular order as provided by the operating system's underlying directory mechanisms. Entries added or removed while iterating over the directory might not be included in the iteration results.
* ### class [Dirent](https://bun.com/reference/node/fs/Dirent)<Name extends string | [Buffer](https://bun.com/reference/node/buffer/Buffer) = string>

  A representation of a directory entry, which can be a file or a subdirectory within the directory, as returned by reading from an `fs.Dir`. The directory entry is a combination of the file name and file type pairs.

  Additionally, when readdir or readdirSync is called with the `withFileTypes` option set to `true`, the resulting array is filled with `fs.Dirent` objects, rather than strings or `Buffer` s.

  + [name](https://bun.com/reference/node/fs/Dirent/name): Name

    The file name that this `fs.Dirent` object refers to. The type of this value is determined by the `options.encoding` passed to readdir or readdirSync.
  + [parentPath](https://bun.com/reference/node/fs/Dirent/parentPath): string

    The path to the parent directory of the file this `fs.Dirent` object refers to.
  + [isBlockDevice](https://bun.com/reference/node/fs/Dirent/isBlockDevice)(): boolean;

    Returns `true` if the `fs.Dirent` object describes a block device.
  + [isCharacterDevice](https://bun.com/reference/node/fs/Dirent/isCharacterDevice)(): boolean;

    Returns `true` if the `fs.Dirent` object describes a character device.
  + [isDirectory](https://bun.com/reference/node/fs/Dirent/isDirectory)(): boolean;

    Returns `true` if the `fs.Dirent` object describes a file system directory.
  + [isFIFO](https://bun.com/reference/node/fs/Dirent/isFIFO)(): boolean;

    Returns `true` if the `fs.Dirent` object describes a first-in-first-out (FIFO) pipe.
  + [isFile](https://bun.com/reference/node/fs/Dirent/isFile)(): boolean;

    Returns `true` if the `fs.Dirent` object describes a regular file.
  + [isSocket](https://bun.com/reference/node/fs/Dirent/isSocket)(): boolean;

    Returns `true` if the `fs.Dirent` object describes a socket.
  + [isSymbolicLink](https://bun.com/reference/node/fs/Dirent/isSymbolicLink)(): boolean;

    Returns `true` if the `fs.Dirent` object describes a symbolic link.
* ### class [ReadStream](https://bun.com/reference/node/fs/ReadStream)

  Instances of `fs.ReadStream` are created and returned using the createReadStream function.

  + [bytesRead](https://bun.com/reference/node/fs/ReadStream/bytesRead): number

    The number of bytes that have been read so far.
  + readonly [closed](https://bun.com/reference/node/fs/ReadStream/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/fs/ReadStream/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/fs/ReadStream/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [path](https://bun.com/reference/node/fs/ReadStream/path): string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    The path to the file the stream is reading from as specified in the first argument to `fs.createReadStream()`. If `path` is passed as a string, then`readStream.path` will be a string. If `path` is passed as a `Buffer`, then`readStream.path` will be a `Buffer`. If `fd` is specified, then`readStream.path` will be `undefined`.
  + [pending](https://bun.com/reference/node/fs/ReadStream/pending): boolean

    This property is `true` if the underlying file has not been opened yet, i.e. before the `'ready'` event is emitted.
  + [readable](https://bun.com/reference/node/fs/ReadStream/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/fs/ReadStream/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/fs/ReadStream/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/fs/ReadStream/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/fs/ReadStream/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/fs/ReadStream/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/fs/ReadStream/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/fs/ReadStream/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/fs/ReadStream/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + static [captureRejections](https://bun.com/reference/node/fs/ReadStream/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/fs/ReadStream/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/fs/ReadStream/defaultMaxListeners): number

    By default, a maximum of `10` listeners can be registered for any single event. This limit can be changed for individual `EventEmitter` instances using the `emitter.setMaxListeners(n)` method. To change the default for *all*`EventEmitter` instances, the `events.defaultMaxListeners` property can be used. If this value is not a positive number, a `RangeError` is thrown.

    Take caution when setting the `events.defaultMaxListeners` because the change affects *all* `EventEmitter` instances, including those created before the change is made. However, calling `emitter.setMaxListeners(n)` still has precedence over `events.defaultMaxListeners`.

    This is not a hard limit. The `EventEmitter` instance will allow more listeners to be added but will output a trace warning to stderr indicating that a "possible EventEmitter memory leak" has been detected. For any single `EventEmitter`, the `emitter.getMaxListeners()` and `emitter.setMaxListeners()` methods can be used to temporarily avoid this warning:

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.setMaxListeners(emitter.getMaxListeners() + 1);
    emitter.once('event', () => {
      // do stuff
      emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
    });
    ```

    The `--trace-warnings` command-line flag can be used to display the stack trace for such warnings.

    The emitted warning can be inspected with `process.on('warning')` and will have the additional `emitter`, `type`, and `count` properties, referring to the event emitter instance, the event's name and the number of attached listeners, respectively. Its `name` property is set to `'MaxListenersExceededWarning'`.
  + readonly static [errorMonitor](https://bun.com/reference/node/fs/ReadStream/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/fs/ReadStream/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/fs/ReadStream/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/fs/ReadStream/_read)(

    size: number

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/fs/ReadStream/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/fs/ReadStream/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/fs/ReadStream/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/fs/ReadStream/addListener)<K extends symbol | 'close' | 'error' | 'data' | 'end' | 'pause' | 'readable' | 'resume' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: ReadStreamEvents[K]

    ): this;

    events.EventEmitter

    1. open
    2. close
    3. ready
  + [asIndexedPairs](https://bun.com/reference/node/fs/ReadStream/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/fs/ReadStream/close)(

    callback?: (err?: null | ErrnoException) => void

    ): void;
  + [compose](https://bun.com/reference/node/fs/ReadStream/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [destroy](https://bun.com/reference/node/fs/ReadStream/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/fs/ReadStream/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/fs/ReadStream/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/fs/ReadStream/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/fs/ReadStream/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/fs/ReadStream/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/fs/ReadStream/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/fs/ReadStream/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/fs/ReadStream/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/fs/ReadStream/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/fs/ReadStream/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/fs/ReadStream/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/fs/ReadStream/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/fs/ReadStream/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/fs/ReadStream/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/fs/ReadStream/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/fs/ReadStream/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/fs/ReadStream/on)<K extends symbol | 'close' | 'error' | 'data' | 'end' | 'pause' | 'readable' | 'resume' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: ReadStreamEvents[K]

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/fs/ReadStream/once)<K extends symbol | 'close' | 'error' | 'data' | 'end' | 'pause' | 'readable' | 'resume' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: ReadStreamEvents[K]

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [pause](https://bun.com/reference/node/fs/ReadStream/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/fs/ReadStream/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/fs/ReadStream/prependListener)<K extends symbol | 'close' | 'error' | 'data' | 'end' | 'pause' | 'readable' | 'resume' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: ReadStreamEvents[K]

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/fs/ReadStream/prependOnceListener)<K extends symbol | 'close' | 'error' | 'data' | 'end' | 'pause' | 'readable' | 'resume' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: ReadStreamEvents[K]

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [push](https://bun.com/reference/node/fs/ReadStream/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/fs/ReadStream/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/fs/ReadStream/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/fs/ReadStream/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/fs/ReadStream/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/fs/ReadStream/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/ReadStream/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/fs/ReadStream/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setEncoding](https://bun.com/reference/node/fs/ReadStream/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/fs/ReadStream/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/fs/ReadStream/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/fs/ReadStream/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/fs/ReadStream/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [unpipe](https://bun.com/reference/node/fs/ReadStream/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/fs/ReadStream/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/fs/ReadStream/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + static [addAbortListener](https://bun.com/reference/node/fs/ReadStream/addAbortListener)(

    signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

    resource: (event: [Event](https://bun.com/reference/globals/Event)) => void

    ): Disposable;

    Listens once to the `abort` event on the provided `signal`.

    Listening to the `abort` event on abort signals is unsafe and may lead to resource leaks since another third party with the signal can call `e.stopImmediatePropagation()`. Unfortunately Node.js cannot change this since it would violate the web standard. Additionally, the original API makes it easy to forget to remove listeners.

    This API allows safely using `AbortSignal`s in Node.js APIs by solving these two issues by listening to the event such that `stopImmediatePropagation` does not prevent the listener from running.

    Returns a disposable so that it may be unsubscribed from more easily.

    ```
    import { addAbortListener } from 'node:events';

    function example(signal) {
      let disposable;
      try {
        signal.addEventListener('abort', (e) => e.stopImmediatePropagation());
        disposable = addAbortListener(signal, (e) => {
          // Do something when signal is aborted.
        });
      } finally {
        disposable?.[Symbol.dispose]();
      }
    }
    ```

    @returns

    Disposable that removes the `abort` listener.
  + static [from](https://bun.com/reference/node/fs/ReadStream/from)(

    iterable: Iterable<any, any, any> | AsyncIterable<any, any, any>,

    options?: [ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    A utility method for creating Readable Streams out of iterators.

    @param iterable

    Object implementing the `Symbol.asyncIterator` or `Symbol.iterator` iterable protocol. Emits an 'error' event if a null value is passed.

    @param options

    Options provided to `new stream.Readable([options])`. By default, `Readable.from()` will set `options.objectMode` to `true`, unless this is explicitly opted out by setting `options.objectMode` to `false`.
  + static [fromWeb](https://bun.com/reference/node/fs/ReadStream/fromWeb)(

    readableStream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream),

    options?: Pick<[ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>, 'signal' | 'encoding' | 'highWaterMark' | 'objectMode'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    A utility method for creating a `Readable` from a web `ReadableStream`.
  + static [getEventListeners](https://bun.com/reference/node/fs/ReadStream/getEventListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget),

    name: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    For `EventEmitter`s this behaves exactly the same as calling `.listeners` on the emitter.

    For `EventTarget`s this is the only way to get the event listeners for the event target. This is useful for debugging and diagnostic purposes.

    ```
    import { getEventListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      const listener = () => console.log('Events are fun');
      ee.on('foo', listener);
      console.log(getEventListeners(ee, 'foo')); // [ [Function: listener] ]
    }
    {
      const et = new EventTarget();
      const listener = () => console.log('Events are fun');
      et.addEventListener('foo', listener);
      console.log(getEventListeners(et, 'foo')); // [ [Function: listener] ]
    }
    ```
  + static [getMaxListeners](https://bun.com/reference/node/fs/ReadStream/getMaxListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)

    ): number;

    Returns the currently set max amount of listeners.

    For `EventEmitter`s this behaves exactly the same as calling `.getMaxListeners` on the emitter.

    For `EventTarget`s this is the only way to get the max event listeners for the event target. If the number of event handlers on a single EventTarget exceeds the max set, the EventTarget will print a warning.

    ```
    import { getMaxListeners, setMaxListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      console.log(getMaxListeners(ee)); // 10
      setMaxListeners(11, ee);
      console.log(getMaxListeners(ee)); // 11
    }
    {
      const et = new EventTarget();
      console.log(getMaxListeners(et)); // 10
      setMaxListeners(11, et);
      console.log(getMaxListeners(et)); // 11
    }
    ```
  + static [isDisturbed](https://bun.com/reference/node/fs/ReadStream/isDisturbed)(

    stream: [Readable](https://bun.com/reference/node/stream/default/Readable) | ReadableStream

    ): boolean;

    Returns whether the stream has been read from or cancelled.
  + static [on](https://bun.com/reference/node/fs/ReadStream/on)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`

    static [on](https://bun.com/reference/node/fs/ReadStream/on)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`
  + static [once](https://bun.com/reference/node/fs/ReadStream/once)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```

    static [once](https://bun.com/reference/node/fs/ReadStream/once)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```
  + static [setMaxListeners](https://bun.com/reference/node/fs/ReadStream/setMaxListeners)(

    n?: number,

    ...eventTargets: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)[]

    ): void;

    ```
    import { setMaxListeners, EventEmitter } from 'node:events';

    const target = new EventTarget();
    const emitter = new EventEmitter();

    setMaxListeners(5, target, emitter);
    ```

    @param n

    A non-negative number. The maximum number of listeners per `EventTarget` event.

    @param eventTargets

    Zero or more {EventTarget} or {EventEmitter} instances. If none are specified, `n` is set as the default max for all newly created {EventTarget} and {EventEmitter} objects.
  + static [toWeb](https://bun.com/reference/node/fs/ReadStream/toWeb)(

    streamReadable: [Readable](https://bun.com/reference/node/stream/default/Readable),

    options?: { strategy: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<any> }

    ): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream);

    A utility method for creating a web `ReadableStream` from a `Readable`.
* ### class [Stats](https://bun.com/reference/node/fs/Stats)

  A `fs.Stats` object provides information about a file.

  Objects returned from stat, lstat, fstat, and their synchronous counterparts are of this type. If `bigint` in the `options` passed to those methods is true, the numeric values will be `bigint` instead of `number`, and the object will contain additional nanosecond-precision properties suffixed with `Ns`. `Stat` objects are not to be created directly using the `new` keyword.

  ```
  Stats {
    dev: 2114,
    ino: 48064969,
    mode: 33188,
    nlink: 1,
    uid: 85,
    gid: 100,
    rdev: 0,
    size: 527,
    blksize: 4096,
    blocks: 8,
    atimeMs: 1318289051000.1,
    mtimeMs: 1318289051000.1,
    ctimeMs: 1318289051000.1,
    birthtimeMs: 1318289051000.1,
    atime: Mon, 10 Oct 2011 23:24:11 GMT,
    mtime: Mon, 10 Oct 2011 23:24:11 GMT,
    ctime: Mon, 10 Oct 2011 23:24:11 GMT,
    birthtime: Mon, 10 Oct 2011 23:24:11 GMT }
  ```

  `bigint` version:

  ```
  BigIntStats {
    dev: 2114n,
    ino: 48064969n,
    mode: 33188n,
    nlink: 1n,
    uid: 85n,
    gid: 100n,
    rdev: 0n,
    size: 527n,
    blksize: 4096n,
    blocks: 8n,
    atimeMs: 1318289051000n,
    mtimeMs: 1318289051000n,
    ctimeMs: 1318289051000n,
    birthtimeMs: 1318289051000n,
    atimeNs: 1318289051000000000n,
    mtimeNs: 1318289051000000000n,
    ctimeNs: 1318289051000000000n,
    birthtimeNs: 1318289051000000000n,
    atime: Mon, 10 Oct 2011 23:24:11 GMT,
    mtime: Mon, 10 Oct 2011 23:24:11 GMT,
    ctime: Mon, 10 Oct 2011 23:24:11 GMT,
    birthtime: Mon, 10 Oct 2011 23:24:11 GMT }
  ```

  + [atime](https://bun.com/reference/node/fs/Stats/atime): Date
  + [atimeMs](https://bun.com/reference/node/fs/Stats/atimeMs): number
  + [birthtime](https://bun.com/reference/node/fs/Stats/birthtime): Date
  + [birthtimeMs](https://bun.com/reference/node/fs/Stats/birthtimeMs): number
  + [blksize](https://bun.com/reference/node/fs/Stats/blksize): number
  + [blocks](https://bun.com/reference/node/fs/Stats/blocks): number
  + [ctime](https://bun.com/reference/node/fs/Stats/ctime): Date
  + [ctimeMs](https://bun.com/reference/node/fs/Stats/ctimeMs): number
  + [dev](https://bun.com/reference/node/fs/Stats/dev): number
  + [gid](https://bun.com/reference/node/fs/Stats/gid): number
  + [ino](https://bun.com/reference/node/fs/Stats/ino): number
  + [mode](https://bun.com/reference/node/fs/Stats/mode): number
  + [mtime](https://bun.com/reference/node/fs/Stats/mtime): Date
  + [mtimeMs](https://bun.com/reference/node/fs/Stats/mtimeMs): number
  + [nlink](https://bun.com/reference/node/fs/Stats/nlink): number
  + [rdev](https://bun.com/reference/node/fs/Stats/rdev): number
  + [size](https://bun.com/reference/node/fs/Stats/size): number
  + [uid](https://bun.com/reference/node/fs/Stats/uid): number
  + [isBlockDevice](https://bun.com/reference/node/fs/Stats/isBlockDevice)(): boolean;
  + [isCharacterDevice](https://bun.com/reference/node/fs/Stats/isCharacterDevice)(): boolean;
  + [isDirectory](https://bun.com/reference/node/fs/Stats/isDirectory)(): boolean;
  + [isFIFO](https://bun.com/reference/node/fs/Stats/isFIFO)(): boolean;
  + [isFile](https://bun.com/reference/node/fs/Stats/isFile)(): boolean;
  + [isSocket](https://bun.com/reference/node/fs/Stats/isSocket)(): boolean;
  + [isSymbolicLink](https://bun.com/reference/node/fs/Stats/isSymbolicLink)(): boolean;
* ### class [StatsFs](https://bun.com/reference/node/fs/StatsFs)

  Provides information about a mounted file system.

  Objects returned from statfs and its synchronous counterpart are of this type. If `bigint` in the `options` passed to those methods is `true`, the numeric values will be `bigint` instead of `number`.

  ```
  StatFs {
    type: 1397114950,
    bsize: 4096,
    blocks: 121938943,
    bfree: 61058895,
    bavail: 61058895,
    files: 999,
    ffree: 1000000
  }
  ```

  `bigint` version:

  ```
  StatFs {
    type: 1397114950n,
    bsize: 4096n,
    blocks: 121938943n,
    bfree: 61058895n,
    bavail: 61058895n,
    files: 999n,
    ffree: 1000000n
  }
  ```

  + [bavail](https://bun.com/reference/node/fs/StatsFs/bavail): number

    Available blocks for unprivileged users
  + [bfree](https://bun.com/reference/node/fs/StatsFs/bfree): number

    Free blocks in file system.
  + [blocks](https://bun.com/reference/node/fs/StatsFs/blocks): number

    Total data blocks in file system.
  + [bsize](https://bun.com/reference/node/fs/StatsFs/bsize): number

    Optimal transfer block size.
  + [ffree](https://bun.com/reference/node/fs/StatsFs/ffree): number

    Free file nodes in file system.
  + [files](https://bun.com/reference/node/fs/StatsFs/files): number

    Total file nodes in file system.
  + [type](https://bun.com/reference/node/fs/StatsFs/type): number

    Type of file system.
* ### class [Utf8Stream](https://bun.com/reference/node/fs/Utf8Stream)

  An optimized UTF-8 stream writer that allows for flushing all the internal buffering on demand. It handles `EAGAIN` errors correctly, allowing for customization, for example, by dropping content if the disk is busy.

  + readonly [append](https://bun.com/reference/node/fs/Utf8Stream/append): boolean

    Whether the stream is appending to the file or truncating it.
  + readonly [contentMode](https://bun.com/reference/node/fs/Utf8Stream/contentMode): 'utf8' | 'buffer'

    The type of data that can be written to the stream. Supported values are `'utf8'` or `'buffer'`.
  + readonly [fd](https://bun.com/reference/node/fs/Utf8Stream/fd): number

    The file descriptor that is being written to.
  + readonly [file](https://bun.com/reference/node/fs/Utf8Stream/file): string

    The file that is being written to.
  + readonly [fsync](https://bun.com/reference/node/fs/Utf8Stream/fsync): boolean

    Whether the stream is performing a `fs.fsyncSync()` after every write operation.
  + readonly [maxLength](https://bun.com/reference/node/fs/Utf8Stream/maxLength): number

    The maximum length of the internal buffer. If a write operation would cause the buffer to exceed `maxLength`, the data written is dropped and a drop event is emitted with the dropped data.
  + readonly [minLength](https://bun.com/reference/node/fs/Utf8Stream/minLength): number

    The minimum length of the internal buffer that is required to be full before flushing.
  + readonly [mkdir](https://bun.com/reference/node/fs/Utf8Stream/mkdir): boolean

    Whether the stream should ensure that the directory for the `dest` file exists. If `true`, it will create the directory if it does not exist.
  + readonly [mode](https://bun.com/reference/node/fs/Utf8Stream/mode): string | number

    The mode of the file that is being written to.
  + readonly [periodicFlush](https://bun.com/reference/node/fs/Utf8Stream/periodicFlush): number

    The number of milliseconds between flushes. If set to `0`, no periodic flushes will be performed.
  + readonly [sync](https://bun.com/reference/node/fs/Utf8Stream/sync): boolean

    Whether the stream is writing synchronously or asynchronously.
  + readonly [writing](https://bun.com/reference/node/fs/Utf8Stream/writing): boolean

    Whether the stream is currently writing data to the file.
  + static [captureRejections](https://bun.com/reference/node/fs/Utf8Stream/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/fs/Utf8Stream/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/fs/Utf8Stream/defaultMaxListeners): number

    By default, a maximum of `10` listeners can be registered for any single event. This limit can be changed for individual `EventEmitter` instances using the `emitter.setMaxListeners(n)` method. To change the default for *all*`EventEmitter` instances, the `events.defaultMaxListeners` property can be used. If this value is not a positive number, a `RangeError` is thrown.

    Take caution when setting the `events.defaultMaxListeners` because the change affects *all* `EventEmitter` instances, including those created before the change is made. However, calling `emitter.setMaxListeners(n)` still has precedence over `events.defaultMaxListeners`.

    This is not a hard limit. The `EventEmitter` instance will allow more listeners to be added but will output a trace warning to stderr indicating that a "possible EventEmitter memory leak" has been detected. For any single `EventEmitter`, the `emitter.getMaxListeners()` and `emitter.setMaxListeners()` methods can be used to temporarily avoid this warning:

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.setMaxListeners(emitter.getMaxListeners() + 1);
    emitter.once('event', () => {
      // do stuff
      emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
    });
    ```

    The `--trace-warnings` command-line flag can be used to display the stack trace for such warnings.

    The emitted warning can be inspected with `process.on('warning')` and will have the additional `emitter`, `type`, and `count` properties, referring to the event emitter instance, the event's name and the number of attached listeners, respectively. Its `name` property is set to `'MaxListenersExceededWarning'`.
  + readonly static [errorMonitor](https://bun.com/reference/node/fs/Utf8Stream/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/fs/Utf8Stream/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [[Symbol.dispose]](https://bun.com/reference/node/fs/Utf8Stream/[dispose])(): void;

    Calls `utf8Stream.destroy()`.
  + [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: 'drop',

    listener: (data: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: 'ready',

    listener: () => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: 'write',

    listener: (n: number) => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/Utf8Stream/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error
  + [destroy](https://bun.com/reference/node/fs/Utf8Stream/destroy)(): void;

    Close the stream immediately, without flushing the internal buffer.
  + [emit](https://bun.com/reference/node/fs/Utf8Stream/emit)<K>(

    eventName: string | symbol,

    ...args: AnyRest

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```
  + [end](https://bun.com/reference/node/fs/Utf8Stream/end)(): void;

    Close the stream gracefully, flushing the internal buffer before closing.
  + [eventNames](https://bun.com/reference/node/fs/Utf8Stream/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [flush](https://bun.com/reference/node/fs/Utf8Stream/flush)(

    callback: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;

    Writes the current buffer to the file if a write was not in progress. Do nothing if `minLength` is zero or if it is already writing.
  + [flushSync](https://bun.com/reference/node/fs/Utf8Stream/flushSync)(): void;

    Flushes the buffered data synchronously. This is a costly operation.
  + [getMaxListeners](https://bun.com/reference/node/fs/Utf8Stream/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/fs/Utf8Stream/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/fs/Utf8Stream/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/fs/Utf8Stream/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: 'drop',

    listener: (data: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): this;

    [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: 'ready',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: 'write',

    listener: (n: number) => void

    ): this;

    [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: 'drop',

    listener: (data: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): this;

    [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: 'ready',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: 'write',

    listener: (n: number) => void

    ): this;

    [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: 'drop',

    listener: (data: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): this;

    [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: 'ready',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: 'write',

    listener: (n: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/fs/Utf8Stream/prependListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: 'drop',

    listener: (data: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: 'ready',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: 'write',

    listener: (n: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/fs/Utf8Stream/prependOnceListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/fs/Utf8Stream/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [removeAllListeners](https://bun.com/reference/node/fs/Utf8Stream/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/fs/Utf8Stream/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [reopen](https://bun.com/reference/node/fs/Utf8Stream/reopen)(

    file: [PathLike](https://bun.com/reference/node/fs/PathLike)

    ): void;

    Reopen the file in place, useful for log rotation.

    @param file

    A path to a file to be written to (mode controlled by the append option).
  + [setMaxListeners](https://bun.com/reference/node/fs/Utf8Stream/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [write](https://bun.com/reference/node/fs/Utf8Stream/write)(

    data: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    ): boolean;

    When the `options.contentMode` is set to `'utf8'` when the stream is created, the `data` argument must be a string. If the `contentMode` is set to `'buffer'`, the `data` argument must be a `Buffer`.

    @param data

    The data to write.
  + static [addAbortListener](https://bun.com/reference/node/fs/Utf8Stream/addAbortListener)(

    signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

    resource: (event: [Event](https://bun.com/reference/globals/Event)) => void

    ): Disposable;

    Listens once to the `abort` event on the provided `signal`.

    Listening to the `abort` event on abort signals is unsafe and may lead to resource leaks since another third party with the signal can call `e.stopImmediatePropagation()`. Unfortunately Node.js cannot change this since it would violate the web standard. Additionally, the original API makes it easy to forget to remove listeners.

    This API allows safely using `AbortSignal`s in Node.js APIs by solving these two issues by listening to the event such that `stopImmediatePropagation` does not prevent the listener from running.

    Returns a disposable so that it may be unsubscribed from more easily.

    ```
    import { addAbortListener } from 'node:events';

    function example(signal) {
      let disposable;
      try {
        signal.addEventListener('abort', (e) => e.stopImmediatePropagation());
        disposable = addAbortListener(signal, (e) => {
          // Do something when signal is aborted.
        });
      } finally {
        disposable?.[Symbol.dispose]();
      }
    }
    ```

    @returns

    Disposable that removes the `abort` listener.
  + static [getEventListeners](https://bun.com/reference/node/fs/Utf8Stream/getEventListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget),

    name: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    For `EventEmitter`s this behaves exactly the same as calling `.listeners` on the emitter.

    For `EventTarget`s this is the only way to get the event listeners for the event target. This is useful for debugging and diagnostic purposes.

    ```
    import { getEventListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      const listener = () => console.log('Events are fun');
      ee.on('foo', listener);
      console.log(getEventListeners(ee, 'foo')); // [ [Function: listener] ]
    }
    {
      const et = new EventTarget();
      const listener = () => console.log('Events are fun');
      et.addEventListener('foo', listener);
      console.log(getEventListeners(et, 'foo')); // [ [Function: listener] ]
    }
    ```
  + static [getMaxListeners](https://bun.com/reference/node/fs/Utf8Stream/getMaxListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)

    ): number;

    Returns the currently set max amount of listeners.

    For `EventEmitter`s this behaves exactly the same as calling `.getMaxListeners` on the emitter.

    For `EventTarget`s this is the only way to get the max event listeners for the event target. If the number of event handlers on a single EventTarget exceeds the max set, the EventTarget will print a warning.

    ```
    import { getMaxListeners, setMaxListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      console.log(getMaxListeners(ee)); // 10
      setMaxListeners(11, ee);
      console.log(getMaxListeners(ee)); // 11
    }
    {
      const et = new EventTarget();
      console.log(getMaxListeners(et)); // 10
      setMaxListeners(11, et);
      console.log(getMaxListeners(et)); // 11
    }
    ```
  + static [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`

    static [on](https://bun.com/reference/node/fs/Utf8Stream/on)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`
  + static [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```

    static [once](https://bun.com/reference/node/fs/Utf8Stream/once)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```
  + static [setMaxListeners](https://bun.com/reference/node/fs/Utf8Stream/setMaxListeners)(

    n?: number,

    ...eventTargets: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)[]

    ): void;

    ```
    import { setMaxListeners, EventEmitter } from 'node:events';

    const target = new EventTarget();
    const emitter = new EventEmitter();

    setMaxListeners(5, target, emitter);
    ```

    @param n

    A non-negative number. The maximum number of listeners per `EventTarget` event.

    @param eventTargets

    Zero or more {EventTarget} or {EventEmitter} instances. If none are specified, `n` is set as the default max for all newly created {EventTarget} and {EventEmitter} objects.
* ### class [WriteStream](https://bun.com/reference/node/fs/WriteStream)

  + Extends `stream.Writable`

  Instances of `fs.WriteStream` are created and returned using the createWriteStream function.

  + [bytesWritten](https://bun.com/reference/node/fs/WriteStream/bytesWritten): number

    The number of bytes written so far. Does not include data that is still queued for writing.
  + readonly [closed](https://bun.com/reference/node/fs/WriteStream/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/fs/WriteStream/destroyed): boolean

    Is `true` after `writable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/fs/WriteStream/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [path](https://bun.com/reference/node/fs/WriteStream/path): string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    The path to the file the stream is writing to as specified in the first argument to createWriteStream. If `path` is passed as a string, then`writeStream.path` will be a string. If `path` is passed as a `Buffer`, then`writeStream.path` will be a `Buffer`.
  + [pending](https://bun.com/reference/node/fs/WriteStream/pending): boolean

    This property is `true` if the underlying file has not been opened yet, i.e. before the `'ready'` event is emitted.
  + readonly [writable](https://bun.com/reference/node/fs/WriteStream/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/fs/WriteStream/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/fs/WriteStream/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/fs/WriteStream/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/fs/WriteStream/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/fs/WriteStream/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/fs/WriteStream/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/fs/WriteStream/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/fs/WriteStream/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + static [captureRejections](https://bun.com/reference/node/fs/WriteStream/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/fs/WriteStream/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/fs/WriteStream/defaultMaxListeners): number

    By default, a maximum of `10` listeners can be registered for any single event. This limit can be changed for individual `EventEmitter` instances using the `emitter.setMaxListeners(n)` method. To change the default for *all*`EventEmitter` instances, the `events.defaultMaxListeners` property can be used. If this value is not a positive number, a `RangeError` is thrown.

    Take caution when setting the `events.defaultMaxListeners` because the change affects *all* `EventEmitter` instances, including those created before the change is made. However, calling `emitter.setMaxListeners(n)` still has precedence over `events.defaultMaxListeners`.

    This is not a hard limit. The `EventEmitter` instance will allow more listeners to be added but will output a trace warning to stderr indicating that a "possible EventEmitter memory leak" has been detected. For any single `EventEmitter`, the `emitter.getMaxListeners()` and `emitter.setMaxListeners()` methods can be used to temporarily avoid this warning:

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.setMaxListeners(emitter.getMaxListeners() + 1);
    emitter.once('event', () => {
      // do stuff
      emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
    });
    ```

    The `--trace-warnings` command-line flag can be used to display the stack trace for such warnings.

    The emitted warning can be inspected with `process.on('warning')` and will have the additional `emitter`, `type`, and `count` properties, referring to the event emitter instance, the event's name and the number of attached listeners, respectively. Its `name` property is set to `'MaxListenersExceededWarning'`.
  + readonly static [errorMonitor](https://bun.com/reference/node/fs/WriteStream/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/fs/WriteStream/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/fs/WriteStream/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/fs/WriteStream/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_write](https://bun.com/reference/node/fs/WriteStream/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/fs/WriteStream/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/fs/WriteStream/[asyncDispose])(): Promise<void>;

    Calls `writable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/fs/WriteStream/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/fs/WriteStream/addListener)<K extends symbol | 'pipe' | 'close' | 'error' | 'drain' | 'finish' | 'unpipe' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: WriteStreamEvents[K]

    ): this;

    events.EventEmitter

    1. open
    2. close
    3. ready
  + [close](https://bun.com/reference/node/fs/WriteStream/close)(

    callback?: (err?: null | ErrnoException) => void

    ): void;

    Closes `writeStream`. Optionally accepts a callback that will be executed once the `writeStream`is closed.
  + [compose](https://bun.com/reference/node/fs/WriteStream/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/fs/WriteStream/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/fs/WriteStream/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the writable stream has ended and subsequent calls to `write()` or `end()` will result in an `ERR_STREAM_DESTROYED` error. This is a destructive and immediate way to destroy a stream. Previous calls to `write()` may not have drained, and may trigger an `ERR_STREAM_DESTROYED` error. Use `end()` instead of destroy if data should flush before close, or wait for the `'drain'` event before destroying the stream.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `writable._destroy()`.

    @param error

    Optional, an error to emit with `'error'` event.
  + [emit](https://bun.com/reference/node/fs/WriteStream/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/fs/WriteStream/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/fs/WriteStream/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/fs/WriteStream/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/fs/WriteStream/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/fs/WriteStream/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/fs/WriteStream/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/fs/WriteStream/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/fs/WriteStream/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/fs/WriteStream/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/fs/WriteStream/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getMaxListeners](https://bun.com/reference/node/fs/WriteStream/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/fs/WriteStream/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/fs/WriteStream/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/fs/WriteStream/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/fs/WriteStream/on)<K extends symbol | 'pipe' | 'close' | 'error' | 'drain' | 'finish' | 'unpipe' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: WriteStreamEvents[K]

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/fs/WriteStream/once)<K extends symbol | 'pipe' | 'close' | 'error' | 'drain' | 'finish' | 'unpipe' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: WriteStreamEvents[K]

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [pipe](https://bun.com/reference/node/fs/WriteStream/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/fs/WriteStream/prependListener)<K extends symbol | 'pipe' | 'close' | 'error' | 'drain' | 'finish' | 'unpipe' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: WriteStreamEvents[K]

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/fs/WriteStream/prependOnceListener)<K extends symbol | 'pipe' | 'close' | 'error' | 'drain' | 'finish' | 'unpipe' | string & {} | 'open' | 'ready'>(

    event: K,

    listener: WriteStreamEvents[K]

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [rawListeners](https://bun.com/reference/node/fs/WriteStream/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [removeAllListeners](https://bun.com/reference/node/fs/WriteStream/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/fs/WriteStream/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/fs/WriteStream/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/WriteStream/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/WriteStream/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/WriteStream/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/WriteStream/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/fs/WriteStream/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [setDefaultEncoding](https://bun.com/reference/node/fs/WriteStream/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setMaxListeners](https://bun.com/reference/node/fs/WriteStream/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [uncork](https://bun.com/reference/node/fs/WriteStream/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [write](https://bun.com/reference/node/fs/WriteStream/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/fs/WriteStream/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
  + static [addAbortListener](https://bun.com/reference/node/fs/WriteStream/addAbortListener)(

    signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

    resource: (event: [Event](https://bun.com/reference/globals/Event)) => void

    ): Disposable;

    Listens once to the `abort` event on the provided `signal`.

    Listening to the `abort` event on abort signals is unsafe and may lead to resource leaks since another third party with the signal can call `e.stopImmediatePropagation()`. Unfortunately Node.js cannot change this since it would violate the web standard. Additionally, the original API makes it easy to forget to remove listeners.

    This API allows safely using `AbortSignal`s in Node.js APIs by solving these two issues by listening to the event such that `stopImmediatePropagation` does not prevent the listener from running.

    Returns a disposable so that it may be unsubscribed from more easily.

    ```
    import { addAbortListener } from 'node:events';

    function example(signal) {
      let disposable;
      try {
        signal.addEventListener('abort', (e) => e.stopImmediatePropagation());
        disposable = addAbortListener(signal, (e) => {
          // Do something when signal is aborted.
        });
      } finally {
        disposable?.[Symbol.dispose]();
      }
    }
    ```

    @returns

    Disposable that removes the `abort` listener.
  + static [fromWeb](https://bun.com/reference/node/fs/WriteStream/fromWeb)(

    writableStream: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream),

    options?: Pick<[WritableOptions](https://bun.com/reference/node/stream/default/WritableOptions)<[Writable](https://bun.com/reference/node/stream/default/Writable)>, 'signal' | 'decodeStrings' | 'highWaterMark' | 'objectMode'>

    ): [Writable](https://bun.com/reference/node/stream/default/Writable);

    A utility method for creating a `Writable` from a web `WritableStream`.
  + static [getEventListeners](https://bun.com/reference/node/fs/WriteStream/getEventListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget),

    name: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    For `EventEmitter`s this behaves exactly the same as calling `.listeners` on the emitter.

    For `EventTarget`s this is the only way to get the event listeners for the event target. This is useful for debugging and diagnostic purposes.

    ```
    import { getEventListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      const listener = () => console.log('Events are fun');
      ee.on('foo', listener);
      console.log(getEventListeners(ee, 'foo')); // [ [Function: listener] ]
    }
    {
      const et = new EventTarget();
      const listener = () => console.log('Events are fun');
      et.addEventListener('foo', listener);
      console.log(getEventListeners(et, 'foo')); // [ [Function: listener] ]
    }
    ```
  + static [getMaxListeners](https://bun.com/reference/node/fs/WriteStream/getMaxListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)

    ): number;

    Returns the currently set max amount of listeners.

    For `EventEmitter`s this behaves exactly the same as calling `.getMaxListeners` on the emitter.

    For `EventTarget`s this is the only way to get the max event listeners for the event target. If the number of event handlers on a single EventTarget exceeds the max set, the EventTarget will print a warning.

    ```
    import { getMaxListeners, setMaxListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      console.log(getMaxListeners(ee)); // 10
      setMaxListeners(11, ee);
      console.log(getMaxListeners(ee)); // 11
    }
    {
      const et = new EventTarget();
      console.log(getMaxListeners(et)); // 10
      setMaxListeners(11, et);
      console.log(getMaxListeners(et)); // 11
    }
    ```
  + static [on](https://bun.com/reference/node/fs/WriteStream/on)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`

    static [on](https://bun.com/reference/node/fs/WriteStream/on)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`
  + static [once](https://bun.com/reference/node/fs/WriteStream/once)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```

    static [once](https://bun.com/reference/node/fs/WriteStream/once)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```
  + static [setMaxListeners](https://bun.com/reference/node/fs/WriteStream/setMaxListeners)(

    n?: number,

    ...eventTargets: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)[]

    ): void;

    ```
    import { setMaxListeners, EventEmitter } from 'node:events';

    const target = new EventTarget();
    const emitter = new EventEmitter();

    setMaxListeners(5, target, emitter);
    ```

    @param n

    A non-negative number. The maximum number of listeners per `EventTarget` event.

    @param eventTargets

    Zero or more {EventTarget} or {EventEmitter} instances. If none are specified, `n` is set as the default max for all newly created {EventTarget} and {EventEmitter} objects.
  + static [toWeb](https://bun.com/reference/node/fs/WriteStream/toWeb)(

    streamWritable: [Writable](https://bun.com/reference/node/stream/default/Writable)

    ): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream);

    A utility method for creating a web `WritableStream` from a `Writable`.
* const [lstatSync](https://bun.com/reference/node/fs/lstatSync): [StatSyncFn](https://bun.com/reference/node/fs/StatSyncFn)

  Synchronous lstat(2) - Get file status. Does not dereference symbolic links.
* const [statSync](https://bun.com/reference/node/fs/statSync): [StatSyncFn](https://bun.com/reference/node/fs/StatSyncFn)

  Synchronous stat(2) - Get file status.
* function [access](https://bun.com/reference/node/fs/access)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode?: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Tests a user's permissions for the file or directory specified by `path`. The `mode` argument is an optional integer that specifies the accessibility checks to be performed. `mode` should be either the value `fs.constants.F_OK` or a mask consisting of the bitwise OR of any of `fs.constants.R_OK`, `fs.constants.W_OK`, and `fs.constants.X_OK` (e.g.`fs.constants.W_OK | fs.constants.R_OK`). Check `File access constants` for possible values of `mode`.

  The final argument, `callback`, is a callback function that is invoked with a possible error argument. If any of the accessibility checks fail, the error argument will be an `Error` object. The following examples check if `package.json` exists, and if it is readable or writable.

  ```
  import { access, constants } from 'node:fs';

  const file = 'package.json';

  // Check if the file exists in the current directory.
  access(file, constants.F_OK, (err) => {
    console.log(`${file} ${err ? 'does not exist' : 'exists'}`);
  });

  // Check if the file is readable.
  access(file, constants.R_OK, (err) => {
    console.log(`${file} ${err ? 'is not readable' : 'is readable'}`);
  });

  // Check if the file is writable.
  access(file, constants.W_OK, (err) => {
    console.log(`${file} ${err ? 'is not writable' : 'is writable'}`);
  });

  // Check if the file is readable and writable.
  access(file, constants.R_OK | constants.W_OK, (err) => {
    console.log(`${file} ${err ? 'is not' : 'is'} readable and writable`);
  });
  ```

  Do not use `fs.access()` to check for the accessibility of a file before calling `fs.open()`, `fs.readFile()`, or `fs.writeFile()`. Doing so introduces a race condition, since other processes may change the file's state between the two calls. Instead, user code should open/read/write the file directly and handle the error raised if the file is not accessible.

  **write (NOT RECOMMENDED)**

  ```
  import { access, open, close } from 'node:fs';

  access('myfile', (err) => {
    if (!err) {
      console.error('myfile already exists');
      return;
    }

    open('myfile', 'wx', (err, fd) => {
      if (err) throw err;

      try {
        writeMyData(fd);
      } finally {
        close(fd, (err) => {
          if (err) throw err;
        });
      }
    });
  });
  ```

  **write (RECOMMENDED)**

  ```
  import { open, close } from 'node:fs';

  open('myfile', 'wx', (err, fd) => {
    if (err) {
      if (err.code === 'EEXIST') {
        console.error('myfile already exists');
        return;
      }

      throw err;
    }

    try {
      writeMyData(fd);
    } finally {
      close(fd, (err) => {
        if (err) throw err;
      });
    }
  });
  ```

  **read (NOT RECOMMENDED)**

  ```
  import { access, open, close } from 'node:fs';
  access('myfile', (err) => {
    if (err) {
      if (err.code === 'ENOENT') {
        console.error('myfile does not exist');
        return;
      }

      throw err;
    }

    open('myfile', 'r', (err, fd) => {
      if (err) throw err;

      try {
        readMyData(fd);
      } finally {
        close(fd, (err) => {
          if (err) throw err;
        });
      }
    });
  });
  ```

  **read (RECOMMENDED)**

  ```
  import { open, close } from 'node:fs';

  open('myfile', 'r', (err, fd) => {
    if (err) {
      if (err.code === 'ENOENT') {
        console.error('myfile does not exist');
        return;
      }

      throw err;
    }

    try {
      readMyData(fd);
    } finally {
      close(fd, (err) => {
        if (err) throw err;
      });
    }
  });
  ```

  The "not recommended" examples above check for accessibility and then use the file; the "recommended" examples are better because they use the file directly and handle the error, if any.

  In general, check for the accessibility of a file only if the file will not be used directly, for example when its accessibility is a signal from another process.

  On Windows, access-control policies (ACLs) on a directory may limit access to a file or directory. The `fs.access()` function, however, does not check the ACL and therefore may report that a path is accessible even if the ACL restricts the user from reading or writing to it.

  function [access](https://bun.com/reference/node/fs/access)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously tests a user's permissions for the file specified by path.

  @param path

  A path to a file or directory. If a URL is provided, it must use the `file:` protocol.
* function [accessSync](https://bun.com/reference/node/fs/accessSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode?: number

  ): void;

  Synchronously tests a user's permissions for the file or directory specified by `path`. The `mode` argument is an optional integer that specifies the accessibility checks to be performed. `mode` should be either the value `fs.constants.F_OK` or a mask consisting of the bitwise OR of any of `fs.constants.R_OK`, `fs.constants.W_OK`, and `fs.constants.X_OK` (e.g.`fs.constants.W_OK | fs.constants.R_OK`). Check `File access constants` for possible values of `mode`.

  If any of the accessibility checks fail, an `Error` will be thrown. Otherwise, the method will return `undefined`.

  ```
  import { accessSync, constants } from 'node:fs';

  try {
    accessSync('etc/passwd', constants.R_OK | constants.W_OK);
    console.log('can read/write');
  } catch (err) {
    console.error('no access!');
  }
  ```
* function [appendFile](https://bun.com/reference/node/fs/appendFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

  options: [WriteFileOptions](https://bun.com/reference/node/fs/WriteFileOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously append data to a file, creating the file if it does not yet exist. `data` can be a string or a `Buffer`.

  The `mode` option only affects the newly created file. See open for more details.

  ```
  import { appendFile } from 'node:fs';

  appendFile('message.txt', 'data to append', (err) => {
    if (err) throw err;
    console.log('The "data to append" was appended to file!');
  });
  ```

  If `options` is a string, then it specifies the encoding:

  ```
  import { appendFile } from 'node:fs';

  appendFile('message.txt', 'data to append', 'utf8', callback);
  ```

  The `path` may be specified as a numeric file descriptor that has been opened for appending (using `fs.open()` or `fs.openSync()`). The file descriptor will not be closed automatically.

  ```
  import { open, close, appendFile } from 'node:fs';

  function closeFd(fd) {
    close(fd, (err) => {
      if (err) throw err;
    });
  }

  open('message.txt', 'a', (err, fd) => {
    if (err) throw err;

    try {
      appendFile(fd, 'data to append', 'utf8', (err) => {
        closeFd(fd);
        if (err) throw err;
      });
    } catch (err) {
      closeFd(fd);
      throw err;
    }
  });
  ```

  @param path

  filename or file descriptor

  function [appendFile](https://bun.com/reference/node/fs/appendFile)(

  file: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously append data to a file, creating the file if it does not exist.

  @param file

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param data

  The data to write. If something other than a Buffer or Uint8Array is provided, the value is coerced to a string.
* function [appendFileSync](https://bun.com/reference/node/fs/appendFileSync)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

  options?: [WriteFileOptions](https://bun.com/reference/node/fs/WriteFileOptions)

  ): void;

  Synchronously append data to a file, creating the file if it does not yet exist. `data` can be a string or a `Buffer`.

  The `mode` option only affects the newly created file. See open for more details.

  ```
  import { appendFileSync } from 'node:fs';

  try {
    appendFileSync('message.txt', 'data to append');
    console.log('The "data to append" was appended to file!');
  } catch (err) {
    // Handle the error
  }
  ```

  If `options` is a string, then it specifies the encoding:

  ```
  import { appendFileSync } from 'node:fs';

  appendFileSync('message.txt', 'data to append', 'utf8');
  ```

  The `path` may be specified as a numeric file descriptor that has been opened for appending (using `fs.open()` or `fs.openSync()`). The file descriptor will not be closed automatically.

  ```
  import { openSync, closeSync, appendFileSync } from 'node:fs';

  let fd;

  try {
    fd = openSync('message.txt', 'a');
    appendFileSync(fd, 'data to append', 'utf8');
  } catch (err) {
    // Handle the error
  } finally {
    if (fd !== undefined)
      closeSync(fd);
  }
  ```

  @param path

  filename or file descriptor
* function [chmod](https://bun.com/reference/node/fs/chmod)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode: [Mode](https://bun.com/reference/node/fs/Mode),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously changes the permissions of a file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`chmod(2)`](http://man7.org/linux/man-pages/man2/chmod.2.html) documentation for more detail.

  ```
  import { chmod } from 'node:fs';

  chmod('my_file.txt', 0o775, (err) => {
    if (err) throw err;
    console.log('The permissions for file "my_file.txt" have been changed!');
  });
  ```
* function [chmodSync](https://bun.com/reference/node/fs/chmodSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode: [Mode](https://bun.com/reference/node/fs/Mode)

  ): void;

  For detailed information, see the documentation of the asynchronous version of this API: chmod.

  See the POSIX [`chmod(2)`](http://man7.org/linux/man-pages/man2/chmod.2.html) documentation for more detail.
* function [chown](https://bun.com/reference/node/fs/chown)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously changes owner and group of a file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`chown(2)`](http://man7.org/linux/man-pages/man2/chown.2.html) documentation for more detail.
* function [chownSync](https://bun.com/reference/node/fs/chownSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number

  ): void;

  Synchronously changes owner and group of a file. Returns `undefined`. This is the synchronous version of chown.

  See the POSIX [`chown(2)`](http://man7.org/linux/man-pages/man2/chown.2.html) documentation for more detail.
* function [close](https://bun.com/reference/node/fs/close)(

  fd: number,

  callback?: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Closes the file descriptor. No arguments other than a possible exception are given to the completion callback.

  Calling `fs.close()` on any file descriptor (`fd`) that is currently in use through any other `fs` operation may lead to undefined behavior.

  See the POSIX [`close(2)`](http://man7.org/linux/man-pages/man2/close.2.html) documentation for more detail.
* function [closeSync](https://bun.com/reference/node/fs/closeSync)(

  fd: number

  ): void;

  Closes the file descriptor. Returns `undefined`.

  Calling `fs.closeSync()` on any file descriptor (`fd`) that is currently in use through any other `fs` operation may lead to undefined behavior.

  See the POSIX [`close(2)`](http://man7.org/linux/man-pages/man2/close.2.html) documentation for more detail.
* function [copyFile](https://bun.com/reference/node/fs/copyFile)(

  src: [PathLike](https://bun.com/reference/node/fs/PathLike),

  dest: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously copies `src` to `dest`. By default, `dest` is overwritten if it already exists. No arguments other than a possible exception are given to the callback function. Node.js makes no guarantees about the atomicity of the copy operation. If an error occurs after the destination file has been opened for writing, Node.js will attempt to remove the destination.

  `mode` is an optional integer that specifies the behavior of the copy operation. It is possible to create a mask consisting of the bitwise OR of two or more values (e.g.`fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`).

  + `fs.constants.COPYFILE_EXCL`: The copy operation will fail if `dest` already exists.
  + `fs.constants.COPYFILE_FICLONE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then a fallback copy mechanism is used.
  + `fs.constants.COPYFILE_FICLONE_FORCE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then the operation will fail.

  ```
  import { copyFile, constants } from 'node:fs';

  function callback(err) {
    if (err) throw err;
    console.log('source.txt was copied to destination.txt');
  }

  // destination.txt will be created or overwritten by default.
  copyFile('source.txt', 'destination.txt', callback);

  // By using COPYFILE_EXCL, the operation will fail if destination.txt exists.
  copyFile('source.txt', 'destination.txt', constants.COPYFILE_EXCL, callback);
  ```

  @param src

  source filename to copy

  @param dest

  destination filename of the copy operation

  function [copyFile](https://bun.com/reference/node/fs/copyFile)(

  src: [PathLike](https://bun.com/reference/node/fs/PathLike),

  dest: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously copies `src` to `dest`. By default, `dest` is overwritten if it already exists. No arguments other than a possible exception are given to the callback function. Node.js makes no guarantees about the atomicity of the copy operation. If an error occurs after the destination file has been opened for writing, Node.js will attempt to remove the destination.

  `mode` is an optional integer that specifies the behavior of the copy operation. It is possible to create a mask consisting of the bitwise OR of two or more values (e.g.`fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`).

  + `fs.constants.COPYFILE_EXCL`: The copy operation will fail if `dest` already exists.
  + `fs.constants.COPYFILE_FICLONE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then a fallback copy mechanism is used.
  + `fs.constants.COPYFILE_FICLONE_FORCE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then the operation will fail.

  ```
  import { copyFile, constants } from 'node:fs';

  function callback(err) {
    if (err) throw err;
    console.log('source.txt was copied to destination.txt');
  }

  // destination.txt will be created or overwritten by default.
  copyFile('source.txt', 'destination.txt', callback);

  // By using COPYFILE_EXCL, the operation will fail if destination.txt exists.
  copyFile('source.txt', 'destination.txt', constants.COPYFILE_EXCL, callback);
  ```

  @param src

  source filename to copy

  @param dest

  destination filename of the copy operation

  @param mode

  modifiers for copy operation.
* function [copyFileSync](https://bun.com/reference/node/fs/copyFileSync)(

  src: [PathLike](https://bun.com/reference/node/fs/PathLike),

  dest: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode?: number

  ): void;

  Synchronously copies `src` to `dest`. By default, `dest` is overwritten if it already exists. Returns `undefined`. Node.js makes no guarantees about the atomicity of the copy operation. If an error occurs after the destination file has been opened for writing, Node.js will attempt to remove the destination.

  `mode` is an optional integer that specifies the behavior of the copy operation. It is possible to create a mask consisting of the bitwise OR of two or more values (e.g.`fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`).

  + `fs.constants.COPYFILE_EXCL`: The copy operation will fail if `dest` already exists.
  + `fs.constants.COPYFILE_FICLONE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then a fallback copy mechanism is used.
  + `fs.constants.COPYFILE_FICLONE_FORCE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then the operation will fail.

  ```
  import { copyFileSync, constants } from 'node:fs';

  // destination.txt will be created or overwritten by default.
  copyFileSync('source.txt', 'destination.txt');
  console.log('source.txt was copied to destination.txt');

  // By using COPYFILE_EXCL, the operation will fail if destination.txt exists.
  copyFileSync('source.txt', 'destination.txt', constants.COPYFILE_EXCL);
  ```

  @param src

  source filename to copy

  @param dest

  destination filename of the copy operation

  @param mode

  modifiers for copy operation.
* function [cp](https://bun.com/reference/node/fs/cp)(

  source: string | [URL](https://bun.com/reference/node/url/URL),

  destination: string | [URL](https://bun.com/reference/node/url/URL),

  callback: (err: null | ErrnoException) => void

  ): void;

  Asynchronously copies the entire directory structure from `src` to `dest`, including subdirectories and files.

  When copying a directory to another directory, globs are not supported and behavior is similar to `cp dir1/ dir2/`.

  function [cp](https://bun.com/reference/node/fs/cp)(

  source: string | [URL](https://bun.com/reference/node/url/URL),

  destination: string | [URL](https://bun.com/reference/node/url/URL),

  opts: [CopyOptions](https://bun.com/reference/node/fs/CopyOptions),

  callback: (err: null | ErrnoException) => void

  ): void;

  Asynchronously copies the entire directory structure from `src` to `dest`, including subdirectories and files.

  When copying a directory to another directory, globs are not supported and behavior is similar to `cp dir1/ dir2/`.
* function [cpSync](https://bun.com/reference/node/fs/cpSync)(

  source: string | [URL](https://bun.com/reference/node/url/URL),

  destination: string | [URL](https://bun.com/reference/node/url/URL),

  opts?: [CopySyncOptions](https://bun.com/reference/node/fs/CopySyncOptions)

  ): void;

  Synchronously copies the entire directory structure from `src` to `dest`, including subdirectories and files.

  When copying a directory to another directory, globs are not supported and behavior is similar to `cp dir1/ dir2/`.
* function [createReadStream](https://bun.com/reference/node/fs/createReadStream)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: BufferEncoding | ReadStreamOptions

  ): [ReadStream](https://bun.com/reference/node/fs/ReadStream);

  `options` can include `start` and `end` values to read a range of bytes from the file instead of the entire file. Both `start` and `end` are inclusive and start counting at 0, allowed values are in the [0, [`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)] range. If `fd` is specified and `start` is omitted or `undefined`, `fs.createReadStream()` reads sequentially from the current file position. The `encoding` can be any one of those accepted by `Buffer`.

  If `fd` is specified, `ReadStream` will ignore the `path` argument and will use the specified file descriptor. This means that no `'open'` event will be emitted. `fd` should be blocking; non-blocking `fd`s should be passed to `net.Socket`.

  If `fd` points to a character device that only supports blocking reads (such as keyboard or sound card), read operations do not finish until data is available. This can prevent the process from exiting and the stream from closing naturally.

  By default, the stream will emit a `'close'` event after it has been destroyed. Set the `emitClose` option to `false` to change this behavior.

  By providing the `fs` option, it is possible to override the corresponding `fs` implementations for `open`, `read`, and `close`. When providing the `fs` option, an override for `read` is required. If no `fd` is provided, an override for `open` is also required. If `autoClose` is `true`, an override for `close` is also required.

  ```
  import { createReadStream } from 'node:fs';

  // Create a stream from some character device.
  const stream = createReadStream('/dev/input/event0');
  setTimeout(() => {
    stream.close(); // This may not close the stream.
    // Artificially marking end-of-stream, as if the underlying resource had
    // indicated end-of-file by itself, allows the stream to close.
    // This does not cancel pending read operations, and if there is such an
    // operation, the process may still not be able to exit successfully
    // until it finishes.
    stream.push(null);
    stream.read(0);
  }, 100);
  ```

  If `autoClose` is false, then the file descriptor won't be closed, even if there's an error. It is the application's responsibility to close it and make sure there's no file descriptor leak. If `autoClose` is set to true (default behavior), on `'error'` or `'end'` the file descriptor will be closed automatically.

  `mode` sets the file mode (permission and sticky bits), but only if the file was created.

  An example to read the last 10 bytes of a file which is 100 bytes long:

  ```
  import { createReadStream } from 'node:fs';

  createReadStream('sample.txt', { start: 90, end: 99 });
  ```

  If `options` is a string, then it specifies the encoding.
* function [createWriteStream](https://bun.com/reference/node/fs/createWriteStream)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: BufferEncoding | WriteStreamOptions

  ): [WriteStream](https://bun.com/reference/node/fs/WriteStream);

  `options` may also include a `start` option to allow writing data at some position past the beginning of the file, allowed values are in the [0, [`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)] range. Modifying a file rather than replacing it may require the `flags` option to be set to `r+` rather than the default `w`. The `encoding` can be any one of those accepted by `Buffer`.

  If `autoClose` is set to true (default behavior) on `'error'` or `'finish'` the file descriptor will be closed automatically. If `autoClose` is false, then the file descriptor won't be closed, even if there's an error. It is the application's responsibility to close it and make sure there's no file descriptor leak.

  By default, the stream will emit a `'close'` event after it has been destroyed. Set the `emitClose` option to `false` to change this behavior.

  By providing the `fs` option it is possible to override the corresponding `fs` implementations for `open`, `write`, `writev`, and `close`. Overriding `write()` without `writev()` can reduce performance as some optimizations (`_writev()`) will be disabled. When providing the `fs` option, overrides for at least one of `write` and `writev` are required. If no `fd` option is supplied, an override for `open` is also required. If `autoClose` is `true`, an override for `close` is also required.

  Like `fs.ReadStream`, if `fd` is specified, `fs.WriteStream` will ignore the `path` argument and will use the specified file descriptor. This means that no `'open'` event will be emitted. `fd` should be blocking; non-blocking `fd`s should be passed to `net.Socket`.

  If `options` is a string, then it specifies the encoding.

* function [fchmod](https://bun.com/reference/node/fs/fchmod)(

  fd: number,

  mode: [Mode](https://bun.com/reference/node/fs/Mode),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Sets the permissions on the file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`fchmod(2)`](http://man7.org/linux/man-pages/man2/fchmod.2.html) documentation for more detail.
* function [fchmodSync](https://bun.com/reference/node/fs/fchmodSync)(

  fd: number,

  mode: [Mode](https://bun.com/reference/node/fs/Mode)

  ): void;

  Sets the permissions on the file. Returns `undefined`.

  See the POSIX [`fchmod(2)`](http://man7.org/linux/man-pages/man2/fchmod.2.html) documentation for more detail.
* function [fchown](https://bun.com/reference/node/fs/fchown)(

  fd: number,

  uid: number,

  gid: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Sets the owner of the file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`fchown(2)`](http://man7.org/linux/man-pages/man2/fchown.2.html) documentation for more detail.
* function [fchownSync](https://bun.com/reference/node/fs/fchownSync)(

  fd: number,

  uid: number,

  gid: number

  ): void;

  Sets the owner of the file. Returns `undefined`.

  See the POSIX [`fchown(2)`](http://man7.org/linux/man-pages/man2/fchown.2.html) documentation for more detail.

  @param uid

  The file's new owner's user id.

  @param gid

  The file's new group's group id.
* function [fdatasync](https://bun.com/reference/node/fs/fdatasync)(

  fd: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Forces all currently queued I/O operations associated with the file to the operating system's synchronized I/O completion state. Refer to the POSIX [`fdatasync(2)`](http://man7.org/linux/man-pages/man2/fdatasync.2.html) documentation for details. No arguments other than a possible exception are given to the completion callback.
* function [fdatasyncSync](https://bun.com/reference/node/fs/fdatasyncSync)(

  fd: number

  ): void;

  Forces all currently queued I/O operations associated with the file to the operating system's synchronized I/O completion state. Refer to the POSIX [`fdatasync(2)`](http://man7.org/linux/man-pages/man2/fdatasync.2.html) documentation for details. Returns `undefined`.
* function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  options: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.
* function [fstatSync](https://bun.com/reference/node/fs/fstatSync)(

  fd: number,

  options?: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false }

  ): [Stats](https://bun.com/reference/node/fs/Stats);

  Retrieves the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstatSync](https://bun.com/reference/node/fs/fstatSync)(

  fd: number,

  options: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true }

  ): [BigIntStats](https://bun.com/reference/node/fs/BigIntStats);

  Retrieves the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstatSync](https://bun.com/reference/node/fs/fstatSync)(

  fd: number,

  options?: [StatOptions](https://bun.com/reference/node/fs/StatOptions)

  ): [Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats);

  Retrieves the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.
* function [fsync](https://bun.com/reference/node/fs/fsync)(

  fd: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Request that all data for the open file descriptor is flushed to the storage device. The specific implementation is operating system and device specific. Refer to the POSIX [`fsync(2)`](http://man7.org/linux/man-pages/man2/fsync.2.html) documentation for more detail. No arguments other than a possible exception are given to the completion callback.
* function [fsyncSync](https://bun.com/reference/node/fs/fsyncSync)(

  fd: number

  ): void;

  Request that all data for the open file descriptor is flushed to the storage device. The specific implementation is operating system and device specific. Refer to the POSIX [`fsync(2)`](http://man7.org/linux/man-pages/man2/fsync.2.html) documentation for more detail. Returns `undefined`.
* function [ftruncate](https://bun.com/reference/node/fs/ftruncate)(

  fd: number,

  len?: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Truncates the file descriptor. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`ftruncate(2)`](http://man7.org/linux/man-pages/man2/ftruncate.2.html) documentation for more detail.

  If the file referred to by the file descriptor was larger than `len` bytes, only the first `len` bytes will be retained in the file.

  For example, the following program retains only the first four bytes of the file:

  ```
  import { open, close, ftruncate } from 'node:fs';

  function closeFd(fd) {
    close(fd, (err) => {
      if (err) throw err;
    });
  }

  open('temp.txt', 'r+', (err, fd) => {
    if (err) throw err;

    try {
      ftruncate(fd, 4, (err) => {
        closeFd(fd);
        if (err) throw err;
      });
    } catch (err) {
      closeFd(fd);
      if (err) throw err;
    }
  });
  ```

  If the file previously was shorter than `len` bytes, it is extended, and the extended part is filled with null bytes (`'\0'`):

  If `len` is negative then `0` will be used.

  function [ftruncate](https://bun.com/reference/node/fs/ftruncate)(

  fd: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous ftruncate(2) - Truncate a file to a specified length.

  @param fd

  A file descriptor.
* function [ftruncateSync](https://bun.com/reference/node/fs/ftruncateSync)(

  fd: number,

  len?: number

  ): void;

  Truncates the file descriptor. Returns `undefined`.

  For detailed information, see the documentation of the asynchronous version of this API: ftruncate.
* function [futimes](https://bun.com/reference/node/fs/futimes)(

  fd: number,

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Change the file system timestamps of the object referenced by the supplied file descriptor. See utimes.
* function [futimesSync](https://bun.com/reference/node/fs/futimesSync)(

  fd: number,

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike)

  ): void;

  Synchronous version of futimes. Returns `undefined`.
* function [glob](https://bun.com/reference/node/fs/glob)(

  pattern: string | readonly string[],

  callback: (err: null | ErrnoException, matches: string[]) => void

  ): void;

  Retrieves the files matching the specified pattern.

  ```
  import { glob } from 'node:fs';

  glob('*.js', (err, matches) => {
    if (err) throw err;
    console.log(matches);
  });
  ```

  function [glob](https://bun.com/reference/node/fs/glob)(

  pattern: string | readonly string[],

  options: [GlobOptionsWithFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithFileTypes),

  callback: (err: null | ErrnoException, matches: [Dirent](https://bun.com/reference/node/fs/Dirent)<string>[]) => void

  ): void;

  Retrieves the files matching the specified pattern.

  ```
  import { glob } from 'node:fs';

  glob('*.js', (err, matches) => {
    if (err) throw err;
    console.log(matches);
  });
  ```

  function [glob](https://bun.com/reference/node/fs/glob)(

  pattern: string | readonly string[],

  options: [GlobOptionsWithoutFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithoutFileTypes),

  callback: (err: null | ErrnoException, matches: string[]) => void

  ): void;

  Retrieves the files matching the specified pattern.

  ```
  import { glob } from 'node:fs';

  glob('*.js', (err, matches) => {
    if (err) throw err;
    console.log(matches);
  });
  ```

  function [glob](https://bun.com/reference/node/fs/glob)(

  pattern: string | readonly string[],

  options: [GlobOptions](https://bun.com/reference/node/fs/GlobOptions),

  callback: (err: null | ErrnoException, matches: string[] | [Dirent](https://bun.com/reference/node/fs/Dirent)<string>[]) => void

  ): void;

  Retrieves the files matching the specified pattern.

  ```
  import { glob } from 'node:fs';

  glob('*.js', (err, matches) => {
    if (err) throw err;
    console.log(matches);
  });
  ```
* function [globSync](https://bun.com/reference/node/fs/globSync)(

  pattern: string | readonly string[]

  ): string[];

  ```
  import { globSync } from 'node:fs';

  console.log(globSync('*.js'));
  ```

  @returns

  paths of files that match the pattern.

  function [globSync](https://bun.com/reference/node/fs/globSync)(

  pattern: string | readonly string[],

  options: [GlobOptionsWithFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithFileTypes)

  ): [Dirent](https://bun.com/reference/node/fs/Dirent)<string>[];

  ```
  import { globSync } from 'node:fs';

  console.log(globSync('*.js'));
  ```

  @returns

  paths of files that match the pattern.

  function [globSync](https://bun.com/reference/node/fs/globSync)(

  pattern: string | readonly string[],

  options: [GlobOptionsWithoutFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithoutFileTypes)

  ): string[];

  ```
  import { globSync } from 'node:fs';

  console.log(globSync('*.js'));
  ```

  @returns

  paths of files that match the pattern.

  function [globSync](https://bun.com/reference/node/fs/globSync)(

  pattern: string | readonly string[],

  options: [GlobOptions](https://bun.com/reference/node/fs/GlobOptions)

  ): string[] | [Dirent](https://bun.com/reference/node/fs/Dirent)<string>[];

  ```
  import { globSync } from 'node:fs';

  console.log(globSync('*.js'));
  ```

  @returns

  paths of files that match the pattern.

* function [lchown](https://bun.com/reference/node/fs/lchown)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Set the owner of the symbolic link. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`lchown(2)`](http://man7.org/linux/man-pages/man2/lchown.2.html) documentation for more detail.
* function [lchownSync](https://bun.com/reference/node/fs/lchownSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number

  ): void;

  Set the owner for the path. Returns `undefined`.

  See the POSIX [`lchown(2)`](http://man7.org/linux/man-pages/man2/lchown.2.html) documentation for more details.

  @param uid

  The file's new owner's user id.

  @param gid

  The file's new group's group id.
* function [link](https://bun.com/reference/node/fs/link)(

  existingPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Creates a new link from the `existingPath` to the `newPath`. See the POSIX [`link(2)`](http://man7.org/linux/man-pages/man2/link.2.html) documentation for more detail. No arguments other than a possible exception are given to the completion callback.
* function [linkSync](https://bun.com/reference/node/fs/linkSync)(

  existingPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike)

  ): void;

  Creates a new link from the `existingPath` to the `newPath`. See the POSIX [`link(2)`](http://man7.org/linux/man-pages/man2/link.2.html) documentation for more detail. Returns `undefined`.
* function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.

  function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.

  function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.

  function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.
* function [lutimes](https://bun.com/reference/node/fs/lutimes)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Changes the access and modification times of a file in the same way as utimes, with the difference that if the path refers to a symbolic link, then the link is not dereferenced: instead, the timestamps of the symbolic link itself are changed.

  No arguments other than a possible exception are given to the completion callback.
* function [lutimesSync](https://bun.com/reference/node/fs/lutimesSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike)

  ): void;

  Change the file system timestamps of the symbolic link referenced by `path`. Returns `undefined`, or throws an exception when parameters are incorrect or the operation fails. This is the synchronous version of lutimes.
* function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: true },

  callback: (err: null | ErrnoException, path?: string) => void

  ): void;

  Asynchronously creates a directory.

  The callback is given a possible exception and, if `recursive` is `true`, the first directory path created, `(err[, path])`.`path` can still be `undefined` when `recursive` is `true`, if no directory was created (for instance, if it was previously created).

  The optional `options` argument can be an integer specifying `mode` (permission and sticky bits), or an object with a `mode` property and a `recursive` property indicating whether parent directories should be created. Calling `fs.mkdir()` when `path` is a directory that exists results in an error only when `recursive` is false. If `recursive` is false and the directory exists, an `EEXIST` error occurs.

  ```
  import { mkdir } from 'node:fs';

  // Create ./tmp/a/apple, regardless of whether ./tmp and ./tmp/a exist.
  mkdir('./tmp/a/apple', { recursive: true }, (err) => {
    if (err) throw err;
  });
  ```

  On Windows, using `fs.mkdir()` on the root directory even with recursion will result in an error:

  ```
  import { mkdir } from 'node:fs';

  mkdir('/', { recursive: true }, (err) => {
    // => [Error: EPERM: operation not permitted, mkdir 'C:\']
  });
  ```

  See the POSIX [`mkdir(2)`](http://man7.org/linux/man-pages/man2/mkdir.2.html) documentation for more details.

  function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: false },

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.

  function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions),

  callback: (err: null | ErrnoException, path?: string) => void

  ): void;

  Asynchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.

  function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous mkdir(2) - create a directory with a mode of `0o777`.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.
* function [mkdirSync](https://bun.com/reference/node/fs/mkdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: true }

  ): undefined | string;

  Synchronously creates a directory. Returns `undefined`, or if `recursive` is `true`, the first directory path created. This is the synchronous version of mkdir.

  See the POSIX [`mkdir(2)`](http://man7.org/linux/man-pages/man2/mkdir.2.html) documentation for more details.

  function [mkdirSync](https://bun.com/reference/node/fs/mkdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: false }

  ): void;

  Synchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.

  function [mkdirSync](https://bun.com/reference/node/fs/mkdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions)

  ): undefined | string;

  Synchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.
* function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, folder: string) => void

  ): void;

  Creates a unique temporary directory.

  Generates six random characters to be appended behind a required `prefix` to create a unique temporary directory. Due to platform inconsistencies, avoid trailing `X` characters in `prefix`. Some platforms, notably the BSDs, can return more than six random characters, and replace trailing `X` characters in `prefix` with random characters.

  The created directory path is passed as a string to the callback's second parameter.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use.

  ```
  import { mkdtemp } from 'node:fs';
  import { join } from 'node:path';
  import { tmpdir } from 'node:os';

  mkdtemp(join(tmpdir(), 'foo-'), (err, directory) => {
    if (err) throw err;
    console.log(directory);
    // Prints: /tmp/foo-itXde2 or C:\Users\...\AppData\Local\Temp\foo-itXde2
  });
  ```

  The `fs.mkdtemp()` method will append the six randomly selected characters directly to the `prefix` string. For instance, given a directory `/tmp`, if the intention is to create a temporary directory *within*`/tmp`, the `prefix`must end with a trailing platform-specific path separator (`import { sep } from 'node:path'`).

  ```
  import { tmpdir } from 'node:os';
  import { mkdtemp } from 'node:fs';

  // The parent directory for the new temporary directory
  const tmpDir = tmpdir();

  // This method is *INCORRECT*:
  mkdtemp(tmpDir, (err, directory) => {
    if (err) throw err;
    console.log(directory);
    // Will print something similar to `/tmpabc123`.
    // A new temporary directory is created at the file system root
    // rather than *within* the /tmp directory.
  });

  // This method is *CORRECT*:
  import { sep } from 'node:path';
  mkdtemp(`${tmpDir}${sep}`, (err, directory) => {
    if (err) throw err;
    console.log(directory);
    // Will print something similar to `/tmp/abc123`.
    // A new temporary directory is created within
    // the /tmp directory.
  });
  ```

  function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

  callback: (err: null | ErrnoException, folder: NonSharedBuffer) => void

  ): void;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, folder: string | NonSharedBuffer) => void

  ): void;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  callback: (err: null | ErrnoException, folder: string) => void

  ): void;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.
* function [mkdtempDisposableSync](https://bun.com/reference/node/fs/mkdtempDisposableSync)(

  prefix: string,

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): [DisposableTempDir](https://bun.com/reference/node/fs/DisposableTempDir);

  Returns a disposable object whose `path` property holds the created directory path. When the object is disposed, the directory and its contents will be removed if it still exists. If the directory cannot be deleted, disposal will throw an error. The object has a `remove()` method which will perform the same task.

  <!-- TODO: link MDN docs for disposables once https://github.com/mdn/content/pull/38027 lands -->

  For detailed information, see the documentation of `fs.mkdtemp()`.

  There is no callback-based version of this API because it is designed for use with the `using` syntax.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use.
* function [mkdtempSync](https://bun.com/reference/node/fs/mkdtempSync)(

  prefix: string,

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string;

  Returns the created directory path.

  For detailed information, see the documentation of the asynchronous version of this API: mkdtemp.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use.

  function [mkdtempSync](https://bun.com/reference/node/fs/mkdtempSync)(

  prefix: string,

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): NonSharedBuffer;

  Synchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [mkdtempSync](https://bun.com/reference/node/fs/mkdtempSync)(

  prefix: string,

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string | NonSharedBuffer;

  Synchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.
* function [open](https://bun.com/reference/node/fs/open)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  flags?: [OpenMode](https://bun.com/reference/node/fs/OpenMode),

  mode?: null | [Mode](https://bun.com/reference/node/fs/Mode),

  callback: (err: null | ErrnoException, fd: number) => void

  ): void;

  Asynchronous file open. See the POSIX [`open(2)`](http://man7.org/linux/man-pages/man2/open.2.html) documentation for more details.

  `mode` sets the file mode (permission and sticky bits), but only if the file was created. On Windows, only the write permission can be manipulated; see chmod.

  The callback gets two arguments `(err, fd)`.

  Some characters (`< > : " / \ | ? *`) are reserved under Windows as documented by [Naming Files, Paths, and Namespaces](https://docs.microsoft.com/en-us/windows/desktop/FileIO/naming-a-file). Under NTFS, if the filename contains a colon, Node.js will open a file system stream, as described by [this MSDN page](https://docs.microsoft.com/en-us/windows/desktop/FileIO/using-streams).

  Functions based on `fs.open()` exhibit this behavior as well:`fs.writeFile()`, `fs.readFile()`, etc.

  @param flags

  See `support of file system` flags``.

  function [open](https://bun.com/reference/node/fs/open)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  flags?: [OpenMode](https://bun.com/reference/node/fs/OpenMode),

  callback: (err: null | ErrnoException, fd: number) => void

  ): void;

  Asynchronous open(2) - open and possibly create a file. If the file is created, its mode will be `0o666`.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param flags

  See `support of file system` flags``.

  function [open](https://bun.com/reference/node/fs/open)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, fd: number) => void

  ): void;

  Asynchronous open(2) - open and possibly create a file. If the file is created, its mode will be `0o666`.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.
* function [openAsBlob](https://bun.com/reference/node/fs/openAsBlob)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [OpenAsBlobOptions](https://bun.com/reference/node/fs/OpenAsBlobOptions)

  ): Promise<[Blob](https://bun.com/reference/globals/Blob)>;

  Returns a `Blob` whose data is backed by the given file.

  The file must not be modified after the `Blob` is created. Any modifications will cause reading the `Blob` data to fail with a `DOMException` error. Synchronous stat operations on the file when the `Blob` is created, and before each read in order to detect whether the file data has been modified on disk.

  ```
  import { openAsBlob } from 'node:fs';

  const blob = await openAsBlob('the.file.txt');
  const ab = await blob.arrayBuffer();
  blob.stream();
  ```
* function [opendir](https://bun.com/reference/node/fs/opendir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  cb: (err: null | ErrnoException, dir: [Dir](https://bun.com/reference/node/fs/Dir)) => void

  ): void;

  Asynchronously open a directory. See the POSIX [`opendir(3)`](http://man7.org/linux/man-pages/man3/opendir.3.html) documentation for more details.

  Creates an `fs.Dir`, which contains all further functions for reading from and cleaning up the directory.

  The `encoding` option sets the encoding for the `path` while opening the directory and subsequent read operations.

  function [opendir](https://bun.com/reference/node/fs/opendir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [OpenDirOptions](https://bun.com/reference/node/fs/OpenDirOptions),

  cb: (err: null | ErrnoException, dir: [Dir](https://bun.com/reference/node/fs/Dir)) => void

  ): void;

  Asynchronously open a directory. See the POSIX [`opendir(3)`](http://man7.org/linux/man-pages/man3/opendir.3.html) documentation for more details.

  Creates an `fs.Dir`, which contains all further functions for reading from and cleaning up the directory.

  The `encoding` option sets the encoding for the `path` while opening the directory and subsequent read operations.
* function [opendirSync](https://bun.com/reference/node/fs/opendirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [OpenDirOptions](https://bun.com/reference/node/fs/OpenDirOptions)

  ): [Dir](https://bun.com/reference/node/fs/Dir);

  Synchronously open a directory. See [`opendir(3)`](http://man7.org/linux/man-pages/man3/opendir.3.html).

  Creates an `fs.Dir`, which contains all further functions for reading from and cleaning up the directory.

  The `encoding` option sets the encoding for the `path` while opening the directory and subsequent read operations.
* function [openSync](https://bun.com/reference/node/fs/openSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  flags?: [OpenMode](https://bun.com/reference/node/fs/OpenMode),

  mode?: null | [Mode](https://bun.com/reference/node/fs/Mode)

  ): number;

  Returns an integer representing the file descriptor.

  For detailed information, see the documentation of the asynchronous version of this API: open.
* function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset: number,

  length: number,

  position: null | [ReadPosition](https://bun.com/reference/node/fs/ReadPosition),

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.

  @param buffer

  The buffer that the data will be written to.

  @param offset

  The position in `buffer` to write the data to.

  @param length

  The number of bytes to read.

  @param position

  Specifies where to begin reading from in the file. If `position` is `null` or `-1` , data will be read from the current file position, and the file position will be updated. If `position` is an integer, the file position will be unchanged.

  function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike> = NonSharedBuffer>(

  fd: number,

  options: [ReadOptionsWithBuffer](https://bun.com/reference/node/fs/ReadOptionsWithBuffer)<TBuffer>,

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Similar to the above `fs.read` function, this version takes an optional `options` object. If not otherwise specified in an `options` object, `buffer` defaults to `Buffer.alloc(16384)`, `offset` defaults to `0`, `length` defaults to `buffer.byteLength`, `- offset` as of Node 17.6.0 `position` defaults to `null`

  function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  options: [ReadOptions](https://bun.com/reference/node/fs/ReadOptions),

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.

  @param buffer

  The buffer that the data will be written to.

  function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.

  @param buffer

  The buffer that the data will be written to.

  function [read](https://bun.com/reference/node/fs/read)(

  fd: number,

  callback: (err: null | ErrnoException, bytesRead: number, buffer: NonSharedBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.
* function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | BufferEncoding | { encoding: unknown; recursive: boolean; withFileTypes: false },

  callback: (err: null | ErrnoException, files: string[]) => void

  ): void;

  Reads the contents of a directory. The callback gets two arguments `(err, files)` where `files` is an array of the names of the files in the directory excluding `'.'` and `'..'`.

  See the POSIX [`readdir(3)`](http://man7.org/linux/man-pages/man3/readdir.3.html) documentation for more details.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the filenames passed to the callback. If the `encoding` is set to `'buffer'`, the filenames returned will be passed as `Buffer` objects.

  If `options.withFileTypes` is set to `true`, the `files` array will contain `fs.Dirent` objects.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: 'buffer' | { encoding: 'buffer'; recursive: boolean; withFileTypes: false },

  callback: (err: null | ErrnoException, files: NonSharedBuffer[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: false },

  callback: (err: null | ErrnoException, files: string[] | NonSharedBuffer[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, files: string[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: true },

  callback: (err: null | ErrnoException, files: [Dirent](https://bun.com/reference/node/fs/Dirent)<string>[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  If called with `withFileTypes: true` the result data will be an array of Dirent.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: { encoding: 'buffer'; recursive: boolean; withFileTypes: true },

  callback: (err: null | ErrnoException, files: [Dirent](https://bun.com/reference/node/fs/Dirent)<NonSharedBuffer>[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Must include `withFileTypes: true` and `encoding: 'buffer'`.
* function [readdirSync](https://bun.com/reference/node/fs/readdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | { encoding: unknown; recursive: boolean; withFileTypes: false }

  ): string[];

  Reads the contents of the directory.

  See the POSIX [`readdir(3)`](http://man7.org/linux/man-pages/man3/readdir.3.html) documentation for more details.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the filenames returned. If the `encoding` is set to `'buffer'`, the filenames returned will be passed as `Buffer` objects.

  If `options.withFileTypes` is set to `true`, the result will contain `fs.Dirent` objects.

  function [readdirSync](https://bun.com/reference/node/fs/readdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: 'buffer' | { encoding: 'buffer'; recursive: boolean; withFileTypes: false }

  ): NonSharedBuffer[];

  Synchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdirSync](https://bun.com/reference/node/fs/readdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: false }

  ): string[] | NonSharedBuffer[];

  Synchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdirSync](https://bun.com/reference/node/fs/readdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: true }

  ): [Dirent](https://bun.com/reference/node/fs/Dirent)<string>[];

  Synchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  If called with `withFileTypes: true` the result data will be an array of Dirent.

  function [readdirSync](https://bun.com/reference/node/fs/readdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: { encoding: 'buffer'; recursive: boolean; withFileTypes: true }

  ): [Dirent](https://bun.com/reference/node/fs/Dirent)<NonSharedBuffer>[];

  Synchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Must include `withFileTypes: true` and `encoding: 'buffer'`.
* function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options: undefined | null | { encoding: null; flag: string } & [Abortable](https://bun.com/reference/node/events/default/Abortable),

  callback: (err: null | ErrnoException, data: NonSharedBuffer) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  ```
  import { readFile } from 'node:fs';

  readFile('/etc/passwd', (err, data) => {
    if (err) throw err;
    console.log(data);
  });
  ```

  The callback is passed two arguments `(err, data)`, where `data` is the contents of the file.

  If no encoding is specified, then the raw buffer is returned.

  If `options` is a string, then it specifies the encoding:

  ```
  import { readFile } from 'node:fs';

  readFile('/etc/passwd', 'utf8', callback);
  ```

  When the path is a directory, the behavior of `fs.readFile()` and readFileSync is platform-specific. On macOS, Linux, and Windows, an error will be returned. On FreeBSD, a representation of the directory's contents will be returned.

  ```
  import { readFile } from 'node:fs';

  // macOS, Linux, and Windows
  readFile('<directory>', (err, data) => {
    // => [Error: EISDIR: illegal operation on a directory, read <directory>]
  });

  //  FreeBSD
  readFile('<directory>', (err, data) => {
    // => null, <data>
  });
  ```

  It is possible to abort an ongoing request using an `AbortSignal`. If a request is aborted the callback is called with an `AbortError`:

  ```
  import { readFile } from 'node:fs';

  const controller = new AbortController();
  const signal = controller.signal;
  readFile(fileInfo[0].name, { signal }, (err, buf) => {
    // ...
  });
  // When you want to abort the request
  controller.abort();
  ```

  The `fs.readFile()` function buffers the entire file. To minimize memory costs, when possible prefer streaming via `fs.createReadStream()`.

  Aborting an ongoing request does not abort individual operating system requests but rather the internal buffering `fs.readFile` performs.

  @param path

  filename or file descriptor

  function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options: BufferEncoding | { encoding: BufferEncoding; flag: string } & [Abortable](https://bun.com/reference/node/events/default/Abortable),

  callback: (err: null | ErrnoException, data: string) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param options

  Either the encoding for the result, or an object that contains the encoding and an optional flag. If a flag is not provided, it defaults to `'r'`.

  function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options: undefined | null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { flag: string } & [Abortable](https://bun.com/reference/node/events/default/Abortable),

  callback: (err: null | ErrnoException, data: string | NonSharedBuffer) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param options

  Either the encoding for the result, or an object that contains the encoding and an optional flag. If a flag is not provided, it defaults to `'r'`.

  function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  callback: (err: null | ErrnoException, data: NonSharedBuffer) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.
* function [readFileSync](https://bun.com/reference/node/fs/readFileSync)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options?: null | { encoding: null; flag: string }

  ): NonSharedBuffer;

  Returns the contents of the `path`.

  For detailed information, see the documentation of the asynchronous version of this API: readFile.

  If the `encoding` option is specified then this function returns a string. Otherwise it returns a buffer.

  Similar to readFile, when the path is a directory, the behavior of `fs.readFileSync()` is platform-specific.

  ```
  import { readFileSync } from 'node:fs';

  // macOS, Linux, and Windows
  readFileSync('<directory>');
  // => [Error: EISDIR: illegal operation on a directory, read <directory>]

  //  FreeBSD
  readFileSync('<directory>'); // => <data>
  ```

  @param path

  filename or file descriptor

  function [readFileSync](https://bun.com/reference/node/fs/readFileSync)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options: BufferEncoding | { encoding: BufferEncoding; flag: string }

  ): string;

  Synchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param options

  Either the encoding for the result, or an object that contains the encoding and an optional flag. If a flag is not provided, it defaults to `'r'`.

  function [readFileSync](https://bun.com/reference/node/fs/readFileSync)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { flag: string }

  ): string | NonSharedBuffer;

  Synchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param options

  Either the encoding for the result, or an object that contains the encoding and an optional flag. If a flag is not provided, it defaults to `'r'`.
* function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, linkString: string) => void

  ): void;

  Reads the contents of the symbolic link referred to by `path`. The callback gets two arguments `(err, linkString)`.

  See the POSIX [`readlink(2)`](http://man7.org/linux/man-pages/man2/readlink.2.html) documentation for more details.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the link path passed to the callback. If the `encoding` is set to `'buffer'`, the link path returned will be passed as a `Buffer` object.

  function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

  callback: (err: null | ErrnoException, linkString: NonSharedBuffer) => void

  ): void;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, linkString: string | NonSharedBuffer) => void

  ): void;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, linkString: string) => void

  ): void;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.
* function [readlinkSync](https://bun.com/reference/node/fs/readlinkSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string;

  Returns the symbolic link's string value.

  See the POSIX [`readlink(2)`](http://man7.org/linux/man-pages/man2/readlink.2.html) documentation for more details.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the link path returned. If the `encoding` is set to `'buffer'`, the link path returned will be passed as a `Buffer` object.

  function [readlinkSync](https://bun.com/reference/node/fs/readlinkSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): NonSharedBuffer;

  Synchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readlinkSync](https://bun.com/reference/node/fs/readlinkSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string | NonSharedBuffer;

  Synchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.
* function [readSync](https://bun.com/reference/node/fs/readSync)(

  fd: number,

  buffer: ArrayBufferView,

  offset: number,

  length: number,

  position?: null | [ReadPosition](https://bun.com/reference/node/fs/ReadPosition)

  ): number;

  Returns the number of `bytesRead`.

  For detailed information, see the documentation of the asynchronous version of this API: read.

  function [readSync](https://bun.com/reference/node/fs/readSync)(

  fd: number,

  buffer: ArrayBufferView,

  opts?: [ReadOptions](https://bun.com/reference/node/fs/ReadOptions)

  ): number;

  Similar to the above `fs.readSync` function, this version takes an optional `options` object. If no `options` object is specified, it will default with the above values.
* function [readv](https://bun.com/reference/node/fs/readv)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  cb: (err: null | ErrnoException, bytesRead: number, buffers: TBuffers) => void

  ): void;

  Read from a file specified by `fd` and write to an array of `ArrayBufferView`s using `readv()`.

  `position` is the offset from the beginning of the file from where data should be read. If `typeof position !== 'number'`, the data will be read from the current position.

  The callback will be given three arguments: `err`, `bytesRead`, and `buffers`. `bytesRead` is how many bytes were read from the file.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffers` properties.

  function [readv](https://bun.com/reference/node/fs/readv)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  position: null | number,

  cb: (err: null | ErrnoException, bytesRead: number, buffers: TBuffers) => void

  ): void;

  Read from a file specified by `fd` and write to an array of `ArrayBufferView`s using `readv()`.

  `position` is the offset from the beginning of the file from where data should be read. If `typeof position !== 'number'`, the data will be read from the current position.

  The callback will be given three arguments: `err`, `bytesRead`, and `buffers`. `bytesRead` is how many bytes were read from the file.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffers` properties.
* function [readvSync](https://bun.com/reference/node/fs/readvSync)(

  fd: number,

  buffers: readonly ArrayBufferView<ArrayBufferLike>[],

  position?: number

  ): number;

  For detailed information, see the documentation of the asynchronous version of this API: readv.

  @returns

  The number of bytes read.
* function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: string) => void

  ): void;

  Asynchronously computes the canonical pathname by resolving `.`, `..`, and symbolic links.

  A canonical pathname is not necessarily unique. Hard links and bind mounts can expose a file system entity through many pathnames.

  This function behaves like [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html), with some exceptions:

  1. No case conversion is performed on case-insensitive file systems.
  2. The maximum number of symbolic links is platform-independent and generally (much) higher than what the native [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html) implementation supports.

  The `callback` gets two arguments `(err, resolvedPath)`. May use `process.cwd` to resolve relative paths.

  Only paths that can be converted to UTF8 strings are supported.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

  If `path` resolves to a socket or a pipe, the function will return a system dependent name for that object.

  function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: NonSharedBuffer) => void

  ): void;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: string | NonSharedBuffer) => void

  ): void;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [realpath](https://bun.com/reference/node/fs/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, resolvedPath: string) => void

  ): void;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  function [native](https://bun.com/reference/node/fs/realpath/native)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: string) => void

  ): void;

  Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

  The `callback` gets two arguments `(err, resolvedPath)`.

  Only paths that can be converted to UTF8 strings are supported.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

  On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.

  function [native](https://bun.com/reference/node/fs/realpath/native)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: NonSharedBuffer) => void

  ): void;

  Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

  The `callback` gets two arguments `(err, resolvedPath)`.

  Only paths that can be converted to UTF8 strings are supported.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

  On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.

  function [native](https://bun.com/reference/node/fs/realpath/native)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, resolvedPath: string | NonSharedBuffer) => void

  ): void;

  Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

  The `callback` gets two arguments `(err, resolvedPath)`.

  Only paths that can be converted to UTF8 strings are supported.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

  On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.

  function [native](https://bun.com/reference/node/fs/realpath/native)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, resolvedPath: string) => void

  ): void;

  Asynchronous [`realpath(3)`](http://man7.org/linux/man-pages/man3/realpath.3.html).

  The `callback` gets two arguments `(err, resolvedPath)`.

  Only paths that can be converted to UTF8 strings are supported.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path passed to the callback. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

  On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.
* function [realpathSync](https://bun.com/reference/node/fs/realpathSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string;

  Returns the resolved pathname.

  For detailed information, see the documentation of the asynchronous version of this API: realpath.

  function [realpathSync](https://bun.com/reference/node/fs/realpathSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): NonSharedBuffer;

  Synchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [realpathSync](https://bun.com/reference/node/fs/realpathSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string | NonSharedBuffer;

  Synchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [native](https://bun.com/reference/node/fs/realpathSync/native)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string;

  function [native](https://bun.com/reference/node/fs/realpathSync/native)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): NonSharedBuffer;

  function [native](https://bun.com/reference/node/fs/realpathSync/native)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): string | NonSharedBuffer;
* function [rename](https://bun.com/reference/node/fs/rename)(

  oldPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously rename file at `oldPath` to the pathname provided as `newPath`. In the case that `newPath` already exists, it will be overwritten. If there is a directory at `newPath`, an error will be raised instead. No arguments other than a possible exception are given to the completion callback.

  See also: [`rename(2)`](http://man7.org/linux/man-pages/man2/rename.2.html).

  ```
  import { rename } from 'node:fs';

  rename('oldFile.txt', 'newFile.txt', (err) => {
    if (err) throw err;
    console.log('Rename complete!');
  });
  ```
* function [renameSync](https://bun.com/reference/node/fs/renameSync)(

  oldPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike)

  ): void;

  Renames the file from `oldPath` to `newPath`. Returns `undefined`.

  See the POSIX [`rename(2)`](http://man7.org/linux/man-pages/man2/rename.2.html) documentation for more details.
* function [rm](https://bun.com/reference/node/fs/rm)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously removes files and directories (modeled on the standard POSIX `rm` utility). No arguments other than a possible exception are given to the completion callback.

  function [rm](https://bun.com/reference/node/fs/rm)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [RmOptions](https://bun.com/reference/node/fs/RmOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously removes files and directories (modeled on the standard POSIX `rm` utility). No arguments other than a possible exception are given to the completion callback.
* function [rmdir](https://bun.com/reference/node/fs/rmdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous [`rmdir(2)`](http://man7.org/linux/man-pages/man2/rmdir.2.html). No arguments other than a possible exception are given to the completion callback.

  Using `fs.rmdir()` on a file (not a directory) results in an `ENOENT` error on Windows and an `ENOTDIR` error on POSIX.

  To get a behavior similar to the `rm -rf` Unix command, use rm with options `{ recursive: true, force: true }`.

  function [rmdir](https://bun.com/reference/node/fs/rmdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [RmDirOptions](https://bun.com/reference/node/fs/RmDirOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous [`rmdir(2)`](http://man7.org/linux/man-pages/man2/rmdir.2.html). No arguments other than a possible exception are given to the completion callback.

  Using `fs.rmdir()` on a file (not a directory) results in an `ENOENT` error on Windows and an `ENOTDIR` error on POSIX.

  To get a behavior similar to the `rm -rf` Unix command, use rm with options `{ recursive: true, force: true }`.
* function [rmdirSync](https://bun.com/reference/node/fs/rmdirSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [RmDirOptions](https://bun.com/reference/node/fs/RmDirOptions)

  ): void;

  Synchronous [`rmdir(2)`](http://man7.org/linux/man-pages/man2/rmdir.2.html). Returns `undefined`.

  Using `fs.rmdirSync()` on a file (not a directory) results in an `ENOENT` error on Windows and an `ENOTDIR` error on POSIX.

  To get a behavior similar to the `rm -rf` Unix command, use rmSync with options `{ recursive: true, force: true }`.
* function [rmSync](https://bun.com/reference/node/fs/rmSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [RmOptions](https://bun.com/reference/node/fs/RmOptions)

  ): void;

  Synchronously removes files and directories (modeled on the standard POSIX `rm` utility). Returns `undefined`.
* function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```

  function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```

  function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```

  function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```
* function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, stats: [StatsFs](https://bun.com/reference/node/fs/StatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [StatsFs](https://bun.com/reference/node/fs/StatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions),

  callback: (err: null | ErrnoException, stats: [StatsFs](https://bun.com/reference/node/fs/StatsFs) | [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.
* function [statfsSync](https://bun.com/reference/node/fs/statfsSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: false }

  ): [StatsFs](https://bun.com/reference/node/fs/StatsFs);

  Synchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfsSync](https://bun.com/reference/node/fs/statfsSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: true }

  ): [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs);

  Synchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfsSync](https://bun.com/reference/node/fs/statfsSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions)

  ): [StatsFs](https://bun.com/reference/node/fs/StatsFs) | [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs);

  Synchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.
* function [symlink](https://bun.com/reference/node/fs/symlink)(

  target: [PathLike](https://bun.com/reference/node/fs/PathLike),

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  type?: null | [Type](https://bun.com/reference/node/fs/symlink/Type),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Creates the link called `path` pointing to `target`. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`symlink(2)`](http://man7.org/linux/man-pages/man2/symlink.2.html) documentation for more details.

  The `type` argument is only available on Windows and ignored on other platforms. It can be set to `'dir'`, `'file'`, or `'junction'`. If the `type` argument is not a string, Node.js will autodetect `target` type and use `'file'` or `'dir'`. If the `target` does not exist, `'file'` will be used. Windows junction points require the destination path to be absolute. When using `'junction'`, the`target` argument will automatically be normalized to absolute path. Junction points on NTFS volumes can only point to directories.

  Relative targets are relative to the link's parent directory.

  ```
  import { symlink } from 'node:fs';

  symlink('./mew', './mewtwo', callback);
  ```

  The above example creates a symbolic link `mewtwo` which points to `mew` in the same directory:

  ```
  tree .
  ```

  ```
  .
  ├── mew
  └── mewtwo -> ./mew
  ```

  function [symlink](https://bun.com/reference/node/fs/symlink)(

  target: [PathLike](https://bun.com/reference/node/fs/PathLike),

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous symlink(2) - Create a new symbolic link to an existing file.

  @param target

  A path to an existing file. If a URL is provided, it must use the `file:` protocol.

  @param path

  A path to the new symlink. If a URL is provided, it must use the `file:` protocol.

  type [Type](https://bun.com/reference/node/fs/symlink/Type) = 'dir' | 'file' | 'junction'
* function [symlinkSync](https://bun.com/reference/node/fs/symlinkSync)(

  target: [PathLike](https://bun.com/reference/node/fs/PathLike),

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  type?: null | [Type](https://bun.com/reference/node/fs/symlink/Type)

  ): void;

  Returns `undefined`.

  For detailed information, see the documentation of the asynchronous version of this API: symlink.
* function [truncate](https://bun.com/reference/node/fs/truncate)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous truncate(2) - Truncate a file to a specified length.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.
* function [unlink](https://bun.com/reference/node/fs/unlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously removes a file or symbolic link. No arguments other than a possible exception are given to the completion callback.

  ```
  import { unlink } from 'node:fs';
  // Assuming that 'path/file.txt' is a regular file.
  unlink('path/file.txt', (err) => {
    if (err) throw err;
    console.log('path/file.txt was deleted');
  });
  ```

  `fs.unlink()` will not work on a directory, empty or otherwise. To remove a directory, use rmdir.

  See the POSIX [`unlink(2)`](http://man7.org/linux/man-pages/man2/unlink.2.html) documentation for more details.
* function [unlinkSync](https://bun.com/reference/node/fs/unlinkSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike)

  ): void;

  Synchronous [`unlink(2)`](http://man7.org/linux/man-pages/man2/unlink.2.html). Returns `undefined`.
* function [unwatchFile](https://bun.com/reference/node/fs/unwatchFile)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  listener?: [StatsListener](https://bun.com/reference/node/fs/StatsListener)

  ): void;

  Stop watching for changes on `filename`. If `listener` is specified, only that particular listener is removed. Otherwise, *all* listeners are removed, effectively stopping watching of `filename`.

  Calling `fs.unwatchFile()` with a filename that is not being watched is a no-op, not an error.

  Using watch is more efficient than `fs.watchFile()` and `fs.unwatchFile()`. `fs.watch()` should be used instead of `fs.watchFile()` and `fs.unwatchFile()` when possible.

  @param listener

  Optional, a listener previously attached using `fs.watchFile()`

  function [unwatchFile](https://bun.com/reference/node/fs/unwatchFile)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  listener?: [BigIntStatsListener](https://bun.com/reference/node/fs/BigIntStatsListener)

  ): void;

  Stop watching for changes on `filename`. If `listener` is specified, only that particular listener is removed. Otherwise, *all* listeners are removed, effectively stopping watching of `filename`.

  Calling `fs.unwatchFile()` with a filename that is not being watched is a no-op, not an error.

  Using watch is more efficient than `fs.watchFile()` and `fs.unwatchFile()`. `fs.watch()` should be used instead of `fs.watchFile()` and `fs.unwatchFile()` when possible.

  @param listener

  Optional, a listener previously attached using `fs.watchFile()`
* function [utimes](https://bun.com/reference/node/fs/utimes)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Change the file system timestamps of the object referenced by `path`.

  The `atime` and `mtime` arguments follow these rules:

  + Values can be either numbers representing Unix epoch time in seconds, `Date`s, or a numeric string like `'123456789.0'`.
  + If the value can not be converted to a number, or is `NaN`, `Infinity`, or `-Infinity`, an `Error` will be thrown.
* function [utimesSync](https://bun.com/reference/node/fs/utimesSync)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike)

  ): void;

  Returns `undefined`.

  For detailed information, see the documentation of the asynchronous version of this API: utimes.
* function [watch](https://bun.com/reference/node/fs/watch)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | [WatchOptionsWithStringEncoding](https://bun.com/reference/node/fs/WatchOptionsWithStringEncoding),

  listener?: [WatchListener](https://bun.com/reference/node/fs/WatchListener)<string>

  ): [FSWatcher](https://bun.com/reference/node/fs/FSWatcher);

  Watch for changes on `filename`, where `filename` is either a file or a directory.

  The second argument is optional. If `options` is provided as a string, it specifies the `encoding`. Otherwise `options` should be passed as an object.

  The listener callback gets two arguments `(eventType, filename)`. `eventType`is either `'rename'` or `'change'`, and `filename` is the name of the file which triggered the event.

  On most platforms, `'rename'` is emitted whenever a filename appears or disappears in the directory.

  The listener callback is attached to the `'change'` event fired by `fs.FSWatcher`, but it is not the same thing as the `'change'` value of `eventType`.

  If a `signal` is passed, aborting the corresponding AbortController will close the returned `fs.FSWatcher`.

  function [watch](https://bun.com/reference/node/fs/watch)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: 'buffer' | [WatchOptionsWithBufferEncoding](https://bun.com/reference/node/fs/WatchOptionsWithBufferEncoding),

  listener: [WatchListener](https://bun.com/reference/node/fs/WatchListener)<NonSharedBuffer>

  ): [FSWatcher](https://bun.com/reference/node/fs/FSWatcher);

  Watch for changes on `filename`, where `filename` is either a file or a directory.

  The second argument is optional. If `options` is provided as a string, it specifies the `encoding`. Otherwise `options` should be passed as an object.

  The listener callback gets two arguments `(eventType, filename)`. `eventType`is either `'rename'` or `'change'`, and `filename` is the name of the file which triggered the event.

  On most platforms, `'rename'` is emitted whenever a filename appears or disappears in the directory.

  The listener callback is attached to the `'change'` event fired by `fs.FSWatcher`, but it is not the same thing as the `'change'` value of `eventType`.

  If a `signal` is passed, aborting the corresponding AbortController will close the returned `fs.FSWatcher`.

  function [watch](https://bun.com/reference/node/fs/watch)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: null | BufferEncoding | 'buffer' | [WatchOptions](https://bun.com/reference/node/fs/WatchOptions),

  listener: [WatchListener](https://bun.com/reference/node/fs/WatchListener)<string | NonSharedBuffer>

  ): [FSWatcher](https://bun.com/reference/node/fs/FSWatcher);

  Watch for changes on `filename`, where `filename` is either a file or a directory.

  The second argument is optional. If `options` is provided as a string, it specifies the `encoding`. Otherwise `options` should be passed as an object.

  The listener callback gets two arguments `(eventType, filename)`. `eventType`is either `'rename'` or `'change'`, and `filename` is the name of the file which triggered the event.

  On most platforms, `'rename'` is emitted whenever a filename appears or disappears in the directory.

  The listener callback is attached to the `'change'` event fired by `fs.FSWatcher`, but it is not the same thing as the `'change'` value of `eventType`.

  If a `signal` is passed, aborting the corresponding AbortController will close the returned `fs.FSWatcher`.

  function [watch](https://bun.com/reference/node/fs/watch)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  listener: [WatchListener](https://bun.com/reference/node/fs/WatchListener)<string>

  ): [FSWatcher](https://bun.com/reference/node/fs/FSWatcher);

  Watch for changes on `filename`, where `filename` is either a file or a directory.

  The second argument is optional. If `options` is provided as a string, it specifies the `encoding`. Otherwise `options` should be passed as an object.

  The listener callback gets two arguments `(eventType, filename)`. `eventType`is either `'rename'` or `'change'`, and `filename` is the name of the file which triggered the event.

  On most platforms, `'rename'` is emitted whenever a filename appears or disappears in the directory.

  The listener callback is attached to the `'change'` event fired by `fs.FSWatcher`, but it is not the same thing as the `'change'` value of `eventType`.

  If a `signal` is passed, aborting the corresponding AbortController will close the returned `fs.FSWatcher`.
* function [watchFile](https://bun.com/reference/node/fs/watchFile)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [WatchFileOptions](https://bun.com/reference/node/fs/WatchFileOptions) & { bigint: false },

  listener: [StatsListener](https://bun.com/reference/node/fs/StatsListener)

  ): [StatWatcher](https://bun.com/reference/node/fs/StatWatcher);

  Watch for changes on `filename`. The callback `listener` will be called each time the file is accessed.

  The `options` argument may be omitted. If provided, it should be an object. The `options` object may contain a boolean named `persistent` that indicates whether the process should continue to run as long as files are being watched. The `options` object may specify an `interval` property indicating how often the target should be polled in milliseconds.

  The `listener` gets two arguments the current stat object and the previous stat object:

  ```
  import { watchFile } from 'node:fs';

  watchFile('message.text', (curr, prev) => {
    console.log(`the current mtime is: ${curr.mtime}`);
    console.log(`the previous mtime was: ${prev.mtime}`);
  });
  ```

  These stat objects are instances of `fs.Stat`. If the `bigint` option is `true`, the numeric values in these objects are specified as `BigInt`s.

  To be notified when the file was modified, not just accessed, it is necessary to compare `curr.mtimeMs` and `prev.mtimeMs`.

  When an `fs.watchFile` operation results in an `ENOENT` error, it will invoke the listener once, with all the fields zeroed (or, for dates, the Unix Epoch). If the file is created later on, the listener will be called again, with the latest stat objects. This is a change in functionality since v0.10.

  Using watch is more efficient than `fs.watchFile` and `fs.unwatchFile`. `fs.watch` should be used instead of `fs.watchFile` and `fs.unwatchFile` when possible.

  When a file being watched by `fs.watchFile()` disappears and reappears, then the contents of `previous` in the second callback event (the file's reappearance) will be the same as the contents of `previous` in the first callback event (its disappearance).

  This happens when:

  + the file is deleted, followed by a restore
  + the file is renamed and then renamed a second time back to its original name

  function [watchFile](https://bun.com/reference/node/fs/watchFile)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [WatchFileOptions](https://bun.com/reference/node/fs/WatchFileOptions) & { bigint: true },

  listener: [BigIntStatsListener](https://bun.com/reference/node/fs/BigIntStatsListener)

  ): [StatWatcher](https://bun.com/reference/node/fs/StatWatcher);

  Watch for changes on `filename`. The callback `listener` will be called each time the file is accessed.

  The `options` argument may be omitted. If provided, it should be an object. The `options` object may contain a boolean named `persistent` that indicates whether the process should continue to run as long as files are being watched. The `options` object may specify an `interval` property indicating how often the target should be polled in milliseconds.

  The `listener` gets two arguments the current stat object and the previous stat object:

  ```
  import { watchFile } from 'node:fs';

  watchFile('message.text', (curr, prev) => {
    console.log(`the current mtime is: ${curr.mtime}`);
    console.log(`the previous mtime was: ${prev.mtime}`);
  });
  ```

  These stat objects are instances of `fs.Stat`. If the `bigint` option is `true`, the numeric values in these objects are specified as `BigInt`s.

  To be notified when the file was modified, not just accessed, it is necessary to compare `curr.mtimeMs` and `prev.mtimeMs`.

  When an `fs.watchFile` operation results in an `ENOENT` error, it will invoke the listener once, with all the fields zeroed (or, for dates, the Unix Epoch). If the file is created later on, the listener will be called again, with the latest stat objects. This is a change in functionality since v0.10.

  Using watch is more efficient than `fs.watchFile` and `fs.unwatchFile`. `fs.watch` should be used instead of `fs.watchFile` and `fs.unwatchFile` when possible.

  When a file being watched by `fs.watchFile()` disappears and reappears, then the contents of `previous` in the second callback event (the file's reappearance) will be the same as the contents of `previous` in the first callback event (its disappearance).

  This happens when:

  + the file is deleted, followed by a restore
  + the file is renamed and then renamed a second time back to its original name

  function [watchFile](https://bun.com/reference/node/fs/watchFile)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  listener: [StatsListener](https://bun.com/reference/node/fs/StatsListener)

  ): [StatWatcher](https://bun.com/reference/node/fs/StatWatcher);

  Watch for changes on `filename`. The callback `listener` will be called each time the file is accessed.

  @param filename

  A path to a file or directory. If a URL is provided, it must use the `file:` protocol.
* function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset?: null | number,

  length?: null | number,

  position?: null | number,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Write `buffer` to the file specified by `fd`.

  `offset` determines the part of the buffer to be written, and `length` is an integer specifying the number of bytes to write.

  `position` refers to the offset from the beginning of the file where this data should be written. If `typeof position !== 'number'`, the data will be written at the current position. See [`pwrite(2)`](http://man7.org/linux/man-pages/man2/pwrite.2.html).

  The callback will be given three arguments `(err, bytesWritten, buffer)` where `bytesWritten` specifies how many *bytes* were written from `buffer`.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesWritten` and `buffer` properties.

  It is unsafe to use `fs.write()` multiple times on the same file without waiting for the callback. For this scenario, createWriteStream is recommended.

  On Linux, positional writes don't work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset: undefined | null | number,

  length: undefined | null | number,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param offset

  The part of the buffer to be written. If not supplied, defaults to `0`.

  @param length

  The number of bytes to write. If not supplied, defaults to `buffer.length - offset`.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset: undefined | null | number,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param offset

  The part of the buffer to be written. If not supplied, defaults to `0`.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  options: [WriteOptions](https://bun.com/reference/node/fs/WriteOptions),

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param options

  An object with the following properties:

  + `offset` The part of the buffer to be written. If not supplied, defaults to `0`.
  + `length` The number of bytes to write. If not supplied, defaults to `buffer.length - offset`.
  + `position` The offset from the beginning of the file where this data should be written. If not supplied, defaults to the current position.

  function [write](https://bun.com/reference/node/fs/write)(

  fd: number,

  string: string,

  position: undefined | null | number,

  encoding: undefined | null | BufferEncoding,

  callback: (err: null | ErrnoException, written: number, str: string) => void

  ): void;

  Asynchronously writes `string` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param string

  A string to write.

  @param position

  The offset from the beginning of the file where this data should be written. If not supplied, defaults to the current position.

  @param encoding

  The expected string encoding.

  function [write](https://bun.com/reference/node/fs/write)(

  fd: number,

  string: string,

  position: undefined | null | number,

  callback: (err: null | ErrnoException, written: number, str: string) => void

  ): void;

  Asynchronously writes `string` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param string

  A string to write.

  @param position

  The offset from the beginning of the file where this data should be written. If not supplied, defaults to the current position.

  function [write](https://bun.com/reference/node/fs/write)(

  fd: number,

  string: string,

  callback: (err: null | ErrnoException, written: number, str: string) => void

  ): void;

  Asynchronously writes `string` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param string

  A string to write.
* function [writeFile](https://bun.com/reference/node/fs/writeFile)(

  file: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | ArrayBufferView<ArrayBufferLike>,

  options: [WriteFileOptions](https://bun.com/reference/node/fs/WriteFileOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  When `file` is a filename, asynchronously writes data to the file, replacing the file if it already exists. `data` can be a string or a buffer.

  When `file` is a file descriptor, the behavior is similar to calling `fs.write()` directly (which is recommended). See the notes below on using a file descriptor.

  The `encoding` option is ignored if `data` is a buffer.

  The `mode` option only affects the newly created file. See open for more details.

  ```
  import { writeFile } from 'node:fs';
  import { Buffer } from 'node:buffer';

  const data = new Uint8Array(Buffer.from('Hello Node.js'));
  writeFile('message.txt', data, (err) => {
    if (err) throw err;
    console.log('The file has been saved!');
  });
  ```

  If `options` is a string, then it specifies the encoding:

  ```
  import { writeFile } from 'node:fs';

  writeFile('message.txt', 'Hello Node.js', 'utf8', callback);
  ```

  It is unsafe to use `fs.writeFile()` multiple times on the same file without waiting for the callback. For this scenario, createWriteStream is recommended.

  Similarly to `fs.readFile` - `fs.writeFile` is a convenience method that performs multiple `write` calls internally to write the buffer passed to it. For performance sensitive code consider using createWriteStream.

  It is possible to use an `AbortSignal` to cancel an `fs.writeFile()`. Cancelation is "best effort", and some amount of data is likely still to be written.

  ```
  import { writeFile } from 'node:fs';
  import { Buffer } from 'node:buffer';

  const controller = new AbortController();
  const { signal } = controller;
  const data = new Uint8Array(Buffer.from('Hello Node.js'));
  writeFile('message.txt', data, { signal }, (err) => {
    // When a request is aborted - the callback is called with an AbortError
  });
  // When the request should be aborted
  controller.abort();
  ```

  Aborting an ongoing request does not abort individual operating system requests but rather the internal buffering `fs.writeFile` performs.

  @param file

  filename or file descriptor

  function [writeFile](https://bun.com/reference/node/fs/writeFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | ArrayBufferView<ArrayBufferLike>,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously writes data to a file, replacing the file if it already exists.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param data

  The data to write. If something other than a Buffer or Uint8Array is provided, the value is coerced to a string.
* function [writeFileSync](https://bun.com/reference/node/fs/writeFileSync)(

  file: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | ArrayBufferView<ArrayBufferLike>,

  options?: [WriteFileOptions](https://bun.com/reference/node/fs/WriteFileOptions)

  ): void;

  Returns `undefined`.

  The `mode` option only affects the newly created file. See open for more details.

  For detailed information, see the documentation of the asynchronous version of this API: writeFile.

  @param file

  filename or file descriptor
* function [writeSync](https://bun.com/reference/node/fs/writeSync)(

  fd: number,

  buffer: ArrayBufferView,

  offset?: null | number,

  length?: null | number,

  position?: null | number

  ): number;

  For detailed information, see the documentation of the asynchronous version of this API: write.

  @returns

  The number of bytes written.

  function [writeSync](https://bun.com/reference/node/fs/writeSync)(

  fd: number,

  string: string,

  position?: null | number,

  encoding?: null | BufferEncoding

  ): number;

  Synchronously writes `string` to the file referenced by the supplied file descriptor, returning the number of bytes written.

  @param fd

  A file descriptor.

  @param string

  A string to write.

  @param position

  The offset from the beginning of the file where this data should be written. If not supplied, defaults to the current position.

  @param encoding

  The expected string encoding.
* function [writev](https://bun.com/reference/node/fs/writev)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  cb: (err: null | ErrnoException, bytesWritten: number, buffers: TBuffers) => void

  ): void;

  Write an array of `ArrayBufferView`s to the file specified by `fd` using `writev()`.

  `position` is the offset from the beginning of the file where this data should be written. If `typeof position !== 'number'`, the data will be written at the current position.

  The callback will be given three arguments: `err`, `bytesWritten`, and `buffers`. `bytesWritten` is how many bytes were written from `buffers`.

  If this method is `util.promisify()` ed, it returns a promise for an `Object` with `bytesWritten` and `buffers` properties.

  It is unsafe to use `fs.writev()` multiple times on the same file without waiting for the callback. For this scenario, use createWriteStream.

  On Linux, positional writes don't work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.

  function [writev](https://bun.com/reference/node/fs/writev)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  position: null | number,

  cb: (err: null | ErrnoException, bytesWritten: number, buffers: TBuffers) => void

  ): void;

  Write an array of `ArrayBufferView`s to the file specified by `fd` using `writev()`.

  `position` is the offset from the beginning of the file where this data should be written. If `typeof position !== 'number'`, the data will be written at the current position.

  The callback will be given three arguments: `err`, `bytesWritten`, and `buffers`. `bytesWritten` is how many bytes were written from `buffers`.

  If this method is `util.promisify()` ed, it returns a promise for an `Object` with `bytesWritten` and `buffers` properties.

  It is unsafe to use `fs.writev()` multiple times on the same file without waiting for the callback. For this scenario, use createWriteStream.

  On Linux, positional writes don't work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.
* function [writevSync](https://bun.com/reference/node/fs/writevSync)(

  fd: number,

  buffers: readonly ArrayBufferView<ArrayBufferLike>[],

  position?: number

  ): number;

  For detailed information, see the documentation of the asynchronous version of this API: writev.

  @returns

  The number of bytes written.

## Type definitions

* function [access](https://bun.com/reference/node/fs/access)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode?: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Tests a user's permissions for the file or directory specified by `path`. The `mode` argument is an optional integer that specifies the accessibility checks to be performed. `mode` should be either the value `fs.constants.F_OK` or a mask consisting of the bitwise OR of any of `fs.constants.R_OK`, `fs.constants.W_OK`, and `fs.constants.X_OK` (e.g.`fs.constants.W_OK | fs.constants.R_OK`). Check `File access constants` for possible values of `mode`.

  The final argument, `callback`, is a callback function that is invoked with a possible error argument. If any of the accessibility checks fail, the error argument will be an `Error` object. The following examples check if `package.json` exists, and if it is readable or writable.

  ```
  import { access, constants } from 'node:fs';

  const file = 'package.json';

  // Check if the file exists in the current directory.
  access(file, constants.F_OK, (err) => {
    console.log(`${file} ${err ? 'does not exist' : 'exists'}`);
  });

  // Check if the file is readable.
  access(file, constants.R_OK, (err) => {
    console.log(`${file} ${err ? 'is not readable' : 'is readable'}`);
  });

  // Check if the file is writable.
  access(file, constants.W_OK, (err) => {
    console.log(`${file} ${err ? 'is not writable' : 'is writable'}`);
  });

  // Check if the file is readable and writable.
  access(file, constants.R_OK | constants.W_OK, (err) => {
    console.log(`${file} ${err ? 'is not' : 'is'} readable and writable`);
  });
  ```

  Do not use `fs.access()` to check for the accessibility of a file before calling `fs.open()`, `fs.readFile()`, or `fs.writeFile()`. Doing so introduces a race condition, since other processes may change the file's state between the two calls. Instead, user code should open/read/write the file directly and handle the error raised if the file is not accessible.

  **write (NOT RECOMMENDED)**

  ```
  import { access, open, close } from 'node:fs';

  access('myfile', (err) => {
    if (!err) {
      console.error('myfile already exists');
      return;
    }

    open('myfile', 'wx', (err, fd) => {
      if (err) throw err;

      try {
        writeMyData(fd);
      } finally {
        close(fd, (err) => {
          if (err) throw err;
        });
      }
    });
  });
  ```

  **write (RECOMMENDED)**

  ```
  import { open, close } from 'node:fs';

  open('myfile', 'wx', (err, fd) => {
    if (err) {
      if (err.code === 'EEXIST') {
        console.error('myfile already exists');
        return;
      }

      throw err;
    }

    try {
      writeMyData(fd);
    } finally {
      close(fd, (err) => {
        if (err) throw err;
      });
    }
  });
  ```

  **read (NOT RECOMMENDED)**

  ```
  import { access, open, close } from 'node:fs';
  access('myfile', (err) => {
    if (err) {
      if (err.code === 'ENOENT') {
        console.error('myfile does not exist');
        return;
      }

      throw err;
    }

    open('myfile', 'r', (err, fd) => {
      if (err) throw err;

      try {
        readMyData(fd);
      } finally {
        close(fd, (err) => {
          if (err) throw err;
        });
      }
    });
  });
  ```

  **read (RECOMMENDED)**

  ```
  import { open, close } from 'node:fs';

  open('myfile', 'r', (err, fd) => {
    if (err) {
      if (err.code === 'ENOENT') {
        console.error('myfile does not exist');
        return;
      }

      throw err;
    }

    try {
      readMyData(fd);
    } finally {
      close(fd, (err) => {
        if (err) throw err;
      });
    }
  });
  ```

  The "not recommended" examples above check for accessibility and then use the file; the "recommended" examples are better because they use the file directly and handle the error, if any.

  In general, check for the accessibility of a file only if the file will not be used directly, for example when its accessibility is a signal from another process.

  On Windows, access-control policies (ACLs) on a directory may limit access to a file or directory. The `fs.access()` function, however, does not check the ACL and therefore may report that a path is accessible even if the ACL restricts the user from reading or writing to it.

  function [access](https://bun.com/reference/node/fs/access)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously tests a user's permissions for the file specified by path.

  @param path

  A path to a file or directory. If a URL is provided, it must use the `file:` protocol.

  ### namespace [access](https://bun.com/reference/node/fs/access)
* function [appendFile](https://bun.com/reference/node/fs/appendFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

  options: [WriteFileOptions](https://bun.com/reference/node/fs/WriteFileOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously append data to a file, creating the file if it does not yet exist. `data` can be a string or a `Buffer`.

  The `mode` option only affects the newly created file. See open for more details.

  ```
  import { appendFile } from 'node:fs';

  appendFile('message.txt', 'data to append', (err) => {
    if (err) throw err;
    console.log('The "data to append" was appended to file!');
  });
  ```

  If `options` is a string, then it specifies the encoding:

  ```
  import { appendFile } from 'node:fs';

  appendFile('message.txt', 'data to append', 'utf8', callback);
  ```

  The `path` may be specified as a numeric file descriptor that has been opened for appending (using `fs.open()` or `fs.openSync()`). The file descriptor will not be closed automatically.

  ```
  import { open, close, appendFile } from 'node:fs';

  function closeFd(fd) {
    close(fd, (err) => {
      if (err) throw err;
    });
  }

  open('message.txt', 'a', (err, fd) => {
    if (err) throw err;

    try {
      appendFile(fd, 'data to append', 'utf8', (err) => {
        closeFd(fd);
        if (err) throw err;
      });
    } catch (err) {
      closeFd(fd);
      throw err;
    }
  });
  ```

  @param path

  filename or file descriptor

  function [appendFile](https://bun.com/reference/node/fs/appendFile)(

  file: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously append data to a file, creating the file if it does not exist.

  @param file

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param data

  The data to write. If something other than a Buffer or Uint8Array is provided, the value is coerced to a string.

  ### namespace [appendFile](https://bun.com/reference/node/fs/appendFile)
* function [chmod](https://bun.com/reference/node/fs/chmod)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode: [Mode](https://bun.com/reference/node/fs/Mode),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously changes the permissions of a file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`chmod(2)`](http://man7.org/linux/man-pages/man2/chmod.2.html) documentation for more detail.

  ```
  import { chmod } from 'node:fs';

  chmod('my_file.txt', 0o775, (err) => {
    if (err) throw err;
    console.log('The permissions for file "my_file.txt" have been changed!');
  });
  ```

  ### namespace [chmod](https://bun.com/reference/node/fs/chmod)
* function [chown](https://bun.com/reference/node/fs/chown)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously changes owner and group of a file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`chown(2)`](http://man7.org/linux/man-pages/man2/chown.2.html) documentation for more detail.

  ### namespace [chown](https://bun.com/reference/node/fs/chown)
* function [close](https://bun.com/reference/node/fs/close)(

  fd: number,

  callback?: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Closes the file descriptor. No arguments other than a possible exception are given to the completion callback.

  Calling `fs.close()` on any file descriptor (`fd`) that is currently in use through any other `fs` operation may lead to undefined behavior.

  See the POSIX [`close(2)`](http://man7.org/linux/man-pages/man2/close.2.html) documentation for more detail.

  ### namespace [close](https://bun.com/reference/node/fs/close)
* function [copyFile](https://bun.com/reference/node/fs/copyFile)(

  src: [PathLike](https://bun.com/reference/node/fs/PathLike),

  dest: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously copies `src` to `dest`. By default, `dest` is overwritten if it already exists. No arguments other than a possible exception are given to the callback function. Node.js makes no guarantees about the atomicity of the copy operation. If an error occurs after the destination file has been opened for writing, Node.js will attempt to remove the destination.

  `mode` is an optional integer that specifies the behavior of the copy operation. It is possible to create a mask consisting of the bitwise OR of two or more values (e.g.`fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`).

  + `fs.constants.COPYFILE_EXCL`: The copy operation will fail if `dest` already exists.
  + `fs.constants.COPYFILE_FICLONE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then a fallback copy mechanism is used.
  + `fs.constants.COPYFILE_FICLONE_FORCE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then the operation will fail.

  ```
  import { copyFile, constants } from 'node:fs';

  function callback(err) {
    if (err) throw err;
    console.log('source.txt was copied to destination.txt');
  }

  // destination.txt will be created or overwritten by default.
  copyFile('source.txt', 'destination.txt', callback);

  // By using COPYFILE_EXCL, the operation will fail if destination.txt exists.
  copyFile('source.txt', 'destination.txt', constants.COPYFILE_EXCL, callback);
  ```

  @param src

  source filename to copy

  @param dest

  destination filename of the copy operation

  function [copyFile](https://bun.com/reference/node/fs/copyFile)(

  src: [PathLike](https://bun.com/reference/node/fs/PathLike),

  dest: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously copies `src` to `dest`. By default, `dest` is overwritten if it already exists. No arguments other than a possible exception are given to the callback function. Node.js makes no guarantees about the atomicity of the copy operation. If an error occurs after the destination file has been opened for writing, Node.js will attempt to remove the destination.

  `mode` is an optional integer that specifies the behavior of the copy operation. It is possible to create a mask consisting of the bitwise OR of two or more values (e.g.`fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`).

  + `fs.constants.COPYFILE_EXCL`: The copy operation will fail if `dest` already exists.
  + `fs.constants.COPYFILE_FICLONE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then a fallback copy mechanism is used.
  + `fs.constants.COPYFILE_FICLONE_FORCE`: The copy operation will attempt to create a copy-on-write reflink. If the platform does not support copy-on-write, then the operation will fail.

  ```
  import { copyFile, constants } from 'node:fs';

  function callback(err) {
    if (err) throw err;
    console.log('source.txt was copied to destination.txt');
  }

  // destination.txt will be created or overwritten by default.
  copyFile('source.txt', 'destination.txt', callback);

  // By using COPYFILE_EXCL, the operation will fail if destination.txt exists.
  copyFile('source.txt', 'destination.txt', constants.COPYFILE_EXCL, callback);
  ```

  @param src

  source filename to copy

  @param dest

  destination filename of the copy operation

  @param mode

  modifiers for copy operation.

  ### namespace [copyFile](https://bun.com/reference/node/fs/copyFile)
* function [fchmod](https://bun.com/reference/node/fs/fchmod)(

  fd: number,

  mode: [Mode](https://bun.com/reference/node/fs/Mode),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Sets the permissions on the file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`fchmod(2)`](http://man7.org/linux/man-pages/man2/fchmod.2.html) documentation for more detail.

  ### namespace [fchmod](https://bun.com/reference/node/fs/fchmod)
* function [fchown](https://bun.com/reference/node/fs/fchown)(

  fd: number,

  uid: number,

  gid: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Sets the owner of the file. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`fchown(2)`](http://man7.org/linux/man-pages/man2/fchown.2.html) documentation for more detail.

  ### namespace [fchown](https://bun.com/reference/node/fs/fchown)
* function [fdatasync](https://bun.com/reference/node/fs/fdatasync)(

  fd: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Forces all currently queued I/O operations associated with the file to the operating system's synchronized I/O completion state. Refer to the POSIX [`fdatasync(2)`](http://man7.org/linux/man-pages/man2/fdatasync.2.html) documentation for details. No arguments other than a possible exception are given to the completion callback.

  ### namespace [fdatasync](https://bun.com/reference/node/fs/fdatasync)
* function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  options: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  function [fstat](https://bun.com/reference/node/fs/fstat)(

  fd: number,

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Invokes the callback with the `fs.Stats` for the file descriptor.

  See the POSIX [`fstat(2)`](http://man7.org/linux/man-pages/man2/fstat.2.html) documentation for more detail.

  ### namespace [fstat](https://bun.com/reference/node/fs/fstat)
* function [fsync](https://bun.com/reference/node/fs/fsync)(

  fd: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Request that all data for the open file descriptor is flushed to the storage device. The specific implementation is operating system and device specific. Refer to the POSIX [`fsync(2)`](http://man7.org/linux/man-pages/man2/fsync.2.html) documentation for more detail. No arguments other than a possible exception are given to the completion callback.

  ### namespace [fsync](https://bun.com/reference/node/fs/fsync)
* function [ftruncate](https://bun.com/reference/node/fs/ftruncate)(

  fd: number,

  len?: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Truncates the file descriptor. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`ftruncate(2)`](http://man7.org/linux/man-pages/man2/ftruncate.2.html) documentation for more detail.

  If the file referred to by the file descriptor was larger than `len` bytes, only the first `len` bytes will be retained in the file.

  For example, the following program retains only the first four bytes of the file:

  ```
  import { open, close, ftruncate } from 'node:fs';

  function closeFd(fd) {
    close(fd, (err) => {
      if (err) throw err;
    });
  }

  open('temp.txt', 'r+', (err, fd) => {
    if (err) throw err;

    try {
      ftruncate(fd, 4, (err) => {
        closeFd(fd);
        if (err) throw err;
      });
    } catch (err) {
      closeFd(fd);
      if (err) throw err;
    }
  });
  ```

  If the file previously was shorter than `len` bytes, it is extended, and the extended part is filled with null bytes (`'\0'`):

  If `len` is negative then `0` will be used.

  function [ftruncate](https://bun.com/reference/node/fs/ftruncate)(

  fd: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous ftruncate(2) - Truncate a file to a specified length.

  @param fd

  A file descriptor.

  ### namespace [ftruncate](https://bun.com/reference/node/fs/ftruncate)
* function [futimes](https://bun.com/reference/node/fs/futimes)(

  fd: number,

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Change the file system timestamps of the object referenced by the supplied file descriptor. See utimes.

  ### namespace [futimes](https://bun.com/reference/node/fs/futimes)
* function [lchown](https://bun.com/reference/node/fs/lchown)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Set the owner of the symbolic link. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`lchown(2)`](http://man7.org/linux/man-pages/man2/lchown.2.html) documentation for more detail.

  ### namespace [lchown](https://bun.com/reference/node/fs/lchown)
* function [link](https://bun.com/reference/node/fs/link)(

  existingPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Creates a new link from the `existingPath` to the `newPath`. See the POSIX [`link(2)`](http://man7.org/linux/man-pages/man2/link.2.html) documentation for more detail. No arguments other than a possible exception are given to the completion callback.

  ### namespace [link](https://bun.com/reference/node/fs/link)
* function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.

  function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.

  function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.

  function [lstat](https://bun.com/reference/node/fs/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Retrieves the `fs.Stats` for the symbolic link referred to by the path. The callback gets two arguments `(err, stats)` where `stats` is a `fs.Stats` object. `lstat()` is identical to `stat()`, except that if `path` is a symbolic link, then the link itself is stat-ed, not the file that it refers to.

  See the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) documentation for more details.

  ### namespace [lstat](https://bun.com/reference/node/fs/lstat)
* function [lutimes](https://bun.com/reference/node/fs/lutimes)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Changes the access and modification times of a file in the same way as utimes, with the difference that if the path refers to a symbolic link, then the link is not dereferenced: instead, the timestamps of the symbolic link itself are changed.

  No arguments other than a possible exception are given to the completion callback.

  ### namespace [lutimes](https://bun.com/reference/node/fs/lutimes)
* function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: true },

  callback: (err: null | ErrnoException, path?: string) => void

  ): void;

  Asynchronously creates a directory.

  The callback is given a possible exception and, if `recursive` is `true`, the first directory path created, `(err[, path])`.`path` can still be `undefined` when `recursive` is `true`, if no directory was created (for instance, if it was previously created).

  The optional `options` argument can be an integer specifying `mode` (permission and sticky bits), or an object with a `mode` property and a `recursive` property indicating whether parent directories should be created. Calling `fs.mkdir()` when `path` is a directory that exists results in an error only when `recursive` is false. If `recursive` is false and the directory exists, an `EEXIST` error occurs.

  ```
  import { mkdir } from 'node:fs';

  // Create ./tmp/a/apple, regardless of whether ./tmp and ./tmp/a exist.
  mkdir('./tmp/a/apple', { recursive: true }, (err) => {
    if (err) throw err;
  });
  ```

  On Windows, using `fs.mkdir()` on the root directory even with recursion will result in an error:

  ```
  import { mkdir } from 'node:fs';

  mkdir('/', { recursive: true }, (err) => {
    // => [Error: EPERM: operation not permitted, mkdir 'C:\']
  });
  ```

  See the POSIX [`mkdir(2)`](http://man7.org/linux/man-pages/man2/mkdir.2.html) documentation for more details.

  function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: false },

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.

  function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions),

  callback: (err: null | ErrnoException, path?: string) => void

  ): void;

  Asynchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.

  function [mkdir](https://bun.com/reference/node/fs/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous mkdir(2) - create a directory with a mode of `0o777`.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  ### namespace [mkdir](https://bun.com/reference/node/fs/mkdir)
* function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, folder: string) => void

  ): void;

  Creates a unique temporary directory.

  Generates six random characters to be appended behind a required `prefix` to create a unique temporary directory. Due to platform inconsistencies, avoid trailing `X` characters in `prefix`. Some platforms, notably the BSDs, can return more than six random characters, and replace trailing `X` characters in `prefix` with random characters.

  The created directory path is passed as a string to the callback's second parameter.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use.

  ```
  import { mkdtemp } from 'node:fs';
  import { join } from 'node:path';
  import { tmpdir } from 'node:os';

  mkdtemp(join(tmpdir(), 'foo-'), (err, directory) => {
    if (err) throw err;
    console.log(directory);
    // Prints: /tmp/foo-itXde2 or C:\Users\...\AppData\Local\Temp\foo-itXde2
  });
  ```

  The `fs.mkdtemp()` method will append the six randomly selected characters directly to the `prefix` string. For instance, given a directory `/tmp`, if the intention is to create a temporary directory *within*`/tmp`, the `prefix`must end with a trailing platform-specific path separator (`import { sep } from 'node:path'`).

  ```
  import { tmpdir } from 'node:os';
  import { mkdtemp } from 'node:fs';

  // The parent directory for the new temporary directory
  const tmpDir = tmpdir();

  // This method is *INCORRECT*:
  mkdtemp(tmpDir, (err, directory) => {
    if (err) throw err;
    console.log(directory);
    // Will print something similar to `/tmpabc123`.
    // A new temporary directory is created at the file system root
    // rather than *within* the /tmp directory.
  });

  // This method is *CORRECT*:
  import { sep } from 'node:path';
  mkdtemp(`${tmpDir}${sep}`, (err, directory) => {
    if (err) throw err;
    console.log(directory);
    // Will print something similar to `/tmp/abc123`.
    // A new temporary directory is created within
    // the /tmp directory.
  });
  ```

  function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

  callback: (err: null | ErrnoException, folder: NonSharedBuffer) => void

  ): void;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, folder: string | NonSharedBuffer) => void

  ): void;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)(

  prefix: string,

  callback: (err: null | ErrnoException, folder: string) => void

  ): void;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required prefix to create a unique temporary directory.

  ### namespace [mkdtemp](https://bun.com/reference/node/fs/mkdtemp)
* function [open](https://bun.com/reference/node/fs/open)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  flags?: [OpenMode](https://bun.com/reference/node/fs/OpenMode),

  mode?: null | [Mode](https://bun.com/reference/node/fs/Mode),

  callback: (err: null | ErrnoException, fd: number) => void

  ): void;

  Asynchronous file open. See the POSIX [`open(2)`](http://man7.org/linux/man-pages/man2/open.2.html) documentation for more details.

  `mode` sets the file mode (permission and sticky bits), but only if the file was created. On Windows, only the write permission can be manipulated; see chmod.

  The callback gets two arguments `(err, fd)`.

  Some characters (`< > : " / \ | ? *`) are reserved under Windows as documented by [Naming Files, Paths, and Namespaces](https://docs.microsoft.com/en-us/windows/desktop/FileIO/naming-a-file). Under NTFS, if the filename contains a colon, Node.js will open a file system stream, as described by [this MSDN page](https://docs.microsoft.com/en-us/windows/desktop/FileIO/using-streams).

  Functions based on `fs.open()` exhibit this behavior as well:`fs.writeFile()`, `fs.readFile()`, etc.

  @param flags

  See `support of file system` flags``.

  function [open](https://bun.com/reference/node/fs/open)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  flags?: [OpenMode](https://bun.com/reference/node/fs/OpenMode),

  callback: (err: null | ErrnoException, fd: number) => void

  ): void;

  Asynchronous open(2) - open and possibly create a file. If the file is created, its mode will be `0o666`.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param flags

  See `support of file system` flags``.

  function [open](https://bun.com/reference/node/fs/open)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, fd: number) => void

  ): void;

  Asynchronous open(2) - open and possibly create a file. If the file is created, its mode will be `0o666`.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  ### namespace [open](https://bun.com/reference/node/fs/open)
* function [opendir](https://bun.com/reference/node/fs/opendir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  cb: (err: null | ErrnoException, dir: [Dir](https://bun.com/reference/node/fs/Dir)) => void

  ): void;

  Asynchronously open a directory. See the POSIX [`opendir(3)`](http://man7.org/linux/man-pages/man3/opendir.3.html) documentation for more details.

  Creates an `fs.Dir`, which contains all further functions for reading from and cleaning up the directory.

  The `encoding` option sets the encoding for the `path` while opening the directory and subsequent read operations.

  function [opendir](https://bun.com/reference/node/fs/opendir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [OpenDirOptions](https://bun.com/reference/node/fs/OpenDirOptions),

  cb: (err: null | ErrnoException, dir: [Dir](https://bun.com/reference/node/fs/Dir)) => void

  ): void;

  Asynchronously open a directory. See the POSIX [`opendir(3)`](http://man7.org/linux/man-pages/man3/opendir.3.html) documentation for more details.

  Creates an `fs.Dir`, which contains all further functions for reading from and cleaning up the directory.

  The `encoding` option sets the encoding for the `path` while opening the directory and subsequent read operations.

  ### namespace [opendir](https://bun.com/reference/node/fs/opendir)
* function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset: number,

  length: number,

  position: null | [ReadPosition](https://bun.com/reference/node/fs/ReadPosition),

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.

  @param buffer

  The buffer that the data will be written to.

  @param offset

  The position in `buffer` to write the data to.

  @param length

  The number of bytes to read.

  @param position

  Specifies where to begin reading from in the file. If `position` is `null` or `-1` , data will be read from the current file position, and the file position will be updated. If `position` is an integer, the file position will be unchanged.

  function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike> = NonSharedBuffer>(

  fd: number,

  options: [ReadOptionsWithBuffer](https://bun.com/reference/node/fs/ReadOptionsWithBuffer)<TBuffer>,

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Similar to the above `fs.read` function, this version takes an optional `options` object. If not otherwise specified in an `options` object, `buffer` defaults to `Buffer.alloc(16384)`, `offset` defaults to `0`, `length` defaults to `buffer.byteLength`, `- offset` as of Node 17.6.0 `position` defaults to `null`

  function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  options: [ReadOptions](https://bun.com/reference/node/fs/ReadOptions),

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.

  @param buffer

  The buffer that the data will be written to.

  function [read](https://bun.com/reference/node/fs/read)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  callback: (err: null | ErrnoException, bytesRead: number, buffer: TBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.

  @param buffer

  The buffer that the data will be written to.

  function [read](https://bun.com/reference/node/fs/read)(

  fd: number,

  callback: (err: null | ErrnoException, bytesRead: number, buffer: NonSharedBuffer) => void

  ): void;

  Read data from the file specified by `fd`.

  The callback is given the three arguments, `(err, bytesRead, buffer)`.

  If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffer` properties.

  ### namespace [read](https://bun.com/reference/node/fs/read)
* function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | BufferEncoding | { encoding: unknown; recursive: boolean; withFileTypes: false },

  callback: (err: null | ErrnoException, files: string[]) => void

  ): void;

  Reads the contents of a directory. The callback gets two arguments `(err, files)` where `files` is an array of the names of the files in the directory excluding `'.'` and `'..'`.

  See the POSIX [`readdir(3)`](http://man7.org/linux/man-pages/man3/readdir.3.html) documentation for more details.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the filenames passed to the callback. If the `encoding` is set to `'buffer'`, the filenames returned will be passed as `Buffer` objects.

  If `options.withFileTypes` is set to `true`, the `files` array will contain `fs.Dirent` objects.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: 'buffer' | { encoding: 'buffer'; recursive: boolean; withFileTypes: false },

  callback: (err: null | ErrnoException, files: NonSharedBuffer[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: false },

  callback: (err: null | ErrnoException, files: string[] | NonSharedBuffer[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, files: string[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: true },

  callback: (err: null | ErrnoException, files: [Dirent](https://bun.com/reference/node/fs/Dirent)<string>[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  If called with `withFileTypes: true` the result data will be an array of Dirent.

  function [readdir](https://bun.com/reference/node/fs/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: { encoding: 'buffer'; recursive: boolean; withFileTypes: true },

  callback: (err: null | ErrnoException, files: [Dirent](https://bun.com/reference/node/fs/Dirent)<NonSharedBuffer>[]) => void

  ): void;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Must include `withFileTypes: true` and `encoding: 'buffer'`.

  ### namespace [readdir](https://bun.com/reference/node/fs/readdir)
* function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options: undefined | null | { encoding: null; flag: string } & [Abortable](https://bun.com/reference/node/events/default/Abortable),

  callback: (err: null | ErrnoException, data: NonSharedBuffer) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  ```
  import { readFile } from 'node:fs';

  readFile('/etc/passwd', (err, data) => {
    if (err) throw err;
    console.log(data);
  });
  ```

  The callback is passed two arguments `(err, data)`, where `data` is the contents of the file.

  If no encoding is specified, then the raw buffer is returned.

  If `options` is a string, then it specifies the encoding:

  ```
  import { readFile } from 'node:fs';

  readFile('/etc/passwd', 'utf8', callback);
  ```

  When the path is a directory, the behavior of `fs.readFile()` and readFileSync is platform-specific. On macOS, Linux, and Windows, an error will be returned. On FreeBSD, a representation of the directory's contents will be returned.

  ```
  import { readFile } from 'node:fs';

  // macOS, Linux, and Windows
  readFile('<directory>', (err, data) => {
    // => [Error: EISDIR: illegal operation on a directory, read <directory>]
  });

  //  FreeBSD
  readFile('<directory>', (err, data) => {
    // => null, <data>
  });
  ```

  It is possible to abort an ongoing request using an `AbortSignal`. If a request is aborted the callback is called with an `AbortError`:

  ```
  import { readFile } from 'node:fs';

  const controller = new AbortController();
  const signal = controller.signal;
  readFile(fileInfo[0].name, { signal }, (err, buf) => {
    // ...
  });
  // When you want to abort the request
  controller.abort();
  ```

  The `fs.readFile()` function buffers the entire file. To minimize memory costs, when possible prefer streaming via `fs.createReadStream()`.

  Aborting an ongoing request does not abort individual operating system requests but rather the internal buffering `fs.readFile` performs.

  @param path

  filename or file descriptor

  function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options: BufferEncoding | { encoding: BufferEncoding; flag: string } & [Abortable](https://bun.com/reference/node/events/default/Abortable),

  callback: (err: null | ErrnoException, data: string) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param options

  Either the encoding for the result, or an object that contains the encoding and an optional flag. If a flag is not provided, it defaults to `'r'`.

  function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  options: undefined | null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { flag: string } & [Abortable](https://bun.com/reference/node/events/default/Abortable),

  callback: (err: null | ErrnoException, data: string | NonSharedBuffer) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param options

  Either the encoding for the result, or an object that contains the encoding and an optional flag. If a flag is not provided, it defaults to `'r'`.

  function [readFile](https://bun.com/reference/node/fs/readFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  callback: (err: null | ErrnoException, data: NonSharedBuffer) => void

  ): void;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  ### namespace [readFile](https://bun.com/reference/node/fs/readFile)
* function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, linkString: string) => void

  ): void;

  Reads the contents of the symbolic link referred to by `path`. The callback gets two arguments `(err, linkString)`.

  See the POSIX [`readlink(2)`](http://man7.org/linux/man-pages/man2/readlink.2.html) documentation for more details.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the link path passed to the callback. If the `encoding` is set to `'buffer'`, the link path returned will be passed as a `Buffer` object.

  function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption),

  callback: (err: null | ErrnoException, linkString: NonSharedBuffer) => void

  ): void;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption),

  callback: (err: null | ErrnoException, linkString: string | NonSharedBuffer) => void

  ): void;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readlink](https://bun.com/reference/node/fs/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, linkString: string) => void

  ): void;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  ### namespace [readlink](https://bun.com/reference/node/fs/readlink)
* function [readv](https://bun.com/reference/node/fs/readv)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  cb: (err: null | ErrnoException, bytesRead: number, buffers: TBuffers) => void

  ): void;

  Read from a file specified by `fd` and write to an array of `ArrayBufferView`s using `readv()`.

  `position` is the offset from the beginning of the file from where data should be read. If `typeof position !== 'number'`, the data will be read from the current position.

  The callback will be given three arguments: `err`, `bytesRead`, and `buffers`. `bytesRead` is how many bytes were read from the file.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffers` properties.

  function [readv](https://bun.com/reference/node/fs/readv)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  position: null | number,

  cb: (err: null | ErrnoException, bytesRead: number, buffers: TBuffers) => void

  ): void;

  Read from a file specified by `fd` and write to an array of `ArrayBufferView`s using `readv()`.

  `position` is the offset from the beginning of the file from where data should be read. If `typeof position !== 'number'`, the data will be read from the current position.

  The callback will be given three arguments: `err`, `bytesRead`, and `buffers`. `bytesRead` is how many bytes were read from the file.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesRead` and `buffers` properties.

  ### namespace [readv](https://bun.com/reference/node/fs/readv)
* function [rename](https://bun.com/reference/node/fs/rename)(

  oldPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously rename file at `oldPath` to the pathname provided as `newPath`. In the case that `newPath` already exists, it will be overwritten. If there is a directory at `newPath`, an error will be raised instead. No arguments other than a possible exception are given to the completion callback.

  See also: [`rename(2)`](http://man7.org/linux/man-pages/man2/rename.2.html).

  ```
  import { rename } from 'node:fs';

  rename('oldFile.txt', 'newFile.txt', (err) => {
    if (err) throw err;
    console.log('Rename complete!');
  });
  ```

  ### namespace [rename](https://bun.com/reference/node/fs/rename)
* function [rm](https://bun.com/reference/node/fs/rm)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously removes files and directories (modeled on the standard POSIX `rm` utility). No arguments other than a possible exception are given to the completion callback.

  function [rm](https://bun.com/reference/node/fs/rm)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [RmOptions](https://bun.com/reference/node/fs/RmOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously removes files and directories (modeled on the standard POSIX `rm` utility). No arguments other than a possible exception are given to the completion callback.

  ### namespace [rm](https://bun.com/reference/node/fs/rm)
* function [rmdir](https://bun.com/reference/node/fs/rmdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous [`rmdir(2)`](http://man7.org/linux/man-pages/man2/rmdir.2.html). No arguments other than a possible exception are given to the completion callback.

  Using `fs.rmdir()` on a file (not a directory) results in an `ENOENT` error on Windows and an `ENOTDIR` error on POSIX.

  To get a behavior similar to the `rm -rf` Unix command, use rm with options `{ recursive: true, force: true }`.

  function [rmdir](https://bun.com/reference/node/fs/rmdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [RmDirOptions](https://bun.com/reference/node/fs/RmDirOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous [`rmdir(2)`](http://man7.org/linux/man-pages/man2/rmdir.2.html). No arguments other than a possible exception are given to the completion callback.

  Using `fs.rmdir()` on a file (not a directory) results in an `ENOENT` error on Windows and an `ENOTDIR` error on POSIX.

  To get a behavior similar to the `rm -rf` Unix command, use rm with options `{ recursive: true, force: true }`.

  ### namespace [rmdir](https://bun.com/reference/node/fs/rmdir)
* function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```

  function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```

  function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```

  function [stat](https://bun.com/reference/node/fs/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatOptions](https://bun.com/reference/node/fs/StatOptions),

  callback: (err: null | ErrnoException, stats: [Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void

  ): void;

  Asynchronous [`stat(2)`](http://man7.org/linux/man-pages/man2/stat.2.html). The callback gets two arguments `(err, stats)` where`stats` is an `fs.Stats` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  stat follows symbolic links. Use lstat to look at the links themselves.

  Using `fs.stat()` to check for the existence of a file before calling`fs.open()`, `fs.readFile()`, or `fs.writeFile()` is not recommended. Instead, user code should open/read/write the file directly and handle the error raised if the file is not available.

  To check if a file exists without manipulating it afterwards, access is recommended.

  For example, given the following directory structure:

  ```
  - txtDir
  -- file.txt
  - app.js
  ```

  The next program will check for the stats of the given paths:

  ```
  import { stat } from 'node:fs';

  const pathsToCheck = ['./txtDir', './txtDir/file.txt'];

  for (let i = 0; i < pathsToCheck.length; i++) {
    stat(pathsToCheck[i], (err, stats) => {
      console.log(stats.isDirectory());
      console.log(stats);
    });
  }
  ```

  The resulting output will resemble:

  ```
  true
  Stats {
    dev: 16777220,
    mode: 16877,
    nlink: 3,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214262,
    size: 96,
    blocks: 0,
    atimeMs: 1561174653071.963,
    mtimeMs: 1561174614583.3518,
    ctimeMs: 1561174626623.5366,
    birthtimeMs: 1561174126937.2893,
    atime: 2019-06-22T03:37:33.072Z,
    mtime: 2019-06-22T03:36:54.583Z,
    ctime: 2019-06-22T03:37:06.624Z,
    birthtime: 2019-06-22T03:28:46.937Z
  }
  false
  Stats {
    dev: 16777220,
    mode: 33188,
    nlink: 1,
    uid: 501,
    gid: 20,
    rdev: 0,
    blksize: 4096,
    ino: 14214074,
    size: 8,
    blocks: 8,
    atimeMs: 1561174616618.8555,
    mtimeMs: 1561174614584,
    ctimeMs: 1561174614583.8145,
    birthtimeMs: 1561174007710.7478,
    atime: 2019-06-22T03:36:56.619Z,
    mtime: 2019-06-22T03:36:54.584Z,
    ctime: 2019-06-22T03:36:54.584Z,
    birthtime: 2019-06-22T03:26:47.711Z
  }
  ```

  ### namespace [stat](https://bun.com/reference/node/fs/stat)
* function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: (err: null | ErrnoException, stats: [StatsFs](https://bun.com/reference/node/fs/StatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: false },

  callback: (err: null | ErrnoException, stats: [StatsFs](https://bun.com/reference/node/fs/StatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: true },

  callback: (err: null | ErrnoException, stats: [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  function [statfs](https://bun.com/reference/node/fs/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: undefined | [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions),

  callback: (err: null | ErrnoException, stats: [StatsFs](https://bun.com/reference/node/fs/StatsFs) | [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs)) => void

  ): void;

  Asynchronous [`statfs(2)`](http://man7.org/linux/man-pages/man2/statfs.2.html). Returns information about the mounted file system which contains `path`. The callback gets two arguments `(err, stats)` where `stats`is an `fs.StatFs` object.

  In case of an error, the `err.code` will be one of `Common System Errors`.

  @param path

  A path to an existing file or directory on the file system to be queried.

  ### namespace [statfs](https://bun.com/reference/node/fs/statfs)
* function [symlink](https://bun.com/reference/node/fs/symlink)(

  target: [PathLike](https://bun.com/reference/node/fs/PathLike),

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  type?: null | [Type](https://bun.com/reference/node/fs/symlink/Type),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Creates the link called `path` pointing to `target`. No arguments other than a possible exception are given to the completion callback.

  See the POSIX [`symlink(2)`](http://man7.org/linux/man-pages/man2/symlink.2.html) documentation for more details.

  The `type` argument is only available on Windows and ignored on other platforms. It can be set to `'dir'`, `'file'`, or `'junction'`. If the `type` argument is not a string, Node.js will autodetect `target` type and use `'file'` or `'dir'`. If the `target` does not exist, `'file'` will be used. Windows junction points require the destination path to be absolute. When using `'junction'`, the`target` argument will automatically be normalized to absolute path. Junction points on NTFS volumes can only point to directories.

  Relative targets are relative to the link's parent directory.

  ```
  import { symlink } from 'node:fs';

  symlink('./mew', './mewtwo', callback);
  ```

  The above example creates a symbolic link `mewtwo` which points to `mew` in the same directory:

  ```
  tree .
  ```

  ```
  .
  ├── mew
  └── mewtwo -> ./mew
  ```

  function [symlink](https://bun.com/reference/node/fs/symlink)(

  target: [PathLike](https://bun.com/reference/node/fs/PathLike),

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous symlink(2) - Create a new symbolic link to an existing file.

  @param target

  A path to an existing file. If a URL is provided, it must use the `file:` protocol.

  @param path

  A path to the new symlink. If a URL is provided, it must use the `file:` protocol.

  ### namespace [symlink](https://bun.com/reference/node/fs/symlink)

  + type [Type](https://bun.com/reference/node/fs/symlink/Type) = 'dir' | 'file' | 'junction'
* function [truncate](https://bun.com/reference/node/fs/truncate)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronous truncate(2) - Truncate a file to a specified length.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  ### namespace [truncate](https://bun.com/reference/node/fs/truncate)
* function [unlink](https://bun.com/reference/node/fs/unlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously removes a file or symbolic link. No arguments other than a possible exception are given to the completion callback.

  ```
  import { unlink } from 'node:fs';
  // Assuming that 'path/file.txt' is a regular file.
  unlink('path/file.txt', (err) => {
    if (err) throw err;
    console.log('path/file.txt was deleted');
  });
  ```

  `fs.unlink()` will not work on a directory, empty or otherwise. To remove a directory, use rmdir.

  See the POSIX [`unlink(2)`](http://man7.org/linux/man-pages/man2/unlink.2.html) documentation for more details.

  ### namespace [unlink](https://bun.com/reference/node/fs/unlink)
* function [utimes](https://bun.com/reference/node/fs/utimes)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Change the file system timestamps of the object referenced by `path`.

  The `atime` and `mtime` arguments follow these rules:

  + Values can be either numbers representing Unix epoch time in seconds, `Date`s, or a numeric string like `'123456789.0'`.
  + If the value can not be converted to a number, or is `NaN`, `Infinity`, or `-Infinity`, an `Error` will be thrown.

  ### namespace [utimes](https://bun.com/reference/node/fs/utimes)
* function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset?: null | number,

  length?: null | number,

  position?: null | number,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Write `buffer` to the file specified by `fd`.

  `offset` determines the part of the buffer to be written, and `length` is an integer specifying the number of bytes to write.

  `position` refers to the offset from the beginning of the file where this data should be written. If `typeof position !== 'number'`, the data will be written at the current position. See [`pwrite(2)`](http://man7.org/linux/man-pages/man2/pwrite.2.html).

  The callback will be given three arguments `(err, bytesWritten, buffer)` where `bytesWritten` specifies how many *bytes* were written from `buffer`.

  If this method is invoked as its `util.promisify()` ed version, it returns a promise for an `Object` with `bytesWritten` and `buffer` properties.

  It is unsafe to use `fs.write()` multiple times on the same file without waiting for the callback. For this scenario, createWriteStream is recommended.

  On Linux, positional writes don't work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset: undefined | null | number,

  length: undefined | null | number,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param offset

  The part of the buffer to be written. If not supplied, defaults to `0`.

  @param length

  The number of bytes to write. If not supplied, defaults to `buffer.length - offset`.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  offset: undefined | null | number,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param offset

  The part of the buffer to be written. If not supplied, defaults to `0`.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  function [write](https://bun.com/reference/node/fs/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

  fd: number,

  buffer: TBuffer,

  options: [WriteOptions](https://bun.com/reference/node/fs/WriteOptions),

  callback: (err: null | ErrnoException, written: number, buffer: TBuffer) => void

  ): void;

  Asynchronously writes `buffer` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param options

  An object with the following properties:

  + `offset` The part of the buffer to be written. If not supplied, defaults to `0`.
  + `length` The number of bytes to write. If not supplied, defaults to `buffer.length - offset`.
  + `position` The offset from the beginning of the file where this data should be written. If not supplied, defaults to the current position.

  function [write](https://bun.com/reference/node/fs/write)(

  fd: number,

  string: string,

  position: undefined | null | number,

  encoding: undefined | null | BufferEncoding,

  callback: (err: null | ErrnoException, written: number, str: string) => void

  ): void;

  Asynchronously writes `string` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param string

  A string to write.

  @param position

  The offset from the beginning of the file where this data should be written. If not supplied, defaults to the current position.

  @param encoding

  The expected string encoding.

  function [write](https://bun.com/reference/node/fs/write)(

  fd: number,

  string: string,

  position: undefined | null | number,

  callback: (err: null | ErrnoException, written: number, str: string) => void

  ): void;

  Asynchronously writes `string` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param string

  A string to write.

  @param position

  The offset from the beginning of the file where this data should be written. If not supplied, defaults to the current position.

  function [write](https://bun.com/reference/node/fs/write)(

  fd: number,

  string: string,

  callback: (err: null | ErrnoException, written: number, str: string) => void

  ): void;

  Asynchronously writes `string` to the file referenced by the supplied file descriptor.

  @param fd

  A file descriptor.

  @param string

  A string to write.

  ### namespace [write](https://bun.com/reference/node/fs/write)
* function [writeFile](https://bun.com/reference/node/fs/writeFile)(

  file: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | ArrayBufferView<ArrayBufferLike>,

  options: [WriteFileOptions](https://bun.com/reference/node/fs/WriteFileOptions),

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  When `file` is a filename, asynchronously writes data to the file, replacing the file if it already exists. `data` can be a string or a buffer.

  When `file` is a file descriptor, the behavior is similar to calling `fs.write()` directly (which is recommended). See the notes below on using a file descriptor.

  The `encoding` option is ignored if `data` is a buffer.

  The `mode` option only affects the newly created file. See open for more details.

  ```
  import { writeFile } from 'node:fs';
  import { Buffer } from 'node:buffer';

  const data = new Uint8Array(Buffer.from('Hello Node.js'));
  writeFile('message.txt', data, (err) => {
    if (err) throw err;
    console.log('The file has been saved!');
  });
  ```

  If `options` is a string, then it specifies the encoding:

  ```
  import { writeFile } from 'node:fs';

  writeFile('message.txt', 'Hello Node.js', 'utf8', callback);
  ```

  It is unsafe to use `fs.writeFile()` multiple times on the same file without waiting for the callback. For this scenario, createWriteStream is recommended.

  Similarly to `fs.readFile` - `fs.writeFile` is a convenience method that performs multiple `write` calls internally to write the buffer passed to it. For performance sensitive code consider using createWriteStream.

  It is possible to use an `AbortSignal` to cancel an `fs.writeFile()`. Cancelation is "best effort", and some amount of data is likely still to be written.

  ```
  import { writeFile } from 'node:fs';
  import { Buffer } from 'node:buffer';

  const controller = new AbortController();
  const { signal } = controller;
  const data = new Uint8Array(Buffer.from('Hello Node.js'));
  writeFile('message.txt', data, { signal }, (err) => {
    // When a request is aborted - the callback is called with an AbortError
  });
  // When the request should be aborted
  controller.abort();
  ```

  Aborting an ongoing request does not abort individual operating system requests but rather the internal buffering `fs.writeFile` performs.

  @param file

  filename or file descriptor

  function [writeFile](https://bun.com/reference/node/fs/writeFile)(

  path: [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor),

  data: string | ArrayBufferView<ArrayBufferLike>,

  callback: [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback)

  ): void;

  Asynchronously writes data to a file, replacing the file if it already exists.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a file descriptor is provided, the underlying file will *not* be closed automatically.

  @param data

  The data to write. If something other than a Buffer or Uint8Array is provided, the value is coerced to a string.

  ### namespace [writeFile](https://bun.com/reference/node/fs/writeFile)
* function [writev](https://bun.com/reference/node/fs/writev)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  cb: (err: null | ErrnoException, bytesWritten: number, buffers: TBuffers) => void

  ): void;

  Write an array of `ArrayBufferView`s to the file specified by `fd` using `writev()`.

  `position` is the offset from the beginning of the file where this data should be written. If `typeof position !== 'number'`, the data will be written at the current position.

  The callback will be given three arguments: `err`, `bytesWritten`, and `buffers`. `bytesWritten` is how many bytes were written from `buffers`.

  If this method is `util.promisify()` ed, it returns a promise for an `Object` with `bytesWritten` and `buffers` properties.

  It is unsafe to use `fs.writev()` multiple times on the same file without waiting for the callback. For this scenario, use createWriteStream.

  On Linux, positional writes don't work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.

  function [writev](https://bun.com/reference/node/fs/writev)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

  fd: number,

  buffers: TBuffers,

  position: null | number,

  cb: (err: null | ErrnoException, bytesWritten: number, buffers: TBuffers) => void

  ): void;

  Write an array of `ArrayBufferView`s to the file specified by `fd` using `writev()`.

  `position` is the offset from the beginning of the file where this data should be written. If `typeof position !== 'number'`, the data will be written at the current position.

  The callback will be given three arguments: `err`, `bytesWritten`, and `buffers`. `bytesWritten` is how many bytes were written from `buffers`.

  If this method is `util.promisify()` ed, it returns a promise for an `Object` with `bytesWritten` and `buffers` properties.

  It is unsafe to use `fs.writev()` multiple times on the same file without waiting for the callback. For this scenario, use createWriteStream.

  On Linux, positional writes don't work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.

  ### namespace [writev](https://bun.com/reference/node/fs/writev)
* ### interface [BigIntOptions](https://bun.com/reference/node/fs/BigIntOptions)

  + [bigint](https://bun.com/reference/node/fs/BigIntOptions/bigint): true
* ### interface [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)

  + [atime](https://bun.com/reference/node/fs/BigIntStats/atime): Date
  + [atimeMs](https://bun.com/reference/node/fs/BigIntStats/atimeMs): bigint
  + [atimeNs](https://bun.com/reference/node/fs/BigIntStats/atimeNs): bigint
  + [birthtime](https://bun.com/reference/node/fs/BigIntStats/birthtime): Date
  + [birthtimeMs](https://bun.com/reference/node/fs/BigIntStats/birthtimeMs): bigint
  + [birthtimeNs](https://bun.com/reference/node/fs/BigIntStats/birthtimeNs): bigint
  + [blksize](https://bun.com/reference/node/fs/BigIntStats/blksize): bigint
  + [blocks](https://bun.com/reference/node/fs/BigIntStats/blocks): bigint
  + [ctime](https://bun.com/reference/node/fs/BigIntStats/ctime): Date
  + [ctimeMs](https://bun.com/reference/node/fs/BigIntStats/ctimeMs): bigint
  + [ctimeNs](https://bun.com/reference/node/fs/BigIntStats/ctimeNs): bigint
  + [dev](https://bun.com/reference/node/fs/BigIntStats/dev): bigint
  + [gid](https://bun.com/reference/node/fs/BigIntStats/gid): bigint
  + [ino](https://bun.com/reference/node/fs/BigIntStats/ino): bigint
  + [mode](https://bun.com/reference/node/fs/BigIntStats/mode): bigint
  + [mtime](https://bun.com/reference/node/fs/BigIntStats/mtime): Date
  + [mtimeMs](https://bun.com/reference/node/fs/BigIntStats/mtimeMs): bigint
  + [mtimeNs](https://bun.com/reference/node/fs/BigIntStats/mtimeNs): bigint
  + [nlink](https://bun.com/reference/node/fs/BigIntStats/nlink): bigint
  + [rdev](https://bun.com/reference/node/fs/BigIntStats/rdev): bigint
  + [size](https://bun.com/reference/node/fs/BigIntStats/size): bigint
  + [uid](https://bun.com/reference/node/fs/BigIntStats/uid): bigint
  + [isBlockDevice](https://bun.com/reference/node/fs/BigIntStats/isBlockDevice)(): boolean;
  + [isCharacterDevice](https://bun.com/reference/node/fs/BigIntStats/isCharacterDevice)(): boolean;
  + [isDirectory](https://bun.com/reference/node/fs/BigIntStats/isDirectory)(): boolean;
  + [isFIFO](https://bun.com/reference/node/fs/BigIntStats/isFIFO)(): boolean;
  + [isFile](https://bun.com/reference/node/fs/BigIntStats/isFile)(): boolean;
  + [isSocket](https://bun.com/reference/node/fs/BigIntStats/isSocket)(): boolean;
  + [isSymbolicLink](https://bun.com/reference/node/fs/BigIntStats/isSymbolicLink)(): boolean;
* ### interface [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs)

  + [bavail](https://bun.com/reference/node/fs/BigIntStatsFs/bavail): bigint

    Available blocks for unprivileged users
  + [bfree](https://bun.com/reference/node/fs/BigIntStatsFs/bfree): bigint

    Free blocks in file system.
  + [blocks](https://bun.com/reference/node/fs/BigIntStatsFs/blocks): bigint

    Total data blocks in file system.
  + [bsize](https://bun.com/reference/node/fs/BigIntStatsFs/bsize): bigint

    Optimal transfer block size.
  + [ffree](https://bun.com/reference/node/fs/BigIntStatsFs/ffree): bigint

    Free file nodes in file system.
  + [files](https://bun.com/reference/node/fs/BigIntStatsFs/files): bigint

    Total file nodes in file system.
  + [type](https://bun.com/reference/node/fs/BigIntStatsFs/type): bigint

    Type of file system.
* ### interface [CopyOptions](https://bun.com/reference/node/fs/CopyOptions)

  + [dereference](https://bun.com/reference/node/fs/CopyOptions/dereference)?: boolean

    Dereference symlinks
  + [errorOnExist](https://bun.com/reference/node/fs/CopyOptions/errorOnExist)?: boolean

    When `force` is `false`, and the destination exists, throw an error.
  + [filter](https://bun.com/reference/node/fs/CopyOptions/filter)?: (source: string, destination: string) => boolean | Promise<boolean>

    Function to filter copied files/directories. Return `true` to copy the item, `false` to ignore it.
  + [force](https://bun.com/reference/node/fs/CopyOptions/force)?: boolean

    Overwrite existing file or directory. \_The copy operation will ignore errors if you set this to false and the destination exists. Use the `errorOnExist` option to change this behavior.
  + [mode](https://bun.com/reference/node/fs/CopyOptions/mode)?: number

    Modifiers for copy operation. See `mode` flag of ()
  + [preserveTimestamps](https://bun.com/reference/node/fs/CopyOptions/preserveTimestamps)?: boolean

    When `true` timestamps from `src` will be preserved.
  + [recursive](https://bun.com/reference/node/fs/CopyOptions/recursive)?: boolean

    Copy directories recursively.
  + [verbatimSymlinks](https://bun.com/reference/node/fs/CopyOptions/verbatimSymlinks)?: boolean

    When true, path resolution for symlinks will be skipped
* ### interface [CopySyncOptions](https://bun.com/reference/node/fs/CopySyncOptions)

  + [dereference](https://bun.com/reference/node/fs/CopySyncOptions/dereference)?: boolean

    Dereference symlinks
  + [errorOnExist](https://bun.com/reference/node/fs/CopySyncOptions/errorOnExist)?: boolean

    When `force` is `false`, and the destination exists, throw an error.
  + [filter](https://bun.com/reference/node/fs/CopySyncOptions/filter)?: (source: string, destination: string) => boolean

    Function to filter copied files/directories. Return `true` to copy the item, `false` to ignore it.
  + [force](https://bun.com/reference/node/fs/CopySyncOptions/force)?: boolean

    Overwrite existing file or directory. \_The copy operation will ignore errors if you set this to false and the destination exists. Use the `errorOnExist` option to change this behavior.
  + [mode](https://bun.com/reference/node/fs/CopySyncOptions/mode)?: number

    Modifiers for copy operation. See `mode` flag of ()
  + [preserveTimestamps](https://bun.com/reference/node/fs/CopySyncOptions/preserveTimestamps)?: boolean

    When `true` timestamps from `src` will be preserved.
  + [recursive](https://bun.com/reference/node/fs/CopySyncOptions/recursive)?: boolean

    Copy directories recursively.
  + [verbatimSymlinks](https://bun.com/reference/node/fs/CopySyncOptions/verbatimSymlinks)?: boolean

    When true, path resolution for symlinks will be skipped
* ### interface [DisposableTempDir](https://bun.com/reference/node/fs/DisposableTempDir)

  + [path](https://bun.com/reference/node/fs/DisposableTempDir/path): string

    The path of the created directory.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/fs/DisposableTempDir/[asyncDispose])(): Promise<void>;

    The same as `remove`.
  + [remove](https://bun.com/reference/node/fs/DisposableTempDir/remove)(): Promise<void>;

    A function which removes the created directory.
* ### interface [FSWatcher](https://bun.com/reference/node/fs/FSWatcher)

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/fs/FSWatcher/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/fs/FSWatcher/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. change
    2. close
    3. error

    [addListener](https://bun.com/reference/node/fs/FSWatcher/addListener)(

    event: 'change',

    listener: (eventType: string, filename: string | NonSharedBuffer) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/fs/FSWatcher/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/fs/FSWatcher/addListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [close](https://bun.com/reference/node/fs/FSWatcher/close)(): void;

    Stop watching for changes on the given `fs.FSWatcher`. Once stopped, the `fs.FSWatcher` object is no longer usable.
  + [emit](https://bun.com/reference/node/fs/FSWatcher/emit)<K>(

    eventName: string | symbol,

    ...args: AnyRest

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```
  + [eventNames](https://bun.com/reference/node/fs/FSWatcher/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getMaxListeners](https://bun.com/reference/node/fs/FSWatcher/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/fs/FSWatcher/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/fs/FSWatcher/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/fs/FSWatcher/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/fs/FSWatcher/on)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/fs/FSWatcher/on)(

    event: 'change',

    listener: (eventType: string, filename: string | NonSharedBuffer) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/fs/FSWatcher/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/fs/FSWatcher/on)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/fs/FSWatcher/once)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/fs/FSWatcher/once)(

    event: 'change',

    listener: (eventType: string, filename: string | NonSharedBuffer) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/fs/FSWatcher/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/fs/FSWatcher/once)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function
  + [prependListener](https://bun.com/reference/node/fs/FSWatcher/prependListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/fs/FSWatcher/prependListener)(

    event: 'change',

    listener: (eventType: string, filename: string | NonSharedBuffer) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/fs/FSWatcher/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/fs/FSWatcher/prependListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/fs/FSWatcher/prependOnceListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/fs/FSWatcher/prependOnceListener)(

    event: 'change',

    listener: (eventType: string, filename: string | NonSharedBuffer) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/fs/FSWatcher/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/fs/FSWatcher/prependOnceListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function
  + [rawListeners](https://bun.com/reference/node/fs/FSWatcher/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/fs/FSWatcher/ref)(): this;

    When called, requests that the Node.js event loop *not* exit so long as the `fs.FSWatcher` is active. Calling `watcher.ref()` multiple times will have no effect.

    By default, all `fs.FSWatcher` objects are "ref'ed", making it normally unnecessary to call `watcher.ref()` unless `watcher.unref()` had been called previously.
  + [removeAllListeners](https://bun.com/reference/node/fs/FSWatcher/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/fs/FSWatcher/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setMaxListeners](https://bun.com/reference/node/fs/FSWatcher/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [unref](https://bun.com/reference/node/fs/FSWatcher/unref)(): this;

    When called, the active `fs.FSWatcher` object will not require the Node.js event loop to remain active. If there is no other activity keeping the event loop running, the process may exit before the `fs.FSWatcher` object's callback is invoked. Calling `watcher.unref()` multiple times will have no effect.
* ### interface [GlobOptions](https://bun.com/reference/node/fs/GlobOptions)

  + [cwd](https://bun.com/reference/node/fs/GlobOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)

    Current working directory.
  + [exclude](https://bun.com/reference/node/fs/GlobOptions/exclude)?: readonly string[] | (fileName: string | [Dirent](https://bun.com/reference/node/fs/Dirent)<string>) => boolean

    Function to filter out files/directories or a list of glob patterns to be excluded. If a function is provided, return `true` to exclude the item, `false` to include it. If a string array is provided, each string should be a glob pattern that specifies paths to exclude. Note: Negation patterns (e.g., '!foo.js') are not supported.
  + [withFileTypes](https://bun.com/reference/node/fs/GlobOptions/withFileTypes)?: boolean

    `true` if the glob should return paths as `Dirent`s, `false` otherwise.
* ### interface [GlobOptionsWithFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithFileTypes)

  + [cwd](https://bun.com/reference/node/fs/GlobOptionsWithFileTypes/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)

    Current working directory.
  + [exclude](https://bun.com/reference/node/fs/GlobOptionsWithFileTypes/exclude)?: readonly string[] | (fileName: [Dirent](https://bun.com/reference/node/fs/Dirent)) => boolean

    Function to filter out files/directories or a list of glob patterns to be excluded. If a function is provided, return `true` to exclude the item, `false` to include it. If a string array is provided, each string should be a glob pattern that specifies paths to exclude. Note: Negation patterns (e.g., '!foo.js') are not supported.
  + [withFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithFileTypes/withFileTypes): true

    `true` if the glob should return paths as `Dirent`s, `false` otherwise.
* ### interface [GlobOptionsWithoutFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithoutFileTypes)

  + [cwd](https://bun.com/reference/node/fs/GlobOptionsWithoutFileTypes/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)

    Current working directory.
  + [exclude](https://bun.com/reference/node/fs/GlobOptionsWithoutFileTypes/exclude)?: readonly string[] | (fileName: string) => boolean

    Function to filter out files/directories or a list of glob patterns to be excluded. If a function is provided, return `true` to exclude the item, `false` to include it. If a string array is provided, each string should be a glob pattern that specifies paths to exclude. Note: Negation patterns (e.g., '!foo.js') are not supported.
  + [withFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithoutFileTypes/withFileTypes)?: false

    `true` if the glob should return paths as `Dirent`s, `false` otherwise.
* ### interface [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions)

  + [mode](https://bun.com/reference/node/fs/MakeDirectoryOptions/mode)?: [Mode](https://bun.com/reference/node/fs/Mode)

    A file mode. If a string is passed, it is parsed as an octal integer. If not specified
  + [recursive](https://bun.com/reference/node/fs/MakeDirectoryOptions/recursive)?: boolean

    Indicates whether parent folders should be created. If a folder was created, the path to the first created folder will be returned.
* ### interface [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions)

  + [encoding](https://bun.com/reference/node/fs/ObjectEncodingOptions/encoding)?: null | BufferEncoding
* ### interface [OpenAsBlobOptions](https://bun.com/reference/node/fs/OpenAsBlobOptions)

  + [type](https://bun.com/reference/node/fs/OpenAsBlobOptions/type)?: string

    An optional mime type for the blob.
* ### interface [OpenDirOptions](https://bun.com/reference/node/fs/OpenDirOptions)

  + [bufferSize](https://bun.com/reference/node/fs/OpenDirOptions/bufferSize)?: number

    Number of directory entries that are buffered internally when reading from the directory. Higher values lead to better performance but higher memory usage.
  + [encoding](https://bun.com/reference/node/fs/OpenDirOptions/encoding)?: BufferEncoding
  + [recursive](https://bun.com/reference/node/fs/OpenDirOptions/recursive)?: boolean
* ### interface [ReadOptions](https://bun.com/reference/node/fs/ReadOptions)

  + [length](https://bun.com/reference/node/fs/ReadOptions/length)?: number
  + [offset](https://bun.com/reference/node/fs/ReadOptions/offset)?: number
  + [position](https://bun.com/reference/node/fs/ReadOptions/position)?: null | [ReadPosition](https://bun.com/reference/node/fs/ReadPosition)
* ### interface [ReadOptionsWithBuffer](https://bun.com/reference/node/fs/ReadOptionsWithBuffer)<T extends NodeJS.ArrayBufferView>

  + [buffer](https://bun.com/reference/node/fs/ReadOptionsWithBuffer/buffer)?: T
  + [length](https://bun.com/reference/node/fs/ReadOptionsWithBuffer/length)?: number
  + [offset](https://bun.com/reference/node/fs/ReadOptionsWithBuffer/offset)?: number
  + [position](https://bun.com/reference/node/fs/ReadOptionsWithBuffer/position)?: null | [ReadPosition](https://bun.com/reference/node/fs/ReadPosition)
* ### interface [ReadVResult](https://bun.com/reference/node/fs/ReadVResult)<T extends readonly NodeJS.ArrayBufferView[] = NodeJS.ArrayBufferView[]>

  + [buffers](https://bun.com/reference/node/fs/ReadVResult/buffers): T
  + [bytesRead](https://bun.com/reference/node/fs/ReadVResult/bytesRead): number
* ### interface [RmDirOptions](https://bun.com/reference/node/fs/RmDirOptions)

  + [maxRetries](https://bun.com/reference/node/fs/RmDirOptions/maxRetries)?: number

    If an `EBUSY`, `EMFILE`, `ENFILE`, `ENOTEMPTY`, or `EPERM` error is encountered, Node.js will retry the operation with a linear backoff wait of `retryDelay` ms longer on each try. This option represents the number of retries. This option is ignored if the `recursive` option is not `true`.
  + [retryDelay](https://bun.com/reference/node/fs/RmDirOptions/retryDelay)?: number

    The amount of time in milliseconds to wait between retries. This option is ignored if the `recursive` option is not `true`.
* ### interface [RmOptions](https://bun.com/reference/node/fs/RmOptions)

  + [force](https://bun.com/reference/node/fs/RmOptions/force)?: boolean

    When `true`, exceptions will be ignored if `path` does not exist.
  + [maxRetries](https://bun.com/reference/node/fs/RmOptions/maxRetries)?: number

    If an `EBUSY`, `EMFILE`, `ENFILE`, `ENOTEMPTY`, or `EPERM` error is encountered, Node.js will retry the operation with a linear backoff wait of `retryDelay` ms longer on each try. This option represents the number of retries. This option is ignored if the `recursive` option is not `true`.
  + [recursive](https://bun.com/reference/node/fs/RmOptions/recursive)?: boolean

    If `true`, perform a recursive directory removal. In recursive mode, operations are retried on failure.
  + [retryDelay](https://bun.com/reference/node/fs/RmOptions/retryDelay)?: number

    The amount of time in milliseconds to wait between retries. This option is ignored if the `recursive` option is not `true`.
* ### interface [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions)

  + [bigint](https://bun.com/reference/node/fs/StatFsOptions/bigint)?: boolean
* ### interface [StatOptions](https://bun.com/reference/node/fs/StatOptions)

  + [bigint](https://bun.com/reference/node/fs/StatOptions/bigint)?: boolean
* ### interface [StatsBase](https://bun.com/reference/node/fs/StatsBase)<T>

  + [atime](https://bun.com/reference/node/fs/StatsBase/atime): Date
  + [atimeMs](https://bun.com/reference/node/fs/StatsBase/atimeMs): T
  + [birthtime](https://bun.com/reference/node/fs/StatsBase/birthtime): Date
  + [birthtimeMs](https://bun.com/reference/node/fs/StatsBase/birthtimeMs): T
  + [blksize](https://bun.com/reference/node/fs/StatsBase/blksize): T
  + [blocks](https://bun.com/reference/node/fs/StatsBase/blocks): T
  + [ctime](https://bun.com/reference/node/fs/StatsBase/ctime): Date
  + [ctimeMs](https://bun.com/reference/node/fs/StatsBase/ctimeMs): T
  + [dev](https://bun.com/reference/node/fs/StatsBase/dev): T
  + [gid](https://bun.com/reference/node/fs/StatsBase/gid): T
  + [ino](https://bun.com/reference/node/fs/StatsBase/ino): T
  + [mode](https://bun.com/reference/node/fs/StatsBase/mode): T
  + [mtime](https://bun.com/reference/node/fs/StatsBase/mtime): Date
  + [mtimeMs](https://bun.com/reference/node/fs/StatsBase/mtimeMs): T
  + [nlink](https://bun.com/reference/node/fs/StatsBase/nlink): T
  + [rdev](https://bun.com/reference/node/fs/StatsBase/rdev): T
  + [size](https://bun.com/reference/node/fs/StatsBase/size): T
  + [uid](https://bun.com/reference/node/fs/StatsBase/uid): T
  + [isBlockDevice](https://bun.com/reference/node/fs/StatsBase/isBlockDevice)(): boolean;
  + [isCharacterDevice](https://bun.com/reference/node/fs/StatsBase/isCharacterDevice)(): boolean;
  + [isDirectory](https://bun.com/reference/node/fs/StatsBase/isDirectory)(): boolean;
  + [isFIFO](https://bun.com/reference/node/fs/StatsBase/isFIFO)(): boolean;
  + [isFile](https://bun.com/reference/node/fs/StatsBase/isFile)(): boolean;
  + [isSocket](https://bun.com/reference/node/fs/StatsBase/isSocket)(): boolean;
  + [isSymbolicLink](https://bun.com/reference/node/fs/StatsBase/isSymbolicLink)(): boolean;
* ### interface [StatsFsBase](https://bun.com/reference/node/fs/StatsFsBase)<T>

  + [bavail](https://bun.com/reference/node/fs/StatsFsBase/bavail): T

    Available blocks for unprivileged users
  + [bfree](https://bun.com/reference/node/fs/StatsFsBase/bfree): T

    Free blocks in file system.
  + [blocks](https://bun.com/reference/node/fs/StatsFsBase/blocks): T

    Total data blocks in file system.
  + [bsize](https://bun.com/reference/node/fs/StatsFsBase/bsize): T

    Optimal transfer block size.
  + [ffree](https://bun.com/reference/node/fs/StatsFsBase/ffree): T

    Free file nodes in file system.
  + [files](https://bun.com/reference/node/fs/StatsFsBase/files): T

    Total file nodes in file system.
  + [type](https://bun.com/reference/node/fs/StatsFsBase/type): T

    Type of file system.
* ### interface [StatSyncFn](https://bun.com/reference/node/fs/StatSyncFn)

  + [[metadata]](https://bun.com/reference/node/fs/StatSyncFn/[metadata]): null | DecoratorMetadataObject
  + [arguments](https://bun.com/reference/node/fs/StatSyncFn/arguments): any
  + [caller](https://bun.com/reference/node/fs/StatSyncFn/caller): Function
  + readonly [length](https://bun.com/reference/node/fs/StatSyncFn/length): number
  + readonly [name](https://bun.com/reference/node/fs/StatSyncFn/name): string

    Returns the name of the function. Function names are read-only and can not be changed.
  + [prototype](https://bun.com/reference/node/fs/StatSyncFn/prototype): any
  + [[Symbol.hasInstance]](https://bun.com/reference/node/fs/StatSyncFn/[hasInstance])(

    value: any

    ): boolean;

    Determines whether the given value inherits from this function if this function was used as a constructor function.

    A constructor function can control which objects are recognized as its instances by 'instanceof' by overriding this method.
  + [apply](https://bun.com/reference/node/fs/StatSyncFn/apply)(

    this: Function,

    thisArg: any,

    argArray?: any

    ): any;

    Calls the function, substituting the specified object for the this value of the function, and the specified array for the arguments of the function.

    @param thisArg

    The object to be used as the this object.

    @param argArray

    A set of arguments to be passed to the function.
  + [bind](https://bun.com/reference/node/fs/StatSyncFn/bind)(

    this: Function,

    thisArg: any,

    ...argArray: any[]

    ): any;

    For a given function, creates a bound function that has the same body as the original function. The this object of the bound function is associated with the specified object, and has the specified initial parameters.

    @param thisArg

    An object to which the this keyword can refer inside the new function.

    @param argArray

    A list of arguments to be passed to the new function.
  + [call](https://bun.com/reference/node/fs/StatSyncFn/call)(

    this: Function,

    thisArg: any,

    ...argArray: any[]

    ): any;

    Calls a method of an object, substituting another object for the current object.

    @param thisArg

    The object to be used as the current object.

    @param argArray

    A list of arguments to be passed to the method.
  + [toString](https://bun.com/reference/node/fs/StatSyncFn/toString)(): string;

    Returns a string representation of a function.
* ### interface [StatSyncOptions](https://bun.com/reference/node/fs/StatSyncOptions)

  + [bigint](https://bun.com/reference/node/fs/StatSyncOptions/bigint)?: boolean
  + [throwIfNoEntry](https://bun.com/reference/node/fs/StatSyncOptions/throwIfNoEntry)?: boolean
* ### interface [StatWatcher](https://bun.com/reference/node/fs/StatWatcher)

  Class: fs.StatWatcher

  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/fs/StatWatcher/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/fs/StatWatcher/addListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [emit](https://bun.com/reference/node/fs/StatWatcher/emit)<K>(

    eventName: string | symbol,

    ...args: AnyRest

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```
  + [eventNames](https://bun.com/reference/node/fs/StatWatcher/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getMaxListeners](https://bun.com/reference/node/fs/StatWatcher/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/fs/StatWatcher/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/fs/StatWatcher/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/fs/StatWatcher/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/fs/StatWatcher/on)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/fs/StatWatcher/once)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [prependListener](https://bun.com/reference/node/fs/StatWatcher/prependListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/fs/StatWatcher/prependOnceListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [rawListeners](https://bun.com/reference/node/fs/StatWatcher/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/fs/StatWatcher/ref)(): this;

    When called, requests that the Node.js event loop *not* exit so long as the `fs.StatWatcher` is active. Calling `watcher.ref()` multiple times will have no effect.

    By default, all `fs.StatWatcher` objects are "ref'ed", making it normally unnecessary to call `watcher.ref()` unless `watcher.unref()` had been called previously.
  + [removeAllListeners](https://bun.com/reference/node/fs/StatWatcher/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/fs/StatWatcher/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setMaxListeners](https://bun.com/reference/node/fs/StatWatcher/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [unref](https://bun.com/reference/node/fs/StatWatcher/unref)(): this;

    When called, the active `fs.StatWatcher` object will not require the Node.js event loop to remain active. If there is no other activity keeping the event loop running, the process may exit before the `fs.StatWatcher` object's callback is invoked. Calling `watcher.unref()` multiple times will have no effect.
* ### interface [Utf8StreamOptions](https://bun.com/reference/node/fs/Utf8StreamOptions)

  + [append](https://bun.com/reference/node/fs/Utf8StreamOptions/append)?: boolean

    Appends writes to dest file instead of truncating it.
  + [contentMode](https://bun.com/reference/node/fs/Utf8StreamOptions/contentMode)?: 'utf8' | 'buffer'

    Which type of data you can send to the write function, supported values are `'utf8'` or `'buffer'`.
  + [dest](https://bun.com/reference/node/fs/Utf8StreamOptions/dest)?: string

    A path to a file to be written to (mode controlled by the append option).
  + [fd](https://bun.com/reference/node/fs/Utf8StreamOptions/fd)?: number

    A file descriptor, something that is returned by `fs.open()` or `fs.openSync()`.
  + [fs](https://bun.com/reference/node/fs/Utf8StreamOptions/fs)?: object

    An object that has the same API as the `fs` module, useful for mocking, testing, or customizing the behavior of the stream.
  + [fsync](https://bun.com/reference/node/fs/Utf8StreamOptions/fsync)?: boolean

    Perform a `fs.fsyncSync()` every time a write is completed.
  + [maxLength](https://bun.com/reference/node/fs/Utf8StreamOptions/maxLength)?: number

    The maximum length of the internal buffer. If a write operation would cause the buffer to exceed `maxLength`, the data written is dropped and a drop event is emitted with the dropped data
  + [maxWrite](https://bun.com/reference/node/fs/Utf8StreamOptions/maxWrite)?: number

    The maximum number of bytes that can be written;
  + [minLength](https://bun.com/reference/node/fs/Utf8StreamOptions/minLength)?: number

    The minimum length of the internal buffer that is required to be full before flushing.
  + [mkdir](https://bun.com/reference/node/fs/Utf8StreamOptions/mkdir)?: boolean

    Ensure directory for `dest` file exists when true.
  + [mode](https://bun.com/reference/node/fs/Utf8StreamOptions/mode)?: string | number

    Specify the creating file mode (see `fs.open()`).
  + [periodicFlush](https://bun.com/reference/node/fs/Utf8StreamOptions/periodicFlush)?: number

    Calls flush every `periodicFlush` milliseconds.
  + [retryEAGAIN](https://bun.com/reference/node/fs/Utf8StreamOptions/retryEAGAIN)?: (err: null | [Error](https://bun.com/reference/globals/Error), writeBufferLen: number, remainingBufferLen: number) => boolean

    A function that will be called when `write()`, `writeSync()`, or `flushSync()` encounters an `EAGAIN` or `EBUSY` error. If the return value is `true` the operation will be retried, otherwise it will bubble the error. The `err` is the error that caused this function to be called, `writeBufferLen` is the length of the buffer that was written, and `remainingBufferLen` is the length of the remaining buffer that the stream did not try to write.
  + [sync](https://bun.com/reference/node/fs/Utf8StreamOptions/sync)?: boolean

    Perform writes synchronously.
* ### interface [WatchFileOptions](https://bun.com/reference/node/fs/WatchFileOptions)

  Watch for changes on `filename`. The callback `listener` will be called each time the file is accessed.

  The `options` argument may be omitted. If provided, it should be an object. The `options` object may contain a boolean named `persistent` that indicates whether the process should continue to run as long as files are being watched. The `options` object may specify an `interval` property indicating how often the target should be polled in milliseconds.

  The `listener` gets two arguments the current stat object and the previous stat object:

  ```
  import { watchFile } from 'node:fs';

  watchFile('message.text', (curr, prev) => {
    console.log(`the current mtime is: ${curr.mtime}`);
    console.log(`the previous mtime was: ${prev.mtime}`);
  });
  ```

  These stat objects are instances of `fs.Stat`. If the `bigint` option is `true`, the numeric values in these objects are specified as `BigInt`s.

  To be notified when the file was modified, not just accessed, it is necessary to compare `curr.mtimeMs` and `prev.mtimeMs`.

  When an `fs.watchFile` operation results in an `ENOENT` error, it will invoke the listener once, with all the fields zeroed (or, for dates, the Unix Epoch). If the file is created later on, the listener will be called again, with the latest stat objects. This is a change in functionality since v0.10.

  Using watch is more efficient than `fs.watchFile` and `fs.unwatchFile`. `fs.watch` should be used instead of `fs.watchFile` and `fs.unwatchFile` when possible.

  When a file being watched by `fs.watchFile()` disappears and reappears, then the contents of `previous` in the second callback event (the file's reappearance) will be the same as the contents of `previous` in the first callback event (its disappearance).

  This happens when:

  + the file is deleted, followed by a restore
  + the file is renamed and then renamed a second time back to its original name

  + [bigint](https://bun.com/reference/node/fs/WatchFileOptions/bigint)?: boolean
  + [interval](https://bun.com/reference/node/fs/WatchFileOptions/interval)?: number
  + [persistent](https://bun.com/reference/node/fs/WatchFileOptions/persistent)?: boolean
* ### interface [WatchOptions](https://bun.com/reference/node/fs/WatchOptions)

  + [encoding](https://bun.com/reference/node/fs/WatchOptions/encoding)?: BufferEncoding | 'buffer'
  + [persistent](https://bun.com/reference/node/fs/WatchOptions/persistent)?: boolean
  + [recursive](https://bun.com/reference/node/fs/WatchOptions/recursive)?: boolean
  + [signal](https://bun.com/reference/node/fs/WatchOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
* ### interface [WatchOptionsWithBufferEncoding](https://bun.com/reference/node/fs/WatchOptionsWithBufferEncoding)

  + [encoding](https://bun.com/reference/node/fs/WatchOptionsWithBufferEncoding/encoding): 'buffer'
  + [persistent](https://bun.com/reference/node/fs/WatchOptionsWithBufferEncoding/persistent)?: boolean
  + [recursive](https://bun.com/reference/node/fs/WatchOptionsWithBufferEncoding/recursive)?: boolean
  + [signal](https://bun.com/reference/node/fs/WatchOptionsWithBufferEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
* ### interface [WatchOptionsWithStringEncoding](https://bun.com/reference/node/fs/WatchOptionsWithStringEncoding)

  + [encoding](https://bun.com/reference/node/fs/WatchOptionsWithStringEncoding/encoding)?: BufferEncoding
  + [persistent](https://bun.com/reference/node/fs/WatchOptionsWithStringEncoding/persistent)?: boolean
  + [recursive](https://bun.com/reference/node/fs/WatchOptionsWithStringEncoding/recursive)?: boolean
  + [signal](https://bun.com/reference/node/fs/WatchOptionsWithStringEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
* ### interface [WriteOptions](https://bun.com/reference/node/fs/WriteOptions)

  + [length](https://bun.com/reference/node/fs/WriteOptions/length)?: number
  + [offset](https://bun.com/reference/node/fs/WriteOptions/offset)?: number
  + [position](https://bun.com/reference/node/fs/WriteOptions/position)?: null | number
* ### interface [WriteVResult](https://bun.com/reference/node/fs/WriteVResult)<T extends readonly NodeJS.ArrayBufferView[] = NodeJS.ArrayBufferView[]>

  + [buffers](https://bun.com/reference/node/fs/WriteVResult/buffers): T
  + [bytesWritten](https://bun.com/reference/node/fs/WriteVResult/bytesWritten): number
* type [BigIntStatsListener](https://bun.com/reference/node/fs/BigIntStatsListener) = (curr: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats), prev: [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)) => void
* type [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption) = 'buffer' | { encoding: 'buffer' }
* type [EncodingOption](https://bun.com/reference/node/fs/EncodingOption) = [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) | BufferEncoding | undefined | null
* type [Mode](https://bun.com/reference/node/fs/Mode) = number | string
* type [NoParamCallback](https://bun.com/reference/node/fs/NoParamCallback) = (err: NodeJS.ErrnoException | null) => void
* type [OpenMode](https://bun.com/reference/node/fs/OpenMode) = number | string
* type [PathLike](https://bun.com/reference/node/fs/PathLike) = string | [Buffer](https://bun.com/reference/node/buffer/Buffer) | [URL](https://bun.com/reference/node/url/URL)

  Valid types for path values in "fs".
* type [PathOrFileDescriptor](https://bun.com/reference/node/fs/PathOrFileDescriptor) = [PathLike](https://bun.com/reference/node/fs/PathLike) | number
* type [ReadPosition](https://bun.com/reference/node/fs/ReadPosition) = number | bigint
* type [StatsListener](https://bun.com/reference/node/fs/StatsListener) = (curr: [Stats](https://bun.com/reference/node/fs/Stats), prev: [Stats](https://bun.com/reference/node/fs/Stats)) => void
* type [TimeLike](https://bun.com/reference/node/fs/TimeLike) = string | number | Date
* type [WatchEventType](https://bun.com/reference/node/fs/WatchEventType) = 'rename' | 'change'
* type [WatchListener](https://bun.com/reference/node/fs/WatchListener)<T> = (event: [WatchEventType](https://bun.com/reference/node/fs/WatchEventType), filename: T | null) => void
* type [WriteFileOptions](https://bun.com/reference/node/fs/WriteFileOptions) = [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & [Abortable](https://bun.com/reference/node/events/default/Abortable) & { flag: string; flush: boolean; mode: [Mode](https://bun.com/reference/node/fs/Mode) } | BufferEncoding | null