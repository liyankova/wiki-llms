---
url: https://doc.rust-lang.org/std/io/struct.Stdin.html
title: Stdin in std::io - Rust
source_domain: doc.rust-lang.org
---

# Stdin in std::io - Rust

## [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html)

[std](https://doc.rust-lang.org/std/index.html)::[io](https://doc.rust-lang.org/std/io/index.html)

# Struct Stdin

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#250-252)

```
pub struct Stdin { /* private fields */ }
```

Expand description

A handle to the standard input stream of a process.

Each handle is a shared reference to a global buffer of input data to this
process. A handle can be `lock`’d to gain full access to [`BufRead`](https://doc.rust-lang.org/std/io/trait.BufRead.html "trait std::io::BufRead") methods
(e.g., `.lines()`). Reads to this handle are otherwise locked with respect
to other reads.

This handle implements the `Read` trait, but beware that concurrent reads
of `Stdin` must be executed with care.

Created by the [`io::stdin`](https://doc.rust-lang.org/std/io/fn.stdin.html "fn std::io::stdin") method.

#### [§](https://doc.rust-lang.org/std/io/struct.Stdin.html#note-windows-portability-considerations)Note: Windows Portability Considerations

When operating in a console, the Windows implementation of this stream does not support
non-UTF-8 byte sequences. Attempting to read bytes that are not valid UTF-8 will return
an error.

In a process with a detached console, such as one using
`#![windows_subsystem = "windows"]`, or in a child process spawned from such a process,
the contained handle will be null. In such cases, the standard library’s `Read` and
`Write` will do nothing and silently succeed. All other I/O operations, via the
standard library or via raw Windows API calls, will fail.

## [§](https://doc.rust-lang.org/std/io/struct.Stdin.html#examples)Examples

```
use std::io;

fn main() -> io::Result<()> {
    let mut buffer = String::new();
    let stdin = io::stdin(); // We get `Stdin` here.
    stdin.read_line(&mut buffer)?;
    Ok(())
}
```

## Implementations[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#implementations)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#349-435)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Stdin)

### impl [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#372-376)

#### pub fn [lock](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.lock)(&self) -> [StdinLock](https://doc.rust-lang.org/std/io/struct.StdinLock.html "struct std::io::StdinLock")<'static> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html)

Locks this handle to the standard input stream, returning a readable
guard.

The lock is released when the returned lock goes out of scope. The
returned guard also implements the [`Read`](https://doc.rust-lang.org/std/io/trait.Read.html "trait std::io::Read") and [`BufRead`](https://doc.rust-lang.org/std/io/trait.BufRead.html "trait std::io::BufRead") traits for
accessing the underlying data.

##### [§](https://doc.rust-lang.org/std/io/struct.Stdin.html#examples-1)Examples

```
use std::io::{self, BufRead};

fn main() -> io::Result<()> {
    let mut buffer = String::new();
    let stdin = io::stdin();
    let mut handle = stdin.lock();

    handle.read_line(&mut buffer)?;
    Ok(())
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#411-413)

#### pub fn [read\_line](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_line)(&self, buf: &mut [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Locks this handle and reads a line of input, appending it to the specified buffer.

For detailed semantics of this method, see the documentation on
[`BufRead::read_line`](https://doc.rust-lang.org/std/io/trait.BufRead.html#method.read_line "method std::io::BufRead::read_line"). In particular:

* Previous content of the buffer will be preserved. To avoid appending
  to the buffer, you need to [`clear`](https://doc.rust-lang.org/std/string/struct.String.html#method.clear "method std::string::String::clear") it first.
* The trailing newline character, if any, is included in the buffer.

##### [§](https://doc.rust-lang.org/std/io/struct.Stdin.html#examples-2)Examples

```
use std::io;

let mut input = String::new();
match io::stdin().read_line(&mut input) {
    Ok(n) => {
        println!("{n} bytes read");
        println!("{input}");
    }
    Err(error) => println!("error: {error}"),
}
```

You can run the example one of two ways:

* Pipe some text to it, e.g., `printf foo | path/to/executable`
* Give it text interactively by running the executable directly,
  in which case it will wait for the Enter key to be pressed before
  continuing

1.62.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#432-434)

#### pub fn [lines](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.lines)(self) -> [Lines](https://doc.rust-lang.org/std/io/struct.Lines.html "struct std::io::Lines")<[StdinLock](https://doc.rust-lang.org/std/io/struct.StdinLock.html "struct std::io::StdinLock")<'static>> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html)

Consumes this handle and returns an iterator over input lines.

For detailed semantics of this method, see the documentation on
[`BufRead::lines`](https://doc.rust-lang.org/std/io/trait.BufRead.html#method.lines "method std::io::BufRead::lines").

##### [§](https://doc.rust-lang.org/std/io/struct.Stdin.html#examples-3)Examples

```
use std::io;

let lines = io::stdin().lines();
for line in lines {
    println!("got a line: {}", line.unwrap());
}
```

## Trait Implementations[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#trait-implementations)

1.63.0 · [Source](https://doc.rust-lang.org/src/std/os/fd/owned.rs.html#458-463)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-AsFd-for-Stdin)

### impl [AsFd](https://doc.rust-lang.org/std/os/fd/trait.AsFd.html "trait std::os::fd::AsFd") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[Source](https://doc.rust-lang.org/src/std/os/fd/owned.rs.html#460-462)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.as_fd)

#### fn [as\_fd](https://doc.rust-lang.org/std/os/fd/trait.AsFd.html#tymethod.as_fd)(&self) -> [BorrowedFd](https://doc.rust-lang.org/std/os/fd/struct.BorrowedFd.html "struct std::os::fd::BorrowedFd")<'\_>

Borrows the file descriptor. [Read more](https://doc.rust-lang.org/std/os/fd/trait.AsFd.html#tymethod.as_fd)

1.63.0 · [Source](https://doc.rust-lang.org/src/std/os/windows/io/handle.rs.html#550-555)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-AsHandle-for-Stdin)

### impl [AsHandle](https://doc.rust-lang.org/std/os/windows/io/trait.AsHandle.html "trait std::os::windows::io::AsHandle") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

Available on **Windows** only.

[Source](https://doc.rust-lang.org/src/std/os/windows/io/handle.rs.html#552-554)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.as_handle)

#### fn [as\_handle](https://doc.rust-lang.org/std/os/windows/io/trait.AsHandle.html#tymethod.as_handle)(&self) -> [BorrowedHandle](https://doc.rust-lang.org/std/os/windows/io/struct.BorrowedHandle.html "struct std::os::windows::io::BorrowedHandle")<'\_>

Borrows the handle. [Read more](https://doc.rust-lang.org/std/os/windows/io/trait.AsHandle.html#tymethod.as_handle)

1.21.0 · [Source](https://doc.rust-lang.org/src/std/os/fd/raw.rs.html#193-198)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-AsRawFd-for-Stdin)

### impl [AsRawFd](https://doc.rust-lang.org/std/os/fd/trait.AsRawFd.html "trait std::os::fd::AsRawFd") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[Source](https://doc.rust-lang.org/src/std/os/fd/raw.rs.html#195-197)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.as_raw_fd)

#### fn [as\_raw\_fd](https://doc.rust-lang.org/std/os/fd/trait.AsRawFd.html#tymethod.as_raw_fd)(&self) -> [RawFd](https://doc.rust-lang.org/std/os/fd/type.RawFd.html "type std::os::fd::RawFd")

Extracts the raw file descriptor. [Read more](https://doc.rust-lang.org/std/os/fd/trait.AsRawFd.html#tymethod.as_raw_fd)

1.21.0 · [Source](https://doc.rust-lang.org/src/std/os/windows/io/raw.rs.html#102-106)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-AsRawHandle-for-Stdin)

### impl [AsRawHandle](https://doc.rust-lang.org/std/os/windows/io/trait.AsRawHandle.html "trait std::os::windows::io::AsRawHandle") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

Available on **Windows** only.

[Source](https://doc.rust-lang.org/src/std/os/windows/io/raw.rs.html#103-105)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.as_raw_handle)

#### fn [as\_raw\_handle](https://doc.rust-lang.org/std/os/windows/io/trait.AsRawHandle.html#tymethod.as_raw_handle)(&self) -> [RawHandle](https://doc.rust-lang.org/std/os/windows/io/type.RawHandle.html "type std::os::windows::io::RawHandle")

Extracts the raw handle. [Read more](https://doc.rust-lang.org/std/os/windows/io/trait.AsRawHandle.html#tymethod.as_raw_handle)

1.16.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#438-442)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Debug-for-Stdin)

### impl [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#439-441)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/fmt/type.Result.html "type std::fmt::Result")

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

1.70.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#1265)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-IsTerminal-for-Stdin)

### impl [IsTerminal](https://doc.rust-lang.org/std/io/trait.IsTerminal.html "trait std::io::IsTerminal") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#1265)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.is_terminal)

#### fn [is\_terminal](https://doc.rust-lang.org/std/io/trait.IsTerminal.html#tymethod.is_terminal)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the descriptor/handle refers to a terminal/tty. [Read more](https://doc.rust-lang.org/std/io/trait.IsTerminal.html#tymethod.is_terminal)

1.78.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#474-500)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Read-for-%26Stdin)

### impl [Read](https://doc.rust-lang.org/std/io/trait.Read.html "trait std::io::Read") for &[Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#475-477)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read-1)

#### fn [read](https://doc.rust-lang.org/std/io/trait.Read.html#tymethod.read)(&mut self, buf: &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Pull some bytes from this source into the specified buffer, returning
how many bytes were read. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#tymethod.read)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#478-480)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_buf-1)

#### fn [read\_buf](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf)(&mut self, buf: [BorrowedCursor](https://doc.rust-lang.org/std/io/struct.BorrowedCursor.html "struct std::io::BorrowedCursor")<'\_>) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

🔬This is a nightly-only experimental API. (`read_buf` [#78485](https://github.com/rust-lang/rust/issues/78485))

Pull some bytes from this source into the specified buffer. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#481-483)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_vectored-1)

#### fn [read\_vectored](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_vectored)(&mut self, bufs: &mut [[IoSliceMut](https://doc.rust-lang.org/std/io/struct.IoSliceMut.html "struct std::io::IoSliceMut")<'\_>]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Like `read`, except that it reads into a slice of buffers. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_vectored)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#485-487)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.is_read_vectored-1)

#### fn [is\_read\_vectored](https://doc.rust-lang.org/std/io/trait.Read.html#method.is_read_vectored)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`can_vector` [#69941](https://github.com/rust-lang/rust/issues/69941))

Determines if this `Read`er has an efficient `read_vectored`
implementation. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.is_read_vectored)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#488-490)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_to_end-1)

#### fn [read\_to\_end](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_end)(&mut self, buf: &mut [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Reads all bytes until EOF in this source, placing them into `buf`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_end)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#491-493)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_to_string-1)

#### fn [read\_to\_string](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_string)(&mut self, buf: &mut [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Reads all bytes until EOF in this source, appending them to `buf`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_string)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#494-496)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_exact-1)

#### fn [read\_exact](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_exact)(&mut self, buf: &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

Reads the exact number of bytes required to fill `buf`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_exact)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#497-499)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_buf_exact-1)

#### fn [read\_buf\_exact](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf_exact)(&mut self, cursor: [BorrowedCursor](https://doc.rust-lang.org/std/io/struct.BorrowedCursor.html "struct std::io::BorrowedCursor")<'\_>) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

🔬This is a nightly-only experimental API. (`read_buf` [#78485](https://github.com/rust-lang/rust/issues/78485))

Reads the exact number of bytes required to fill `cursor`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf_exact)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1119-1124)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.by_ref-1)

#### fn [by\_ref](https://doc.rust-lang.org/std/io/trait.Read.html#method.by_ref)(&mut self) -> &mut Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Creates a “by reference” adaptor for this instance of `Read`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.by_ref)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1162-1167)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.bytes-1)

#### fn [bytes](https://doc.rust-lang.org/std/io/trait.Read.html#method.bytes)(self) -> [Bytes](https://doc.rust-lang.org/std/io/struct.Bytes.html "struct std::io::Bytes")<Self> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html) where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Transforms this `Read` instance to an [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator") over its bytes. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.bytes)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1200-1205)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.chain-1)

#### fn [chain](https://doc.rust-lang.org/std/io/trait.Read.html#method.chain)<R: [Read](https://doc.rust-lang.org/std/io/trait.Read.html "trait std::io::Read")>(self, next: R) -> [Chain](https://doc.rust-lang.org/std/io/struct.Chain.html "struct std::io::Chain")<Self, R> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html) where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Creates an adapter which will chain this stream with another. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.chain)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1239-1244)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.take-1)

#### fn [take](https://doc.rust-lang.org/std/io/trait.Read.html#method.take)(self, limit: [u64](https://doc.rust-lang.org/std/primitive.u64.html)) -> [Take](https://doc.rust-lang.org/std/io/struct.Take.html "struct std::io::Take")<Self> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html) where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Creates an adapter which will read at most `limit` bytes from it. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.take)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#445-471)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Read-for-Stdin)

### impl [Read](https://doc.rust-lang.org/std/io/trait.Read.html "trait std::io::Read") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#446-448)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read)

#### fn [read](https://doc.rust-lang.org/std/io/trait.Read.html#tymethod.read)(&mut self, buf: &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Pull some bytes from this source into the specified buffer, returning
how many bytes were read. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#tymethod.read)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#449-451)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_buf)

#### fn [read\_buf](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf)(&mut self, buf: [BorrowedCursor](https://doc.rust-lang.org/std/io/struct.BorrowedCursor.html "struct std::io::BorrowedCursor")<'\_>) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

🔬This is a nightly-only experimental API. (`read_buf` [#78485](https://github.com/rust-lang/rust/issues/78485))

Pull some bytes from this source into the specified buffer. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#452-454)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_vectored)

#### fn [read\_vectored](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_vectored)(&mut self, bufs: &mut [[IoSliceMut](https://doc.rust-lang.org/std/io/struct.IoSliceMut.html "struct std::io::IoSliceMut")<'\_>]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Like `read`, except that it reads into a slice of buffers. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_vectored)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#456-458)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.is_read_vectored)

#### fn [is\_read\_vectored](https://doc.rust-lang.org/std/io/trait.Read.html#method.is_read_vectored)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`can_vector` [#69941](https://github.com/rust-lang/rust/issues/69941))

Determines if this `Read`er has an efficient `read_vectored`
implementation. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.is_read_vectored)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#459-461)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_to_end)

#### fn [read\_to\_end](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_end)(&mut self, buf: &mut [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Reads all bytes until EOF in this source, placing them into `buf`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_end)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#462-464)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_to_string)

#### fn [read\_to\_string](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_string)(&mut self, buf: &mut [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Reads all bytes until EOF in this source, appending them to `buf`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_to_string)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#465-467)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_exact)

#### fn [read\_exact](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_exact)(&mut self, buf: &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

Reads the exact number of bytes required to fill `buf`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_exact)

[Source](https://doc.rust-lang.org/src/std/io/stdio.rs.html#468-470)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.read_buf_exact)

#### fn [read\_buf\_exact](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf_exact)(&mut self, cursor: [BorrowedCursor](https://doc.rust-lang.org/std/io/struct.BorrowedCursor.html "struct std::io::BorrowedCursor")<'\_>) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

🔬This is a nightly-only experimental API. (`read_buf` [#78485](https://github.com/rust-lang/rust/issues/78485))

Reads the exact number of bytes required to fill `cursor`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.read_buf_exact)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1119-1124)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.by_ref)

#### fn [by\_ref](https://doc.rust-lang.org/std/io/trait.Read.html#method.by_ref)(&mut self) -> &mut Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Creates a “by reference” adaptor for this instance of `Read`. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.by_ref)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1162-1167)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.bytes)

#### fn [bytes](https://doc.rust-lang.org/std/io/trait.Read.html#method.bytes)(self) -> [Bytes](https://doc.rust-lang.org/std/io/struct.Bytes.html "struct std::io::Bytes")<Self> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html) where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Transforms this `Read` instance to an [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator") over its bytes. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.bytes)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1200-1205)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.chain)

#### fn [chain](https://doc.rust-lang.org/std/io/trait.Read.html#method.chain)<R: [Read](https://doc.rust-lang.org/std/io/trait.Read.html "trait std::io::Read")>(self, next: R) -> [Chain](https://doc.rust-lang.org/std/io/struct.Chain.html "struct std::io::Chain")<Self, R> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html) where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Creates an adapter which will chain this stream with another. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.chain)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1239-1244)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.take)

#### fn [take](https://doc.rust-lang.org/std/io/trait.Read.html#method.take)(self, limit: [u64](https://doc.rust-lang.org/std/primitive.u64.html)) -> [Take](https://doc.rust-lang.org/std/io/struct.Take.html "struct std::io::Take")<Self> [ⓘ](https://doc.rust-lang.org/std/io/struct.Stdin.html) where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Creates an adapter which will read at most `limit` bytes from it. [Read more](https://doc.rust-lang.org/std/io/trait.Read.html#method.take)

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Freeze-for-Stdin)

### impl [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-RefUnwindSafe-for-Stdin)

### impl [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Send-for-Stdin)

### impl [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Sync-for-Stdin)

### impl [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Unpin-for-Stdin)

### impl [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-UnwindSafe-for-Stdin)

### impl [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html "struct std::io::Stdin")

## Blanket Implementations[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#785)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-From%3CT%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#788)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: T) -> T

Returns the argument unchanged.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#767-769)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-Into%3CU%3E-for-T)

### impl<T, U> [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<U> for T where U: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#777)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.into)

#### fn [into](https://doc.rust-lang.org/std/convert/trait.Into.html#tymethod.into)(self) -> U

Calls `U::from(self)`.

That is, this conversion is whatever the implementation of
`From<T> for U` chooses to do.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#827-829)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-TryFrom%3CU%3E-for-T)

### impl<T, U> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U> for T where U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#831)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#834)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: U) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, <T as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#811-813)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#impl-TryInto%3CU%3E-for-T)

### impl<T, U> [TryInto](https://doc.rust-lang.org/std/convert/trait.TryInto.html "trait std::convert::TryInto")<U> for T where U: [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#815)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryInto.html#associatedtype.Error) = <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#818)[§](https://doc.rust-lang.org/std/io/struct.Stdin.html#method.try_into)

#### fn [try\_into](https://doc.rust-lang.org/std/convert/trait.TryInto.html#tymethod.try_into)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.