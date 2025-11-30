---
url: https://doc.rust-lang.org/std/ops/trait.Drop.html
title: Drop in std::ops - Rust
source_domain: doc.rust-lang.org
---

# Drop in std::ops - Rust

## [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html)

[std](https://doc.rust-lang.org/std/index.html)::[ops](https://doc.rust-lang.org/std/ops/index.html)

# Trait Drop

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/133214 "Tracking issue for const_destruct")) · [Source](https://doc.rust-lang.org/src/core/ops/drop.rs.html#207)

```
pub trait Drop {
    // Required method
    fn drop(&mut self);
}
```

Expand description

Custom code within the destructor.

When a value is no longer needed, Rust will run a “destructor” on that value.
The most common way that a value is no longer needed is when it goes out of
scope. Destructors may still run in other circumstances, but we’re going to
focus on scope for the examples here. To learn about some of those other cases,
please see [the reference](https://doc.rust-lang.org/reference/destructors.html) section on destructors.

This destructor consists of two components:

* A call to `Drop::drop` for that value, if this special `Drop` trait is implemented for its type.
* The automatically generated “drop glue” which recursively calls the destructors
  of all the fields of this value.

As Rust automatically calls the destructors of all contained fields,
you don’t have to implement `Drop` in most cases. But there are some cases where
it is useful, for example for types which directly manage a resource.
That resource may be memory, it may be a file descriptor, it may be a network socket.
Once a value of that type is no longer going to be used, it should “clean up” its
resource by freeing the memory or closing the file or socket. This is
the job of a destructor, and therefore the job of `Drop::drop`.

### [§](https://doc.rust-lang.org/std/ops/trait.Drop.html#examples)Examples

To see destructors in action, let’s take a look at the following program:

```
struct HasDrop;

impl Drop for HasDrop {
    fn drop(&mut self) {
        println!("Dropping HasDrop!");
    }
}

struct HasTwoDrops {
    one: HasDrop,
    two: HasDrop,
}

impl Drop for HasTwoDrops {
    fn drop(&mut self) {
        println!("Dropping HasTwoDrops!");
    }
}

fn main() {
    let _x = HasTwoDrops { one: HasDrop, two: HasDrop };
    println!("Running!");
}
```

Rust will first call `Drop::drop` for `_x` and then for both `_x.one` and `_x.two`,
meaning that running this will print

```
Running!
Dropping HasTwoDrops!
Dropping HasDrop!
Dropping HasDrop!
```

Even if we remove the implementation of `Drop` for `HasTwoDrop`, the destructors of its fields are still called.
This would result in

```
Running!
Dropping HasDrop!
Dropping HasDrop!
```

### [§](https://doc.rust-lang.org/std/ops/trait.Drop.html#you-cannot-call-dropdrop-yourself)You cannot call `Drop::drop` yourself

Because `Drop::drop` is used to clean up a value, it may be dangerous to use this value after
the method has been called. As `Drop::drop` does not take ownership of its input,
Rust prevents misuse by not allowing you to call `Drop::drop` directly.

In other words, if you tried to explicitly call `Drop::drop` in the above example, you’d get a compiler error.

If you’d like to explicitly call the destructor of a value, [`mem::drop`](https://doc.rust-lang.org/std/mem/fn.drop.html "fn std::mem::drop") can be used instead.

### [§](https://doc.rust-lang.org/std/ops/trait.Drop.html#drop-order)Drop order

Which of our two `HasDrop` drops first, though? For structs, it’s the same
order that they’re declared: first `one`, then `two`. If you’d like to try
this yourself, you can modify `HasDrop` above to contain some data, like an
integer, and then use it in the `println!` inside of `Drop`. This behavior is
guaranteed by the language.

Unlike for structs, local variables are dropped in reverse order:

```
struct Foo;

impl Drop for Foo {
    fn drop(&mut self) {
        println!("Dropping Foo!")
    }
}

struct Bar;

impl Drop for Bar {
    fn drop(&mut self) {
        println!("Dropping Bar!")
    }
}

fn main() {
    let _foo = Foo;
    let _bar = Bar;
}
```

This will print

```
Dropping Bar!
Dropping Foo!
```

Please see [the reference](https://doc.rust-lang.org/reference/destructors.html) for the full rules.

### [§](https://doc.rust-lang.org/std/ops/trait.Drop.html#copy-and-drop-are-exclusive)`Copy` and `Drop` are exclusive

You cannot implement both [`Copy`](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy") and `Drop` on the same type. Types that
are `Copy` get implicitly duplicated by the compiler, making it very
hard to predict when, and how often destructors will be executed. As such,
these types cannot have destructors.

### [§](https://doc.rust-lang.org/std/ops/trait.Drop.html#drop-check)Drop check

Dropping interacts with the borrow checker in subtle ways: when a type `T` is being implicitly
dropped as some variable of this type goes out of scope, the borrow checker needs to ensure that
calling `T`’s destructor at this moment is safe. In particular, it also needs to be safe to
recursively drop all the fields of `T`. For example, it is crucial that code like the following
is being rejected:

[ⓘ](https://doc.rust-lang.org/std/ops/trait.Drop.html "This example deliberately fails to compile")

```
use std::cell::Cell;

struct S<'a>(Cell<Option<&'a S<'a>>>, Box<i32>);
impl Drop for S<'_> {
    fn drop(&mut self) {
        if let Some(r) = self.0.get() {
            // Print the contents of the `Box` in `r`.
            println!("{}", r.1);
        }
    }
}

fn main() {
    // Set up two `S` that point to each other.
    let s1 = S(Cell::new(None), Box::new(42));
    let s2 = S(Cell::new(Some(&s1)), Box::new(42));
    s1.0.set(Some(&s2));
    // Now they both get dropped. But whichever is the 2nd one
    // to be dropped will access the `Box` in the first one,
    // which is a use-after-free!
}
```

The Nomicon discusses the need for [drop check in more detail](https://doc.rust-lang.org/nomicon/dropck.html).

To reject such code, the “drop check” analysis determines which types and lifetimes need to
still be live when `T` gets dropped. The exact details of this analysis are not yet
stably guaranteed and **subject to change**. Currently, the analysis works as follows:

* If `T` has no drop glue, then trivially nothing is required to be live. This is the case if
  neither `T` nor any of its (recursive) fields have a destructor (`impl Drop`). [`PhantomData`](https://doc.rust-lang.org/std/marker/struct.PhantomData.html "struct std::marker::PhantomData"),
  arrays of length 0 and [`ManuallyDrop`](https://doc.rust-lang.org/std/mem/struct.ManuallyDrop.html "struct std::mem::ManuallyDrop") are considered to never have a destructor, no matter
  their field type.
* If `T` has drop glue, then, for all types `U` that are *owned* by any field of `T`,
  recursively add the types and lifetimes that need to be live when `U` gets dropped. The set of
  owned types is determined by recursively traversing `T`:
  + Recursively descend through `PhantomData`, `Box`, tuples, and arrays (excluding arrays of
    length 0).
  + Stop at reference and raw pointer types as well as function pointers and function items;
    they do not own anything.
  + Stop at non-composite types (type parameters that remain generic in the current context and
    base types such as integers and `bool`); these types are owned.
  + When hitting an ADT with `impl Drop`, stop there; this type is owned.
  + When hitting an ADT without `impl Drop`, recursively descend to its fields. (For an `enum`,
    consider all fields of all variants.)
* Furthermore, if `T` implements `Drop`, then all generic (lifetime and type) parameters of `T`
  must be live.

In the above example, the last clause implies that `'a` must be live when `S<'a>` is dropped,
and hence the example is rejected. If we remove the `impl Drop`, the liveness requirement
disappears and the example is accepted.

There exists an unstable way for a type to opt-out of the last clause; this is called “drop
check eyepatch” or `may_dangle`. For more details on this nightly-only feature, see the
[discussion in the Nomicon](https://doc.rust-lang.org/nomicon/phantom-data.html#an-exception-the-special-case-of-the-standard-library-and-its-unstable-may_dangle).

## Required Methods[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#required-methods)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/ops/drop.rs.html#240)

#### fn [drop](https://doc.rust-lang.org/std/ops/trait.Drop.html#tymethod.drop)(&mut self)

Executes the destructor for this type.

This method is called implicitly when the value goes out of scope,
and cannot be called explicitly (this is compiler error [E0040](https://doc.rust-lang.org/error_codes/E0040.html)).
However, the [`mem::drop`](https://doc.rust-lang.org/std/mem/fn.drop.html "fn std::mem::drop") function in the prelude can be
used to call the argument’s `Drop` implementation.

When this method has been called, `self` has not yet been deallocated.
That only happens after the method is over.
If this wasn’t the case, `self` would be a dangling reference.

##### [§](https://doc.rust-lang.org/std/ops/trait.Drop.html#panics)Panics

Implementations should generally avoid [`panic!`](https://doc.rust-lang.org/core/macro.panic.html "macro core::panic")ing, because `drop()` may itself be called
during unwinding due to a panic, and if the `drop()` panics in that situation (a “double
panic”), this will likely abort the program. It is possible to check [`panicking()`](https://doc.rust-lang.org/std/thread/fn.panicking.html) first,
which may be desirable for a `Drop` implementation that is reporting a bug of the kind
“you didn’t finish using this before it was dropped”; but most types should simply clean up
their owned allocations or other resources and return normally from `drop()`, regardless of
what state they are in.

Note that even if this panics, the value is considered to be dropped;
you must not cause `drop` to be called again. This is normally automatically
handled by the compiler, but when using unsafe code, can sometimes occur
unintentionally, particularly when using [`ptr::drop_in_place`](https://doc.rust-lang.org/std/ptr/fn.drop_in_place.html "fn std::ptr::drop_in_place").

## Implementors[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#implementors)

1.13.0 · [Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#698)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-CString)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString")

1.63.0 · [Source](https://doc.rust-lang.org/src/std/os/fd/owned.rs.html#170-196)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-OwnedFd)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [OwnedFd](https://doc.rust-lang.org/std/os/fd/struct.OwnedFd.html "struct std::os::fd::OwnedFd")

1.63.0 · [Source](https://doc.rust-lang.org/src/std/os/windows/io/handle.rs.html#251-260)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-HandleOrInvalid)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [HandleOrInvalid](https://doc.rust-lang.org/std/os/windows/io/struct.HandleOrInvalid.html "struct std::os::windows::io::HandleOrInvalid")

Available on **Windows** only.

1.63.0 · [Source](https://doc.rust-lang.org/src/std/os/windows/io/handle.rs.html#173-182)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-HandleOrNull)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [HandleOrNull](https://doc.rust-lang.org/std/os/windows/io/struct.HandleOrNull.html "struct std::os::windows::io::HandleOrNull")

Available on **Windows** only.

1.63.0 · [Source](https://doc.rust-lang.org/src/std/os/windows/io/handle.rs.html#384-391)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-OwnedHandle)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [OwnedHandle](https://doc.rust-lang.org/std/os/windows/io/struct.OwnedHandle.html "struct std::os::windows::io::OwnedHandle")

Available on **Windows** only.

1.63.0 · [Source](https://doc.rust-lang.org/src/std/os/windows/io/socket.rs.html#194-201)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-OwnedSocket)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [OwnedSocket](https://doc.rust-lang.org/std/os/windows/io/struct.OwnedSocket.html "struct std::os::windows::io::OwnedSocket")

Available on **Windows** only.

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3412)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Drain%3C'_%3E)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::string::[Drain](https://doc.rust-lang.org/std/string/struct.Drain.html "struct std::string::Drain")<'\_>

[Source](https://doc.rust-lang.org/src/core/task/wake.rs.html#913)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-LocalWaker)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [LocalWaker](https://doc.rust-lang.org/std/task/struct.LocalWaker.html "struct std::task::LocalWaker")

1.36.0 · [Source](https://doc.rust-lang.org/src/core/task/wake.rs.html#646)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Waker)

### impl [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Waker](https://doc.rust-lang.org/std/task/struct.Waker.html "struct std::task::Waker")

[Source](https://doc.rust-lang.org/src/std/os/windows/process.rs.html#488-499)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-ProcThreadAttributeList%3C'a%3E)

### impl<'a> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [ProcThreadAttributeList](https://doc.rust-lang.org/std/os/windows/process/struct.ProcThreadAttributeList.html "struct std::os::windows::process::ProcThreadAttributeList")<'a>

Available on **Windows** only.

[Source](https://doc.rust-lang.org/src/alloc/collections/binary_heap/mod.rs.html#1813)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-DrainSorted%3C'a,+T,+A%3E)

### impl<'a, T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [DrainSorted](https://doc.rust-lang.org/std/collections/binary_heap/struct.DrainSorted.html "struct std::collections::binary_heap::DrainSorted")<'a, T, A> where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/core/ffi/va_list.rs.html#287)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-VaListImpl%3C'f%3E)

### impl<'f> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [VaListImpl](https://doc.rust-lang.org/std/ffi/struct.VaListImpl.html "struct std::ffi::VaListImpl")<'f>

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/splice.rs.html#54)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Splice%3C'_,+I,+A%3E)

### impl<I, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Splice](https://doc.rust-lang.org/std/vec/struct.Splice.html "struct std::vec::Splice")<'\_, I, A> where I: [Iterator](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.7.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/btree/map.rs.html#1728)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-IntoIter%3CK,+V,+A%3E)

### impl<K, V, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::collections::btree\_map::[IntoIter](https://doc.rust-lang.org/std/collections/btree_map/struct.IntoIter.html "struct std::collections::btree_map::IntoIter")<K, V, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator") + [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

1.7.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/btree/map.rs.html#203)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-BTreeMap%3CK,+V,+A%3E)

### impl<K, V, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [BTreeMap](https://doc.rust-lang.org/std/collections/struct.BTreeMap.html "struct std::collections::BTreeMap")<K, V, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator") + [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/boxed/thin.rs.html#163)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-ThinBox%3CT%3E)

### impl<T> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [ThinBox](https://doc.rust-lang.org/std/boxed/struct.ThinBox.html "struct std::boxed::ThinBox")<T> where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/std/sync/mpmc/mod.rs.html#1354-1364)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Receiver%3CT%3E)

### impl<T> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Receiver](https://doc.rust-lang.org/std/sync/mpmc/struct.Receiver.html "struct std::sync::mpmc::Receiver")<T>

[Source](https://doc.rust-lang.org/src/std/sync/mpmc/mod.rs.html#628-638)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Sender%3CT%3E)

### impl<T> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Sender](https://doc.rust-lang.org/std/sync/mpmc/struct.Sender.html "struct std::sync::mpmc::Sender")<T>

1.70.0 · [Source](https://doc.rust-lang.org/src/std/sync/once_lock.rs.html#683-693)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-OnceLock%3CT%3E)

### impl<T> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [OnceLock](https://doc.rust-lang.org/std/sync/struct.OnceLock.html "struct std::sync::OnceLock")<T>

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed.rs.html#1656)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Box%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

1.12.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/binary_heap/mod.rs.html#308)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-PeekMut%3C'_,+T,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [PeekMut](https://doc.rust-lang.org/std/collections/binary_heap/struct.PeekMut.html "struct std::collections::binary_heap::PeekMut")<'\_, T, A> where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/linked_list.rs.html#1179)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-LinkedList%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [LinkedList](https://doc.rust-lang.org/std/collections/struct.LinkedList.html "struct std::collections::LinkedList")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/mod.rs.html#125)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-VecDeque%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [VecDeque](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/drain.rs.html#93)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Drain%3C'_,+T,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::collections::vec\_deque::[Drain](https://doc.rust-lang.org/std/collections/vec_deque/struct.Drain.html "struct std::collections::vec_deque::Drain")<'\_, T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2281)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Rc%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#4094)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-UniqueRc%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [UniqueRc](https://doc.rust-lang.org/std/rc/struct.UniqueRc.html "struct std::rc::UniqueRc")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#3460)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Weak%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::rc::[Weak](https://doc.rust-lang.org/std/rc/struct.Weak.html "struct std::rc::Weak")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#2611)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Arc%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#4530)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-UniqueArc%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [UniqueArc](https://doc.rust-lang.org/std/sync/struct.UniqueArc.html "struct std::sync::UniqueArc")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3274)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Weak%3CT,+A%3E-1)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::[Weak](https://doc.rust-lang.org/std/sync/struct.Weak.html "struct std::sync::Weak")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/drain.rs.html#174)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Drain%3C'_,+T,+A%3E-1)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::vec::[Drain](https://doc.rust-lang.org/std/vec/struct.Drain.html "struct std::vec::Drain")<'\_, T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/into_iter.rs.html#486)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-IntoIter%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::vec::[IntoIter](https://doc.rust-lang.org/std/vec/struct.IntoIter.html "struct std::vec::IntoIter")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4043)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-Vec%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/core/mem/drop_guard.rs.html#131-133)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-DropGuard%3CT,+F%3E)

### impl<T, F> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [DropGuard](https://doc.rust-lang.org/std/mem/struct.DropGuard.html "struct std::mem::DropGuard")<T, F> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T),

1.80.0 · [Source](https://doc.rust-lang.org/src/std/sync/lazy_lock.rs.html#332-342)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-LazyLock%3CT,+F%3E)

### impl<T, F> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [LazyLock](https://doc.rust-lang.org/std/sync/struct.LazyLock.html "struct std::sync::LazyLock")<T, F>

1.87.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/extract_if.rs.html#96)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-ExtractIf%3C'_,+T,+F,+A%3E)

### impl<T, F, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [ExtractIf](https://doc.rust-lang.org/std/vec/struct.ExtractIf.html "struct std::vec::ExtractIf")<'\_, T, F, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.40.0 · [Source](https://doc.rust-lang.org/src/core/array/iter.rs.html#323)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-IntoIter%3CT,+N%3E)

### impl<T, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::array::[IntoIter](https://doc.rust-lang.org/std/array/struct.IntoIter.html "struct std::array::IntoIter")<T, N>

[Source](https://doc.rust-lang.org/src/std/sync/nonpoison/mutex.rs.html#538-545)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MappedMutexGuard%3C'_,+T%3E)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::nonpoison::[MappedMutexGuard](https://doc.rust-lang.org/std/sync/nonpoison/struct.MappedMutexGuard.html "struct std::sync::nonpoison::MappedMutexGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/nonpoison/rwlock.rs.html#939-947)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MappedRwLockReadGuard%3C'_,+T%3E)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::nonpoison::[MappedRwLockReadGuard](https://doc.rust-lang.org/std/sync/nonpoison/struct.MappedRwLockReadGuard.html "struct std::sync::nonpoison::MappedRwLockReadGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/nonpoison/rwlock.rs.html#951-959)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MappedRwLockWriteGuard%3C'_,+T%3E)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::nonpoison::[MappedRwLockWriteGuard](https://doc.rust-lang.org/std/sync/nonpoison/struct.MappedRwLockWriteGuard.html "struct std::sync::nonpoison::MappedRwLockWriteGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/nonpoison/mutex.rs.html#437-444)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MutexGuard%3C'_,+T%3E)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::nonpoison::[MutexGuard](https://doc.rust-lang.org/std/sync/nonpoison/struct.MutexGuard.html "struct std::sync::nonpoison::MutexGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/nonpoison/rwlock.rs.html#918-925)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-RwLockReadGuard%3C'_,+T%3E)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::nonpoison::[RwLockReadGuard](https://doc.rust-lang.org/std/sync/nonpoison/struct.RwLockReadGuard.html "struct std::sync::nonpoison::RwLockReadGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/nonpoison/rwlock.rs.html#928-935)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-RwLockWriteGuard%3C'_,+T%3E)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::nonpoison::[RwLockWriteGuard](https://doc.rust-lang.org/std/sync/nonpoison/struct.RwLockWriteGuard.html "struct std::sync::nonpoison::RwLockWriteGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/poison/mutex.rs.html#853-861)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MappedMutexGuard%3C'_,+T%3E-1)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::[MappedMutexGuard](https://doc.rust-lang.org/std/sync/struct.MappedMutexGuard.html "struct std::sync::MappedMutexGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/poison/rwlock.rs.html#1123-1131)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MappedRwLockReadGuard%3C'_,+T%3E-1)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::[MappedRwLockReadGuard](https://doc.rust-lang.org/std/sync/struct.MappedRwLockReadGuard.html "struct std::sync::MappedRwLockReadGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/poison/rwlock.rs.html#1134-1143)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MappedRwLockWriteGuard%3C'_,+T%3E-1)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::[MappedRwLockWriteGuard](https://doc.rust-lang.org/std/sync/struct.MappedRwLockWriteGuard.html "struct std::sync::MappedRwLockWriteGuard")<'\_, T>

1.0.0 · [Source](https://doc.rust-lang.org/src/std/sync/poison/mutex.rs.html#736-744)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-MutexGuard%3C'_,+T%3E-1)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::[MutexGuard](https://doc.rust-lang.org/std/sync/struct.MutexGuard.html "struct std::sync::MutexGuard")<'\_, T>

[Source](https://doc.rust-lang.org/src/std/sync/reentrant_lock.rs.html#420-432)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-ReentrantLockGuard%3C'_,+T%3E)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [ReentrantLockGuard](https://doc.rust-lang.org/std/sync/struct.ReentrantLockGuard.html "struct std::sync::ReentrantLockGuard")<'\_, T>

1.0.0 · [Source](https://doc.rust-lang.org/src/std/sync/poison/rwlock.rs.html#1102-1109)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-RwLockReadGuard%3C'_,+T%3E-1)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::[RwLockReadGuard](https://doc.rust-lang.org/std/sync/struct.RwLockReadGuard.html "struct std::sync::RwLockReadGuard")<'\_, T>

1.0.0 · [Source](https://doc.rust-lang.org/src/std/sync/poison/rwlock.rs.html#1112-1120)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-RwLockWriteGuard%3C'_,+T%3E-1)

### impl<T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for std::sync::[RwLockWriteGuard](https://doc.rust-lang.org/std/sync/struct.RwLockWriteGuard.html "struct std::sync::RwLockWriteGuard")<'\_, T>

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/buffered/bufwriter.rs.html#673-680)[§](https://doc.rust-lang.org/std/ops/trait.Drop.html#impl-Drop-for-BufWriter%3CW%3E)

### impl<W: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized") + [Write](https://doc.rust-lang.org/std/io/trait.Write.html "trait std::io::Write")> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [BufWriter](https://doc.rust-lang.org/std/io/struct.BufWriter.html "struct std::io::BufWriter")<W>