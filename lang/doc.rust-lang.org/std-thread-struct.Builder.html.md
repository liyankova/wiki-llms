---
url: https://doc.rust-lang.org/std/thread/struct.Builder.html
title: Builder in std::thread - Rust
source_domain: doc.rust-lang.org
---

# Builder in std::thread - Rust

## [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html)

[std](https://doc.rust-lang.org/std/index.html)::[thread](https://doc.rust-lang.org/std/thread/index.html)

# Struct Builder

1.0.0 · [Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#260-267)

```
pub struct Builder { /* private fields */ }
```

Expand description

Thread factory, which can be used in order to configure the properties of
a new thread.

Methods can be chained on it in order to configure it.

The two configurations available are:

* [`name`](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.name "method std::thread::Builder::name"): specifies an [associated name for the thread](https://doc.rust-lang.org/std/thread/index.html#naming-threads)
* [`stack_size`](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.stack_size "method std::thread::Builder::stack_size"): specifies the [desired stack size for the thread](https://doc.rust-lang.org/std/thread/index.html#stack-size)

The [`spawn`](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.spawn "method std::thread::Builder::spawn") method will take ownership of the builder and create an
[`io::Result`](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result") to the thread handle with the given configuration.

The [`thread::spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html "fn std::thread::spawn") free function uses a `Builder` with default
configuration and [`unwrap`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap "method std::result::Result::unwrap")s its return value.

You may want to use [`spawn`](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.spawn "method std::thread::Builder::spawn") instead of [`thread::spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html "fn std::thread::spawn"), when you want
to recover from a failure to launch a thread, indeed the free function will
panic where the `Builder` method will return a [`io::Result`](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result").

## [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#examples)Examples

```
use std::thread;

let builder = thread::Builder::new();

let handler = builder.spawn(|| {
    // thread code
}).unwrap();

handler.join().unwrap();
```

## Implementations[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#implementations)

[Source](https://doc.rust-lang.org/src/std/thread/scoped.rs.html#204-263)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Builder)

### impl [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

1.63.0 · [Source](https://doc.rust-lang.org/src/std/thread/scoped.rs.html#252-262)

#### pub fn [spawn\_scoped](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.spawn_scoped)<'scope, 'env, F, T>( self, scope: &'scope [Scope](https://doc.rust-lang.org/std/thread/struct.Scope.html "struct std::thread::Scope")<'scope, 'env>, f: F, ) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[ScopedJoinHandle](https://doc.rust-lang.org/std/thread/struct.ScopedJoinHandle.html "struct std::thread::ScopedJoinHandle")<'scope, T>> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> T + [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + 'scope, T: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + 'scope,

Spawns a new scoped thread using the settings set through this `Builder`.

Unlike [`Scope::spawn`](https://doc.rust-lang.org/std/thread/struct.Scope.html#method.spawn "method std::thread::Scope::spawn"), this method yields an [`io::Result`](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result") to
capture any failure to create the thread at the OS level.

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#panics)Panics

Panics if a thread name was set and it contained null bytes.

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#example)Example

```
use std::thread;

let mut a = vec![1, 2, 3];
let mut x = 0;

thread::scope(|s| {
    thread::Builder::new()
        .name("first".to_string())
        .spawn_scoped(s, ||
    {
        println!("hello from the {:?} scoped thread", thread::current().name());
        // We can borrow `a` here.
        dbg!(&a);
    })
    .unwrap();
    thread::Builder::new()
        .name("second".to_string())
        .spawn_scoped(s, ||
    {
        println!("hello from the {:?} scoped thread", thread::current().name());
        // We can even mutably borrow `x` here,
        // because no other threads are using it.
        x += a[0] + a[2];
    })
    .unwrap();
    println!("hello from the main thread");
});

// After the scope, we can modify and access our variables again:
a.push(4);
assert_eq!(x, a.len());
```

[Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#269-603)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Builder-1)

### impl [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

1.0.0 · [Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#289-291)

#### pub fn [new](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.new)() -> [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

Generates the base configuration for spawning a thread, from which
configuration methods can be chained.

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#examples-1)Examples

```
use std::thread;

let builder = thread::Builder::new()
                              .name("foo".into())
                              .stack_size(32 * 1024);

let handler = builder.spawn(|| {
    // thread code
}).unwrap();

handler.join().unwrap();
```

1.0.0 · [Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#318-321)

#### pub fn [name](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.name)(self, name: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

Names the thread-to-be. Currently the name is used for identification
only in panic messages.

The name must not contain null bytes (`\0`).

For more information about named threads, see
[this module-level documentation](https://doc.rust-lang.org/std/thread/index.html#naming-threads).

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#examples-2)Examples

```
use std::thread;

let builder = thread::Builder::new()
    .name("foo".into());

let handler = builder.spawn(|| {
    assert_eq!(thread::current().name(), Some("foo"))
}).unwrap();

handler.join().unwrap();
```

1.0.0 · [Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#341-344)

#### pub fn [stack\_size](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.stack_size)(self, size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

Sets the size of the stack (in bytes) for the new thread.

The actual stack size may be greater than this value if
the platform specifies a minimal stack size.

For more information about the stack size for threads, see
[this module-level documentation](https://doc.rust-lang.org/std/thread/index.html#stack-size).

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#examples-3)Examples

```
use std::thread;

let builder = thread::Builder::new().stack_size(32 * 1024);
```

[Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#351-354)

#### pub fn [no\_hooks](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.no_hooks)(self) -> [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

🔬This is a nightly-only experimental API. (`thread_spawn_hook` [#132951](https://github.com/rust-lang/rust/issues/132951))

Disables running and inheriting [spawn hooks](https://doc.rust-lang.org/std/thread/fn.add_spawn_hook.html "fn std::thread::add_spawn_hook").

Use this if the parent thread is in no way relevant for the child thread.
For example, when lazily spawning threads for a thread pool.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#393-400)

#### pub fn [spawn](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.spawn)<F, T>(self, f: F) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[JoinHandle](https://doc.rust-lang.org/std/thread/struct.JoinHandle.html "struct std::thread::JoinHandle")<T>> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> T + [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + 'static, T: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + 'static,

Spawns a new thread by taking ownership of the `Builder`, and returns an
[`io::Result`](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result") to its [`JoinHandle`](https://doc.rust-lang.org/std/thread/struct.JoinHandle.html "struct std::thread::JoinHandle").

The spawned thread may outlive the caller (unless the caller thread
is the main thread; the whole process is terminated when the main
thread finishes). The join handle can be used to block on
termination of the spawned thread, including recovering its panics.

For a more complete documentation see [`thread::spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html "fn std::thread::spawn").

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#errors)Errors

Unlike the [`spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html "fn std::thread::spawn") free function, this method yields an
[`io::Result`](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result") to capture any failure to create the thread at
the OS level.

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#panics-1)Panics

Panics if a thread name was set and it contained null bytes.

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#examples-4)Examples

```
use std::thread;

let builder = thread::Builder::new();

let handler = builder.spawn(|| {
    // thread code
}).unwrap();

handler.join().unwrap();
```

1.82.0 · [Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#461-468)

#### pub unsafe fn [spawn\_unchecked](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.spawn_unchecked)<F, T>(self, f: F) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[JoinHandle](https://doc.rust-lang.org/std/thread/struct.JoinHandle.html "struct std::thread::JoinHandle")<T>> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> T + [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send"), T: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send"),

Spawns a new thread without any lifetime restrictions by taking ownership
of the `Builder`, and returns an [`io::Result`](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result") to its [`JoinHandle`](https://doc.rust-lang.org/std/thread/struct.JoinHandle.html "struct std::thread::JoinHandle").

The spawned thread may outlive the caller (unless the caller thread
is the main thread; the whole process is terminated when the main
thread finishes). The join handle can be used to block on
termination of the spawned thread, including recovering its panics.

This method is identical to [`thread::Builder::spawn`](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.spawn "method std::thread::Builder::spawn"),
except for the relaxed lifetime bounds, which render it unsafe.
For a more complete documentation see [`thread::spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html "fn std::thread::spawn").

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#errors-1)Errors

Unlike the [`spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html "fn std::thread::spawn") free function, this method yields an
[`io::Result`](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result") to capture any failure to create the thread at
the OS level.

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#panics-2)Panics

Panics if a thread name was set and it contained null bytes.

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#safety)Safety

The caller has to ensure that the spawned thread does not outlive any
references in the supplied thread closure and its return type.
This can be guaranteed in two ways:

* ensure that [`join`](https://doc.rust-lang.org/std/thread/struct.JoinHandle.html#method.join "method std::thread::JoinHandle::join") is called before any referenced
  data is dropped
* use only types with `'static` lifetime bounds, i.e., those with no or only
  `'static` references (both [`thread::Builder::spawn`](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.spawn "method std::thread::Builder::spawn")
  and [`thread::spawn`](https://doc.rust-lang.org/std/thread/fn.spawn.html "fn std::thread::spawn") enforce this property statically)

##### [§](https://doc.rust-lang.org/std/thread/struct.Builder.html#examples-5)Examples

```
use std::thread;

let builder = thread::Builder::new();

let x = 1;
let thread_x = &x;

let handler = unsafe {
    builder.spawn_unchecked(move || {
        println!("x = {}", *thread_x);
    }).unwrap()
};

// caller has to ensure `join()` is called, otherwise
// it is possible to access freed memory if `x` gets
// dropped before the thread closure is executed!
handler.join().unwrap();
```

## Trait Implementations[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#trait-implementations)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#259)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Debug-for-Builder)

### impl [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

[Source](https://doc.rust-lang.org/src/std/thread/mod.rs.html#259)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/fmt/type.Result.html "type std::fmt::Result")

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Freeze-for-Builder)

### impl [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-RefUnwindSafe-for-Builder)

### impl [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Send-for-Builder)

### impl [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Sync-for-Builder)

### impl [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Unpin-for-Builder)

### impl [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-UnwindSafe-for-Builder)

### impl [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [Builder](https://doc.rust-lang.org/std/thread/struct.Builder.html "struct std::thread::Builder")

## Blanket Implementations[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#785)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-From%3CT%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#788)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: T) -> T

Returns the argument unchanged.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#767-769)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-Into%3CU%3E-for-T)

### impl<T, U> [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<U> for T where U: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#777)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.into)

#### fn [into](https://doc.rust-lang.org/std/convert/trait.Into.html#tymethod.into)(self) -> U

Calls `U::from(self)`.

That is, this conversion is whatever the implementation of
`From<T> for U` chooses to do.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#827-829)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-TryFrom%3CU%3E-for-T)

### impl<T, U> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U> for T where U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#831)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#834)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: U) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, <T as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#811-813)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#impl-TryInto%3CU%3E-for-T)

### impl<T, U> [TryInto](https://doc.rust-lang.org/std/convert/trait.TryInto.html "trait std::convert::TryInto")<U> for T where U: [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#815)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryInto.html#associatedtype.Error) = <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#818)[§](https://doc.rust-lang.org/std/thread/struct.Builder.html#method.try_into)

#### fn [try\_into](https://doc.rust-lang.org/std/convert/trait.TryInto.html#tymethod.try_into)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.