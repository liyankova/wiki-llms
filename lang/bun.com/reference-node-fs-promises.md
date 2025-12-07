---
url: https://bun.com/reference/node/fs/promises
title: Node.js fs/promises module | API Reference | Bun
source_domain: bun.com
---

# Node.js fs/promises module | API Reference | Bun

Node.js module

# [fs/promises](https://bun.com/reference/node/fs/promises)

The `'node:fs/promises'` module provides Promise-based variants of the `fs` API, allowing asynchronous file operations to be performed with async/await syntax.

* const [constants](https://bun.com/reference/node/fs/promises/constants): typeof [fsConstants](https://bun.com/reference/node/fs/constants)
* function [access](https://bun.com/reference/node/fs/promises/access)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode?: number

  ): Promise<void>;

  Tests a user's permissions for the file or directory specified by `path`. The `mode` argument is an optional integer that specifies the accessibility checks to be performed. `mode` should be either the value `fs.constants.F_OK` or a mask consisting of the bitwise OR of any of `fs.constants.R_OK`, `fs.constants.W_OK`, and `fs.constants.X_OK` (e.g.`fs.constants.W_OK | fs.constants.R_OK`). Check `File access constants` for possible values of `mode`.

  If the accessibility check is successful, the promise is fulfilled with no value. If any of the accessibility checks fail, the promise is rejected with an [Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) object. The following example checks if the file`/etc/passwd` can be read and written by the current process.

  ```
  import { access, constants } from 'node:fs/promises';

  try {
    await access('/etc/passwd', constants.R_OK | constants.W_OK);
    console.log('can access');
  } catch {
    console.error('cannot access');
  }
  ```

  Using `fsPromises.access()` to check for the accessibility of a file before calling `fsPromises.open()` is not recommended. Doing so introduces a race condition, since other processes may change the file's state between the two calls. Instead, user code should open/read/write the file directly and handle the error raised if the file is not accessible.

  @returns

  Fulfills with `undefined` upon success.
* function [appendFile](https://bun.com/reference/node/fs/promises/appendFile)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike) | [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle),

  data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & [FlagAndOpenMode](https://bun.com/reference/node/fs/promises/FlagAndOpenMode) & { flush: boolean }

  ): Promise<void>;

  Asynchronously append data to a file, creating the file if it does not yet exist. `data` can be a string or a `Buffer`.

  If `options` is a string, then it specifies the `encoding`.

  The `mode` option only affects the newly created file. See `fs.open()` for more details.

  The `path` may be specified as a `FileHandle` that has been opened for appending (using `fsPromises.open()`).

  @param path

  filename or {FileHandle}

  @returns

  Fulfills with `undefined` upon success.
* function [chmod](https://bun.com/reference/node/fs/promises/chmod)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode: [Mode](https://bun.com/reference/node/fs/Mode)

  ): Promise<void>;

  Changes the permissions of a file.

  @returns

  Fulfills with `undefined` upon success.
* function [chown](https://bun.com/reference/node/fs/promises/chown)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number

  ): Promise<void>;

  Changes the ownership of a file.

  @returns

  Fulfills with `undefined` upon success.
* function [copyFile](https://bun.com/reference/node/fs/promises/copyFile)(

  src: [PathLike](https://bun.com/reference/node/fs/PathLike),

  dest: [PathLike](https://bun.com/reference/node/fs/PathLike),

  mode?: number

  ): Promise<void>;

  Asynchronously copies `src` to `dest`. By default, `dest` is overwritten if it already exists.

  No guarantees are made about the atomicity of the copy operation. If an error occurs after the destination file has been opened for writing, an attempt will be made to remove the destination.

  ```
  import { copyFile, constants } from 'node:fs/promises';

  try {
    await copyFile('source.txt', 'destination.txt');
    console.log('source.txt was copied to destination.txt');
  } catch {
    console.error('The file could not be copied');
  }

  // By using COPYFILE_EXCL, the operation will fail if destination.txt exists.
  try {
    await copyFile('source.txt', 'destination.txt', constants.COPYFILE_EXCL);
    console.log('source.txt was copied to destination.txt');
  } catch {
    console.error('The file could not be copied');
  }
  ```

  @param src

  source filename to copy

  @param dest

  destination filename of the copy operation

  @param mode

  Optional modifiers that specify the behavior of the copy operation. It is possible to create a mask consisting of the bitwise OR of two or more values (e.g. `fs.constants.COPYFILE_EXCL | fs.constants.COPYFILE_FICLONE`)

  @returns

  Fulfills with `undefined` upon success.
* function [cp](https://bun.com/reference/node/fs/promises/cp)(

  source: string | [URL](https://bun.com/reference/globals/URL),

  destination: string | [URL](https://bun.com/reference/globals/URL),

  opts?: [CopyOptions](https://bun.com/reference/node/fs/CopyOptions)

  ): Promise<void>;

  Asynchronously copies the entire directory structure from `src` to `dest`, including subdirectories and files.

  When copying a directory to another directory, globs are not supported and behavior is similar to `cp dir1/ dir2/`.

  @returns

  Fulfills with `undefined` upon success.
* function [exists](https://bun.com/reference/node/fs/promises/exists)(

  path: [PathLike](https://bun.com/reference/bun/PathLike)

  ): Promise<boolean>;
* function [glob](https://bun.com/reference/node/fs/promises/glob)(

  pattern: string | readonly string[]

  ): AsyncIterator<string>;

  ```
  import { glob } from 'node:fs/promises';

  for await (const entry of glob('*.js'))
    console.log(entry);
  ```

  @returns

  An AsyncIterator that yields the paths of files that match the pattern.

  function [glob](https://bun.com/reference/node/fs/promises/glob)(

  pattern: string | readonly string[],

  options: [GlobOptionsWithFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithFileTypes)

  ): AsyncIterator<[Dirent](https://bun.com/reference/node/fs/Dirent)<string>>;

  ```
  import { glob } from 'node:fs/promises';

  for await (const entry of glob('*.js'))
    console.log(entry);
  ```

  @returns

  An AsyncIterator that yields the paths of files that match the pattern.

  function [glob](https://bun.com/reference/node/fs/promises/glob)(

  pattern: string | readonly string[],

  options: [GlobOptionsWithoutFileTypes](https://bun.com/reference/node/fs/GlobOptionsWithoutFileTypes)

  ): AsyncIterator<string>;

  ```
  import { glob } from 'node:fs/promises';

  for await (const entry of glob('*.js'))
    console.log(entry);
  ```

  @returns

  An AsyncIterator that yields the paths of files that match the pattern.

  function [glob](https://bun.com/reference/node/fs/promises/glob)(

  pattern: string | readonly string[],

  options: [GlobOptions](https://bun.com/reference/node/fs/GlobOptions)

  ): AsyncIterator<string | [Dirent](https://bun.com/reference/node/fs/Dirent)<string>>;

  ```
  import { glob } from 'node:fs/promises';

  for await (const entry of glob('*.js'))
    console.log(entry);
  ```

  @returns

  An AsyncIterator that yields the paths of files that match the pattern.
* function [lchown](https://bun.com/reference/node/fs/promises/lchown)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  uid: number,

  gid: number

  ): Promise<void>;

  Changes the ownership on a symbolic link.

  @returns

  Fulfills with `undefined` upon success.
* function [link](https://bun.com/reference/node/fs/promises/link)(

  existingPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike)

  ): Promise<void>;

  Creates a new link from the `existingPath` to the `newPath`. See the POSIX [`link(2)`](http://man7.org/linux/man-pages/man2/link.2.html) documentation for more detail.

  @returns

  Fulfills with `undefined` upon success.
* function [lstat](https://bun.com/reference/node/fs/promises/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts?: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false }

  ): Promise<[Stats](https://bun.com/reference/node/fs/Stats)>;

  Equivalent to `fsPromises.stat()` unless `path` refers to a symbolic link, in which case the link itself is stat-ed, not the file that it refers to. Refer to the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) document for more detail.

  @returns

  Fulfills with the {fs.Stats} object for the given symbolic link `path`.

  function [lstat](https://bun.com/reference/node/fs/promises/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true }

  ): Promise<[BigIntStats](https://bun.com/reference/node/fs/BigIntStats)>;

  Equivalent to `fsPromises.stat()` unless `path` refers to a symbolic link, in which case the link itself is stat-ed, not the file that it refers to. Refer to the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) document for more detail.

  @returns

  Fulfills with the {fs.Stats} object for the given symbolic link `path`.

  function [lstat](https://bun.com/reference/node/fs/promises/lstat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts?: [StatOptions](https://bun.com/reference/node/fs/StatOptions)

  ): Promise<[Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)>;

  Equivalent to `fsPromises.stat()` unless `path` refers to a symbolic link, in which case the link itself is stat-ed, not the file that it refers to. Refer to the POSIX [`lstat(2)`](http://man7.org/linux/man-pages/man2/lstat.2.html) document for more detail.

  @returns

  Fulfills with the {fs.Stats} object for the given symbolic link `path`.
* function [lutimes](https://bun.com/reference/node/fs/promises/lutimes)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike)

  ): Promise<void>;

  Changes the access and modification times of a file in the same way as `fsPromises.utimes()`, with the difference that if the path refers to a symbolic link, then the link is not dereferenced: instead, the timestamps of the symbolic link itself are changed.

  @returns

  Fulfills with `undefined` upon success.
* function [mkdir](https://bun.com/reference/node/fs/promises/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: true }

  ): Promise<undefined | string>;

  Asynchronously creates a directory.

  The optional `options` argument can be an integer specifying `mode` (permission and sticky bits), or an object with a `mode` property and a `recursive` property indicating whether parent directories should be created. Calling `fsPromises.mkdir()` when `path` is a directory that exists results in a rejection only when `recursive` is false.

  ```
  import { mkdir } from 'node:fs/promises';

  try {
    const projectFolder = new URL('./test/project/', import.meta.url);
    const createDir = await mkdir(projectFolder, { recursive: true });

    console.log(`created ${createDir}`);
  } catch (err) {
    console.error(err.message);
  }
  ```

  @returns

  Upon success, fulfills with `undefined` if `recursive` is `false`, or the first directory path created if `recursive` is `true`.

  function [mkdir](https://bun.com/reference/node/fs/promises/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions) & { recursive: false }

  ): Promise<void>;

  Asynchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.

  function [mkdir](https://bun.com/reference/node/fs/promises/mkdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | [Mode](https://bun.com/reference/node/fs/Mode) | [MakeDirectoryOptions](https://bun.com/reference/node/fs/MakeDirectoryOptions)

  ): Promise<undefined | string>;

  Asynchronous mkdir(2) - create a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  Either the file mode, or an object optionally specifying the file mode and whether parent folders should be created. If a string is passed, it is parsed as an octal integer. If not specified, defaults to `0o777`.
* function [mkdtemp](https://bun.com/reference/node/fs/promises/mkdtemp)(

  prefix: string,

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions)

  ): Promise<string>;

  Creates a unique temporary directory. A unique directory name is generated by appending six random characters to the end of the provided `prefix`. Due to platform inconsistencies, avoid trailing `X` characters in `prefix`. Some platforms, notably the BSDs, can return more than six random characters, and replace trailing `X` characters in `prefix` with random characters.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use.

  ```
  import { mkdtemp } from 'node:fs/promises';
  import { join } from 'node:path';
  import { tmpdir } from 'node:os';

  try {
    await mkdtemp(join(tmpdir(), 'foo-'));
  } catch (err) {
    console.error(err);
  }
  ```

  The `fsPromises.mkdtemp()` method will append the six randomly selected characters directly to the `prefix` string. For instance, given a directory `/tmp`, if the intention is to create a temporary directory *within* `/tmp`, the `prefix` must end with a trailing platform-specific path separator (`import { sep } from 'node:path'`).

  @returns

  Fulfills with a string containing the file system path of the newly created temporary directory.

  function [mkdtemp](https://bun.com/reference/node/fs/promises/mkdtemp)(

  prefix: string,

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): Promise<NonSharedBuffer>;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required `prefix` to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [mkdtemp](https://bun.com/reference/node/fs/promises/mkdtemp)(

  prefix: string,

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions)

  ): Promise<string | NonSharedBuffer>;

  Asynchronously creates a unique temporary directory. Generates six random characters to be appended behind a required `prefix` to create a unique temporary directory.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.
* function [mkdtempDisposable](https://bun.com/reference/node/fs/promises/mkdtempDisposable)(

  prefix: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [EncodingOption](https://bun.com/reference/node/fs/EncodingOption)

  ): Promise<[DisposableTempDir](https://bun.com/reference/node/fs/DisposableTempDir)>;

  The resulting Promise holds an async-disposable object whose `path` property holds the created directory path. When the object is disposed, the directory and its contents will be removed asynchronously if it still exists. If the directory cannot be deleted, disposal will throw an error. The object has an async `remove()` method which will perform the same task.

  Both this function and the disposal function on the resulting object are async, so it should be used with `await` + `await using` as in `await using dir = await fsPromises.mkdtempDisposable('prefix')`.

  <!-- TODO: link MDN docs for disposables once https://github.com/mdn/content/pull/38027 lands -->

  For detailed information, see the documentation of `fsPromises.mkdtemp()`.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use.
* function [open](https://bun.com/reference/node/fs/promises/open)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  flags?: string | number,

  mode?: [Mode](https://bun.com/reference/node/fs/Mode)

  ): Promise<[FileHandle](https://bun.com/reference/node/fs/promises/FileHandle)>;

  Opens a `FileHandle`.

  Refer to the POSIX [`open(2)`](http://man7.org/linux/man-pages/man2/open.2.html) documentation for more detail.

  Some characters (`< > : " / \ | ? *`) are reserved under Windows as documented by [Naming Files, Paths, and Namespaces](https://docs.microsoft.com/en-us/windows/desktop/FileIO/naming-a-file). Under NTFS, if the filename contains a colon, Node.js will open a file system stream, as described by [this MSDN page](https://docs.microsoft.com/en-us/windows/desktop/FileIO/using-streams).

  @param flags

  See `support of file system` flags``.

  @param mode

  Sets the file mode (permission and sticky bits) if the file is created.

  @returns

  Fulfills with a {FileHandle} object.
* function [opendir](https://bun.com/reference/node/fs/promises/opendir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [OpenDirOptions](https://bun.com/reference/node/fs/OpenDirOptions)

  ): Promise<[Dir](https://bun.com/reference/node/fs/Dir)>;

  Asynchronously open a directory for iterative scanning. See the POSIX [`opendir(3)`](http://man7.org/linux/man-pages/man3/opendir.3.html) documentation for more detail.

  Creates an `fs.Dir`, which contains all further functions for reading from and cleaning up the directory.

  The `encoding` option sets the encoding for the `path` while opening the directory and subsequent read operations.

  Example using async iteration:

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

  @returns

  Fulfills with an {fs.Dir}.
* function [readdir](https://bun.com/reference/node/fs/promises/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: false }

  ): Promise<string[]>;

  Reads the contents of a directory.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the filenames. If the `encoding` is set to `'buffer'`, the filenames returned will be passed as `Buffer` objects.

  If `options.withFileTypes` is set to `true`, the returned array will contain `fs.Dirent` objects.

  ```
  import { readdir } from 'node:fs/promises';

  try {
    const files = await readdir(path);
    for (const file of files)
      console.log(file);
  } catch (err) {
    console.error(err);
  }
  ```

  @returns

  Fulfills with an array of the names of the files in the directory excluding `'.'` and `'..'`.

  function [readdir](https://bun.com/reference/node/fs/promises/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: 'buffer' | { encoding: 'buffer'; recursive: boolean; withFileTypes: false }

  ): Promise<NonSharedBuffer[]>;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdir](https://bun.com/reference/node/fs/promises/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: false }

  ): Promise<string[] | NonSharedBuffer[]>;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readdir](https://bun.com/reference/node/fs/promises/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { recursive: boolean; withFileTypes: true }

  ): Promise<[Dirent](https://bun.com/reference/node/fs/Dirent)<string>[]>;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  If called with `withFileTypes: true` the result data will be an array of Dirent.

  function [readdir](https://bun.com/reference/node/fs/promises/readdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: { encoding: 'buffer'; recursive: boolean; withFileTypes: true }

  ): Promise<[Dirent](https://bun.com/reference/node/fs/Dirent)<NonSharedBuffer>[]>;

  Asynchronous readdir(3) - read a directory.

  @param path

  A path to a directory. If a URL is provided, it must use the `file:` protocol.

  @param options

  Must include `withFileTypes: true` and `encoding: 'buffer'`.
* function [readFile](https://bun.com/reference/node/fs/promises/readFile)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike) | [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle),

  options?: null | { encoding: null; flag: [OpenMode](https://bun.com/reference/node/fs/OpenMode) } & [Abortable](https://bun.com/reference/node/events/default/Abortable)

  ): Promise<NonSharedBuffer>;

  Asynchronously reads the entire contents of a file.

  If no encoding is specified (using `options.encoding`), the data is returned as a `Buffer` object. Otherwise, the data will be a string.

  If `options` is a string, then it specifies the encoding.

  When the `path` is a directory, the behavior of `fsPromises.readFile()` is platform-specific. On macOS, Linux, and Windows, the promise will be rejected with an error. On FreeBSD, a representation of the directory's contents will be returned.

  An example of reading a `package.json` file located in the same directory of the running code:

  ```
  import { readFile } from 'node:fs/promises';
  try {
    const filePath = new URL('./package.json', import.meta.url);
    const contents = await readFile(filePath, { encoding: 'utf8' });
    console.log(contents);
  } catch (err) {
    console.error(err.message);
  }
  ```

  It is possible to abort an ongoing `readFile` using an `AbortSignal`. If a request is aborted the promise returned is rejected with an `AbortError`:

  ```
  import { readFile } from 'node:fs/promises';

  try {
    const controller = new AbortController();
    const { signal } = controller;
    const promise = readFile(fileName, { signal });

    // Abort the request before the promise settles.
    controller.abort();

    await promise;
  } catch (err) {
    // When a request is aborted - err is an AbortError
    console.error(err);
  }
  ```

  Aborting an ongoing request does not abort individual operating system requests but rather the internal buffering `fs.readFile` performs.

  Any specified `FileHandle` has to support reading.

  @param path

  filename or `FileHandle`

  @returns

  Fulfills with the contents of the file.

  function [readFile](https://bun.com/reference/node/fs/promises/readFile)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike) | [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle),

  options: BufferEncoding | { encoding: BufferEncoding; flag: unknown } & [Abortable](https://bun.com/reference/node/events/default/Abortable)

  ): Promise<string>;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a `FileHandle` is provided, the underlying file will *not* be closed automatically.

  @param options

  An object that may contain an optional flag. If a flag is not provided, it defaults to `'r'`.

  function [readFile](https://bun.com/reference/node/fs/promises/readFile)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike) | [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & [Abortable](https://bun.com/reference/node/events/default/Abortable) & { flag: unknown }

  ): Promise<string | NonSharedBuffer>;

  Asynchronously reads the entire contents of a file.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol. If a `FileHandle` is provided, the underlying file will *not* be closed automatically.

  @param options

  An object that may contain an optional flag. If a flag is not provided, it defaults to `'r'`.
* function [readlink](https://bun.com/reference/node/fs/promises/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions)

  ): Promise<string>;

  Reads the contents of the symbolic link referred to by `path`. See the POSIX [`readlink(2)`](http://man7.org/linux/man-pages/man2/readlink.2.html) documentation for more detail. The promise is fulfilled with the`linkString` upon success.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the link path returned. If the `encoding` is set to `'buffer'`, the link path returned will be passed as a `Buffer` object.

  @returns

  Fulfills with the `linkString` upon success.

  function [readlink](https://bun.com/reference/node/fs/promises/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): Promise<NonSharedBuffer>;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [readlink](https://bun.com/reference/node/fs/promises/readlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | string | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions)

  ): Promise<string | NonSharedBuffer>;

  Asynchronous readlink(2) - read value of a symbolic link.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.
* function [realpath](https://bun.com/reference/node/fs/promises/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions)

  ): Promise<string>;

  Determines the actual location of `path` using the same semantics as the `fs.realpath.native()` function.

  Only paths that can be converted to UTF8 strings are supported.

  The optional `options` argument can be a string specifying an encoding, or an object with an `encoding` property specifying the character encoding to use for the path. If the `encoding` is set to `'buffer'`, the path returned will be passed as a `Buffer` object.

  On Linux, when Node.js is linked against musl libc, the procfs file system must be mounted on `/proc` in order for this function to work. Glibc does not have this restriction.

  @returns

  Fulfills with the resolved path upon success.

  function [realpath](https://bun.com/reference/node/fs/promises/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: [BufferEncodingOption](https://bun.com/reference/node/fs/BufferEncodingOption)

  ): Promise<NonSharedBuffer>;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.

  function [realpath](https://bun.com/reference/node/fs/promises/realpath)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions)

  ): Promise<string | NonSharedBuffer>;

  Asynchronous realpath(3) - return the canonicalized absolute pathname.

  @param path

  A path to a file. If a URL is provided, it must use the `file:` protocol.

  @param options

  The encoding (or an object specifying the encoding), used as the encoding of the result. If not provided, `'utf8'` is used.
* function [rename](https://bun.com/reference/node/fs/promises/rename)(

  oldPath: [PathLike](https://bun.com/reference/node/fs/PathLike),

  newPath: [PathLike](https://bun.com/reference/node/fs/PathLike)

  ): Promise<void>;

  Renames `oldPath` to `newPath`.

  @returns

  Fulfills with `undefined` upon success.
* function [rm](https://bun.com/reference/node/fs/promises/rm)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [RmOptions](https://bun.com/reference/node/fs/RmOptions)

  ): Promise<void>;

  Removes files and directories (modeled on the standard POSIX `rm` utility).

  @returns

  Fulfills with `undefined` upon success.
* function [rmdir](https://bun.com/reference/node/fs/promises/rmdir)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: [RmDirOptions](https://bun.com/reference/node/fs/RmDirOptions)

  ): Promise<void>;

  Removes the directory identified by `path`.

  Using `fsPromises.rmdir()` on a file (not a directory) results in the promise being rejected with an `ENOENT` error on Windows and an `ENOTDIR` error on POSIX.

  To get a behavior similar to the `rm -rf` Unix command, use `fsPromises.rm()` with options `{ recursive: true, force: true }`.

  @returns

  Fulfills with `undefined` upon success.
* function [stat](https://bun.com/reference/node/fs/promises/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts?: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false }

  ): Promise<[Stats](https://bun.com/reference/node/fs/Stats)>;

  @returns

  Fulfills with the {fs.Stats} object for the given `path`.

  function [stat](https://bun.com/reference/node/fs/promises/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true }

  ): Promise<[BigIntStats](https://bun.com/reference/node/fs/BigIntStats)>;

  @returns

  Fulfills with the {fs.Stats} object for the given `path`.

  function [stat](https://bun.com/reference/node/fs/promises/stat)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts?: [StatOptions](https://bun.com/reference/node/fs/StatOptions)

  ): Promise<[Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)>;

  @returns

  Fulfills with the {fs.Stats} object for the given `path`.
* function [statfs](https://bun.com/reference/node/fs/promises/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts?: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: false }

  ): Promise<[StatsFs](https://bun.com/reference/node/fs/StatsFs)>;

  @returns

  Fulfills with the {fs.StatFs} object for the given `path`.

  function [statfs](https://bun.com/reference/node/fs/promises/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions) & { bigint: true }

  ): Promise<[BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs)>;

  @returns

  Fulfills with the {fs.StatFs} object for the given `path`.

  function [statfs](https://bun.com/reference/node/fs/promises/statfs)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  opts?: [StatFsOptions](https://bun.com/reference/node/fs/StatFsOptions)

  ): Promise<[StatsFs](https://bun.com/reference/node/fs/StatsFs) | [BigIntStatsFs](https://bun.com/reference/node/fs/BigIntStatsFs)>;

  @returns

  Fulfills with the {fs.StatFs} object for the given `path`.
* function [symlink](https://bun.com/reference/node/fs/promises/symlink)(

  target: [PathLike](https://bun.com/reference/node/fs/PathLike),

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  type?: null | string

  ): Promise<void>;

  Creates a symbolic link.

  The `type` argument is only used on Windows platforms and can be one of `'dir'`, `'file'`, or `'junction'`. If the `type` argument is not a string, Node.js will autodetect `target` type and use `'file'` or `'dir'`. If the `target` does not exist, `'file'` will be used. Windows junction points require the destination path to be absolute. When using `'junction'`, the `target` argument will automatically be normalized to absolute path. Junction points on NTFS volumes can only point to directories.

  @returns

  Fulfills with `undefined` upon success.
* function [truncate](https://bun.com/reference/node/fs/promises/truncate)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  len?: number

  ): Promise<void>;

  Truncates (shortens or extends the length) of the content at `path` to `len` bytes.

  @returns

  Fulfills with `undefined` upon success.
* function [unlink](https://bun.com/reference/node/fs/promises/unlink)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike)

  ): Promise<void>;

  If `path` refers to a symbolic link, then the link is removed without affecting the file or directory to which that link refers. If the `path` refers to a file path that is not a symbolic link, the file is deleted. See the POSIX [`unlink(2)`](http://man7.org/linux/man-pages/man2/unlink.2.html) documentation for more detail.

  @returns

  Fulfills with `undefined` upon success.
* function [utimes](https://bun.com/reference/node/fs/promises/utimes)(

  path: [PathLike](https://bun.com/reference/node/fs/PathLike),

  atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

  mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike)

  ): Promise<void>;

  Change the file system timestamps of the object referenced by `path`.

  The `atime` and `mtime` arguments follow these rules:

  + Values can be either numbers representing Unix epoch time, `Date`s, or a numeric string like `'123456789.0'`.
  + If the value can not be converted to a number, or is `NaN`, `Infinity`, or `-Infinity`, an `Error` will be thrown.

  @returns

  Fulfills with `undefined` upon success.
* function [watch](https://bun.com/reference/node/fs/promises/watch)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options?: BufferEncoding | [WatchOptionsWithStringEncoding](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding)

  ): AsyncIterator<[FileChangeInfo](https://bun.com/reference/node/fs/promises/FileChangeInfo)<string>>;

  Returns an async iterator that watches for changes on `filename`, where `filename`is either a file or a directory.

  ```
  import { watch } from 'node:fs/promises';

  const ac = new AbortController();
  const { signal } = ac;
  setTimeout(() => ac.abort(), 10000);

  (async () => {
    try {
      const watcher = watch(__filename, { signal });
      for await (const event of watcher)
        console.log(event);
    } catch (err) {
      if (err.name === 'AbortError')
        return;
      throw err;
    }
  })();
  ```

  On most platforms, `'rename'` is emitted whenever a filename appears or disappears in the directory.

  All the `caveats` for `fs.watch()` also apply to `fsPromises.watch()`.

  @returns

  of objects with the properties:

  function [watch](https://bun.com/reference/node/fs/promises/watch)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: 'buffer' | [WatchOptionsWithBufferEncoding](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding)

  ): AsyncIterator<[FileChangeInfo](https://bun.com/reference/node/fs/promises/FileChangeInfo)<NonSharedBuffer>>;

  Returns an async iterator that watches for changes on `filename`, where `filename`is either a file or a directory.

  ```
  import { watch } from 'node:fs/promises';

  const ac = new AbortController();
  const { signal } = ac;
  setTimeout(() => ac.abort(), 10000);

  (async () => {
    try {
      const watcher = watch(__filename, { signal });
      for await (const event of watcher)
        console.log(event);
    } catch (err) {
      if (err.name === 'AbortError')
        return;
      throw err;
    }
  })();
  ```

  On most platforms, `'rename'` is emitted whenever a filename appears or disappears in the directory.

  All the `caveats` for `fs.watch()` also apply to `fsPromises.watch()`.

  @returns

  of objects with the properties:

  function [watch](https://bun.com/reference/node/fs/promises/watch)(

  filename: [PathLike](https://bun.com/reference/node/fs/PathLike),

  options: BufferEncoding | 'buffer' | [WatchOptions](https://bun.com/reference/node/fs/promises/WatchOptions)

  ): AsyncIterator<[FileChangeInfo](https://bun.com/reference/node/fs/promises/FileChangeInfo)<string | NonSharedBuffer>>;

  Returns an async iterator that watches for changes on `filename`, where `filename`is either a file or a directory.

  ```
  import { watch } from 'node:fs/promises';

  const ac = new AbortController();
  const { signal } = ac;
  setTimeout(() => ac.abort(), 10000);

  (async () => {
    try {
      const watcher = watch(__filename, { signal });
      for await (const event of watcher)
        console.log(event);
    } catch (err) {
      if (err.name === 'AbortError')
        return;
      throw err;
    }
  })();
  ```

  On most platforms, `'rename'` is emitted whenever a filename appears or disappears in the directory.

  All the `caveats` for `fs.watch()` also apply to `fsPromises.watch()`.

  @returns

  of objects with the properties:
* function [writeFile](https://bun.com/reference/node/fs/promises/writeFile)(

  file: [PathLike](https://bun.com/reference/node/fs/PathLike) | [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle),

  data: string | [Stream](https://bun.com/reference/node/stream/default) | ArrayBufferView<ArrayBufferLike> | Iterable<unknown, any, any> | AsyncIterable<unknown, any, any>,

  options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & { flag: unknown; flush: boolean; mode: unknown } & [Abortable](https://bun.com/reference/node/events/default/Abortable)

  ): Promise<void>;

  Asynchronously writes data to a file, replacing the file if it already exists. `data` can be a string, a buffer, an [AsyncIterable](https://tc39.github.io/ecma262/#sec-asynciterable-interface), or an [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol) object.

  The `encoding` option is ignored if `data` is a buffer.

  If `options` is a string, then it specifies the encoding.

  The `mode` option only affects the newly created file. See `fs.open()` for more details.

  Any specified `FileHandle` has to support writing.

  It is unsafe to use `fsPromises.writeFile()` multiple times on the same file without waiting for the promise to be settled.

  Similarly to `fsPromises.readFile` - `fsPromises.writeFile` is a convenience method that performs multiple `write` calls internally to write the buffer passed to it. For performance sensitive code consider using `fs.createWriteStream()` or `filehandle.createWriteStream()`.

  It is possible to use an `AbortSignal` to cancel an `fsPromises.writeFile()`. Cancelation is "best effort", and some amount of data is likely still to be written.

  ```
  import { writeFile } from 'node:fs/promises';
  import { Buffer } from 'node:buffer';

  try {
    const controller = new AbortController();
    const { signal } = controller;
    const data = new Uint8Array(Buffer.from('Hello Node.js'));
    const promise = writeFile('message.txt', data, { signal });

    // Abort the request before the promise settles.
    controller.abort();

    await promise;
  } catch (err) {
    // When a request is aborted - err is an AbortError
    console.error(err);
  }
  ```

  Aborting an ongoing request does not abort individual operating system requests but rather the internal buffering `fs.writeFile` performs.

  @param file

  filename or `FileHandle`

  @returns

  Fulfills with `undefined` upon success.

## Type definitions

* ### interface [CreateReadStreamOptions](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions)

  + [autoClose](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions/autoClose)?: boolean
  + [emitClose](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions/emitClose)?: boolean
  + [encoding](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions/encoding)?: null | BufferEncoding
  + [end](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions/end)?: number
  + [highWaterMark](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions/highWaterMark)?: number
  + [signal](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [start](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions/start)?: number
* ### interface [CreateWriteStreamOptions](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions)

  + [autoClose](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions/autoClose)?: boolean
  + [emitClose](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions/emitClose)?: boolean
  + [encoding](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions/encoding)?: null | BufferEncoding
  + [flush](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions/flush)?: boolean
  + [highWaterMark](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions/highWaterMark)?: number
  + [start](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions/start)?: number
* ### interface [FileChangeInfo](https://bun.com/reference/node/fs/promises/FileChangeInfo)<T extends string | [Buffer](https://bun.com/reference/node/buffer/Buffer)>

  + [eventType](https://bun.com/reference/node/fs/promises/FileChangeInfo/eventType): [WatchEventType](https://bun.com/reference/node/fs/WatchEventType)
  + [filename](https://bun.com/reference/node/fs/promises/FileChangeInfo/filename): null | T
* ### interface [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle)

  + readonly [fd](https://bun.com/reference/node/fs/promises/FileHandle/fd): number

    The numeric file descriptor managed by the {FileHandle} object.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/fs/promises/FileHandle/[asyncDispose])(): Promise<void>;

    Calls `filehandle.close()` and returns a promise that fulfills when the filehandle is closed.
  + [appendFile](https://bun.com/reference/node/fs/promises/FileHandle/appendFile)(

    data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & [Abortable](https://bun.com/reference/node/events/default/Abortable)

    ): Promise<void>;

    Alias of `filehandle.writeFile()`.

    When operating on file handles, the mode cannot be changed from what it was set to with `fsPromises.open()`. Therefore, this is equivalent to `filehandle.writeFile()`.

    @returns

    Fulfills with `undefined` upon success.
  + [chmod](https://bun.com/reference/node/fs/promises/FileHandle/chmod)(

    mode: [Mode](https://bun.com/reference/node/fs/Mode)

    ): Promise<void>;

    Modifies the permissions on the file. See [`chmod(2)`](http://man7.org/linux/man-pages/man2/chmod.2.html).

    @param mode

    the file mode bit mask.

    @returns

    Fulfills with `undefined` upon success.
  + [chown](https://bun.com/reference/node/fs/promises/FileHandle/chown)(

    uid: number,

    gid: number

    ): Promise<void>;

    Changes the ownership of the file. A wrapper for [`chown(2)`](http://man7.org/linux/man-pages/man2/chown.2.html).

    @param uid

    The file's new owner's user id.

    @param gid

    The file's new group's group id.

    @returns

    Fulfills with `undefined` upon success.
  + [close](https://bun.com/reference/node/fs/promises/FileHandle/close)(): Promise<void>;

    Closes the file handle after waiting for any pending operation on the handle to complete.

    ```
    import { open } from 'node:fs/promises';

    let filehandle;
    try {
      filehandle = await open('thefile.txt', 'r');
    } finally {
      await filehandle?.close();
    }
    ```

    @returns

    Fulfills with `undefined` upon success.
  + [createReadStream](https://bun.com/reference/node/fs/promises/FileHandle/createReadStream)(

    options?: [CreateReadStreamOptions](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions)

    ): [ReadStream](https://bun.com/reference/node/fs/ReadStream);

    Unlike the 16 KiB default `highWaterMark` for a `stream.Readable`, the stream returned by this method has a default `highWaterMark` of 64 KiB.

    `options` can include `start` and `end` values to read a range of bytes from the file instead of the entire file. Both `start` and `end` are inclusive and start counting at 0, allowed values are in the [0, [`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)] range. If `start` is omitted or `undefined`, `filehandle.createReadStream()` reads sequentially from the current file position. The `encoding` can be any one of those accepted by `Buffer`.

    If the `FileHandle` points to a character device that only supports blocking reads (such as keyboard or sound card), read operations do not finish until data is available. This can prevent the process from exiting and the stream from closing naturally.

    By default, the stream will emit a `'close'` event after it has been destroyed. Set the `emitClose` option to `false` to change this behavior.

    ```
    import { open } from 'node:fs/promises';

    const fd = await open('/dev/input/event0');
    // Create a stream from some character device.
    const stream = fd.createReadStream();
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

    An example to read the last 10 bytes of a file which is 100 bytes long:

    ```
    import { open } from 'node:fs/promises';

    const fd = await open('sample.txt');
    fd.createReadStream({ start: 90, end: 99 });
    ```
  + [createWriteStream](https://bun.com/reference/node/fs/promises/FileHandle/createWriteStream)(

    options?: [CreateWriteStreamOptions](https://bun.com/reference/node/fs/promises/CreateWriteStreamOptions)

    ): [WriteStream](https://bun.com/reference/node/fs/WriteStream);

    `options` may also include a `start` option to allow writing data at some position past the beginning of the file, allowed values are in the [0, [`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)] range. Modifying a file rather than replacing it may require the `flags` `open` option to be set to `r+` rather than the default `r`. The `encoding` can be any one of those accepted by `Buffer`.

    If `autoClose` is set to true (default behavior) on `'error'` or `'finish'` the file descriptor will be closed automatically. If `autoClose` is false, then the file descriptor won't be closed, even if there's an error. It is the application's responsibility to close it and make sure there's no file descriptor leak.

    By default, the stream will emit a `'close'` event after it has been destroyed. Set the `emitClose` option to `false` to change this behavior.
  + [datasync](https://bun.com/reference/node/fs/promises/FileHandle/datasync)(): Promise<void>;

    Forces all currently queued I/O operations associated with the file to the operating system's synchronized I/O completion state. Refer to the POSIX [`fdatasync(2)`](http://man7.org/linux/man-pages/man2/fdatasync.2.html) documentation for details.

    Unlike `filehandle.sync` this method does not flush modified metadata.

    @returns

    Fulfills with `undefined` upon success.
  + [read](https://bun.com/reference/node/fs/promises/FileHandle/read)<T extends ArrayBufferView<ArrayBufferLike>>(

    buffer: T,

    offset?: null | number,

    length?: null | number,

    position?: null | [ReadPosition](https://bun.com/reference/node/fs/ReadPosition)

    ): Promise<[FileReadResult](https://bun.com/reference/node/fs/promises/FileReadResult)<T>>;

    Reads data from the file and stores that in the given buffer.

    If the file is not modified concurrently, the end-of-file is reached when the number of bytes read is zero.

    @param buffer

    A buffer that will be filled with the file data read.

    @param offset

    The location in the buffer at which to start filling.

    @param length

    The number of bytes to read.

    @param position

    The location where to begin reading data from the file. If `null`, data will be read from the current file position, and the position will be updated. If `position` is an integer, the current file position will remain unchanged.

    @returns

    Fulfills upon success with an object with two properties:

    [read](https://bun.com/reference/node/fs/promises/FileHandle/read)<T extends ArrayBufferView<ArrayBufferLike>>(

    buffer: T,

    options?: [ReadOptions](https://bun.com/reference/node/fs/ReadOptions)

    ): Promise<[FileReadResult](https://bun.com/reference/node/fs/promises/FileReadResult)<T>>;

    [read](https://bun.com/reference/node/fs/promises/FileHandle/read)<T extends ArrayBufferView<ArrayBufferLike> = NonSharedBuffer>(

    options?: [ReadOptionsWithBuffer](https://bun.com/reference/node/fs/ReadOptionsWithBuffer)<T>

    ): Promise<[FileReadResult](https://bun.com/reference/node/fs/promises/FileReadResult)<T>>;
  + [readableWebStream](https://bun.com/reference/node/fs/promises/FileHandle/readableWebStream)(

    options?: [ReadableWebStreamOptions](https://bun.com/reference/node/fs/promises/ReadableWebStreamOptions)

    ): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream);

    Returns a byte-oriented `ReadableStream` that may be used to read the file's contents.

    An error will be thrown if this method is called more than once or is called after the `FileHandle` is closed or closing.

    ```
    import {
      open,
    } from 'node:fs/promises';

    const file = await open('./some/file/to/read');

    for await (const chunk of file.readableWebStream())
      console.log(chunk);

    await file.close();
    ```

    While the `ReadableStream` will read the file to completion, it will not close the `FileHandle` automatically. User code must still call the`fileHandle.close()` method.
  + [readFile](https://bun.com/reference/node/fs/promises/FileHandle/readFile)(

    options?: null | { encoding: null } & [Abortable](https://bun.com/reference/node/events/default/Abortable)

    ): Promise<NonSharedBuffer>;

    Asynchronously reads the entire contents of a file.

    If `options` is a string, then it specifies the `encoding`.

    The `FileHandle` has to support reading.

    If one or more `filehandle.read()` calls are made on a file handle and then a `filehandle.readFile()` call is made, the data will be read from the current position till the end of the file. It doesn't always read from the beginning of the file.

    @returns

    Fulfills upon a successful read with the contents of the file. If no encoding is specified (using `options.encoding`), the data is returned as a {Buffer} object. Otherwise, the data will be a string.

    [readFile](https://bun.com/reference/node/fs/promises/FileHandle/readFile)(

    options: BufferEncoding | { encoding: BufferEncoding } & [Abortable](https://bun.com/reference/node/events/default/Abortable)

    ): Promise<string>;

    Asynchronously reads the entire contents of a file. The underlying file will *not* be closed automatically. The `FileHandle` must have been opened for reading.

    [readFile](https://bun.com/reference/node/fs/promises/FileHandle/readFile)(

    options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & [Abortable](https://bun.com/reference/node/events/default/Abortable)

    ): Promise<string | NonSharedBuffer>;

    Asynchronously reads the entire contents of a file. The underlying file will *not* be closed automatically. The `FileHandle` must have been opened for reading.
  + [readLines](https://bun.com/reference/node/fs/promises/FileHandle/readLines)(

    options?: [CreateReadStreamOptions](https://bun.com/reference/node/fs/promises/CreateReadStreamOptions)

    ): [Interface](https://bun.com/reference/node/readline/Interface);

    Convenience method to create a `readline` interface and stream over the file. See `filehandle.createReadStream()` for the options.

    ```
    import { open } from 'node:fs/promises';

    const file = await open('./some/file/to/read');

    for await (const line of file.readLines()) {
      console.log(line);
    }
    ```
  + [readv](https://bun.com/reference/node/fs/promises/FileHandle/readv)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

    buffers: TBuffers,

    position?: number

    ): Promise<[ReadVResult](https://bun.com/reference/node/fs/ReadVResult)<TBuffers>>;

    Read from a file and write to an array of [ArrayBufferView](https://developer.mozilla.org/en-US/docs/Web/API/ArrayBufferView) s

    @param position

    The offset from the beginning of the file where the data should be read from. If `position` is not a `number`, the data will be read from the current position.

    @returns

    Fulfills upon success an object containing two properties:
  + [stat](https://bun.com/reference/node/fs/promises/FileHandle/stat)(

    opts?: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: false }

    ): Promise<[Stats](https://bun.com/reference/node/fs/Stats)>;

    @returns

    Fulfills with an {fs.Stats} for the file.

    [stat](https://bun.com/reference/node/fs/promises/FileHandle/stat)(

    opts: [StatOptions](https://bun.com/reference/node/fs/StatOptions) & { bigint: true }

    ): Promise<[BigIntStats](https://bun.com/reference/node/fs/BigIntStats)>;

    [stat](https://bun.com/reference/node/fs/promises/FileHandle/stat)(

    opts?: [StatOptions](https://bun.com/reference/node/fs/StatOptions)

    ): Promise<[Stats](https://bun.com/reference/node/fs/Stats) | [BigIntStats](https://bun.com/reference/node/fs/BigIntStats)>;
  + [sync](https://bun.com/reference/node/fs/promises/FileHandle/sync)(): Promise<void>;

    Request that all data for the open file descriptor is flushed to the storage device. The specific implementation is operating system and device specific. Refer to the POSIX [`fsync(2)`](http://man7.org/linux/man-pages/man2/fsync.2.html) documentation for more detail.

    @returns

    Fulfills with `undefined` upon success.
  + [truncate](https://bun.com/reference/node/fs/promises/FileHandle/truncate)(

    len?: number

    ): Promise<void>;

    Truncates the file.

    If the file was larger than `len` bytes, only the first `len` bytes will be retained in the file.

    The following example retains only the first four bytes of the file:

    ```
    import { open } from 'node:fs/promises';

    let filehandle = null;
    try {
      filehandle = await open('temp.txt', 'r+');
      await filehandle.truncate(4);
    } finally {
      await filehandle?.close();
    }
    ```

    If the file previously was shorter than `len` bytes, it is extended, and the extended part is filled with null bytes (`'\0'`):

    If `len` is negative then `0` will be used.

    @returns

    Fulfills with `undefined` upon success.
  + [utimes](https://bun.com/reference/node/fs/promises/FileHandle/utimes)(

    atime: [TimeLike](https://bun.com/reference/node/fs/TimeLike),

    mtime: [TimeLike](https://bun.com/reference/node/fs/TimeLike)

    ): Promise<void>;

    Change the file system timestamps of the object referenced by the `FileHandle` then fulfills the promise with no arguments upon success.
  + [write](https://bun.com/reference/node/fs/promises/FileHandle/write)<TBuffer extends ArrayBufferView<ArrayBufferLike>>(

    buffer: TBuffer,

    offset?: null | number,

    length?: null | number,

    position?: null | number

    ): Promise<{ buffer: TBuffer; bytesWritten: number }>;

    Write `buffer` to the file.

    The promise is fulfilled with an object containing two properties:

    It is unsafe to use `filehandle.write()` multiple times on the same file without waiting for the promise to be fulfilled (or rejected). For this scenario, use `filehandle.createWriteStream()`.

    On Linux, positional writes do not work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.

    @param offset

    The start position from within `buffer` where the data to write begins.

    @param length

    The number of bytes from `buffer` to write.

    @param position

    The offset from the beginning of the file where the data from `buffer` should be written. If `position` is not a `number`, the data will be written at the current position. See the POSIX pwrite(2) documentation for more detail.

    [write](https://bun.com/reference/node/fs/promises/FileHandle/write)<TBuffer extends [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>(

    buffer: TBuffer,

    options?: { length: number; offset: number; position: number }

    ): Promise<{ buffer: TBuffer; bytesWritten: number }>;

    [write](https://bun.com/reference/node/fs/promises/FileHandle/write)(

    data: string,

    position?: null | number,

    encoding?: null | BufferEncoding

    ): Promise<{ buffer: string; bytesWritten: number }>;
  + [writeFile](https://bun.com/reference/node/fs/promises/FileHandle/writeFile)(

    data: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    options?: null | BufferEncoding | [ObjectEncodingOptions](https://bun.com/reference/node/fs/ObjectEncodingOptions) & [Abortable](https://bun.com/reference/node/events/default/Abortable)

    ): Promise<void>;

    Asynchronously writes data to a file, replacing the file if it already exists. `data` can be a string, a buffer, an [AsyncIterable](https://tc39.github.io/ecma262/#sec-asynciterable-interface), or an [Iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#The_iterable_protocol) object. The promise is fulfilled with no arguments upon success.

    If `options` is a string, then it specifies the `encoding`.

    The `FileHandle` has to support writing.

    It is unsafe to use `filehandle.writeFile()` multiple times on the same file without waiting for the promise to be fulfilled (or rejected).

    If one or more `filehandle.write()` calls are made on a file handle and then a`filehandle.writeFile()` call is made, the data will be written from the current position till the end of the file. It doesn't always write from the beginning of the file.
  + [writev](https://bun.com/reference/node/fs/promises/FileHandle/writev)<TBuffers extends readonly ArrayBufferView<ArrayBufferLike>[]>(

    buffers: TBuffers,

    position?: number

    ): Promise<[WriteVResult](https://bun.com/reference/node/fs/WriteVResult)<TBuffers>>;

    Write an array of [ArrayBufferView](https://developer.mozilla.org/en-US/docs/Web/API/ArrayBufferView) s to the file.

    The promise is fulfilled with an object containing a two properties:

    It is unsafe to call `writev()` multiple times on the same file without waiting for the promise to be fulfilled (or rejected).

    On Linux, positional writes don't work when the file is opened in append mode. The kernel ignores the position argument and always appends the data to the end of the file.

    @param position

    The offset from the beginning of the file where the data from `buffers` should be written. If `position` is not a `number`, the data will be written at the current position.
* ### interface [FileReadResult](https://bun.com/reference/node/fs/promises/FileReadResult)<T extends NodeJS.ArrayBufferView>

  + [buffer](https://bun.com/reference/node/fs/promises/FileReadResult/buffer): T
  + [bytesRead](https://bun.com/reference/node/fs/promises/FileReadResult/bytesRead): number
* ### interface [FlagAndOpenMode](https://bun.com/reference/node/fs/promises/FlagAndOpenMode)

  + [flag](https://bun.com/reference/node/fs/promises/FlagAndOpenMode/flag)?: [OpenMode](https://bun.com/reference/node/fs/OpenMode)
  + [mode](https://bun.com/reference/node/fs/promises/FlagAndOpenMode/mode)?: [Mode](https://bun.com/reference/node/fs/Mode)
* ### interface [ReadableWebStreamOptions](https://bun.com/reference/node/fs/promises/ReadableWebStreamOptions)

  + [autoClose](https://bun.com/reference/node/fs/promises/ReadableWebStreamOptions/autoClose)?: boolean
* ### interface [WatchOptions](https://bun.com/reference/node/fs/promises/WatchOptions)

  + [encoding](https://bun.com/reference/node/fs/promises/WatchOptions/encoding)?: BufferEncoding | 'buffer'
  + [maxQueue](https://bun.com/reference/node/fs/promises/WatchOptions/maxQueue)?: number
  + [overflow](https://bun.com/reference/node/fs/promises/WatchOptions/overflow)?: 'ignore' | 'throw'
  + [persistent](https://bun.com/reference/node/fs/promises/WatchOptions/persistent)?: boolean
  + [recursive](https://bun.com/reference/node/fs/promises/WatchOptions/recursive)?: boolean
  + [signal](https://bun.com/reference/node/fs/promises/WatchOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
* ### interface [WatchOptionsWithBufferEncoding](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding)

  + [encoding](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding/encoding): 'buffer'
  + [maxQueue](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding/maxQueue)?: number
  + [overflow](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding/overflow)?: 'ignore' | 'throw'
  + [persistent](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding/persistent)?: boolean
  + [recursive](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding/recursive)?: boolean
  + [signal](https://bun.com/reference/node/fs/promises/WatchOptionsWithBufferEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
* ### interface [WatchOptionsWithStringEncoding](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding)

  + [encoding](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding/encoding)?: BufferEncoding
  + [maxQueue](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding/maxQueue)?: number
  + [overflow](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding/overflow)?: 'ignore' | 'throw'
  + [persistent](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding/persistent)?: boolean
  + [recursive](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding/recursive)?: boolean
  + [signal](https://bun.com/reference/node/fs/promises/WatchOptionsWithStringEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.