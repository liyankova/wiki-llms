---
url: https://doc.rust-lang.org/std/vec/struct.Vec.html
title: Vec in std::vec - Rust
source_domain: doc.rust-lang.org
---

# Vec in std::vec - Rust

## [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html)

[std](https://doc.rust-lang.org/std/index.html)::[vec](https://doc.rust-lang.org/std/vec/index.html)

# Struct Vec

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#434)

```
pub struct Vec<T, A = Global>

where
    A: Allocator,

{ /* private fields */ }
```

Expand description

A contiguous growable array type, written as `Vec<T>`, short for ‘vector’.

## [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples)Examples

```
let mut vec = Vec::new();
vec.push(1);
vec.push(2);

assert_eq!(vec.len(), 2);
assert_eq!(vec[0], 1);

assert_eq!(vec.pop(), Some(2));
assert_eq!(vec.len(), 1);

vec[0] = 7;
assert_eq!(vec[0], 7);

vec.extend([1, 2, 3]);

for x in &vec {
    println!("{x}");
}
assert_eq!(vec, [7, 1, 2, 3]);
```

The [`vec!`](https://doc.rust-lang.org/std/macro.vec.html "macro std::vec") macro is provided for convenient initialization:

```
let mut vec1 = vec![1, 2, 3];
vec1.push(4);
let vec2 = Vec::from([1, 2, 3, 4]);
assert_eq!(vec1, vec2);
```

It can also initialize each element of a `Vec<T>` with a given value.
This may be more efficient than performing allocation and initialization
in separate steps, especially when initializing a vector of zeros:

```
let vec = vec![0; 5];
assert_eq!(vec, [0, 0, 0, 0, 0]);

// The following is equivalent, but potentially slower:
let mut vec = Vec::with_capacity(5);
vec.resize(5, 0);
assert_eq!(vec, [0, 0, 0, 0, 0]);
```

For more information, see
[Capacity and Reallocation](https://doc.rust-lang.org/std/vec/struct.Vec.html#capacity-and-reallocation).

Use a `Vec<T>` as an efficient stack:

```
let mut stack = Vec::new();

stack.push(1);
stack.push(2);
stack.push(3);

while let Some(top) = stack.pop() {
    // Prints 3, 2, 1
    println!("{top}");
}
```

## [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#indexing)Indexing

The `Vec` type allows access to values by index, because it implements the
[`Index`](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index") trait. An example will be more explicit:

```
let v = vec![0, 2, 4, 6];
println!("{}", v[1]); // it will display '2'
```

However be careful: if you try to access an index which isn’t in the `Vec`,
your software will panic! You cannot do this:

[ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html "This example panics")

```
let v = vec![0, 2, 4, 6];
println!("{}", v[6]); // it will panic!
```

Use [`get`](https://doc.rust-lang.org/std/primitive.slice.html#method.get "method slice::get") and [`get_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.get_mut "method slice::get_mut") if you want to check whether the index is in
the `Vec`.

## [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#slicing)Slicing

A `Vec` can be mutable. On the other hand, slices are read-only objects.
To get a [slice](https://doc.rust-lang.org/std/primitive.slice.html "primitive slice"), use [`&`](https://doc.rust-lang.org/std/primitive.reference.html "primitive reference"). Example:

```
fn read_slice(slice: &[usize]) {
    // ...
}

let v = vec![0, 1];
read_slice(&v);

// ... and that's all!
// you can also do it like this:
let u: &[usize] = &v;
// or like this:
let u: &[_] = &v;
```

In Rust, it’s more common to pass slices as arguments rather than vectors
when you just want to provide read access. The same goes for [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") and
[`&str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str").

## [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#capacity-and-reallocation)Capacity and reallocation

The capacity of a vector is the amount of space allocated for any future
elements that will be added onto the vector. This is not to be confused with
the *length* of a vector, which specifies the number of actual elements
within the vector. If a vector’s length exceeds its capacity, its capacity
will automatically be increased, but its elements will have to be
reallocated.

For example, a vector with capacity 10 and length 0 would be an empty vector
with space for 10 more elements. Pushing 10 or fewer elements onto the
vector will not change its capacity or cause reallocation to occur. However,
if the vector’s length is increased to 11, it will have to reallocate, which
can be slow. For this reason, it is recommended to use [`Vec::with_capacity`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.with_capacity "associated function std::vec::Vec::with_capacity")
whenever possible to specify how big the vector is expected to get.

## [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#guarantees)Guarantees

Due to its incredibly fundamental nature, `Vec` makes a lot of guarantees
about its design. This ensures that it’s as low-overhead as possible in
the general case, and can be correctly manipulated in primitive ways
by unsafe code. Note that these guarantees refer to an unqualified `Vec<T>`.
If additional type parameters are added (e.g., to support custom allocators),
overriding their defaults may change the behavior.

Most fundamentally, `Vec` is and always will be a (pointer, capacity, length)
triplet. No more, no less. The order of these fields is completely
unspecified, and you should use the appropriate methods to modify these.
The pointer will never be null, so this type is null-pointer-optimized.

However, the pointer might not actually point to allocated memory. In particular,
if you construct a `Vec` with capacity 0 via [`Vec::new`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.new "associated function std::vec::Vec::new"), [`vec![]`](https://doc.rust-lang.org/std/macro.vec.html "macro std::vec"),
[`Vec::with_capacity(0)`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.with_capacity "associated function std::vec::Vec::with_capacity"), or by calling [`shrink_to_fit`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to_fit "method std::vec::Vec::shrink_to_fit")
on an empty Vec, it will not allocate memory. Similarly, if you store zero-sized
types inside a `Vec`, it will not allocate space for them. *Note that in this case
the `Vec` might not report a [`capacity`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.capacity "method std::vec::Vec::capacity") of 0*. `Vec` will allocate if and only
if `size_of::<T>() * capacity() > 0`. In general, `Vec`’s allocation
details are very subtle — if you intend to allocate memory using a `Vec`
and use it for something else (either to pass to unsafe code, or to build your
own memory-backed collection), be sure to deallocate this memory by using
`from_raw_parts` to recover the `Vec` and then dropping it.

If a `Vec` *has* allocated memory, then the memory it points to is on the heap
(as defined by the allocator Rust is configured to use by default), and its
pointer points to [`len`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.len "method std::vec::Vec::len") initialized, contiguous elements in order (what
you would see if you coerced it to a slice), followed by `capacity - len`
logically uninitialized, contiguous elements.

A vector containing the elements `'a'` and `'b'` with capacity 4 can be
visualized as below. The top part is the `Vec` struct, it contains a
pointer to the head of the allocation in the heap, length and capacity.
The bottom part is the allocation on the heap, a contiguous memory block.

```
            ptr      len  capacity
       +--------+--------+--------+
       | 0x0123 |      2 |      4 |
       +--------+--------+--------+
            |
            v
Heap   +--------+--------+--------+--------+
       |    'a' |    'b' | uninit | uninit |
       +--------+--------+--------+--------+
```

* **uninit** represents memory that is not initialized, see [`MaybeUninit`](https://doc.rust-lang.org/std/mem/union.MaybeUninit.html "union std::mem::MaybeUninit").
* Note: the ABI is not stable and `Vec` makes no guarantees about its memory
  layout (including the order of fields).

`Vec` will never perform a “small optimization” where elements are actually
stored on the stack for two reasons:

* It would make it more difficult for unsafe code to correctly manipulate
  a `Vec`. The contents of a `Vec` wouldn’t have a stable address if it were
  only moved, and it would be more difficult to determine if a `Vec` had
  actually allocated memory.
* It would penalize the general case, incurring an additional branch
  on every access.

`Vec` will never automatically shrink itself, even if completely empty. This
ensures no unnecessary allocations or deallocations occur. Emptying a `Vec`
and then filling it back up to the same [`len`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.len "method std::vec::Vec::len") should incur no calls to
the allocator. If you wish to free up unused memory, use
[`shrink_to_fit`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to_fit "method std::vec::Vec::shrink_to_fit") or [`shrink_to`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to "method std::vec::Vec::shrink_to").

[`push`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push "method std::vec::Vec::push") and [`insert`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.insert "method std::vec::Vec::insert") will never (re)allocate if the reported capacity is
sufficient. [`push`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push "method std::vec::Vec::push") and [`insert`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.insert "method std::vec::Vec::insert") *will* (re)allocate if
`len == capacity`. That is, the reported capacity is completely
accurate, and can be relied on. It can even be used to manually free the memory
allocated by a `Vec` if desired. Bulk insertion methods *may* reallocate, even
when not necessary.

`Vec` does not guarantee any particular growth strategy when reallocating
when full, nor when [`reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reserve "method std::vec::Vec::reserve") is called. The current strategy is basic
and it may prove desirable to use a non-constant growth factor. Whatever
strategy is used will of course guarantee *O*(1) amortized [`push`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push "method std::vec::Vec::push").

It is guaranteed, in order to respect the intentions of the programmer, that
all of `vec![e_1, e_2, ..., e_n]`, `vec![x; n]`, and [`Vec::with_capacity(n)`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.with_capacity "associated function std::vec::Vec::with_capacity") produce a `Vec`
that requests an allocation of the exact size needed for precisely `n` elements from the allocator,
and no other size (such as, for example: a size rounded up to the nearest power of 2).
The allocator will return an allocation that is at least as large as requested, but it may be larger.

It is guaranteed that the [`Vec::capacity`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.capacity "method std::vec::Vec::capacity") method returns a value that is at least the requested capacity
and not more than the allocated capacity.

The method [`Vec::shrink_to_fit`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to_fit "method std::vec::Vec::shrink_to_fit") will attempt to discard excess capacity an allocator has given to a `Vec`.
If `len == capacity`, then a `Vec<T>` can be converted
to and from a [`Box<[T]>`](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box") without reallocating or moving the elements.
`Vec` exploits this fact as much as reasonable when implementing common conversions
such as [`into_boxed_slice`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_boxed_slice "method std::vec::Vec::into_boxed_slice").

`Vec` will not specifically overwrite any data that is removed from it,
but also won’t specifically preserve it. Its uninitialized memory is
scratch space that it may use however it wants. It will generally just do
whatever is most efficient or otherwise easy to implement. Do not rely on
removed data to be erased for security purposes. Even if you drop a `Vec`, its
buffer may simply be reused by another allocation. Even if you zero a `Vec`’s memory
first, that might not actually happen because the optimizer does not consider
this a side-effect that must be preserved. There is one case which we will
not break, however: using `unsafe` code to write to the excess capacity,
and then increasing the length to match, is always valid.

Currently, `Vec` does not guarantee the order in which elements are dropped.
The order has changed in the past and may change again.

## Implementations[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#implementations)

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#443)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Vec%3CT%3E)

### impl<T> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

1.0.0 (const: 1.39.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#459)

#### pub const fn [new](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.new)() -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Constructs a new, empty `Vec<T>`.

The vector will not allocate until elements are pushed onto it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-1)Examples

```
let mut vec: Vec<i32> = Vec::new();
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#519)

#### pub fn [with\_capacity](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.with_capacity)(capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Constructs a new, empty `Vec<T>` with at least the specified capacity.

The vector will be able to hold at least `capacity` elements without
reallocating. This method is allowed to allocate for more elements than
`capacity`. If `capacity` is zero, the vector will not allocate.

It is important to note that although the returned vector has the
minimum *capacity* specified, the vector will have a zero *length*. For
an explanation of the difference between length and capacity, see
*[Capacity and reallocation](https://doc.rust-lang.org/std/vec/struct.Vec.html#capacity-and-reallocation)*.

If it is important to know the exact allocated capacity of a `Vec`,
always use the [`capacity`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.capacity "method std::vec::Vec::capacity") method after construction.

For `Vec<T>` where `T` is a zero-sized type, there will be no allocation
and the capacity will always be `usize::MAX`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-2)Examples

```
let mut vec = Vec::with_capacity(10);

// The vector contains no items, even though it has capacity for more
assert_eq!(vec.len(), 0);
assert!(vec.capacity() >= 10);

// These are all done without reallocating...
for i in 0..10 {
    vec.push(i);
}
assert_eq!(vec.len(), 10);
assert!(vec.capacity() >= 10);

// ...but this may make the vector reallocate
vec.push(11);
assert_eq!(vec.len(), 11);
assert!(vec.capacity() >= 11);

// A vector of a zero-sized type will always over-allocate, since no
// allocation is necessary
let vec_units = Vec::<()>::with_capacity(10);
assert_eq!(vec_units.capacity(), usize::MAX);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#535)

#### pub fn [try\_with\_capacity](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_with_capacity)(capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>, [TryReserveError](https://doc.rust-lang.org/std/collections/struct.TryReserveError.html "struct std::collections::TryReserveError")>

🔬This is a nightly-only experimental API. (`try_with_capacity` [#91913](https://github.com/rust-lang/rust/issues/91913))

Constructs a new, empty `Vec<T>` with at least the specified capacity.

The vector will be able to hold at least `capacity` elements without
reallocating. This method is allowed to allocate for more elements than
`capacity`. If `capacity` is zero, the vector will not allocate.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#errors)Errors

Returns an error if the capacity exceeds `isize::MAX` *bytes*,
or if the allocator reports allocation failure.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#647)

#### pub unsafe fn [from\_raw\_parts](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_raw_parts)( ptr: [\*mut T](https://doc.rust-lang.org/std/primitive.pointer.html), length: [usize](https://doc.rust-lang.org/std/primitive.usize.html), capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Creates a `Vec<T>` directly from a pointer, a length, and a capacity.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety)Safety

This is highly unsafe, due to the number of invariants that aren’t
checked:

* If `T` is not a zero-sized type and the capacity is nonzero, `ptr` must have
  been allocated using the global allocator, such as via the [`alloc::alloc`](https://doc.rust-lang.org/std/alloc/fn.alloc.html "fn std::alloc::alloc")
  function. If `T` is a zero-sized type or the capacity is zero, `ptr` need
  only be non-null and aligned.
* `T` needs to have the same alignment as what `ptr` was allocated with,
  if the pointer is required to be allocated.
  (`T` having a less strict alignment is not sufficient, the alignment really
  needs to be equal to satisfy the [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") requirement that memory must be
  allocated and deallocated with the same layout.)
* The size of `T` times the `capacity` (ie. the allocated size in bytes), if
  nonzero, needs to be the same size as the pointer was allocated with.
  (Because similar to alignment, [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") must be called with the same
  layout `size`.)
* `length` needs to be less than or equal to `capacity`.
* The first `length` values must be properly initialized values of type `T`.
* `capacity` needs to be the capacity that the pointer was allocated with,
  if the pointer is required to be allocated.
* The allocated size in bytes must be no larger than `isize::MAX`.
  See the safety documentation of [`pointer::offset`](https://doc.rust-lang.org/std/primitive.pointer.html#method.offset "method pointer::offset").

These requirements are always upheld by any `ptr` that has been allocated
via `Vec<T>`. Other allocation sources are allowed if the invariants are
upheld.

Violating these may cause problems like corrupting the allocator’s
internal data structures. For example it is normally **not** safe
to build a `Vec<u8>` from a pointer to a C `char` array with length
`size_t`, doing so is only safe if the array was initially allocated by
a `Vec` or `String`.
It’s also not safe to build one from a `Vec<u16>` and its length, because
the allocator cares about the alignment, and these two types have different
alignments. The buffer was allocated with alignment 2 (for `u16`), but after
turning it into a `Vec<u8>` it’ll be deallocated with alignment 1. To avoid
these issues, it is often preferable to do casting/transmuting using
[`slice::from_raw_parts`](https://doc.rust-lang.org/std/slice/fn.from_raw_parts.html "fn std::slice::from_raw_parts") instead.

The ownership of `ptr` is effectively transferred to the
`Vec<T>` which may then deallocate, reallocate or change the
contents of memory pointed to by the pointer at will. Ensure
that nothing else uses the pointer after calling this
function.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-3)Examples

```
use std::ptr;
use std::mem;

let v = vec![1, 2, 3];

// Prevent running `v`'s destructor so we are in complete control
// of the allocation.
let mut v = mem::ManuallyDrop::new(v);

// Pull out the various important pieces of information about `v`
let p = v.as_mut_ptr();
let len = v.len();
let cap = v.capacity();

unsafe {
    // Overwrite memory with 4, 5, 6
    for i in 0..len {
        ptr::write(p.add(i), 4 + i);
    }

    // Put everything back together into a Vec
    let rebuilt = Vec::from_raw_parts(p, len, cap);
    assert_eq!(rebuilt, [4, 5, 6]);
}
```

Using memory that was allocated elsewhere:

```
use std::alloc::{alloc, Layout};

fn main() {
    let layout = Layout::array::<u32>(16).expect("overflow cannot happen");

    let vec = unsafe {
        let mem = alloc(layout).cast::<u32>();
        if mem.is_null() {
            return;
        }

        mem.write(1_000_000);

        Vec::from_raw_parts(mem, 1, 16)
    };

    assert_eq!(vec, &[1_000_000]);
    assert_eq!(vec.capacity(), 16);
}
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#759)

#### pub unsafe fn [from\_parts](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_parts)( ptr: [NonNull](https://doc.rust-lang.org/std/ptr/struct.NonNull.html "struct std::ptr::NonNull")<T>, length: [usize](https://doc.rust-lang.org/std/primitive.usize.html), capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

🔬This is a nightly-only experimental API. (`box_vec_non_null` [#130364](https://github.com/rust-lang/rust/issues/130364))

Creates a `Vec<T>` directly from a `NonNull` pointer, a length, and a capacity.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-1)Safety

This is highly unsafe, due to the number of invariants that aren’t
checked:

* `ptr` must have been allocated using the global allocator, such as via
  the [`alloc::alloc`](https://doc.rust-lang.org/std/alloc/fn.alloc.html "fn std::alloc::alloc") function.
* `T` needs to have the same alignment as what `ptr` was allocated with.
  (`T` having a less strict alignment is not sufficient, the alignment really
  needs to be equal to satisfy the [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") requirement that memory must be
  allocated and deallocated with the same layout.)
* The size of `T` times the `capacity` (ie. the allocated size in bytes) needs
  to be the same size as the pointer was allocated with. (Because similar to
  alignment, [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") must be called with the same layout `size`.)
* `length` needs to be less than or equal to `capacity`.
* The first `length` values must be properly initialized values of type `T`.
* `capacity` needs to be the capacity that the pointer was allocated with.
* The allocated size in bytes must be no larger than `isize::MAX`.
  See the safety documentation of [`pointer::offset`](https://doc.rust-lang.org/std/primitive.pointer.html#method.offset "method pointer::offset").

These requirements are always upheld by any `ptr` that has been allocated
via `Vec<T>`. Other allocation sources are allowed if the invariants are
upheld.

Violating these may cause problems like corrupting the allocator’s
internal data structures. For example it is normally **not** safe
to build a `Vec<u8>` from a pointer to a C `char` array with length
`size_t`, doing so is only safe if the array was initially allocated by
a `Vec` or `String`.
It’s also not safe to build one from a `Vec<u16>` and its length, because
the allocator cares about the alignment, and these two types have different
alignments. The buffer was allocated with alignment 2 (for `u16`), but after
turning it into a `Vec<u8>` it’ll be deallocated with alignment 1. To avoid
these issues, it is often preferable to do casting/transmuting using
[`NonNull::slice_from_raw_parts`](https://doc.rust-lang.org/std/ptr/struct.NonNull.html#method.slice_from_raw_parts "associated function std::ptr::NonNull::slice_from_raw_parts") instead.

The ownership of `ptr` is effectively transferred to the
`Vec<T>` which may then deallocate, reallocate or change the
contents of memory pointed to by the pointer at will. Ensure
that nothing else uses the pointer after calling this
function.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-4)Examples

```
#![feature(box_vec_non_null)]

use std::ptr::NonNull;
use std::mem;

let v = vec![1, 2, 3];

// Prevent running `v`'s destructor so we are in complete control
// of the allocation.
let mut v = mem::ManuallyDrop::new(v);

// Pull out the various important pieces of information about `v`
let p = unsafe { NonNull::new_unchecked(v.as_mut_ptr()) };
let len = v.len();
let cap = v.capacity();

unsafe {
    // Overwrite memory with 4, 5, 6
    for i in 0..len {
        p.add(i).write(4 + i);
    }

    // Put everything back together into a Vec
    let rebuilt = Vec::from_parts(p, len, cap);
    assert_eq!(rebuilt, [4, 5, 6]);
}
```

Using memory that was allocated elsewhere:

```
#![feature(box_vec_non_null)]

use std::alloc::{alloc, Layout};
use std::ptr::NonNull;

fn main() {
    let layout = Layout::array::<u32>(16).expect("overflow cannot happen");

    let vec = unsafe {
        let Some(mem) = NonNull::new(alloc(layout).cast::<u32>()) else {
            return;
        };

        mem.write(1_000_000);

        Vec::from_parts(mem, 1, 16)
    };

    assert_eq!(vec, &[1_000_000]);
    assert_eq!(vec.capacity(), 16);
}
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#786)

#### pub fn [peek\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.peek_mut)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[PeekMut](https://doc.rust-lang.org/std/vec/struct.PeekMut.html "struct std::vec::PeekMut")<'\_, T>>

🔬This is a nightly-only experimental API. (`vec_peek_mut` [#122742](https://github.com/rust-lang/rust/issues/122742))

Returns a mutable reference to the last item in the vector, or
`None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-5)Examples

Basic usage:

```
#![feature(vec_peek_mut)]
let mut vec = Vec::new();
assert!(vec.peek_mut().is_none());

vec.push(1);
vec.push(5);
vec.push(2);
assert_eq!(vec.last(), Some(&2));
if let Some(mut val) = vec.peek_mut() {
    *val = 0;
}
assert_eq!(vec.last(), Some(&0));
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#828)

#### pub fn [into\_raw\_parts](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_raw_parts)(self) -> ([\*mut T](https://doc.rust-lang.org/std/primitive.pointer.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`vec_into_raw_parts` [#65816](https://github.com/rust-lang/rust/issues/65816))

Decomposes a `Vec<T>` into its raw components: `(pointer, length, capacity)`.

Returns the raw pointer to the underlying data, the length of
the vector (in elements), and the allocated capacity of the
data (in elements). These are the same arguments in the same
order as the arguments to [`from_raw_parts`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_raw_parts "associated function std::vec::Vec::from_raw_parts").

After calling this function, the caller is responsible for the
memory previously managed by the `Vec`. Most often, one does
this by converting the raw pointer, length, and capacity back
into a `Vec` with the [`from_raw_parts`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_raw_parts "associated function std::vec::Vec::from_raw_parts") function; more generally,
if `T` is non-zero-sized and the capacity is nonzero, one may use
any method that calls [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") with a layout of
`Layout::array::<T>(capacity)`; if `T` is zero-sized or the
capacity is zero, nothing needs to be done.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-6)Examples

```
#![feature(vec_into_raw_parts)]
let v: Vec<i32> = vec![-1, 0, 1];

let (ptr, len, cap) = v.into_raw_parts();

let rebuilt = unsafe {
    // We can now make changes to the components, such as
    // transmuting the raw pointer to a compatible type.
    let ptr = ptr as *mut u32;

    Vec::from_raw_parts(ptr, len, cap)
};
assert_eq!(rebuilt, [4294967295, 0, 1]);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#870)

#### pub fn [into\_parts](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_parts)(self) -> ([NonNull](https://doc.rust-lang.org/std/ptr/struct.NonNull.html "struct std::ptr::NonNull")<T>, [usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`box_vec_non_null` [#130364](https://github.com/rust-lang/rust/issues/130364))

Decomposes a `Vec<T>` into its raw components: `(NonNull pointer, length, capacity)`.

Returns the `NonNull` pointer to the underlying data, the length of
the vector (in elements), and the allocated capacity of the
data (in elements). These are the same arguments in the same
order as the arguments to [`from_parts`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_parts "associated function std::vec::Vec::from_parts").

After calling this function, the caller is responsible for the
memory previously managed by the `Vec`. The only way to do
this is to convert the `NonNull` pointer, length, and capacity back
into a `Vec` with the [`from_parts`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_parts "associated function std::vec::Vec::from_parts") function, allowing
the destructor to perform the cleanup.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-7)Examples

```
#![feature(vec_into_raw_parts, box_vec_non_null)]

let v: Vec<i32> = vec![-1, 0, 1];

let (ptr, len, cap) = v.into_parts();

let rebuilt = unsafe {
    // We can now make changes to the components, such as
    // transmuting the raw pointer to a compatible type.
    let ptr = ptr.cast::<u32>();

    Vec::from_parts(ptr, len, cap)
};
assert_eq!(rebuilt, [4294967295, 0, 1]);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#877)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Vec%3CT,+A%3E)

### impl<T, A> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#894)

#### pub const fn [new\_in](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.new_in)(alloc: A) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Constructs a new, empty `Vec<T, A>`.

The vector will not allocate until elements are pushed onto it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-8)Examples

```
#![feature(allocator_api)]

use std::alloc::System;

let mut vec: Vec<i32, _> = Vec::new_in(System);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#957)

#### pub fn [with\_capacity\_in](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.with_capacity_in)(capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html), alloc: A) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Constructs a new, empty `Vec<T, A>` with at least the specified capacity
with the provided allocator.

The vector will be able to hold at least `capacity` elements without
reallocating. This method is allowed to allocate for more elements than
`capacity`. If `capacity` is zero, the vector will not allocate.

It is important to note that although the returned vector has the
minimum *capacity* specified, the vector will have a zero *length*. For
an explanation of the difference between length and capacity, see
*[Capacity and reallocation](https://doc.rust-lang.org/std/vec/struct.Vec.html#capacity-and-reallocation)*.

If it is important to know the exact allocated capacity of a `Vec`,
always use the [`capacity`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.capacity "method std::vec::Vec::capacity") method after construction.

For `Vec<T, A>` where `T` is a zero-sized type, there will be no allocation
and the capacity will always be `usize::MAX`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-1)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-9)Examples

```
#![feature(allocator_api)]

use std::alloc::System;

let mut vec = Vec::with_capacity_in(10, System);

// The vector contains no items, even though it has capacity for more
assert_eq!(vec.len(), 0);
assert!(vec.capacity() >= 10);

// These are all done without reallocating...
for i in 0..10 {
    vec.push(i);
}
assert_eq!(vec.len(), 10);
assert!(vec.capacity() >= 10);

// ...but this may make the vector reallocate
vec.push(11);
assert_eq!(vec.len(), 11);
assert!(vec.capacity() >= 11);

// A vector of a zero-sized type will always over-allocate, since no
// allocation is necessary
let vec_units = Vec::<(), System>::with_capacity_in(10, System);
assert_eq!(vec_units.capacity(), usize::MAX);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#975)

#### pub fn [try\_with\_capacity\_in](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_with_capacity_in)( capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html), alloc: A, ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>, [TryReserveError](https://doc.rust-lang.org/std/collections/struct.TryReserveError.html "struct std::collections::TryReserveError")>

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Constructs a new, empty `Vec<T, A>` with at least the specified capacity
with the provided allocator.

The vector will be able to hold at least `capacity` elements without
reallocating. This method is allowed to allocate for more elements than
`capacity`. If `capacity` is zero, the vector will not allocate.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#errors-1)Errors

Returns an error if the capacity exceeds `isize::MAX` *bytes*,
or if the allocator reports allocation failure.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1089)

#### pub unsafe fn [from\_raw\_parts\_in](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_raw_parts_in)( ptr: [\*mut T](https://doc.rust-lang.org/std/primitive.pointer.html), length: [usize](https://doc.rust-lang.org/std/primitive.usize.html), capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html), alloc: A, ) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Creates a `Vec<T, A>` directly from a pointer, a length, a capacity,
and an allocator.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-2)Safety

This is highly unsafe, due to the number of invariants that aren’t
checked:

* `ptr` must be [*currently allocated*](https://doc.rust-lang.org/std/alloc/trait.Allocator.html#currently-allocated-memory "trait std::alloc::Allocator") via the given allocator `alloc`.
* `T` needs to have the same alignment as what `ptr` was allocated with.
  (`T` having a less strict alignment is not sufficient, the alignment really
  needs to be equal to satisfy the [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") requirement that memory must be
  allocated and deallocated with the same layout.)
* The size of `T` times the `capacity` (ie. the allocated size in bytes) needs
  to be the same size as the pointer was allocated with. (Because similar to
  alignment, [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") must be called with the same layout `size`.)
* `length` needs to be less than or equal to `capacity`.
* The first `length` values must be properly initialized values of type `T`.
* `capacity` needs to [*fit*](https://doc.rust-lang.org/std/alloc/trait.Allocator.html#memory-fitting "trait std::alloc::Allocator") the layout size that the pointer was allocated with.
* The allocated size in bytes must be no larger than `isize::MAX`.
  See the safety documentation of [`pointer::offset`](https://doc.rust-lang.org/std/primitive.pointer.html#method.offset "method pointer::offset").

These requirements are always upheld by any `ptr` that has been allocated
via `Vec<T, A>`. Other allocation sources are allowed if the invariants are
upheld.

Violating these may cause problems like corrupting the allocator’s
internal data structures. For example it is **not** safe
to build a `Vec<u8>` from a pointer to a C `char` array with length `size_t`.
It’s also not safe to build one from a `Vec<u16>` and its length, because
the allocator cares about the alignment, and these two types have different
alignments. The buffer was allocated with alignment 2 (for `u16`), but after
turning it into a `Vec<u8>` it’ll be deallocated with alignment 1.

The ownership of `ptr` is effectively transferred to the
`Vec<T>` which may then deallocate, reallocate or change the
contents of memory pointed to by the pointer at will. Ensure
that nothing else uses the pointer after calling this
function.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-10)Examples

```
#![feature(allocator_api)]

use std::alloc::System;

use std::ptr;
use std::mem;

let mut v = Vec::with_capacity_in(3, System);
v.push(1);
v.push(2);
v.push(3);

// Prevent running `v`'s destructor so we are in complete control
// of the allocation.
let mut v = mem::ManuallyDrop::new(v);

// Pull out the various important pieces of information about `v`
let p = v.as_mut_ptr();
let len = v.len();
let cap = v.capacity();
let alloc = v.allocator();

unsafe {
    // Overwrite memory with 4, 5, 6
    for i in 0..len {
        ptr::write(p.add(i), 4 + i);
    }

    // Put everything back together into a Vec
    let rebuilt = Vec::from_raw_parts_in(p, len, cap, alloc.clone());
    assert_eq!(rebuilt, [4, 5, 6]);
}
```

Using memory that was allocated elsewhere:

```
#![feature(allocator_api)]

use std::alloc::{AllocError, Allocator, Global, Layout};

fn main() {
    let layout = Layout::array::<u32>(16).expect("overflow cannot happen");

    let vec = unsafe {
        let mem = match Global.allocate(layout) {
            Ok(mem) => mem.cast::<u32>().as_ptr(),
            Err(AllocError) => return,
        };

        mem.write(1_000_000);

        Vec::from_raw_parts_in(mem, 1, 16, Global)
    };

    assert_eq!(vec, &[1_000_000]);
    assert_eq!(vec.capacity(), 16);
}
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1210)

#### pub unsafe fn [from\_parts\_in](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_parts_in)( ptr: [NonNull](https://doc.rust-lang.org/std/ptr/struct.NonNull.html "struct std::ptr::NonNull")<T>, length: [usize](https://doc.rust-lang.org/std/primitive.usize.html), capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html), alloc: A, ) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Creates a `Vec<T, A>` directly from a `NonNull` pointer, a length, a capacity,
and an allocator.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-3)Safety

This is highly unsafe, due to the number of invariants that aren’t
checked:

* `ptr` must be [*currently allocated*](https://doc.rust-lang.org/std/alloc/trait.Allocator.html#currently-allocated-memory "trait std::alloc::Allocator") via the given allocator `alloc`.
* `T` needs to have the same alignment as what `ptr` was allocated with.
  (`T` having a less strict alignment is not sufficient, the alignment really
  needs to be equal to satisfy the [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") requirement that memory must be
  allocated and deallocated with the same layout.)
* The size of `T` times the `capacity` (ie. the allocated size in bytes) needs
  to be the same size as the pointer was allocated with. (Because similar to
  alignment, [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") must be called with the same layout `size`.)
* `length` needs to be less than or equal to `capacity`.
* The first `length` values must be properly initialized values of type `T`.
* `capacity` needs to [*fit*](https://doc.rust-lang.org/std/alloc/trait.Allocator.html#memory-fitting "trait std::alloc::Allocator") the layout size that the pointer was allocated with.
* The allocated size in bytes must be no larger than `isize::MAX`.
  See the safety documentation of [`pointer::offset`](https://doc.rust-lang.org/std/primitive.pointer.html#method.offset "method pointer::offset").

These requirements are always upheld by any `ptr` that has been allocated
via `Vec<T, A>`. Other allocation sources are allowed if the invariants are
upheld.

Violating these may cause problems like corrupting the allocator’s
internal data structures. For example it is **not** safe
to build a `Vec<u8>` from a pointer to a C `char` array with length `size_t`.
It’s also not safe to build one from a `Vec<u16>` and its length, because
the allocator cares about the alignment, and these two types have different
alignments. The buffer was allocated with alignment 2 (for `u16`), but after
turning it into a `Vec<u8>` it’ll be deallocated with alignment 1.

The ownership of `ptr` is effectively transferred to the
`Vec<T>` which may then deallocate, reallocate or change the
contents of memory pointed to by the pointer at will. Ensure
that nothing else uses the pointer after calling this
function.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-11)Examples

```
#![feature(allocator_api, box_vec_non_null)]

use std::alloc::System;

use std::ptr::NonNull;
use std::mem;

let mut v = Vec::with_capacity_in(3, System);
v.push(1);
v.push(2);
v.push(3);

// Prevent running `v`'s destructor so we are in complete control
// of the allocation.
let mut v = mem::ManuallyDrop::new(v);

// Pull out the various important pieces of information about `v`
let p = unsafe { NonNull::new_unchecked(v.as_mut_ptr()) };
let len = v.len();
let cap = v.capacity();
let alloc = v.allocator();

unsafe {
    // Overwrite memory with 4, 5, 6
    for i in 0..len {
        p.add(i).write(4 + i);
    }

    // Put everything back together into a Vec
    let rebuilt = Vec::from_parts_in(p, len, cap, alloc.clone());
    assert_eq!(rebuilt, [4, 5, 6]);
}
```

Using memory that was allocated elsewhere:

```
#![feature(allocator_api, box_vec_non_null)]

use std::alloc::{AllocError, Allocator, Global, Layout};

fn main() {
    let layout = Layout::array::<u32>(16).expect("overflow cannot happen");

    let vec = unsafe {
        let mem = match Global.allocate(layout) {
            Ok(mem) => mem.cast::<u32>(),
            Err(AllocError) => return,
        };

        mem.write(1_000_000);

        Vec::from_parts_in(mem, 1, 16, Global)
    };

    assert_eq!(vec, &[1_000_000]);
    assert_eq!(vec.capacity(), 16);
}
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1259)

#### pub fn [into\_raw\_parts\_with\_alloc](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_raw_parts_with_alloc)(self) -> ([\*mut T](https://doc.rust-lang.org/std/primitive.pointer.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html), A)

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Decomposes a `Vec<T>` into its raw components: `(pointer, length, capacity, allocator)`.

Returns the raw pointer to the underlying data, the length of the vector (in elements),
the allocated capacity of the data (in elements), and the allocator. These are the same
arguments in the same order as the arguments to [`from_raw_parts_in`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_raw_parts_in "associated function std::vec::Vec::from_raw_parts_in").

After calling this function, the caller is responsible for the
memory previously managed by the `Vec`. The only way to do
this is to convert the raw pointer, length, and capacity back
into a `Vec` with the [`from_raw_parts_in`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_raw_parts_in "associated function std::vec::Vec::from_raw_parts_in") function, allowing
the destructor to perform the cleanup.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-12)Examples

```
#![feature(allocator_api, vec_into_raw_parts)]

use std::alloc::System;

let mut v: Vec<i32, System> = Vec::new_in(System);
v.push(-1);
v.push(0);
v.push(1);

let (ptr, len, cap, alloc) = v.into_raw_parts_with_alloc();

let rebuilt = unsafe {
    // We can now make changes to the components, such as
    // transmuting the raw pointer to a compatible type.
    let ptr = ptr as *mut u32;

    Vec::from_raw_parts_in(ptr, len, cap, alloc)
};
assert_eq!(rebuilt, [4294967295, 0, 1]);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1310)

#### pub fn [into\_parts\_with\_alloc](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_parts_with_alloc)(self) -> ([NonNull](https://doc.rust-lang.org/std/ptr/struct.NonNull.html "struct std::ptr::NonNull")<T>, [usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html), A)

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Decomposes a `Vec<T>` into its raw components: `(NonNull pointer, length, capacity, allocator)`.

Returns the `NonNull` pointer to the underlying data, the length of the vector (in elements),
the allocated capacity of the data (in elements), and the allocator. These are the same
arguments in the same order as the arguments to [`from_parts_in`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_parts_in "associated function std::vec::Vec::from_parts_in").

After calling this function, the caller is responsible for the
memory previously managed by the `Vec`. The only way to do
this is to convert the `NonNull` pointer, length, and capacity back
into a `Vec` with the [`from_parts_in`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_parts_in "associated function std::vec::Vec::from_parts_in") function, allowing
the destructor to perform the cleanup.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-13)Examples

```
#![feature(allocator_api, vec_into_raw_parts, box_vec_non_null)]

use std::alloc::System;

let mut v: Vec<i32, System> = Vec::new_in(System);
v.push(-1);
v.push(0);
v.push(1);

let (ptr, len, cap, alloc) = v.into_parts_with_alloc();

let rebuilt = unsafe {
    // We can now make changes to the components, such as
    // transmuting the raw pointer to a compatible type.
    let ptr = ptr.cast::<u32>();

    Vec::from_parts_in(ptr, len, cap, alloc)
};
assert_eq!(rebuilt, [4294967295, 0, 1]);
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1342)

#### pub const fn [capacity](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.capacity)(&self) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Returns the total number of elements the vector can hold without
reallocating.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-14)Examples

```
let mut vec: Vec<i32> = Vec::with_capacity(10);
vec.push(42);
assert!(vec.capacity() >= 10);
```

A vector with zero-sized elements will always have a capacity of usize::MAX:

```
#[derive(Clone)]
struct ZeroSized;

fn main() {
    assert_eq!(std::mem::size_of::<ZeroSized>(), 0);
    let v = vec![ZeroSized; 0];
    assert_eq!(v.capacity(), usize::MAX);
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1367)

#### pub fn [reserve](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Reserves capacity for at least `additional` more elements to be inserted
in the given `Vec<T>`. The collection may reserve more space to
speculatively avoid frequent reallocations. After calling `reserve`,
capacity will be greater than or equal to `self.len() + additional`.
Does nothing if capacity is already sufficient.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-2)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-15)Examples

```
let mut vec = vec![1];
vec.reserve(10);
assert!(vec.capacity() >= 11);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1398)

#### pub fn [reserve\_exact](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reserve_exact)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Reserves the minimum capacity for at least `additional` more elements to
be inserted in the given `Vec<T>`. Unlike [`reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reserve "method std::vec::Vec::reserve"), this will not
deliberately over-allocate to speculatively avoid frequent allocations.
After calling `reserve_exact`, capacity will be greater than or equal to
`self.len() + additional`. Does nothing if the capacity is already
sufficient.

Note that the allocator may give the collection more space than it
requests. Therefore, capacity can not be relied upon to be precisely
minimal. Prefer [`reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reserve "method std::vec::Vec::reserve") if future insertions are expected.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-3)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-16)Examples

```
let mut vec = vec![1];
vec.reserve_exact(10);
assert!(vec.capacity() >= 11);
```

1.57.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1435)

#### pub fn [try\_reserve](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [TryReserveError](https://doc.rust-lang.org/std/collections/struct.TryReserveError.html "struct std::collections::TryReserveError")>

Tries to reserve capacity for at least `additional` more elements to be inserted
in the given `Vec<T>`. The collection may reserve more space to speculatively avoid
frequent reallocations. After calling `try_reserve`, capacity will be
greater than or equal to `self.len() + additional` if it returns
`Ok(())`. Does nothing if capacity is already sufficient. This method
preserves the contents even if an error occurs.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#errors-2)Errors

If the capacity overflows, or the allocator reports a failure, then an error
is returned.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-17)Examples

```
use std::collections::TryReserveError;

fn process_data(data: &[u32]) -> Result<Vec<u32>, TryReserveError> {
    let mut output = Vec::new();

    // Pre-reserve the memory, exiting if we can't
    output.try_reserve(data.len())?;

    // Now we know this can't OOM in the middle of our complex work
    output.extend(data.iter().map(|&val| {
        val * 2 + 5 // very complicated
    }));

    Ok(output)
}
```

1.57.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1478)

#### pub fn [try\_reserve\_exact](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_reserve_exact)( &mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [TryReserveError](https://doc.rust-lang.org/std/collections/struct.TryReserveError.html "struct std::collections::TryReserveError")>

Tries to reserve the minimum capacity for at least `additional`
elements to be inserted in the given `Vec<T>`. Unlike [`try_reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_reserve "method std::vec::Vec::try_reserve"),
this will not deliberately over-allocate to speculatively avoid frequent
allocations. After calling `try_reserve_exact`, capacity will be greater
than or equal to `self.len() + additional` if it returns `Ok(())`.
Does nothing if the capacity is already sufficient.

Note that the allocator may give the collection more space than it
requests. Therefore, capacity can not be relied upon to be precisely
minimal. Prefer [`try_reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_reserve "method std::vec::Vec::try_reserve") if future insertions are expected.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#errors-3)Errors

If the capacity overflows, or the allocator reports a failure, then an error
is returned.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-18)Examples

```
use std::collections::TryReserveError;

fn process_data(data: &[u32]) -> Result<Vec<u32>, TryReserveError> {
    let mut output = Vec::new();

    // Pre-reserve the memory, exiting if we can't
    output.try_reserve_exact(data.len())?;

    // Now we know this can't OOM in the middle of our complex work
    output.extend(data.iter().map(|&val| {
        val * 2 + 5 // very complicated
    }));

    Ok(output)
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1503)

#### pub fn [shrink\_to\_fit](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to_fit)(&mut self)

Shrinks the capacity of the vector as much as possible.

The behavior of this method depends on the allocator, which may either shrink the vector
in-place or reallocate. The resulting vector might still have some excess capacity, just as
is the case for [`with_capacity`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.with_capacity "associated function std::vec::Vec::with_capacity"). See [`Allocator::shrink`](https://doc.rust-lang.org/std/alloc/trait.Allocator.html#method.shrink "method std::alloc::Allocator::shrink") for more details.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-19)Examples

```
let mut vec = Vec::with_capacity(10);
vec.extend([1, 2, 3]);
assert!(vec.capacity() >= 10);
vec.shrink_to_fit();
assert!(vec.capacity() >= 3);
```

1.56.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1533)

#### pub fn [shrink\_to](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to)(&mut self, min\_capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Shrinks the capacity of the vector with a lower bound.

The capacity will remain at least as large as both the length
and the supplied value.

If the current capacity is less than the lower limit, this is a no-op.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-20)Examples

```
let mut vec = Vec::with_capacity(10);
vec.extend([1, 2, 3]);
assert!(vec.capacity() >= 10);
vec.shrink_to(4);
assert!(vec.capacity() >= 4);
vec.shrink_to(0);
assert!(vec.capacity() >= 3);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1567)

#### pub fn [into\_boxed\_slice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_boxed_slice)(self) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A>

Converts the vector into [`Box<[T]>`](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box").

Before doing the conversion, this method discards excess capacity like [`shrink_to_fit`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to_fit "method std::vec::Vec::shrink_to_fit").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-21)Examples

```
let v = vec![1, 2, 3];

let slice = v.into_boxed_slice();
```

Any excess capacity is removed:

```
let mut vec = Vec::with_capacity(10);
vec.extend([1, 2, 3]);

assert!(vec.capacity() >= 10);
let slice = vec.into_boxed_slice();
assert_eq!(slice.into_vec().capacity(), 3);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1620)

#### pub fn [truncate](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.truncate)(&mut self, len: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Shortens the vector, keeping the first `len` elements and dropping
the rest.

If `len` is greater or equal to the vector’s current length, this has
no effect.

The [`drain`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.drain "method std::vec::Vec::drain") method can emulate `truncate`, but causes the excess
elements to be returned instead of dropped.

Note that this method has no effect on the allocated capacity
of the vector.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-22)Examples

Truncating a five element vector to two elements:

```
let mut vec = vec![1, 2, 3, 4, 5];
vec.truncate(2);
assert_eq!(vec, [1, 2]);
```

No truncation occurs when `len` is greater than the vector’s current
length:

```
let mut vec = vec![1, 2, 3];
vec.truncate(8);
assert_eq!(vec, [1, 2, 3]);
```

Truncating when `len == 0` is equivalent to calling the [`clear`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clear "method std::vec::Vec::clear")
method.

```
let mut vec = vec![1, 2, 3];
vec.truncate(0);
assert_eq!(vec, []);
```

1.7.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1657)

#### pub const fn [as\_slice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_slice)(&self) -> &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Extracts a slice containing the entire vector.

Equivalent to `&s[..]`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-23)Examples

```
use std::io::{self, Write};
let buffer = vec![1, 2, 3, 5, 8];
io::sink().write(buffer.as_slice()).unwrap();
```

1.7.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1689)

#### pub const fn [as\_mut\_slice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_slice)(&mut self) -> &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Extracts a mutable slice of the entire vector.

Equivalent to `&mut s[..]`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-24)Examples

```
use std::io::{self, Read};
let mut buffer = vec![0; 3];
io::repeat(0b101).read_exact(buffer.as_mut_slice()).unwrap();
```

1.37.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1764)

#### pub const fn [as\_ptr](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ptr)(&self) -> [\*const T](https://doc.rust-lang.org/std/primitive.pointer.html)

Returns a raw pointer to the vector’s buffer, or a dangling raw pointer
valid for zero sized reads if the vector didn’t allocate.

The caller must ensure that the vector outlives the pointer this
function returns, or else it will end up dangling.
Modifying the vector may cause its buffer to be reallocated,
which would also make any pointers to it invalid.

The caller must also ensure that the memory the pointer (non-transitively) points to
is never written to (except inside an `UnsafeCell`) using this pointer or any pointer
derived from it. If you need to mutate the contents of the slice, use [`as_mut_ptr`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_ptr "method std::vec::Vec::as_mut_ptr").

This method guarantees that for the purpose of the aliasing model, this method
does not materialize a reference to the underlying slice, and thus the returned pointer
will remain valid when mixed with other calls to [`as_ptr`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ptr "method std::vec::Vec::as_ptr"), [`as_mut_ptr`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_ptr "method std::vec::Vec::as_mut_ptr"),
and [`as_non_null`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_non_null "method std::vec::Vec::as_non_null").
Note that calling other methods that materialize mutable references to the slice,
or mutable references to specific elements you are planning on accessing through this pointer,
as well as writing to those elements, may still invalidate this pointer.
See the second example below for how this guarantee can be used.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-25)Examples

```
let x = vec![1, 2, 4];
let x_ptr = x.as_ptr();

unsafe {
    for i in 0..x.len() {
        assert_eq!(*x_ptr.add(i), 1 << i);
    }
}
```

Due to the aliasing guarantee, the following code is legal:

```
unsafe {
    let mut v = vec![0, 1, 2];
    let ptr1 = v.as_ptr();
    let _ = ptr1.read();
    let ptr2 = v.as_mut_ptr().offset(2);
    ptr2.write(2);
    // Notably, the write to `ptr2` did *not* invalidate `ptr1`
    // because it mutated a different element:
    let _ = ptr1.read();
}
```

1.37.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1848)

#### pub const fn [as\_mut\_ptr](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_ptr)(&mut self) -> [\*mut T](https://doc.rust-lang.org/std/primitive.pointer.html)

Returns a raw mutable pointer to the vector’s buffer, or a dangling
raw pointer valid for zero sized reads if the vector didn’t allocate.

The caller must ensure that the vector outlives the pointer this
function returns, or else it will end up dangling.
Modifying the vector may cause its buffer to be reallocated,
which would also make any pointers to it invalid.

This method guarantees that for the purpose of the aliasing model, this method
does not materialize a reference to the underlying slice, and thus the returned pointer
will remain valid when mixed with other calls to [`as_ptr`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ptr "method std::vec::Vec::as_ptr"), [`as_mut_ptr`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_ptr "method std::vec::Vec::as_mut_ptr"),
and [`as_non_null`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_non_null "method std::vec::Vec::as_non_null").
Note that calling other methods that materialize references to the slice,
or references to specific elements you are planning on accessing through this pointer,
may still invalidate this pointer.
See the second example below for how this guarantee can be used.

The method also guarantees that, as long as `T` is not zero-sized and the capacity is
nonzero, the pointer may be passed into [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") with a layout of
`Layout::array::<T>(capacity)` in order to deallocate the backing memory. If this is done,
be careful not to run the destructor of the `Vec`, as dropping it will result in
double-frees. Wrapping the `Vec` in a [`ManuallyDrop`](https://doc.rust-lang.org/std/mem/struct.ManuallyDrop.html "struct std::mem::ManuallyDrop") is the typical way to achieve this.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-26)Examples

```
// Allocate vector big enough for 4 elements.
let size = 4;
let mut x: Vec<i32> = Vec::with_capacity(size);
let x_ptr = x.as_mut_ptr();

// Initialize elements via raw pointer writes, then set length.
unsafe {
    for i in 0..size {
        *x_ptr.add(i) = i as i32;
    }
    x.set_len(size);
}
assert_eq!(&*x, &[0, 1, 2, 3]);
```

Due to the aliasing guarantee, the following code is legal:

```
unsafe {
    let mut v = vec![0];
    let ptr1 = v.as_mut_ptr();
    ptr1.write(1);
    let ptr2 = v.as_mut_ptr();
    ptr2.write(2);
    // Notably, the write to `ptr2` did *not* invalidate `ptr1`:
    ptr1.write(3);
}
```

Deallocating a vector using [`Box`](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box") (which uses [`dealloc`](https://doc.rust-lang.org/std/alloc/trait.GlobalAlloc.html#tymethod.dealloc "method std::alloc::GlobalAlloc::dealloc") internally):

```
use std::mem::{ManuallyDrop, MaybeUninit};

let mut v = ManuallyDrop::new(vec![0, 1, 2]);
let ptr = v.as_mut_ptr();
let capacity = v.capacity();
let slice_ptr: *mut [MaybeUninit<i32>] =
    std::ptr::slice_from_raw_parts_mut(ptr.cast(), capacity);
drop(unsafe { Box::from_raw(slice_ptr) });
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1913)

#### pub const fn [as\_non\_null](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_non_null)(&mut self) -> [NonNull](https://doc.rust-lang.org/std/ptr/struct.NonNull.html "struct std::ptr::NonNull")<T>

🔬This is a nightly-only experimental API. (`box_vec_non_null` [#130364](https://github.com/rust-lang/rust/issues/130364))

Returns a `NonNull` pointer to the vector’s buffer, or a dangling
`NonNull` pointer valid for zero sized reads if the vector didn’t allocate.

The caller must ensure that the vector outlives the pointer this
function returns, or else it will end up dangling.
Modifying the vector may cause its buffer to be reallocated,
which would also make any pointers to it invalid.

This method guarantees that for the purpose of the aliasing model, this method
does not materialize a reference to the underlying slice, and thus the returned pointer
will remain valid when mixed with other calls to [`as_ptr`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ptr "method std::vec::Vec::as_ptr"), [`as_mut_ptr`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_ptr "method std::vec::Vec::as_mut_ptr"),
and [`as_non_null`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_non_null "method std::vec::Vec::as_non_null").
Note that calling other methods that materialize references to the slice,
or references to specific elements you are planning on accessing through this pointer,
may still invalidate this pointer.
See the second example below for how this guarantee can be used.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-27)Examples

```
#![feature(box_vec_non_null)]

// Allocate vector big enough for 4 elements.
let size = 4;
let mut x: Vec<i32> = Vec::with_capacity(size);
let x_ptr = x.as_non_null();

// Initialize elements via raw pointer writes, then set length.
unsafe {
    for i in 0..size {
        x_ptr.add(i).write(i as i32);
    }
    x.set_len(size);
}
assert_eq!(&*x, &[0, 1, 2, 3]);
```

Due to the aliasing guarantee, the following code is legal:

```
#![feature(box_vec_non_null)]

unsafe {
    let mut v = vec![0];
    let ptr1 = v.as_non_null();
    ptr1.write(1);
    let ptr2 = v.as_non_null();
    ptr2.write(2);
    // Notably, the write to `ptr2` did *not* invalidate `ptr1`:
    ptr1.write(3);
}
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#1920)

#### pub fn [allocator](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.allocator)(&self) -> [&A](https://doc.rust-lang.org/std/primitive.reference.html)

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Returns a reference to the underlying allocator.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2012)

#### pub unsafe fn [set\_len](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.set_len)(&mut self, new\_len: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Forces the length of the vector to `new_len`.

This is a low-level operation that maintains none of the normal
invariants of the type. Normally changing the length of a vector
is done using one of the safe operations instead, such as
[`truncate`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.truncate "method std::vec::Vec::truncate"), [`resize`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.resize "method std::vec::Vec::resize"), [`extend`](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend "method std::iter::Extend::extend"), or [`clear`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clear "method std::vec::Vec::clear").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-4)Safety

* `new_len` must be less than or equal to [`capacity()`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.capacity "method std::vec::Vec::capacity").
* The elements at `old_len..new_len` must be initialized.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-28)Examples

See [`spare_capacity_mut()`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.spare_capacity_mut "method std::vec::Vec::spare_capacity_mut") for an example with safe
initialization of capacity elements and use of this method.

`set_len()` can be useful for situations in which the vector
is serving as a buffer for other code, particularly over FFI:

```
pub fn get_dictionary(&self) -> Option<Vec<u8>> {
    // Per the FFI method's docs, "32768 bytes is always enough".
    let mut dict = Vec::with_capacity(32_768);
    let mut dict_length = 0;
    // SAFETY: When `deflateGetDictionary` returns `Z_OK`, it holds that:
    // 1. `dict_length` elements were initialized.
    // 2. `dict_length` <= the capacity (32_768)
    // which makes `set_len` safe to call.
    unsafe {
        // Make the FFI call...
        let r = deflateGetDictionary(self.strm, dict.as_mut_ptr(), &mut dict_length);
        if r == Z_OK {
            // ...and update the length to what was initialized.
            dict.set_len(dict_length);
            Some(dict)
        } else {
            None
        }
    }
}
```

While the following example is sound, there is a memory leak since
the inner vectors were not freed prior to the `set_len` call:

```
let mut vec = vec![vec![1, 0, 0],
                   vec![0, 1, 0],
                   vec![0, 0, 1]];
// SAFETY:
// 1. `old_len..0` is empty so no elements need to be initialized.
// 2. `0 <= capacity` always holds whatever `capacity` is.
unsafe {
    vec.set_len(0);
}
```

Normally, here, one would use [`clear`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clear "method std::vec::Vec::clear") instead to correctly drop
the contents and thus not leak memory.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2048)

#### pub fn [swap\_remove](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.swap_remove)(&mut self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> T

Removes an element from the vector and returns it.

The removed element is replaced by the last element of the vector.

This does not preserve ordering of the remaining elements, but is *O*(1).
If you need to preserve the element order, use [`remove`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.remove "method std::vec::Vec::remove") instead.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-4)Panics

Panics if `index` is out of bounds.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-29)Examples

```
let mut v = vec!["foo", "bar", "baz", "qux"];

assert_eq!(v.swap_remove(1), "bar");
assert_eq!(v, ["foo", "qux", "baz"]);

assert_eq!(v.swap_remove(0), "foo");
assert_eq!(v, ["baz", "qux"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2098)

#### pub fn [insert](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.insert)(&mut self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html), element: T)

Inserts an element at position `index` within the vector, shifting all
elements after it to the right.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-5)Panics

Panics if `index > len`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-30)Examples

```
let mut vec = vec!['a', 'b', 'c'];
vec.insert(1, 'd');
assert_eq!(vec, ['a', 'd', 'b', 'c']);
vec.insert(4, 'e');
assert_eq!(vec, ['a', 'd', 'b', 'c', 'e']);
```

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#time-complexity)Time complexity

Takes *O*([`Vec::len`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.len "method std::vec::Vec::len")) time. All items after the insertion index must be
shifted to the right. In the worst case, all elements are shifted when
the insertion index is 0.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2130)

#### pub fn [insert\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.insert_mut)(&mut self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html), element: T) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

🔬This is a nightly-only experimental API. (`push_mut` [#135974](https://github.com/rust-lang/rust/issues/135974))

Inserts an element at position `index` within the vector, shifting all
elements after it to the right, and returning a reference to the new
element.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-6)Panics

Panics if `index > len`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-31)Examples

```
#![feature(push_mut)]
let mut vec = vec![1, 3, 5, 9];
let x = vec.insert_mut(3, 6);
*x += 1;
assert_eq!(vec, [1, 3, 5, 7, 9]);
```

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#time-complexity-1)Time complexity

Takes *O*([`Vec::len`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.len "method std::vec::Vec::len")) time. All items after the insertion index must be
shifted to the right. In the worst case, all elements are shifted when
the insertion index is 0.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2194)

#### pub fn [remove](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.remove)(&mut self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> T

Removes and returns the element at position `index` within the vector,
shifting all elements after it to the left.

Note: Because this shifts over the remaining elements, it has a
worst-case performance of *O*(*n*). If you don’t need the order of elements
to be preserved, use [`swap_remove`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.swap_remove "method std::vec::Vec::swap_remove") instead. If you’d like to remove
elements from the beginning of the `Vec`, consider using
[`VecDeque::pop_front`](https://doc.rust-lang.org/std/collections/struct.VecDeque.html#method.pop_front "method std::collections::VecDeque::pop_front") instead.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-7)Panics

Panics if `index` is out of bounds.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-32)Examples

```
let mut v = vec!['a', 'b', 'c'];
assert_eq!(v.remove(1), 'b');
assert_eq!(v, ['a', 'c']);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2250-2252)

#### pub fn [retain](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.retain)<F>(&mut self, f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Retains only the elements specified by the predicate.

In other words, remove all elements `e` for which `f(&e)` returns `false`.
This method operates in place, visiting each element exactly once in the
original order, and preserves the order of the retained elements.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-33)Examples

```
let mut vec = vec![1, 2, 3, 4];
vec.retain(|&x| x % 2 == 0);
assert_eq!(vec, [2, 4]);
```

Because the elements are visited exactly once in the original order,
external state may be used to decide which elements to keep.

```
let mut vec = vec![1, 2, 3, 4, 5];
let keep = [false, true, true, false, true];
let mut iter = keep.iter();
vec.retain(|_| *iter.next().unwrap());
assert_eq!(vec, [2, 3, 5]);
```

1.61.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2276-2278)

#### pub fn [retain\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.retain_mut)<F>(&mut self, f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Retains only the elements specified by the predicate, passing a mutable reference to it.

In other words, remove all elements `e` such that `f(&mut e)` returns `false`.
This method operates in place, visiting each element exactly once in the
original order, and preserves the order of the retained elements.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-34)Examples

```
let mut vec = vec![1, 2, 3, 4];
vec.retain_mut(|x| if *x <= 3 {
    *x += 1;
    true
} else {
    false
});
assert_eq!(vec, [2, 3, 4]);
```

1.16.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2391-2394)

#### pub fn [dedup\_by\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.dedup_by_key)<F, K>(&mut self, key: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> K, K: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

Removes all but the first of consecutive elements in the vector that resolve to the same
key.

If the vector is sorted, this removes all duplicates.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-35)Examples

```
let mut vec = vec![10, 20, 21, 30, 20];

vec.dedup_by_key(|i| *i / 10);

assert_eq!(vec, [10, 20, 30, 20]);
```

1.16.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2418-2420)

#### pub fn [dedup\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.dedup_by)<F>(&mut self, same\_bucket: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html), [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Removes all but the first of consecutive elements in the vector satisfying a given equality
relation.

The `same_bucket` function is passed references to two elements from the vector and
must determine if the elements compare equal. The elements are passed in opposite order
from their order in the slice, so if `same_bucket(a, b)` returns `true`, `a` is removed.

If the vector is sorted, this removes all duplicates.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-36)Examples

```
let mut vec = vec!["foo", "bar", "Bar", "baz", "bar"];

vec.dedup_by(|a, b| a.eq_ignore_ascii_case(b));

assert_eq!(vec, ["foo", "bar", "baz", "bar"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2571)

#### pub fn [push](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push)(&mut self, value: T)

Appends an element to the back of a collection.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-8)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-37)Examples

```
let mut vec = vec![1, 2];
vec.push(3);
assert_eq!(vec, [1, 2, 3]);
```

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#time-complexity-2)Time complexity

Takes amortized *O*(1) time. If the vector’s length would exceed its
capacity after the push, *O*(*capacity*) time is taken to copy the
vector’s elements to a larger allocation. This expensive operation is
offset by the *capacity* *O*(1) insertions it allows.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2612)

#### pub fn [push\_within\_capacity](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push_within_capacity)(&mut self, value: T) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), T>

🔬This is a nightly-only experimental API. (`vec_push_within_capacity` [#100486](https://github.com/rust-lang/rust/issues/100486))

Appends an element if there is sufficient spare capacity, otherwise an error is returned
with the element.

Unlike [`push`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push "method std::vec::Vec::push") this method will not reallocate when there’s insufficient capacity.
The caller should use [`reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reserve "method std::vec::Vec::reserve") or [`try_reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_reserve "method std::vec::Vec::try_reserve") to ensure that there is enough capacity.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-38)Examples

A manual, panic-free alternative to [`FromIterator`](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator"):

```
#![feature(vec_push_within_capacity)]

use std::collections::TryReserveError;
fn from_iter_fallible<T>(iter: impl Iterator<Item=T>) -> Result<Vec<T>, TryReserveError> {
    let mut vec = Vec::new();
    for value in iter {
        if let Err(value) = vec.push_within_capacity(value) {
            vec.try_reserve(1)?;
            // this cannot fail, the previous line either returned or added at least 1 free slot
            let _ = vec.push_within_capacity(value);
        }
    }
    Ok(vec)
}
assert_eq!(from_iter_fallible(0..100), Ok(Vec::from_iter(0..100)));
```

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#time-complexity-3)Time complexity

Takes *O*(1) time.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2649)

#### pub fn [push\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push_mut)(&mut self, value: T) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

🔬This is a nightly-only experimental API. (`push_mut` [#135974](https://github.com/rust-lang/rust/issues/135974))

Appends an element to the back of a collection, returning a reference to it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-9)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-39)Examples

```
#![feature(push_mut)]

let mut vec = vec![1, 2];
let last = vec.push_mut(3);
assert_eq!(*last, 3);
assert_eq!(vec, [1, 2, 3]);

let last = vec.push_mut(3);
*last += 1;
assert_eq!(vec, [1, 2, 3, 4]);
```

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#time-complexity-4)Time complexity

Takes amortized *O*(1) time. If the vector’s length would exceed its
capacity after the push, *O*(*capacity*) time is taken to copy the
vector’s elements to a larger allocation. This expensive operation is
offset by the *capacity* *O*(1) insertions it allows.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2683)

#### pub fn [push\_mut\_within\_capacity](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push_mut_within_capacity)(&mut self, value: T) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html), T>

🔬This is a nightly-only experimental API. (`push_mut` [#135974](https://github.com/rust-lang/rust/issues/135974))

Appends an element and returns a reference to it if there is sufficient spare capacity,
otherwise an error is returned with the element.

Unlike [`push_mut`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push_mut "method std::vec::Vec::push_mut") this method will not reallocate when there’s insufficient capacity.
The caller should use [`reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reserve "method std::vec::Vec::reserve") or [`try_reserve`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_reserve "method std::vec::Vec::try_reserve") to ensure that there is enough capacity.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#time-complexity-5)Time complexity

Takes *O*(1) time.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2718)

#### pub fn [pop](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.pop)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Removes the last element from a vector and returns it, or [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if it
is empty.

If you’d like to pop the first element, consider using
[`VecDeque::pop_front`](https://doc.rust-lang.org/std/collections/struct.VecDeque.html#method.pop_front "method std::collections::VecDeque::pop_front") instead.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-40)Examples

```
let mut vec = vec![1, 2, 3];
assert_eq!(vec.pop(), Some(3));
assert_eq!(vec, [1, 2]);
```

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#time-complexity-6)Time complexity

Takes *O*(1) time.

1.86.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2745)

#### pub fn [pop\_if](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.pop_if)(&mut self, predicate: impl [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Removes and returns the last element from a vector if the predicate
returns `true`, or [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the predicate returns false or the vector
is empty (the predicate will not be called in that case).

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-41)Examples

```
let mut vec = vec![1, 2, 3, 4];
let pred = |x: &mut i32| *x % 2 == 0;

assert_eq!(vec.pop_if(pred), Some(4));
assert_eq!(vec, [1, 2, 3]);
assert_eq!(vec.pop_if(pred), None);
```

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2769)

#### pub fn [append](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.append)(&mut self, other: &mut [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>)

Moves all the elements of `other` into `self`, leaving `other` empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-10)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-42)Examples

```
let mut vec = vec![1, 2, 3];
let mut vec2 = vec![4, 5, 6];
vec.append(&mut vec2);
assert_eq!(vec, [1, 2, 3, 4, 5, 6]);
assert_eq!(vec2, []);
```

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2821-2823)

#### pub fn [drain](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.drain)<R>(&mut self, range: R) -> [Drain](https://doc.rust-lang.org/std/vec/struct.Drain.html "struct std::vec::Drain")<'\_, T, A> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Removes the subslice indicated by the given range from the vector,
returning a double-ended iterator over the removed subslice.

If the iterator is dropped before being fully consumed,
it drops the remaining removed elements.

The returned iterator keeps a mutable borrow on the vector to optimize
its implementation.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-11)Panics

Panics if the starting point is greater than the end point or if
the end point is greater than the length of the vector.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#leaking)Leaking

If the returned iterator goes out of scope without being dropped (due to
[`mem::forget`](https://doc.rust-lang.org/std/mem/fn.forget.html "fn std::mem::forget"), for example), the vector may have lost and leaked
elements arbitrarily, including elements outside the range.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-43)Examples

```
let mut v = vec![1, 2, 3];
let u: Vec<_> = v.drain(1..).collect();
assert_eq!(v, &[1]);
assert_eq!(u, &[2, 3]);

// A full range clears the vector, like `clear()` does
v.drain(..);
assert_eq!(v, &[]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2867)

#### pub fn [clear](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clear)(&mut self)

Clears the vector, removing all values.

Note that this method has no effect on the allocated capacity
of the vector.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-44)Examples

```
let mut v = vec![1, 2, 3];

v.clear();

assert!(v.is_empty());
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2895)

#### pub const fn [len](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.len)(&self) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Returns the number of elements in the vector, also referred to
as its ‘length’.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-45)Examples

```
let a = vec![1, 2, 3];
assert_eq!(a.len(), 3);
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2920)

#### pub const fn [is\_empty](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.is_empty)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the vector contains no elements.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-46)Examples

```
let mut v = Vec::new();
assert!(v.is_empty());

v.push(1);
assert!(!v.is_empty());
```

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#2953-2955)

#### pub fn [split\_off](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_off)(&mut self, at: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Splits the collection into two at the given index.

Returns a newly allocated vector containing the elements in the range
`[at, len)`. After the call, the original vector will be left containing
the elements `[0, at)` with its previous capacity unchanged.

* If you want to take ownership of the entire contents and capacity of
  the vector, see [`mem::take`](https://doc.rust-lang.org/std/mem/fn.take.html "fn std::mem::take") or [`mem::replace`](https://doc.rust-lang.org/std/mem/fn.replace.html "fn std::mem::replace").
* If you don’t need the returned vector at all, see [`Vec::truncate`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.truncate "method std::vec::Vec::truncate").
* If you want to take ownership of an arbitrary subslice, or you don’t
  necessarily want to store the removed items in a vector, see [`Vec::drain`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.drain "method std::vec::Vec::drain").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-12)Panics

Panics if `at > len`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-47)Examples

```
let mut vec = vec!['a', 'b', 'c'];
let vec2 = vec.split_off(1);
assert_eq!(vec, ['a']);
assert_eq!(vec2, ['b', 'c']);
```

1.33.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3015-3017)

#### pub fn [resize\_with](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.resize_with)<F>(&mut self, new\_len: [usize](https://doc.rust-lang.org/std/primitive.usize.html), f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")() -> T,

Resizes the `Vec` in-place so that `len` is equal to `new_len`.

If `new_len` is greater than `len`, the `Vec` is extended by the
difference, with each additional slot filled with the result of
calling the closure `f`. The return values from `f` will end up
in the `Vec` in the order they have been generated.

If `new_len` is less than `len`, the `Vec` is simply truncated.

This method uses a closure to create new values on every push. If
you’d rather [`Clone`](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") a given value, use [`Vec::resize`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.resize "method std::vec::Vec::resize"). If you
want to use the [`Default`](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") trait to generate values, you can
pass [`Default::default`](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default "associated function std::default::Default::default") as the second argument.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-13)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-48)Examples

```
let mut vec = vec![1, 2, 3];
vec.resize_with(5, Default::default);
assert_eq!(vec, [1, 2, 3, 0, 0]);

let mut vec = vec![];
let mut p = 1;
vec.resize_with(4, || { p *= 2; p });
assert_eq!(vec, [2, 4, 8, 16]);
```

1.47.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3057-3059)

#### pub fn [leak](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.leak)<'a>(self) -> &'a mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html) where A: 'a,

Consumes and leaks the `Vec`, returning a mutable reference to the contents,
`&'a mut [T]`.

Note that the type `T` must outlive the chosen lifetime `'a`. If the type
has only static references, or none at all, then this may be chosen to be
`'static`.

As of Rust 1.57, this method does not reallocate or shrink the `Vec`,
so the leaked allocation may include unused capacity that is not part
of the returned slice.

This function is mainly useful for data that lives for the remainder of
the program’s life. Dropping the returned reference will cause a memory
leak.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-49)Examples

Simple usage:

```
let x = vec![1, 2, 3];
let static_ref: &'static mut [usize] = x.leak();
static_ref[0] += 1;
assert_eq!(static_ref, &[2, 2, 3]);
```

1.60.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3095)

#### pub fn [spare\_capacity\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.spare_capacity_mut)(&mut self) -> &mut [[MaybeUninit](https://doc.rust-lang.org/std/mem/union.MaybeUninit.html "union std::mem::MaybeUninit")<T>]

Returns the remaining spare capacity of the vector as a slice of
`MaybeUninit<T>`.

The returned slice can be used to fill the vector with data (e.g. by
reading from a file) before marking the data as initialized using the
[`set_len`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.set_len "method std::vec::Vec::set_len") method.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-50)Examples

```
// Allocate vector big enough for 10 elements.
let mut v = Vec::with_capacity(10);

// Fill in the first 3 elements.
let uninit = v.spare_capacity_mut();
uninit[0].write(0);
uninit[1].write(1);
uninit[2].write(2);

// Mark the first 3 elements of the vector as being initialized.
unsafe {
    v.set_len(3);
}

assert_eq!(&v, &[0, 1, 2]);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3160)

#### pub fn [split\_at\_spare\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_at_spare_mut)(&mut self) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[MaybeUninit](https://doc.rust-lang.org/std/mem/union.MaybeUninit.html "union std::mem::MaybeUninit")<T>])

🔬This is a nightly-only experimental API. (`vec_split_at_spare` [#81944](https://github.com/rust-lang/rust/issues/81944))

Returns vector content as a slice of `T`, along with the remaining spare
capacity of the vector as a slice of `MaybeUninit<T>`.

The returned spare capacity slice can be used to fill the vector with data
(e.g. by reading from a file) before marking the data as initialized using
the [`set_len`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.set_len "method std::vec::Vec::set_len") method.

Note that this is a low-level API, which should be used with care for
optimization purposes. If you need to append data to a `Vec`
you can use [`push`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.push "method std::vec::Vec::push"), [`extend`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend "method std::vec::Vec::extend"), [`extend_from_slice`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_from_slice "method std::vec::Vec::extend_from_slice"),
[`extend_from_within`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_from_within "method std::vec::Vec::extend_from_within"), [`insert`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.insert "method std::vec::Vec::insert"), [`append`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.append "method std::vec::Vec::append"), [`resize`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.resize "method std::vec::Vec::resize") or
[`resize_with`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.resize_with "method std::vec::Vec::resize_with"), depending on your exact needs.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-51)Examples

```
#![feature(vec_split_at_spare)]

let mut v = vec![1, 1, 2];

// Reserve additional space big enough for 10 elements.
v.reserve(10);

let (init, uninit) = v.split_at_spare_mut();
let sum = init.iter().copied().sum::<u32>();

// Fill in the next 4 elements.
uninit[0].write(sum);
uninit[1].write(sum * 2);
uninit[2].write(sum * 3);
uninit[3].write(sum * 4);

// Mark the 4 elements of the vector as being initialized.
unsafe {
    let len = v.len();
    v.set_len(len + 4);
}

assert_eq!(&v, &[1, 1, 2, 4, 8, 12, 16]);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3219)

#### pub fn [into\_chunks](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_chunks)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(self) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[[T; N]](https://doc.rust-lang.org/std/primitive.array.html), A>

🔬This is a nightly-only experimental API. (`vec_into_chunks` [#142137](https://github.com/rust-lang/rust/issues/142137))

Groups every `N` elements in the `Vec<T>` into chunks to produce a `Vec<[T; N]>`, dropping
elements in the remainder. `N` must be greater than zero.

If the capacity is not a multiple of the chunk size, the buffer will shrink down to the
nearest multiple with a reallocation or deallocation.

This function can be used to reverse [`Vec::into_flattened`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_flattened "method std::vec::Vec::into_flattened").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-52)Examples

```
#![feature(vec_into_chunks)]

let vec = vec![0, 1, 2, 3, 4, 5, 6, 7];
assert_eq!(vec.into_chunks::<3>(), [[0, 1, 2], [3, 4, 5]]);

let vec = vec![0, 1, 2, 3];
let chunks: Vec<[u8; 10]> = vec.into_chunks();
assert!(chunks.is_empty());

let flat = vec![0; 8 * 8 * 8];
let reshaped: Vec<[[[u8; 8]; 8]; 8]> = flat.into_chunks().into_chunks().into_chunks();
assert_eq!(reshaped.len(), 1);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3249)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Vec%3CT,+A%3E-1)

### impl<T, A> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.5.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3280)

#### pub fn [resize](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.resize)(&mut self, new\_len: [usize](https://doc.rust-lang.org/std/primitive.usize.html), value: T)

Resizes the `Vec` in-place so that `len` is equal to `new_len`.

If `new_len` is greater than `len`, the `Vec` is extended by the
difference, with each additional slot filled with `value`.
If `new_len` is less than `len`, the `Vec` is simply truncated.

This method requires `T` to implement [`Clone`](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),
in order to be able to clone the passed value.
If you need more flexibility (or want to rely on [`Default`](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") instead of
[`Clone`](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone")), use [`Vec::resize_with`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.resize_with "method std::vec::Vec::resize_with").
If you only need to resize to a smaller size, use [`Vec::truncate`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.truncate "method std::vec::Vec::truncate").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-14)Panics

Panics if the new capacity exceeds `isize::MAX` *bytes*.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-53)Examples

```
let mut vec = vec!["hello"];
vec.resize(3, "world");
assert_eq!(vec, ["hello", "world", "world"]);

let mut vec = vec!['a', 'b', 'c', 'd'];
vec.resize(2, '_');
assert_eq!(vec, ['a', 'b']);
```

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3311)

#### pub fn [extend\_from\_slice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_from_slice)(&mut self, other: &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Clones and appends all elements in a slice to the `Vec`.

Iterates over the slice `other`, clones each element, and then appends
it to this `Vec`. The `other` slice is traversed in-order.

Note that this function is the same as [`extend`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend "method std::vec::Vec::extend"),
except that it also works with slice elements that are Clone but not Copy.
If Rust gets specialization this function may be deprecated.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-54)Examples

```
let mut vec = vec![1];
vec.extend_from_slice(&[2, 3, 4]);
assert_eq!(vec, [1, 2, 3, 4]);
```

1.53.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3342-3344)

#### pub fn [extend\_from\_within](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_from_within)<R>(&mut self, src: R) where R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Given a range `src`, clones a slice of elements in that range and appends it to the end.

`src` must be a range that can form a valid subslice of the `Vec`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-15)Panics

Panics if starting index is greater than the end index
or if the index is greater than the length of the vector.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-55)Examples

```
let mut characters = vec!['a', 'b', 'c', 'd', 'e'];
characters.extend_from_within(2..);
assert_eq!(characters, ['a', 'b', 'c', 'd', 'e', 'c', 'd', 'e']);

let mut numbers = vec![0, 1, 2, 3, 4];
numbers.extend_from_within(..2);
assert_eq!(numbers, [0, 1, 2, 3, 4, 0, 1]);

let mut strings = vec![String::from("hello"), String::from("world"), String::from("!")];
strings.extend_from_within(1..=2);
assert_eq!(strings, ["hello", "world", "!", "world", "!"]);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3357)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Vec%3C%5BT;+N%5D,+A%3E)

### impl<T, A, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[[T; N]](https://doc.rust-lang.org/std/primitive.array.html), A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3378)

#### pub fn [into\_flattened](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_flattened)(self) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

Takes a `Vec<[T; N]>` and flattens it into a `Vec<T>`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-16)Panics

Panics if the length of the resulting vector would overflow a `usize`.

This is only possible when flattening a vector of arrays of zero-sized
types, and thus tends to be irrelevant in practice. If
`size_of::<T>() > 0`, this will never panic.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-56)Examples

```
let mut vec = vec![[1, 2, 3], [4, 5, 6], [7, 8, 9]];
assert_eq!(vec.pop(), Some([7, 8, 9]));

let mut flattened = vec.into_flattened();
assert_eq!(flattened.pop(), Some(6));
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3433)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Vec%3CT,+A%3E-2)

### impl<T, A> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3450)

#### pub fn [dedup](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.dedup)(&mut self)

Removes consecutive repeated elements in the vector according to the
[`PartialEq`](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq") trait implementation.

If the vector is sorted, this removes all duplicates.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-57)Examples

```
let mut vec = vec![1, 2, 2, 3, 2];

vec.dedup();

assert_eq!(vec, [1, 2, 3, 2]);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3778)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Vec%3CT,+A%3E-3)

### impl<T, A> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3888-3891)

#### pub fn [splice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.splice)<R, I>( &mut self, range: R, replace\_with: I, ) -> [Splice](https://doc.rust-lang.org/std/vec/struct.Splice.html "struct std::vec::Splice")<'\_, <I as [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")>::[IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter "type std::iter::IntoIterator::IntoIter"), A> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>, I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = T>,

Creates a splicing iterator that replaces the specified range in the vector
with the given `replace_with` iterator and yields the removed items.
`replace_with` does not need to be the same length as `range`.

`range` is removed even if the `Splice` iterator is not consumed before it is dropped.

It is unspecified how many elements are removed from the vector
if the `Splice` value is leaked.

The input iterator `replace_with` is only consumed when the `Splice` value is dropped.

This is optimal if:

* The tail (elements in the vector after `range`) is empty,
* or `replace_with` yields fewer or equal elements than `range`’s length
* or the lower bound of its `size_hint()` is exact.

Otherwise, a temporary vector is allocated and the tail is moved twice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-17)Panics

Panics if the starting point is greater than the end point or if
the end point is greater than the length of the vector.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-58)Examples

```
let mut v = vec![1, 2, 3, 4];
let new = [7, 8, 9];
let u: Vec<_> = v.splice(1..3, new).collect();
assert_eq!(v, [1, 7, 8, 9, 4]);
assert_eq!(u, [2, 3]);
```

Using `splice` to insert new items into a vector efficiently at a specific position
indicated by an empty range:

```
let mut v = vec![1, 5];
let new = [2, 3, 4];
v.splice(1..1, new);
assert_eq!(v, [1, 2, 3, 4, 5]);
```

1.87.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3970-3973)

#### pub fn [extract\_if](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extract_if)<F, R>( &mut self, range: R, filter: F, ) -> [ExtractIf](https://doc.rust-lang.org/std/vec/struct.ExtractIf.html "struct std::vec::ExtractIf")<'\_, T, F, A> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html), R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Creates an iterator which uses a closure to determine if an element in the range should be removed.

If the closure returns `true`, the element is removed from the vector
and yielded. If the closure returns `false`, or panics, the element
remains in the vector and will not be yielded.

Only elements that fall in the provided range are considered for extraction, but any elements
after the range will still have to be moved if any element has been extracted.

If the returned `ExtractIf` is not exhausted, e.g. because it is dropped without iterating
or the iteration short-circuits, then the remaining elements will be retained.
Use [`retain_mut`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.retain_mut "method std::vec::Vec::retain_mut") with a negated predicate if you do not need the returned iterator.

Using this method is equivalent to the following code:

```
let mut i = range.start;
let end_items = vec.len() - range.end;

while i < vec.len() - end_items {
    if some_predicate(&mut vec[i]) {
        let val = vec.remove(i);
        // your code here
    } else {
        i += 1;
    }
}
```

But `extract_if` is easier to use. `extract_if` is also more efficient,
because it can backshift the elements of the array in bulk.

The iterator also lets you mutate the value of each element in the
closure, regardless of whether you choose to keep or remove it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-18)Panics

If `range` is out of bounds.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-59)Examples

Splitting a vector into even and odd values, reusing the original vector:

```
let mut numbers = vec![1, 2, 3, 4, 5, 6, 8, 9, 11, 13, 14, 15];

let evens = numbers.extract_if(.., |x| *x % 2 == 0).collect::<Vec<_>>();
let odds = numbers;

assert_eq!(evens, vec![2, 4, 6, 8, 14]);
assert_eq!(odds, vec![1, 3, 5, 9, 11, 13, 15]);
```

Using the range argument to only process a part of the vector:

```
let mut items = vec![0, 0, 0, 0, 0, 0, 0, 1, 2, 1, 2, 1, 2];
let ones = items.extract_if(7.., |x| *x == 1).collect::<Vec<_>>();
assert_eq!(items, vec![0, 0, 0, 0, 0, 0, 0, 2, 2, 2]);
assert_eq!(ones.len(), 3);
```

## Methods from [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")<Target = [[T]](https://doc.rust-lang.org/std/primitive.slice.html)>[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#deref-methods-%5BT%5D)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#114)

#### pub fn [len](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.len-1)(&self) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Returns the number of elements in the slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-60)Examples

```
let a = [1, 2, 3];
assert_eq!(a.len(), 3);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#134)

#### pub fn [is\_empty](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.is_empty-1)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the slice has a length of 0.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-61)Examples

```
let a = [1, 2, 3];
assert!(!a.is_empty());

let b: &[i32] = &[];
assert!(b.is_empty());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#153)

#### pub fn [first](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.first)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&T](https://doc.rust-lang.org/std/primitive.reference.html)>

Returns the first element of the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-62)Examples

```
let v = [10, 40, 30];
assert_eq!(Some(&10), v.first());

let w: &[i32] = &[];
assert_eq!(None, w.first());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#176)

#### pub fn [first\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.first_mut)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

Returns a mutable reference to the first element of the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-63)Examples

```
let x = &mut [0, 1, 2];

if let Some(first) = x.first_mut() {
    *first = 5;
}
assert_eq!(x, &[5, 1, 2]);

let y: &mut [i32] = &mut [];
assert_eq!(None, y.first_mut());
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#196)

#### pub fn [split\_first](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_first)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<([&T](https://doc.rust-lang.org/std/primitive.reference.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Returns the first and all the rest of the elements of the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-64)Examples

```
let x = &[0, 1, 2];

if let Some((first, elements)) = x.split_first() {
    assert_eq!(first, &0);
    assert_eq!(elements, &[1, 2]);
}
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#218)

#### pub fn [split\_first\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_first_mut)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<([&mut T](https://doc.rust-lang.org/std/primitive.reference.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Returns the first and all the rest of the elements of the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-65)Examples

```
let x = &mut [0, 1, 2];

if let Some((first, elements)) = x.split_first_mut() {
    *first = 3;
    elements[0] = 4;
    elements[1] = 5;
}
assert_eq!(x, &[3, 4, 5]);
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#238)

#### pub fn [split\_last](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_last)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<([&T](https://doc.rust-lang.org/std/primitive.reference.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Returns the last and all the rest of the elements of the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-66)Examples

```
let x = &[0, 1, 2];

if let Some((last, elements)) = x.split_last() {
    assert_eq!(last, &2);
    assert_eq!(elements, &[0, 1]);
}
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#260)

#### pub fn [split\_last\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_last_mut)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<([&mut T](https://doc.rust-lang.org/std/primitive.reference.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Returns the last and all the rest of the elements of the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-67)Examples

```
let x = &mut [0, 1, 2];

if let Some((last, elements)) = x.split_last_mut() {
    *last = 3;
    elements[0] = 4;
    elements[1] = 5;
}
assert_eq!(x, &[4, 5, 3]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#279)

#### pub fn [last](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.last)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&T](https://doc.rust-lang.org/std/primitive.reference.html)>

Returns the last element of the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-68)Examples

```
let v = [10, 40, 30];
assert_eq!(Some(&30), v.last());

let w: &[i32] = &[];
assert_eq!(None, w.last());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#302)

#### pub fn [last\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.last_mut)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

Returns a mutable reference to the last item in the slice, or `None` if it is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-69)Examples

```
let x = &mut [0, 1, 2];

if let Some(last) = x.last_mut() {
    *last = 10;
}
assert_eq!(x, &[0, 1, 10]);

let y: &mut [i32] = &mut [];
assert_eq!(None, y.last_mut());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#325)

#### pub fn [first\_chunk](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.first_chunk)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>

Returns an array reference to the first `N` items in the slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-70)Examples

```
let u = [10, 40, 30];
assert_eq!(Some(&[10, 40]), u.first_chunk::<2>());

let v: &[i32] = &[10];
assert_eq!(None, v.first_chunk::<2>());

let w: &[i32] = &[];
assert_eq!(Some(&[]), w.first_chunk::<0>());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#355)

#### pub fn [first\_chunk\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.first_chunk_mut)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut [[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>

Returns a mutable array reference to the first `N` items in the slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-71)Examples

```
let x = &mut [0, 1, 2];

if let Some(first) = x.first_chunk_mut::<2>() {
    first[0] = 5;
    first[1] = 4;
}
assert_eq!(x, &[5, 4, 2]);

assert_eq!(None, x.first_chunk_mut::<4>());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#385)

#### pub fn [split\_first\_chunk](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_first_chunk)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[[T; N]](https://doc.rust-lang.org/std/primitive.array.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Returns an array reference to the first `N` items in the slice and the remaining slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-72)Examples

```
let x = &[0, 1, 2];

if let Some((first, elements)) = x.split_first_chunk::<2>() {
    assert_eq!(first, &[0, 1]);
    assert_eq!(elements, &[2]);
}

assert_eq!(None, x.split_first_chunk::<4>());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#415-417)

#### pub fn [split\_first\_chunk\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_first_chunk_mut)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>( &mut self, ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&mut [[T; N]](https://doc.rust-lang.org/std/primitive.array.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Returns a mutable array reference to the first `N` items in the slice and the remaining
slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-73)Examples

```
let x = &mut [0, 1, 2];

if let Some((first, elements)) = x.split_first_chunk_mut::<2>() {
    first[0] = 3;
    first[1] = 4;
    elements[0] = 5;
}
assert_eq!(x, &[3, 4, 5]);

assert_eq!(None, x.split_first_chunk_mut::<4>());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#445)

#### pub fn [split\_last\_chunk](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_last_chunk)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[T; N]](https://doc.rust-lang.org/std/primitive.array.html))>

Returns an array reference to the last `N` items in the slice and the remaining slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-74)Examples

```
let x = &[0, 1, 2];

if let Some((elements, last)) = x.split_last_chunk::<2>() {
    assert_eq!(elements, &[0]);
    assert_eq!(last, &[1, 2]);
}

assert_eq!(None, x.split_last_chunk::<4>());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#476-478)

#### pub fn [split\_last\_chunk\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_last_chunk_mut)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>( &mut self, ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T; N]](https://doc.rust-lang.org/std/primitive.array.html))>

Returns a mutable array reference to the last `N` items in the slice and the remaining
slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-75)Examples

```
let x = &mut [0, 1, 2];

if let Some((elements, last)) = x.split_last_chunk_mut::<2>() {
    last[0] = 3;
    last[1] = 4;
    elements[0] = 5;
}
assert_eq!(x, &[5, 3, 4]);

assert_eq!(None, x.split_last_chunk_mut::<4>());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#507)

#### pub fn [last\_chunk](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.last_chunk)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>

Returns an array reference to the last `N` items in the slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-76)Examples

```
let u = [10, 40, 30];
assert_eq!(Some(&[40, 30]), u.last_chunk::<2>());

let v: &[i32] = &[10];
assert_eq!(None, v.last_chunk::<2>());

let w: &[i32] = &[];
assert_eq!(Some(&[]), w.last_chunk::<0>());
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#537)

#### pub fn [last\_chunk\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.last_chunk_mut)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut [[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>

Returns a mutable array reference to the last `N` items in the slice.

If the slice is not at least `N` in length, this will return `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-77)Examples

```
let x = &mut [0, 1, 2];

if let Some(last) = x.last_chunk_mut::<2>() {
    last[0] = 10;
    last[1] = 20;
}
assert_eq!(x, &[0, 10, 20]);

assert_eq!(None, x.last_chunk_mut::<4>());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#570-572)

#### pub fn [get](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.get)<I>(&self, index: I) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>,

Returns a reference to an element or subslice depending on the type of
index.

* If given a position, returns a reference to the element at that
  position or `None` if out of bounds.
* If given a range, returns the subslice corresponding to that range,
  or `None` if out of bounds.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-78)Examples

```
let v = [10, 40, 30];
assert_eq!(Some(&40), v.get(1));
assert_eq!(Some(&[10, 40][..]), v.get(0..2));
assert_eq!(None, v.get(3));
assert_eq!(None, v.get(0..4));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#597-599)

#### pub fn [get\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.get_mut)<I>( &mut self, index: I, ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>,

Returns a mutable reference to an element or subslice depending on the
type of index (see [`get`](https://doc.rust-lang.org/std/primitive.slice.html#method.get "method slice::get")) or `None` if the index is out of bounds.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-79)Examples

```
let x = &mut [0, 1, 2];

if let Some(elem) = x.get_mut(1) {
    *elem = 42;
}
assert_eq!(x, &[0, 42, 2]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#637-639)

#### pub unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.get_unchecked)<I>( &self, index: I, ) -> &<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>,

Returns a reference to an element or subslice, without doing bounds
checking.

For a safe alternative see [`get`](https://doc.rust-lang.org/std/primitive.slice.html#method.get "method slice::get").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-5)Safety

Calling this method with an out-of-bounds index is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*
even if the resulting reference is not used.

You can think of this like `.get(index).unwrap_unchecked()`. It’s UB
to call `.get_unchecked(len)`, even if you immediately convert to a
pointer. And it’s UB to call `.get_unchecked(..len + 1)`,
`.get_unchecked(..=len)`, or similar.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-80)Examples

```
let x = &[1, 2, 4];

unsafe {
    assert_eq!(x.get_unchecked(1), &2);
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#682-684)

#### pub unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.get_unchecked_mut)<I>( &mut self, index: I, ) -> &mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>,

Returns a mutable reference to an element or subslice, without doing
bounds checking.

For a safe alternative see [`get_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.get_mut "method slice::get_mut").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-6)Safety

Calling this method with an out-of-bounds index is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*
even if the resulting reference is not used.

You can think of this like `.get_mut(index).unwrap_unchecked()`. It’s
UB to call `.get_unchecked_mut(len)`, even if you immediately convert
to a pointer. And it’s UB to call `.get_unchecked_mut(..len + 1)`,
`.get_unchecked_mut(..=len)`, or similar.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-81)Examples

```
let x = &mut [1, 2, 4];

unsafe {
    let elem = x.get_unchecked_mut(1);
    *elem = 13;
}
assert_eq!(x, &[1, 13, 4]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#724)

#### pub fn [as\_ptr](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ptr-1)(&self) -> [\*const T](https://doc.rust-lang.org/std/primitive.pointer.html)

Returns a raw pointer to the slice’s buffer.

The caller must ensure that the slice outlives the pointer this
function returns, or else it will end up dangling.

The caller must also ensure that the memory the pointer (non-transitively) points to
is never written to (except inside an `UnsafeCell`) using this pointer or any pointer
derived from it. If you need to mutate the contents of the slice, use [`as_mut_ptr`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_mut_ptr "method slice::as_mut_ptr").

Modifying the container referenced by this slice may cause its buffer
to be reallocated, which would also make any pointers to it invalid.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-82)Examples

```
let x = &[1, 2, 4];
let x_ptr = x.as_ptr();

unsafe {
    for i in 0..x.len() {
        assert_eq!(x.get_unchecked(i), &*x_ptr.add(i));
    }
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#755)

#### pub fn [as\_mut\_ptr](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_ptr-1)(&mut self) -> [\*mut T](https://doc.rust-lang.org/std/primitive.pointer.html)

Returns an unsafe mutable pointer to the slice’s buffer.

The caller must ensure that the slice outlives the pointer this
function returns, or else it will end up dangling.

Modifying the container referenced by this slice may cause its buffer
to be reallocated, which would also make any pointers to it invalid.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-83)Examples

```
let x = &mut [1, 2, 4];
let x_ptr = x.as_mut_ptr();

unsafe {
    for i in 0..x.len() {
        *x_ptr.add(i) += 2;
    }
}
assert_eq!(x, &[3, 4, 6]);
```

1.48.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#791)

#### pub fn [as\_ptr\_range](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ptr_range)(&self) -> [Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[\*const T](https://doc.rust-lang.org/std/primitive.pointer.html)> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns the two raw pointers spanning the slice.

The returned range is half-open, which means that the end pointer
points *one past* the last element of the slice. This way, an empty
slice is represented by two equal pointers, and the difference between
the two pointers represents the size of the slice.

See [`as_ptr`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_ptr "method slice::as_ptr") for warnings on using these pointers. The end pointer
requires extra caution, as it does not point to a valid element in the
slice.

This function is useful for interacting with foreign interfaces which
use two pointers to refer to a range of elements in memory, as is
common in C++.

It can also be useful to check if a pointer to an element refers to an
element of this slice:

```
let a = [1, 2, 3];
let x = &a[1] as *const _;
let y = &5 as *const _;

assert!(a.as_ptr_range().contains(&x));
assert!(!a.as_ptr_range().contains(&y));
```

1.48.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#834)

#### pub fn [as\_mut\_ptr\_range](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_ptr_range)(&mut self) -> [Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[\*mut T](https://doc.rust-lang.org/std/primitive.pointer.html)> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns the two unsafe mutable pointers spanning the slice.

The returned range is half-open, which means that the end pointer
points *one past* the last element of the slice. This way, an empty
slice is represented by two equal pointers, and the difference between
the two pointers represents the size of the slice.

See [`as_mut_ptr`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_mut_ptr "method slice::as_mut_ptr") for warnings on using these pointers. The end
pointer requires extra caution, as it does not point to a valid element
in the slice.

This function is useful for interacting with foreign interfaces which
use two pointers to refer to a range of elements in memory, as is
common in C++.

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#847)

#### pub fn [as\_array](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_array)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>

🔬This is a nightly-only experimental API. (`slice_as_array` [#133508](https://github.com/rust-lang/rust/issues/133508))

Gets a reference to the underlying array.

If `N` is not exactly equal to the length of `self`, then this method returns `None`.

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#865)

#### pub fn [as\_mut\_array](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut_array)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut [[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>

🔬This is a nightly-only experimental API. (`slice_as_array` [#133508](https://github.com/rust-lang/rust/issues/133508))

Gets a mutable reference to the slice’s underlying array.

If `N` is not exactly equal to the length of `self`, then this method returns `None`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#901)

#### pub fn [swap](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.swap)(&mut self, a: [usize](https://doc.rust-lang.org/std/primitive.usize.html), b: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Swaps two elements in the slice.

If `a` equals to `b`, it’s guaranteed that elements won’t change value.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#arguments)Arguments

* a - The index of the first element
* b - The index of the second element

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-19)Panics

Panics if `a` or `b` are out of bounds.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-84)Examples

```
let mut v = ["a", "b", "c", "d", "e"];
v.swap(2, 4);
assert!(v == ["a", "b", "e", "d", "c"]);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#944)

#### pub unsafe fn [swap\_unchecked](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.swap_unchecked)(&mut self, a: [usize](https://doc.rust-lang.org/std/primitive.usize.html), b: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`slice_swap_unchecked` [#88539](https://github.com/rust-lang/rust/issues/88539))

Swaps two elements in the slice, without doing bounds checking.

For a safe alternative see [`swap`](https://doc.rust-lang.org/std/primitive.slice.html#method.swap "method slice::swap").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#arguments-1)Arguments

* a - The index of the first element
* b - The index of the second element

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-7)Safety

Calling this method with an out-of-bounds index is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*.
The caller has to ensure that `a < self.len()` and `b < self.len()`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-85)Examples

```
#![feature(slice_swap_unchecked)]

let mut v = ["a", "b", "c", "d"];
// SAFETY: we know that 1 and 3 are both indices of the slice
unsafe { v.swap_unchecked(1, 3) };
assert!(v == ["a", "d", "c", "b"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#974)

#### pub fn [reverse](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.reverse)(&mut self)

Reverses the order of elements in the slice, in place.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-86)Examples

```
let mut v = [1, 2, 3];
v.reverse();
assert!(v == [3, 2, 1]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1036)

#### pub fn [iter](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.iter)(&self) -> [Iter](https://doc.rust-lang.org/std/slice/struct.Iter.html "struct std::slice::Iter")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over the slice.

The iterator yields all items from start to end.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-87)Examples

```
let x = &[1, 2, 4];
let mut iterator = x.iter();

assert_eq!(iterator.next(), Some(&1));
assert_eq!(iterator.next(), Some(&2));
assert_eq!(iterator.next(), Some(&4));
assert_eq!(iterator.next(), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1056)

#### pub fn [iter\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.iter_mut)(&mut self) -> [IterMut](https://doc.rust-lang.org/std/slice/struct.IterMut.html "struct std::slice::IterMut")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator that allows modifying each value.

The iterator yields all items from start to end.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-88)Examples

```
let x = &mut [1, 2, 4];
for elem in x.iter_mut() {
    *elem += 2;
}
assert_eq!(x, &[3, 4, 6]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1111)

#### pub fn [windows](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.windows)(&self, size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Windows](https://doc.rust-lang.org/std/slice/struct.Windows.html "struct std::slice::Windows")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over all contiguous windows of length
`size`. The windows overlap. If the slice is shorter than
`size`, the iterator returns no values.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-20)Panics

Panics if `size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-89)Examples

```
let slice = ['l', 'o', 'r', 'e', 'm'];
let mut iter = slice.windows(3);
assert_eq!(iter.next().unwrap(), &['l', 'o', 'r']);
assert_eq!(iter.next().unwrap(), &['o', 'r', 'e']);
assert_eq!(iter.next().unwrap(), &['r', 'e', 'm']);
assert!(iter.next().is_none());
```

If the slice is shorter than `size`:

```
let slice = ['f', 'o', 'o'];
let mut iter = slice.windows(4);
assert!(iter.next().is_none());
```

Because the [Iterator](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator") trait cannot represent the required lifetimes,
there is no `windows_mut` analog to `windows`;
`[0,1,2].windows_mut(2).collect()` would violate [the rules of references](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#the-rules-of-references)
(though a [LendingIterator](https://blog.rust-lang.org/2022/10/28/gats-stabilization.html) analog is possible). You can sometimes use
[`Cell::as_slice_of_cells`](https://doc.rust-lang.org/std/cell/struct.Cell.html#method.as_slice_of_cells "method std::cell::Cell::as_slice_of_cells") in
conjunction with `windows` instead:

```
use std::cell::Cell;

let mut array = ['R', 'u', 's', 't', ' ', '2', '0', '1', '5'];
let slice = &mut array[..];
let slice_of_cells: &[Cell<char>] = Cell::from_mut(slice).as_slice_of_cells();
for w in slice_of_cells.windows(3) {
    Cell::swap(&w[0], &w[2]);
}
assert_eq!(array, ['s', 't', ' ', '2', '0', '1', '5', 'u', 'R']);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1151)

#### pub fn [chunks](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.chunks)(&self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Chunks](https://doc.rust-lang.org/std/slice/struct.Chunks.html "struct std::slice::Chunks")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the
beginning of the slice.

The chunks are slices and do not overlap. If `chunk_size` does not divide the length of the
slice, then the last chunk will not have length `chunk_size`.

See [`chunks_exact`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_exact "method slice::chunks_exact") for a variant of this iterator that returns chunks of always exactly
`chunk_size` elements, and [`rchunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks "method slice::rchunks") for the same iterator but starting at the end of the
slice.

If your `chunk_size` is a constant, consider using [`as_chunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_chunks "method slice::as_chunks") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-21)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-90)Examples

```
let slice = ['l', 'o', 'r', 'e', 'm'];
let mut iter = slice.chunks(2);
assert_eq!(iter.next().unwrap(), &['l', 'o']);
assert_eq!(iter.next().unwrap(), &['r', 'e']);
assert_eq!(iter.next().unwrap(), &['m']);
assert!(iter.next().is_none());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1195)

#### pub fn [chunks\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.chunks_mut)(&mut self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [ChunksMut](https://doc.rust-lang.org/std/slice/struct.ChunksMut.html "struct std::slice::ChunksMut")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the
beginning of the slice.

The chunks are mutable slices, and do not overlap. If `chunk_size` does not divide the
length of the slice, then the last chunk will not have length `chunk_size`.

See [`chunks_exact_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_exact_mut "method slice::chunks_exact_mut") for a variant of this iterator that returns chunks of always
exactly `chunk_size` elements, and [`rchunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks_mut "method slice::rchunks_mut") for the same iterator but starting at
the end of the slice.

If your `chunk_size` is a constant, consider using [`as_chunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_chunks_mut "method slice::as_chunks_mut") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-22)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-91)Examples

```
let v = &mut [0, 0, 0, 0, 0];
let mut count = 1;

for chunk in v.chunks_mut(2) {
    for elem in chunk.iter_mut() {
        *elem += count;
    }
    count += 1;
}
assert_eq!(v, &[1, 1, 2, 2, 3]);
```

1.31.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1238)

#### pub fn [chunks\_exact](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.chunks_exact)(&self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [ChunksExact](https://doc.rust-lang.org/std/slice/struct.ChunksExact.html "struct std::slice::ChunksExact")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the
beginning of the slice.

The chunks are slices and do not overlap. If `chunk_size` does not divide the length of the
slice, then the last up to `chunk_size-1` elements will be omitted and can be retrieved
from the `remainder` function of the iterator.

Due to each chunk having exactly `chunk_size` elements, the compiler can often optimize the
resulting code better than in the case of [`chunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks "method slice::chunks").

See [`chunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks "method slice::chunks") for a variant of this iterator that also returns the remainder as a smaller
chunk, and [`rchunks_exact`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks_exact "method slice::rchunks_exact") for the same iterator but starting at the end of the slice.

If your `chunk_size` is a constant, consider using [`as_chunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_chunks "method slice::as_chunks") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-23)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-92)Examples

```
let slice = ['l', 'o', 'r', 'e', 'm'];
let mut iter = slice.chunks_exact(2);
assert_eq!(iter.next().unwrap(), &['l', 'o']);
assert_eq!(iter.next().unwrap(), &['r', 'e']);
assert!(iter.next().is_none());
assert_eq!(iter.remainder(), &['m']);
```

1.31.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1286)

#### pub fn [chunks\_exact\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.chunks_exact_mut)(&mut self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [ChunksExactMut](https://doc.rust-lang.org/std/slice/struct.ChunksExactMut.html "struct std::slice::ChunksExactMut")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the
beginning of the slice.

The chunks are mutable slices, and do not overlap. If `chunk_size` does not divide the
length of the slice, then the last up to `chunk_size-1` elements will be omitted and can be
retrieved from the `into_remainder` function of the iterator.

Due to each chunk having exactly `chunk_size` elements, the compiler can often optimize the
resulting code better than in the case of [`chunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_mut "method slice::chunks_mut").

See [`chunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_mut "method slice::chunks_mut") for a variant of this iterator that also returns the remainder as a
smaller chunk, and [`rchunks_exact_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks_exact_mut "method slice::rchunks_exact_mut") for the same iterator but starting at the end of
the slice.

If your `chunk_size` is a constant, consider using [`as_chunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_chunks_mut "method slice::as_chunks_mut") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-24)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-93)Examples

```
let v = &mut [0, 0, 0, 0, 0];
let mut count = 1;

for chunk in v.chunks_exact_mut(2) {
    for elem in chunk.iter_mut() {
        *elem += count;
    }
    count += 1;
}
assert_eq!(v, &[1, 1, 2, 2, 0]);
```

1.88.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1334)

#### pub unsafe fn [as\_chunks\_unchecked](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_chunks_unchecked)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> &[[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)]

Splits the slice into a slice of `N`-element arrays,
assuming that there’s no remainder.

This is the inverse operation to [`as_flattened`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_flattened "method slice::as_flattened").

As this is `unsafe`, consider whether you could use [`as_chunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_chunks "method slice::as_chunks") or
[`as_rchunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_rchunks "method slice::as_rchunks") instead, perhaps via something like
`if let (chunks, []) = slice.as_chunks()` or
`let (chunks, []) = slice.as_chunks() else { unreachable!() };`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-8)Safety

This may only be called when

* The slice splits exactly into `N`-element chunks (aka `self.len() % N == 0`).
* `N != 0`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-94)Examples

```
let slice: &[char] = &['l', 'o', 'r', 'e', 'm', '!'];
let chunks: &[[char; 1]] =
    // SAFETY: 1-element chunks never have remainder
    unsafe { slice.as_chunks_unchecked() };
assert_eq!(chunks, &[['l'], ['o'], ['r'], ['e'], ['m'], ['!']]);
let chunks: &[[char; 3]] =
    // SAFETY: The slice length (6) is a multiple of 3
    unsafe { slice.as_chunks_unchecked() };
assert_eq!(chunks, &[['l', 'o', 'r'], ['e', 'm', '!']]);

// These would be unsound:
// let chunks: &[[_; 5]] = slice.as_chunks_unchecked() // The slice length is not a multiple of 5
// let chunks: &[[_; 0]] = slice.as_chunks_unchecked() // Zero-length chunks are never allowed
```

1.88.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1392)

#### pub fn [as\_chunks](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_chunks)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> (&[[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)], &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Splits the slice into a slice of `N`-element arrays,
starting at the beginning of the slice,
and a remainder slice with length strictly less than `N`.

The remainder is meaningful in the division sense. Given
`let (chunks, remainder) = slice.as_chunks()`, then:

* `chunks.len()` equals `slice.len() / N`,
* `remainder.len()` equals `slice.len() % N`, and
* `slice.len()` equals `chunks.len() * N + remainder.len()`.

You can flatten the chunks back into a slice-of-`T` with [`as_flattened`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_flattened "method slice::as_flattened").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-25)Panics

Panics if `N` is zero.

Note that this check is against a const generic parameter, not a runtime
value, and thus a particular monomorphization will either always panic
or it will never panic.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-95)Examples

```
let slice = ['l', 'o', 'r', 'e', 'm'];
let (chunks, remainder) = slice.as_chunks();
assert_eq!(chunks, &[['l', 'o'], ['r', 'e']]);
assert_eq!(remainder, &['m']);
```

If you expect the slice to be an exact multiple, you can combine
`let`-`else` with an empty slice pattern:

```
let slice = ['R', 'u', 's', 't'];
let (chunks, []) = slice.as_chunks::<2>() else {
    panic!("slice didn't have even length")
};
assert_eq!(chunks, &[['R', 'u'], ['s', 't']]);
```

1.88.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1439)

#### pub fn [as\_rchunks](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_rchunks)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> (&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)])

Splits the slice into a slice of `N`-element arrays,
starting at the end of the slice,
and a remainder slice with length strictly less than `N`.

The remainder is meaningful in the division sense. Given
`let (remainder, chunks) = slice.as_rchunks()`, then:

* `remainder.len()` equals `slice.len() % N`,
* `chunks.len()` equals `slice.len() / N`, and
* `slice.len()` equals `chunks.len() * N + remainder.len()`.

You can flatten the chunks back into a slice-of-`T` with [`as_flattened`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_flattened "method slice::as_flattened").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-26)Panics

Panics if `N` is zero.

Note that this check is against a const generic parameter, not a runtime
value, and thus a particular monomorphization will either always panic
or it will never panic.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-96)Examples

```
let slice = ['l', 'o', 'r', 'e', 'm'];
let (remainder, chunks) = slice.as_rchunks();
assert_eq!(remainder, &['l']);
assert_eq!(chunks, &[['o', 'r'], ['e', 'm']]);
```

1.88.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1494)

#### pub unsafe fn [as\_chunks\_unchecked\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_chunks_unchecked_mut)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>( &mut self, ) -> &mut [[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)]

Splits the slice into a slice of `N`-element arrays,
assuming that there’s no remainder.

This is the inverse operation to [`as_flattened_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_flattened_mut "method slice::as_flattened_mut").

As this is `unsafe`, consider whether you could use [`as_chunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_chunks_mut "method slice::as_chunks_mut") or
[`as_rchunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_rchunks_mut "method slice::as_rchunks_mut") instead, perhaps via something like
`if let (chunks, []) = slice.as_chunks_mut()` or
`let (chunks, []) = slice.as_chunks_mut() else { unreachable!() };`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-9)Safety

This may only be called when

* The slice splits exactly into `N`-element chunks (aka `self.len() % N == 0`).
* `N != 0`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-97)Examples

```
let slice: &mut [char] = &mut ['l', 'o', 'r', 'e', 'm', '!'];
let chunks: &mut [[char; 1]] =
    // SAFETY: 1-element chunks never have remainder
    unsafe { slice.as_chunks_unchecked_mut() };
chunks[0] = ['L'];
assert_eq!(chunks, &[['L'], ['o'], ['r'], ['e'], ['m'], ['!']]);
let chunks: &mut [[char; 3]] =
    // SAFETY: The slice length (6) is a multiple of 3
    unsafe { slice.as_chunks_unchecked_mut() };
chunks[1] = ['a', 'x', '?'];
assert_eq!(slice, &['L', 'o', 'r', 'a', 'x', '?']);

// These would be unsound:
// let chunks: &[[_; 5]] = slice.as_chunks_unchecked_mut() // The slice length is not a multiple of 5
// let chunks: &[[_; 0]] = slice.as_chunks_unchecked_mut() // Zero-length chunks are never allowed
```

1.88.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1548)

#### pub fn [as\_chunks\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_chunks_mut)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&mut self) -> (&mut [[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)], &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Splits the slice into a slice of `N`-element arrays,
starting at the beginning of the slice,
and a remainder slice with length strictly less than `N`.

The remainder is meaningful in the division sense. Given
`let (chunks, remainder) = slice.as_chunks_mut()`, then:

* `chunks.len()` equals `slice.len() / N`,
* `remainder.len()` equals `slice.len() % N`, and
* `slice.len()` equals `chunks.len() * N + remainder.len()`.

You can flatten the chunks back into a slice-of-`T` with [`as_flattened_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_flattened_mut "method slice::as_flattened_mut").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-27)Panics

Panics if `N` is zero.

Note that this check is against a const generic parameter, not a runtime
value, and thus a particular monomorphization will either always panic
or it will never panic.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-98)Examples

```
let v = &mut [0, 0, 0, 0, 0];
let mut count = 1;

let (chunks, remainder) = v.as_chunks_mut();
remainder[0] = 9;
for chunk in chunks {
    *chunk = [count; 2];
    count += 1;
}
assert_eq!(v, &[1, 1, 2, 2, 9]);
```

1.88.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1601)

#### pub fn [as\_rchunks\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_rchunks_mut)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&mut self) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)])

Splits the slice into a slice of `N`-element arrays,
starting at the end of the slice,
and a remainder slice with length strictly less than `N`.

The remainder is meaningful in the division sense. Given
`let (remainder, chunks) = slice.as_rchunks_mut()`, then:

* `remainder.len()` equals `slice.len() % N`,
* `chunks.len()` equals `slice.len() / N`, and
* `slice.len()` equals `chunks.len() * N + remainder.len()`.

You can flatten the chunks back into a slice-of-`T` with [`as_flattened_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_flattened_mut "method slice::as_flattened_mut").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-28)Panics

Panics if `N` is zero.

Note that this check is against a const generic parameter, not a runtime
value, and thus a particular monomorphization will either always panic
or it will never panic.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-99)Examples

```
let v = &mut [0, 0, 0, 0, 0];
let mut count = 1;

let (remainder, chunks) = v.as_rchunks_mut();
remainder[0] = 9;
for chunk in chunks {
    *chunk = [count; 2];
    count += 1;
}
assert_eq!(v, &[9, 1, 1, 2, 2]);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1640)

#### pub fn [array\_windows](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.array_windows)<const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> [ArrayWindows](https://doc.rust-lang.org/std/slice/struct.ArrayWindows.html "struct std::slice::ArrayWindows")<'\_, T, N> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

🔬This is a nightly-only experimental API. (`array_windows` [#75027](https://github.com/rust-lang/rust/issues/75027))

Returns an iterator over overlapping windows of `N` elements of a slice,
starting at the beginning of the slice.

This is the const generic equivalent of [`windows`](https://doc.rust-lang.org/std/primitive.slice.html#method.windows "method slice::windows").

If `N` is greater than the size of the slice, it will return no windows.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-29)Panics

Panics if `N` is zero. This check will most probably get changed to a compile time
error before this method gets stabilized.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-100)Examples

```
#![feature(array_windows)]
let slice = [0, 1, 2, 3];
let mut iter = slice.array_windows();
assert_eq!(iter.next().unwrap(), &[0, 1]);
assert_eq!(iter.next().unwrap(), &[1, 2]);
assert_eq!(iter.next().unwrap(), &[2, 3]);
assert!(iter.next().is_none());
```

1.31.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1680)

#### pub fn [rchunks](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rchunks)(&self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [RChunks](https://doc.rust-lang.org/std/slice/struct.RChunks.html "struct std::slice::RChunks")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the end
of the slice.

The chunks are slices and do not overlap. If `chunk_size` does not divide the length of the
slice, then the last chunk will not have length `chunk_size`.

See [`rchunks_exact`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks_exact "method slice::rchunks_exact") for a variant of this iterator that returns chunks of always exactly
`chunk_size` elements, and [`chunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks "method slice::chunks") for the same iterator but starting at the beginning
of the slice.

If your `chunk_size` is a constant, consider using [`as_rchunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_rchunks "method slice::as_rchunks") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-30)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-101)Examples

```
let slice = ['l', 'o', 'r', 'e', 'm'];
let mut iter = slice.rchunks(2);
assert_eq!(iter.next().unwrap(), &['e', 'm']);
assert_eq!(iter.next().unwrap(), &['o', 'r']);
assert_eq!(iter.next().unwrap(), &['l']);
assert!(iter.next().is_none());
```

1.31.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1724)

#### pub fn [rchunks\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rchunks_mut)(&mut self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [RChunksMut](https://doc.rust-lang.org/std/slice/struct.RChunksMut.html "struct std::slice::RChunksMut")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the end
of the slice.

The chunks are mutable slices, and do not overlap. If `chunk_size` does not divide the
length of the slice, then the last chunk will not have length `chunk_size`.

See [`rchunks_exact_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks_exact_mut "method slice::rchunks_exact_mut") for a variant of this iterator that returns chunks of always
exactly `chunk_size` elements, and [`chunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_mut "method slice::chunks_mut") for the same iterator but starting at the
beginning of the slice.

If your `chunk_size` is a constant, consider using [`as_rchunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_rchunks_mut "method slice::as_rchunks_mut") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-31)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-102)Examples

```
let v = &mut [0, 0, 0, 0, 0];
let mut count = 1;

for chunk in v.rchunks_mut(2) {
    for elem in chunk.iter_mut() {
        *elem += count;
    }
    count += 1;
}
assert_eq!(v, &[3, 2, 2, 1, 1]);
```

1.31.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1769)

#### pub fn [rchunks\_exact](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rchunks_exact)(&self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [RChunksExact](https://doc.rust-lang.org/std/slice/struct.RChunksExact.html "struct std::slice::RChunksExact")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the
end of the slice.

The chunks are slices and do not overlap. If `chunk_size` does not divide the length of the
slice, then the last up to `chunk_size-1` elements will be omitted and can be retrieved
from the `remainder` function of the iterator.

Due to each chunk having exactly `chunk_size` elements, the compiler can often optimize the
resulting code better than in the case of [`rchunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks "method slice::rchunks").

See [`rchunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks "method slice::rchunks") for a variant of this iterator that also returns the remainder as a smaller
chunk, and [`chunks_exact`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_exact "method slice::chunks_exact") for the same iterator but starting at the beginning of the
slice.

If your `chunk_size` is a constant, consider using [`as_rchunks`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_rchunks "method slice::as_rchunks") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-32)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-103)Examples

```
let slice = ['l', 'o', 'r', 'e', 'm'];
let mut iter = slice.rchunks_exact(2);
assert_eq!(iter.next().unwrap(), &['e', 'm']);
assert_eq!(iter.next().unwrap(), &['o', 'r']);
assert!(iter.next().is_none());
assert_eq!(iter.remainder(), &['l']);
```

1.31.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1818)

#### pub fn [rchunks\_exact\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rchunks_exact_mut)(&mut self, chunk\_size: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [RChunksExactMut](https://doc.rust-lang.org/std/slice/struct.RChunksExactMut.html "struct std::slice::RChunksExactMut")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Returns an iterator over `chunk_size` elements of the slice at a time, starting at the end
of the slice.

The chunks are mutable slices, and do not overlap. If `chunk_size` does not divide the
length of the slice, then the last up to `chunk_size-1` elements will be omitted and can be
retrieved from the `into_remainder` function of the iterator.

Due to each chunk having exactly `chunk_size` elements, the compiler can often optimize the
resulting code better than in the case of [`chunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_mut "method slice::chunks_mut").

See [`rchunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.rchunks_mut "method slice::rchunks_mut") for a variant of this iterator that also returns the remainder as a
smaller chunk, and [`chunks_exact_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.chunks_exact_mut "method slice::chunks_exact_mut") for the same iterator but starting at the beginning
of the slice.

If your `chunk_size` is a constant, consider using [`as_rchunks_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_rchunks_mut "method slice::as_rchunks_mut") instead, which will
give references to arrays of exactly that length, rather than slices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-33)Panics

Panics if `chunk_size` is zero.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-104)Examples

```
let v = &mut [0, 0, 0, 0, 0];
let mut count = 1;

for chunk in v.rchunks_exact_mut(2) {
    for elem in chunk.iter_mut() {
        *elem += count;
    }
    count += 1;
}
assert_eq!(v, &[0, 2, 2, 1, 1]);
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1858-1860)

#### pub fn [chunk\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.chunk_by)<F>(&self, pred: F) -> [ChunkBy](https://doc.rust-lang.org/std/slice/struct.ChunkBy.html "struct std::slice::ChunkBy")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html), [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over the slice producing non-overlapping runs
of elements using the predicate to separate them.

The predicate is called for every pair of consecutive elements,
meaning that it is called on `slice[0]` and `slice[1]`,
followed by `slice[1]` and `slice[2]`, and so on.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-105)Examples

```
let slice = &[1, 1, 1, 3, 3, 2, 2, 2];

let mut iter = slice.chunk_by(|a, b| a == b);

assert_eq!(iter.next(), Some(&[1, 1, 1][..]));
assert_eq!(iter.next(), Some(&[3, 3][..]));
assert_eq!(iter.next(), Some(&[2, 2, 2][..]));
assert_eq!(iter.next(), None);
```

This method can be used to extract the sorted subslices:

```
let slice = &[1, 1, 2, 3, 2, 3, 2, 3, 4];

let mut iter = slice.chunk_by(|a, b| a <= b);

assert_eq!(iter.next(), Some(&[1, 1, 2, 3][..]));
assert_eq!(iter.next(), Some(&[2, 3][..]));
assert_eq!(iter.next(), Some(&[2, 3, 4][..]));
assert_eq!(iter.next(), None);
```

1.77.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1900-1902)

#### pub fn [chunk\_by\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.chunk_by_mut)<F>(&mut self, pred: F) -> [ChunkByMut](https://doc.rust-lang.org/std/slice/struct.ChunkByMut.html "struct std::slice::ChunkByMut")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html), [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over the slice producing non-overlapping mutable
runs of elements using the predicate to separate them.

The predicate is called for every pair of consecutive elements,
meaning that it is called on `slice[0]` and `slice[1]`,
followed by `slice[1]` and `slice[2]`, and so on.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-106)Examples

```
let slice = &mut [1, 1, 1, 3, 3, 2, 2, 2];

let mut iter = slice.chunk_by_mut(|a, b| a == b);

assert_eq!(iter.next(), Some(&mut [1, 1, 1][..]));
assert_eq!(iter.next(), Some(&mut [3, 3][..]));
assert_eq!(iter.next(), Some(&mut [2, 2, 2][..]));
assert_eq!(iter.next(), None);
```

This method can be used to extract the sorted subslices:

```
let slice = &mut [1, 1, 2, 3, 2, 3, 2, 3, 4];

let mut iter = slice.chunk_by_mut(|a, b| a <= b);

assert_eq!(iter.next(), Some(&mut [1, 1, 2, 3][..]));
assert_eq!(iter.next(), Some(&mut [2, 3][..]));
assert_eq!(iter.next(), Some(&mut [2, 3, 4][..]));
assert_eq!(iter.next(), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1946)

#### pub fn [split\_at](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_at)(&self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> (&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Divides one slice into two at an index.

The first will contain all indices from `[0, mid)` (excluding
the index `mid` itself) and the second will contain all
indices from `[mid, len)` (excluding the index `len` itself).

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-34)Panics

Panics if `mid > len`. For a non-panicking alternative see
[`split_at_checked`](https://doc.rust-lang.org/std/primitive.slice.html#method.split_at_checked "method slice::split_at_checked").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-107)Examples

```
let v = ['a', 'b', 'c'];

{
   let (left, right) = v.split_at(0);
   assert_eq!(left, []);
   assert_eq!(right, ['a', 'b', 'c']);
}

{
    let (left, right) = v.split_at(2);
    assert_eq!(left, ['a', 'b']);
    assert_eq!(right, ['c']);
}

{
    let (left, right) = v.split_at(3);
    assert_eq!(left, ['a', 'b', 'c']);
    assert_eq!(right, []);
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#1980)

#### pub fn [split\_at\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_at_mut)(&mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Divides one mutable slice into two at an index.

The first will contain all indices from `[0, mid)` (excluding
the index `mid` itself) and the second will contain all
indices from `[mid, len)` (excluding the index `len` itself).

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-35)Panics

Panics if `mid > len`. For a non-panicking alternative see
[`split_at_mut_checked`](https://doc.rust-lang.org/std/primitive.slice.html#method.split_at_mut_checked "method slice::split_at_mut_checked").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-108)Examples

```
let mut v = [1, 0, 3, 0, 5, 6];
let (left, right) = v.split_at_mut(2);
assert_eq!(left, [1, 0]);
assert_eq!(right, [3, 0, 5, 6]);
left[1] = 2;
right[1] = 4;
assert_eq!(v, [1, 2, 3, 4, 5, 6]);
```

1.79.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2032)

#### pub unsafe fn [split\_at\_unchecked](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_at_unchecked)(&self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> (&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Divides one slice into two at an index, without doing bounds checking.

The first will contain all indices from `[0, mid)` (excluding
the index `mid` itself) and the second will contain all
indices from `[mid, len)` (excluding the index `len` itself).

For a safe alternative see [`split_at`](https://doc.rust-lang.org/std/primitive.slice.html#method.split_at "method slice::split_at").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-10)Safety

Calling this method with an out-of-bounds index is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*
even if the resulting reference is not used. The caller has to ensure that
`0 <= mid <= self.len()`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-109)Examples

```
let v = ['a', 'b', 'c'];

unsafe {
   let (left, right) = v.split_at_unchecked(0);
   assert_eq!(left, []);
   assert_eq!(right, ['a', 'b', 'c']);
}

unsafe {
    let (left, right) = v.split_at_unchecked(2);
    assert_eq!(left, ['a', 'b']);
    assert_eq!(right, ['c']);
}

unsafe {
    let (left, right) = v.split_at_unchecked(3);
    assert_eq!(left, ['a', 'b', 'c']);
    assert_eq!(right, []);
}
```

1.79.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2086)

#### pub unsafe fn [split\_at\_mut\_unchecked](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_at_mut_unchecked)( &mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Divides one mutable slice into two at an index, without doing bounds checking.

The first will contain all indices from `[0, mid)` (excluding
the index `mid` itself) and the second will contain all
indices from `[mid, len)` (excluding the index `len` itself).

For a safe alternative see [`split_at_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.split_at_mut "method slice::split_at_mut").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-11)Safety

Calling this method with an out-of-bounds index is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*
even if the resulting reference is not used. The caller has to ensure that
`0 <= mid <= self.len()`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-110)Examples

```
let mut v = [1, 0, 3, 0, 5, 6];
// scoped to restrict the lifetime of the borrows
unsafe {
    let (left, right) = v.split_at_mut_unchecked(2);
    assert_eq!(left, [1, 0]);
    assert_eq!(right, [3, 0, 5, 6]);
    left[1] = 2;
    right[1] = 4;
}
assert_eq!(v, [1, 2, 3, 4, 5, 6]);
```

1.80.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2147)

#### pub fn [split\_at\_checked](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_at_checked)(&self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Divides one slice into two at an index, returning `None` if the slice is
too short.

If `mid ≤ len` returns a pair of slices where the first will contain all
indices from `[0, mid)` (excluding the index `mid` itself) and the
second will contain all indices from `[mid, len)` (excluding the index
`len` itself).

Otherwise, if `mid > len`, returns `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-111)Examples

```
let v = [1, -2, 3, -4, 5, -6];

{
   let (left, right) = v.split_at_checked(0).unwrap();
   assert_eq!(left, []);
   assert_eq!(right, [1, -2, 3, -4, 5, -6]);
}

{
    let (left, right) = v.split_at_checked(2).unwrap();
    assert_eq!(left, [1, -2]);
    assert_eq!(right, [3, -4, 5, -6]);
}

{
    let (left, right) = v.split_at_checked(6).unwrap();
    assert_eq!(left, [1, -2, 3, -4, 5, -6]);
    assert_eq!(right, []);
}

assert_eq!(None, v.split_at_checked(7));
```

1.80.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2186)

#### pub fn [split\_at\_mut\_checked](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_at_mut_checked)( &mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))>

Divides one mutable slice into two at an index, returning `None` if the
slice is too short.

If `mid ≤ len` returns a pair of slices where the first will contain all
indices from `[0, mid)` (excluding the index `mid` itself) and the
second will contain all indices from `[mid, len)` (excluding the index
`len` itself).

Otherwise, if `mid > len`, returns `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-112)Examples

```
let mut v = [1, 0, 3, 0, 5, 6];

if let Some((left, right)) = v.split_at_mut_checked(2) {
    assert_eq!(left, [1, 0]);
    assert_eq!(right, [3, 0, 5, 6]);
    left[1] = 2;
    right[1] = 4;
}
assert_eq!(v, [1, 2, 3, 4, 5, 6]);

assert_eq!(None, v.split_at_mut_checked(7));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2238-2240)

#### pub fn [split](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split)<F>(&self, pred: F) -> [Split](https://doc.rust-lang.org/std/slice/struct.Split.html "struct std::slice::Split")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over subslices separated by elements that match
`pred`. The matched element is not contained in the subslices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-113)Examples

```
let slice = [10, 40, 33, 20];
let mut iter = slice.split(|num| num % 3 == 0);

assert_eq!(iter.next().unwrap(), &[10, 40]);
assert_eq!(iter.next().unwrap(), &[20]);
assert!(iter.next().is_none());
```

If the first element is matched, an empty slice will be the first item
returned by the iterator. Similarly, if the last element in the slice
is matched, an empty slice will be the last item returned by the
iterator:

```
let slice = [10, 40, 33];
let mut iter = slice.split(|num| num % 3 == 0);

assert_eq!(iter.next().unwrap(), &[10, 40]);
assert_eq!(iter.next().unwrap(), &[]);
assert!(iter.next().is_none());
```

If two matched elements are directly adjacent, an empty slice will be
present between them:

```
let slice = [10, 6, 33, 20];
let mut iter = slice.split(|num| num % 3 == 0);

assert_eq!(iter.next().unwrap(), &[10]);
assert_eq!(iter.next().unwrap(), &[]);
assert_eq!(iter.next().unwrap(), &[20]);
assert!(iter.next().is_none());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2260-2262)

#### pub fn [split\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_mut)<F>(&mut self, pred: F) -> [SplitMut](https://doc.rust-lang.org/std/slice/struct.SplitMut.html "struct std::slice::SplitMut")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over mutable subslices separated by elements that
match `pred`. The matched element is not contained in the subslices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-114)Examples

```
let mut v = [10, 40, 30, 20, 60, 50];

for group in v.split_mut(|num| *num % 3 == 0) {
    group[0] = 1;
}
assert_eq!(v, [1, 40, 30, 1, 60, 1]);
```

1.51.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2296-2298)

#### pub fn [split\_inclusive](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_inclusive)<F>(&self, pred: F) -> [SplitInclusive](https://doc.rust-lang.org/std/slice/struct.SplitInclusive.html "struct std::slice::SplitInclusive")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over subslices separated by elements that match
`pred`. The matched element is contained in the end of the previous
subslice as a terminator.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-115)Examples

```
let slice = [10, 40, 33, 20];
let mut iter = slice.split_inclusive(|num| num % 3 == 0);

assert_eq!(iter.next().unwrap(), &[10, 40, 33]);
assert_eq!(iter.next().unwrap(), &[20]);
assert!(iter.next().is_none());
```

If the last element of the slice is matched,
that element will be considered the terminator of the preceding slice.
That slice will be the last item returned by the iterator.

```
let slice = [3, 10, 40, 33];
let mut iter = slice.split_inclusive(|num| num % 3 == 0);

assert_eq!(iter.next().unwrap(), &[3]);
assert_eq!(iter.next().unwrap(), &[10, 40, 33]);
assert!(iter.next().is_none());
```

1.51.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2320-2322)

#### pub fn [split\_inclusive\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_inclusive_mut)<F>(&mut self, pred: F) -> [SplitInclusiveMut](https://doc.rust-lang.org/std/slice/struct.SplitInclusiveMut.html "struct std::slice::SplitInclusiveMut")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over mutable subslices separated by elements that
match `pred`. The matched element is contained in the previous
subslice as a terminator.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-116)Examples

```
let mut v = [10, 40, 30, 20, 60, 50];

for group in v.split_inclusive_mut(|num| *num % 3 == 0) {
    let terminator_idx = group.len()-1;
    group[terminator_idx] = 1;
}
assert_eq!(v, [10, 40, 1, 20, 1, 1]);
```

1.27.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2356-2358)

#### pub fn [rsplit](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rsplit)<F>(&self, pred: F) -> [RSplit](https://doc.rust-lang.org/std/slice/struct.RSplit.html "struct std::slice::RSplit")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over subslices separated by elements that match
`pred`, starting at the end of the slice and working backwards.
The matched element is not contained in the subslices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-117)Examples

```
let slice = [11, 22, 33, 0, 44, 55];
let mut iter = slice.rsplit(|num| *num == 0);

assert_eq!(iter.next().unwrap(), &[44, 55]);
assert_eq!(iter.next().unwrap(), &[11, 22, 33]);
assert_eq!(iter.next(), None);
```

As with `split()`, if the first or last element is matched, an empty
slice will be the first (or last) item returned by the iterator.

```
let v = &[0, 1, 1, 2, 3, 5, 8];
let mut it = v.rsplit(|n| *n % 2 == 0);
assert_eq!(it.next().unwrap(), &[]);
assert_eq!(it.next().unwrap(), &[3, 5]);
assert_eq!(it.next().unwrap(), &[1, 1]);
assert_eq!(it.next().unwrap(), &[]);
assert_eq!(it.next(), None);
```

1.27.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2382-2384)

#### pub fn [rsplit\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rsplit_mut)<F>(&mut self, pred: F) -> [RSplitMut](https://doc.rust-lang.org/std/slice/struct.RSplitMut.html "struct std::slice::RSplitMut")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over mutable subslices separated by elements that
match `pred`, starting at the end of the slice and working
backwards. The matched element is not contained in the subslices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-118)Examples

```
let mut v = [100, 400, 300, 200, 600, 500];

let mut count = 0;
for group in v.rsplit_mut(|num| *num % 3 == 0) {
    count += 1;
    group[0] = count;
}
assert_eq!(v, [3, 400, 300, 2, 600, 1]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2410-2412)

#### pub fn [splitn](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.splitn)<F>(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pred: F) -> [SplitN](https://doc.rust-lang.org/std/slice/struct.SplitN.html "struct std::slice::SplitN")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over subslices separated by elements that match
`pred`, limited to returning at most `n` items. The matched element is
not contained in the subslices.

The last element returned, if any, will contain the remainder of the
slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-119)Examples

Print the slice split once by numbers divisible by 3 (i.e., `[10, 40]`,
`[20, 60, 50]`):

```
let v = [10, 40, 30, 20, 60, 50];

for group in v.splitn(2, |num| *num % 3 == 0) {
    println!("{group:?}");
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2436-2438)

#### pub fn [splitn\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.splitn_mut)<F>(&mut self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pred: F) -> [SplitNMut](https://doc.rust-lang.org/std/slice/struct.SplitNMut.html "struct std::slice::SplitNMut")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over mutable subslices separated by elements that match
`pred`, limited to returning at most `n` items. The matched element is
not contained in the subslices.

The last element returned, if any, will contain the remainder of the
slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-120)Examples

```
let mut v = [10, 40, 30, 20, 60, 50];

for group in v.splitn_mut(2, |num| *num % 3 == 0) {
    group[0] = 1;
}
assert_eq!(v, [1, 40, 30, 1, 60, 50]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2465-2467)

#### pub fn [rsplitn](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rsplitn)<F>(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pred: F) -> [RSplitN](https://doc.rust-lang.org/std/slice/struct.RSplitN.html "struct std::slice::RSplitN")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over subslices separated by elements that match
`pred` limited to returning at most `n` items. This starts at the end of
the slice and works backwards. The matched element is not contained in
the subslices.

The last element returned, if any, will contain the remainder of the
slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-121)Examples

Print the slice split once, starting from the end, by numbers divisible
by 3 (i.e., `[50]`, `[10, 40, 30, 20]`):

```
let v = [10, 40, 30, 20, 60, 50];

for group in v.rsplitn(2, |num| *num % 3 == 0) {
    println!("{group:?}");
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2492-2494)

#### pub fn [rsplitn\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rsplitn_mut)<F>(&mut self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pred: F) -> [RSplitNMut](https://doc.rust-lang.org/std/slice/struct.RSplitNMut.html "struct std::slice::RSplitNMut")<'\_, T, F> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns an iterator over subslices separated by elements that match
`pred` limited to returning at most `n` items. This starts at the end of
the slice and works backwards. The matched element is not contained in
the subslices.

The last element returned, if any, will contain the remainder of the
slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-122)Examples

```
let mut s = [10, 40, 30, 20, 60, 50];

for group in s.rsplitn_mut(2, |num| *num % 3 == 0) {
    group[0] = 1;
}
assert_eq!(s, [1, 40, 30, 20, 60, 1]);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2519-2521)

#### pub fn [split\_once](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_once)<F>(&self, pred: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))> where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

🔬This is a nightly-only experimental API. (`slice_split_once` [#112811](https://github.com/rust-lang/rust/issues/112811))

Splits the slice on the first element that matches the specified
predicate.

If any matching elements are present in the slice, returns the prefix
before the match and suffix after. The matching element itself is not
included. If no elements match, returns `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-123)Examples

```
#![feature(slice_split_once)]
let s = [1, 2, 3, 2, 4];
assert_eq!(s.split_once(|&x| x == 2), Some((
    &[1][..],
    &[3, 2, 4][..]
)));
assert_eq!(s.split_once(|&x| x == 0), None);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2547-2549)

#### pub fn [rsplit\_once](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rsplit_once)<F>(&self, pred: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))> where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

🔬This is a nightly-only experimental API. (`slice_split_once` [#112811](https://github.com/rust-lang/rust/issues/112811))

Splits the slice on the last element that matches the specified
predicate.

If any matching elements are present in the slice, returns the prefix
before the match and suffix after. The matching element itself is not
included. If no elements match, returns `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-124)Examples

```
#![feature(slice_split_once)]
let s = [1, 2, 3, 2, 4];
assert_eq!(s.rsplit_once(|&x| x == 2), Some((
    &[1, 2, 3][..],
    &[4][..]
)));
assert_eq!(s.rsplit_once(|&x| x == 0), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2583-2585)

#### pub fn [contains](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.contains)(&self, x: [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

Returns `true` if the slice contains an element with the given value.

This operation is *O*(*n*).

Note that if you have a sorted slice, [`binary_search`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search "method slice::binary_search") may be faster.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-125)Examples

```
let v = [10, 40, 30];
assert!(v.contains(&30));
assert!(!v.contains(&50));
```

If you do not have a `&T`, but some other value that you can compare
with one (for example, `String` implements `PartialEq<str>`), you can
use `iter().any`:

```
let v = [String::from("hello"), String::from("world")]; // slice of `String`
assert!(v.iter().any(|e| e == "hello")); // search with `&str`
assert!(!v.iter().any(|e| e == "hi"));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2613-2615)

#### pub fn [starts\_with](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.starts_with)(&self, needle: &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

Returns `true` if `needle` is a prefix of the slice or equal to the slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-126)Examples

```
let v = [10, 40, 30];
assert!(v.starts_with(&[10]));
assert!(v.starts_with(&[10, 40]));
assert!(v.starts_with(&v));
assert!(!v.starts_with(&[50]));
assert!(!v.starts_with(&[10, 50]));
```

Always returns `true` if `needle` is an empty slice:

```
let v = &[10, 40, 30];
assert!(v.starts_with(&[]));
let v: &[u8] = &[];
assert!(v.starts_with(&[]));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2644-2646)

#### pub fn [ends\_with](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ends_with)(&self, needle: &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

Returns `true` if `needle` is a suffix of the slice or equal to the slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-127)Examples

```
let v = [10, 40, 30];
assert!(v.ends_with(&[30]));
assert!(v.ends_with(&[40, 30]));
assert!(v.ends_with(&v));
assert!(!v.ends_with(&[50]));
assert!(!v.ends_with(&[50, 30]));
```

Always returns `true` if `needle` is an empty slice:

```
let v = &[10, 40, 30];
assert!(v.ends_with(&[]));
let v: &[u8] = &[];
assert!(v.ends_with(&[]));
```

1.51.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2676-2678)

#### pub fn [strip\_prefix](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.strip_prefix)<P>(&self, prefix: [&P](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[[T]](https://doc.rust-lang.org/std/primitive.slice.html)> where P: [SlicePattern](https://doc.rust-lang.org/core/slice/trait.SlicePattern.html "trait core::slice::SlicePattern")<Item = T> + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

Returns a subslice with the prefix removed.

If the slice starts with `prefix`, returns the subslice after the prefix, wrapped in `Some`.
If `prefix` is empty, simply returns the original slice. If `prefix` is equal to the
original slice, returns an empty slice.

If the slice does not start with `prefix`, returns `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-128)Examples

```
let v = &[10, 40, 30];
assert_eq!(v.strip_prefix(&[10]), Some(&[40, 30][..]));
assert_eq!(v.strip_prefix(&[10, 40]), Some(&[30][..]));
assert_eq!(v.strip_prefix(&[10, 40, 30]), Some(&[][..]));
assert_eq!(v.strip_prefix(&[50]), None);
assert_eq!(v.strip_prefix(&[10, 50]), None);

let prefix : &str = "he";
assert_eq!(b"hello".strip_prefix(prefix.as_bytes()),
           Some(b"llo".as_ref()));
```

1.51.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2712-2714)

#### pub fn [strip\_suffix](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.strip_suffix)<P>(&self, suffix: [&P](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[[T]](https://doc.rust-lang.org/std/primitive.slice.html)> where P: [SlicePattern](https://doc.rust-lang.org/core/slice/trait.SlicePattern.html "trait core::slice::SlicePattern")<Item = T> + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

Returns a subslice with the suffix removed.

If the slice ends with `suffix`, returns the subslice before the suffix, wrapped in `Some`.
If `suffix` is empty, simply returns the original slice. If `suffix` is equal to the
original slice, returns an empty slice.

If the slice does not end with `suffix`, returns `None`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-129)Examples

```
let v = &[10, 40, 30];
assert_eq!(v.strip_suffix(&[30]), Some(&[10, 40][..]));
assert_eq!(v.strip_suffix(&[40, 30]), Some(&[10][..]));
assert_eq!(v.strip_suffix(&[10, 40, 30]), Some(&[][..]));
assert_eq!(v.strip_suffix(&[50]), None);
assert_eq!(v.strip_suffix(&[50, 30]), None);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2755-2757)

#### pub fn [trim\_prefix](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.trim_prefix)<P>(&self, prefix: [&P](https://doc.rust-lang.org/std/primitive.reference.html)) -> &[[T]](https://doc.rust-lang.org/std/primitive.slice.html) where P: [SlicePattern](https://doc.rust-lang.org/core/slice/trait.SlicePattern.html "trait core::slice::SlicePattern")<Item = T> + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

🔬This is a nightly-only experimental API. (`trim_prefix_suffix` [#142312](https://github.com/rust-lang/rust/issues/142312))

Returns a subslice with the optional prefix removed.

If the slice starts with `prefix`, returns the subslice after the prefix. If `prefix`
is empty or the slice does not start with `prefix`, simply returns the original slice.
If `prefix` is equal to the original slice, returns an empty slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-130)Examples

```
#![feature(trim_prefix_suffix)]

let v = &[10, 40, 30];

// Prefix present - removes it
assert_eq!(v.trim_prefix(&[10]), &[40, 30][..]);
assert_eq!(v.trim_prefix(&[10, 40]), &[30][..]);
assert_eq!(v.trim_prefix(&[10, 40, 30]), &[][..]);

// Prefix absent - returns original slice
assert_eq!(v.trim_prefix(&[50]), &[10, 40, 30][..]);
assert_eq!(v.trim_prefix(&[10, 50]), &[10, 40, 30][..]);

let prefix : &str = "he";
assert_eq!(b"hello".trim_prefix(prefix.as_bytes()), b"llo".as_ref());
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2795-2797)

#### pub fn [trim\_suffix](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.trim_suffix)<P>(&self, suffix: [&P](https://doc.rust-lang.org/std/primitive.reference.html)) -> &[[T]](https://doc.rust-lang.org/std/primitive.slice.html) where P: [SlicePattern](https://doc.rust-lang.org/core/slice/trait.SlicePattern.html "trait core::slice::SlicePattern")<Item = T> + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

🔬This is a nightly-only experimental API. (`trim_prefix_suffix` [#142312](https://github.com/rust-lang/rust/issues/142312))

Returns a subslice with the optional suffix removed.

If the slice ends with `suffix`, returns the subslice before the suffix. If `suffix`
is empty or the slice does not end with `suffix`, simply returns the original slice.
If `suffix` is equal to the original slice, returns an empty slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-131)Examples

```
#![feature(trim_prefix_suffix)]

let v = &[10, 40, 30];

// Suffix present - removes it
assert_eq!(v.trim_suffix(&[30]), &[10, 40][..]);
assert_eq!(v.trim_suffix(&[40, 30]), &[10][..]);
assert_eq!(v.trim_suffix(&[10, 40, 30]), &[][..]);

// Suffix absent - returns original slice
assert_eq!(v.trim_suffix(&[50]), &[10, 40, 30][..]);
assert_eq!(v.trim_suffix(&[50, 30]), &[10, 40, 30][..]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2881-2883)

#### pub fn [binary\_search](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.binary_search)(&self, x: [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html)> where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Binary searches this slice for a given element.
If the slice is not sorted, the returned result is unspecified and
meaningless.

If the value is found then [`Result::Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") is returned, containing the
index of the matching element. If there are multiple matches, then any
one of the matches could be returned. The index is chosen
deterministically, but is subject to change in future versions of Rust.
If the value is not found then [`Result::Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") is returned, containing
the index where a matching element could be inserted while maintaining
sorted order.

See also [`binary_search_by`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search_by "method slice::binary_search_by"), [`binary_search_by_key`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search_by_key "method slice::binary_search_by_key"), and [`partition_point`](https://doc.rust-lang.org/std/primitive.slice.html#method.partition_point "method slice::partition_point").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-132)Examples

Looks up a series of four elements. The first is found, with a
uniquely determined position; the second and third are not
found; the fourth could match any position in `[1, 4]`.

```
let s = [0, 1, 1, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];

assert_eq!(s.binary_search(&13),  Ok(9));
assert_eq!(s.binary_search(&4),   Err(7));
assert_eq!(s.binary_search(&100), Err(13));
let r = s.binary_search(&1);
assert!(match r { Ok(1..=4) => true, _ => false, });
```

If you want to find that whole *range* of matching items, rather than
an arbitrary matching one, that can be done using [`partition_point`](https://doc.rust-lang.org/std/primitive.slice.html#method.partition_point "method slice::partition_point"):

```
let s = [0, 1, 1, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];

let low = s.partition_point(|x| x < &1);
assert_eq!(low, 1);
let high = s.partition_point(|x| x <= &1);
assert_eq!(high, 5);
let r = s.binary_search(&1);
assert!((low..high).contains(&r.unwrap()));

assert!(s[..low].iter().all(|&x| x < 1));
assert!(s[low..high].iter().all(|&x| x == 1));
assert!(s[high..].iter().all(|&x| x > 1));

// For something not found, the "range" of equal items is empty
assert_eq!(s.partition_point(|x| x < &11), 9);
assert_eq!(s.partition_point(|x| x <= &11), 9);
assert_eq!(s.binary_search(&11), Err(9));
```

If you want to insert an item to a sorted vector, while maintaining
sort order, consider using [`partition_point`](https://doc.rust-lang.org/std/primitive.slice.html#method.partition_point "method slice::partition_point"):

```
let mut s = vec![0, 1, 1, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
let num = 42;
let idx = s.partition_point(|&x| x <= num);
// If `num` is unique, `s.partition_point(|&x| x < num)` (with `<`) is equivalent to
// `s.binary_search(&num).unwrap_or_else(|x| x)`, but using `<=` will allow `insert`
// to shift less elements.
s.insert(idx, num);
assert_eq!(s, [0, 1, 1, 1, 1, 2, 3, 5, 8, 13, 21, 34, 42, 55]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#2932-2934)

#### pub fn [binary\_search\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.binary_search_by)<'a, F>(&'a self, f: F) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html)> where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&'a T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering"),

Binary searches this slice with a comparator function.

The comparator function should return an order code that indicates
whether its argument is `Less`, `Equal` or `Greater` the desired
target.
If the slice is not sorted or if the comparator function does not
implement an order consistent with the sort order of the underlying
slice, the returned result is unspecified and meaningless.

If the value is found then [`Result::Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") is returned, containing the
index of the matching element. If there are multiple matches, then any
one of the matches could be returned. The index is chosen
deterministically, but is subject to change in future versions of Rust.
If the value is not found then [`Result::Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") is returned, containing
the index where a matching element could be inserted while maintaining
sorted order.

See also [`binary_search`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search "method slice::binary_search"), [`binary_search_by_key`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search_by_key "method slice::binary_search_by_key"), and [`partition_point`](https://doc.rust-lang.org/std/primitive.slice.html#method.partition_point "method slice::partition_point").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-133)Examples

Looks up a series of four elements. The first is found, with a
uniquely determined position; the second and third are not
found; the fourth could match any position in `[1, 4]`.

```
let s = [0, 1, 1, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];

let seek = 13;
assert_eq!(s.binary_search_by(|probe| probe.cmp(&seek)), Ok(9));
let seek = 4;
assert_eq!(s.binary_search_by(|probe| probe.cmp(&seek)), Err(7));
let seek = 100;
assert_eq!(s.binary_search_by(|probe| probe.cmp(&seek)), Err(13));
let seek = 1;
let r = s.binary_search_by(|probe| probe.cmp(&seek));
assert!(match r { Ok(1..=4) => true, _ => false, });
```

1.10.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3033-3036)

#### pub fn [binary\_search\_by\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.binary_search_by_key)<'a, B, F>( &'a self, b: [&B](https://doc.rust-lang.org/std/primitive.reference.html), f: F, ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html)> where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&'a T](https://doc.rust-lang.org/std/primitive.reference.html)) -> B, B: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Binary searches this slice with a key extraction function.

Assumes that the slice is sorted by the key, for instance with
[`sort_by_key`](https://doc.rust-lang.org/std/primitive.slice.html#method.sort_by_key "method slice::sort_by_key") using the same key extraction function.
If the slice is not sorted by the key, the returned result is
unspecified and meaningless.

If the value is found then [`Result::Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") is returned, containing the
index of the matching element. If there are multiple matches, then any
one of the matches could be returned. The index is chosen
deterministically, but is subject to change in future versions of Rust.
If the value is not found then [`Result::Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") is returned, containing
the index where a matching element could be inserted while maintaining
sorted order.

See also [`binary_search`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search "method slice::binary_search"), [`binary_search_by`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search_by "method slice::binary_search_by"), and [`partition_point`](https://doc.rust-lang.org/std/primitive.slice.html#method.partition_point "method slice::partition_point").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-134)Examples

Looks up a series of four elements in a slice of pairs sorted by
their second elements. The first is found, with a uniquely
determined position; the second and third are not found; the
fourth could match any position in `[1, 4]`.

```
let s = [(0, 0), (2, 1), (4, 1), (5, 1), (3, 1),
         (1, 2), (2, 3), (4, 5), (5, 8), (3, 13),
         (1, 21), (2, 34), (4, 55)];

assert_eq!(s.binary_search_by_key(&13, |&(a, b)| b),  Ok(9));
assert_eq!(s.binary_search_by_key(&4, |&(a, b)| b),   Err(7));
assert_eq!(s.binary_search_by_key(&100, |&(a, b)| b), Err(13));
let r = s.binary_search_by_key(&1, |&(a, b)| b);
assert!(match r { Ok(1..=4) => true, _ => false, });
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3095-3097)

#### pub fn [sort\_unstable](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_unstable)(&mut self) where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Sorts the slice in ascending order **without** preserving the initial order of equal elements.

This sort is unstable (i.e., may reorder equal elements), in-place (i.e., does not
allocate), and *O*(*n* \* log(*n*)) worst-case.

If the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `T` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), the function
may panic; even if the function exits normally, the resulting order of elements in the slice
is unspecified. See also the note on panicking below.

For example `|a, b| (a - b).cmp(a)` is a comparison function that is neither transitive nor
reflexive nor total, `a < b < c < a` with `a = 1, b = 2, c = 3`. For more information and
examples see the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") documentation.

All original elements will remain in the slice and any possible modifications via interior
mutability are observed in the input. Same is true if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `T` panics.

Sorting types that only implement [`PartialOrd`](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd") such as [`f32`](https://doc.rust-lang.org/std/primitive.f32.html "primitive f32") and [`f64`](https://doc.rust-lang.org/std/primitive.f64.html "primitive f64") require
additional precautions. For example, `f32::NAN != f32::NAN`, which doesn’t fulfill the
reflexivity requirement of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"). By using an alternative comparison function with
`slice::sort_unstable_by` such as [`f32::total_cmp`](https://doc.rust-lang.org/std/primitive.f32.html#method.total_cmp "method f32::total_cmp") or [`f64::total_cmp`](https://doc.rust-lang.org/std/primitive.f64.html#method.total_cmp "method f64::total_cmp") that defines a
[total order](https://en.wikipedia.org/wiki/Total_order) users can sort slices containing floating-point values. Alternatively, if all
values in the slice are guaranteed to be in a subset for which [`PartialOrd::partial_cmp`](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp "method std::cmp::PartialOrd::partial_cmp")
forms a [total order](https://en.wikipedia.org/wiki/Total_order), it’s possible to sort the slice with `sort_unstable_by(|a, b| a.partial_cmp(b).unwrap())`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation)Current implementation

The current implementation is based on [ipnsort](https://github.com/Voultapher/sort-research-rs/tree/main/ipnsort) by Lukas Bergdoll and Orson Peters, which
combines the fast average case of quicksort with the fast worst case of heapsort, achieving
linear time on fully sorted and reversed inputs. On inputs with k distinct elements, the
expected time to sort the data is *O*(*n* \* log(*k*)).

It is typically faster than stable sorting, except in a few special cases, e.g., when the
slice is partially sorted.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-36)Panics

May panic if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `T` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), or if
the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") implementation panics.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-135)Examples

```
let mut v = [4, -5, 1, -3, 2];

v.sort_unstable();
assert_eq!(v, [-5, -3, 1, 2, 4]);
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3150-3152)

#### pub fn [sort\_unstable\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_unstable_by)<F>(&mut self, compare: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html), [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering"),

Sorts the slice in ascending order with a comparison function, **without** preserving the
initial order of equal elements.

This sort is unstable (i.e., may reorder equal elements), in-place (i.e., does not
allocate), and *O*(*n* \* log(*n*)) worst-case.

If the comparison function `compare` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), the function
may panic; even if the function exits normally, the resulting order of elements in the slice
is unspecified. See also the note on panicking below.

For example `|a, b| (a - b).cmp(a)` is a comparison function that is neither transitive nor
reflexive nor total, `a < b < c < a` with `a = 1, b = 2, c = 3`. For more information and
examples see the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") documentation.

All original elements will remain in the slice and any possible modifications via interior
mutability are observed in the input. Same is true if `compare` panics.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-1)Current implementation

The current implementation is based on [ipnsort](https://github.com/Voultapher/sort-research-rs/tree/main/ipnsort) by Lukas Bergdoll and Orson Peters, which
combines the fast average case of quicksort with the fast worst case of heapsort, achieving
linear time on fully sorted and reversed inputs. On inputs with k distinct elements, the
expected time to sort the data is *O*(*n* \* log(*k*)).

It is typically faster than stable sorting, except in a few special cases, e.g., when the
slice is partially sorted.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-37)Panics

May panic if the `compare` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), or if
the `compare` itself panics.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-136)Examples

```
let mut v = [4, -5, 1, -3, 2];
v.sort_unstable_by(|a, b| a.cmp(b));
assert_eq!(v, [-5, -3, 1, 2, 4]);

// reverse sorting
v.sort_unstable_by(|a, b| b.cmp(a));
assert_eq!(v, [4, 2, 1, -3, -5]);
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3202-3205)

#### pub fn [sort\_unstable\_by\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_unstable_by_key)<K, F>(&mut self, f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> K, K: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Sorts the slice in ascending order with a key extraction function, **without** preserving
the initial order of equal elements.

This sort is unstable (i.e., may reorder equal elements), in-place (i.e., does not
allocate), and *O*(*n* \* log(*n*)) worst-case.

If the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `K` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), the function
may panic; even if the function exits normally, the resulting order of elements in the slice
is unspecified. See also the note on panicking below.

For example `|a, b| (a - b).cmp(a)` is a comparison function that is neither transitive nor
reflexive nor total, `a < b < c < a` with `a = 1, b = 2, c = 3`. For more information and
examples see the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") documentation.

All original elements will remain in the slice and any possible modifications via interior
mutability are observed in the input. Same is true if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `K` panics.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-2)Current implementation

The current implementation is based on [ipnsort](https://github.com/Voultapher/sort-research-rs/tree/main/ipnsort) by Lukas Bergdoll and Orson Peters, which
combines the fast average case of quicksort with the fast worst case of heapsort, achieving
linear time on fully sorted and reversed inputs. On inputs with k distinct elements, the
expected time to sort the data is *O*(*n* \* log(*k*)).

It is typically faster than stable sorting, except in a few special cases, e.g., when the
slice is partially sorted.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-38)Panics

May panic if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `K` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), or if
the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") implementation panics.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-137)Examples

```
let mut v = [4i32, -5, 1, -3, 2];

v.sort_unstable_by_key(|k| k.abs());
assert_eq!(v, [1, 2, -3, 4, -5]);
```

1.49.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3265-3267)

#### pub fn [select\_nth\_unstable](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.select_nth_unstable)( &mut self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), [&mut T](https://doc.rust-lang.org/std/primitive.reference.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Reorders the slice such that the element at `index` is at a sort-order position. All
elements before `index` will be `<=` to this value, and all elements after will be `>=` to
it.

This reordering is unstable (i.e. any element that compares equal to the nth element may end
up at that position), in-place (i.e. does not allocate), and runs in *O*(*n*) time. This
function is also known as “kth element” in other libraries.

Returns a triple that partitions the reordered slice:

* The unsorted subslice before `index`, whose elements all satisfy `x <= self[index]`.
* The element at `index`.
* The unsorted subslice after `index`, whose elements all satisfy `x >= self[index]`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-3)Current implementation

The current algorithm is an introselect implementation based on [ipnsort](https://github.com/Voultapher/sort-research-rs/tree/main/ipnsort) by Lukas Bergdoll
and Orson Peters, which is also the basis for [`sort_unstable`](https://doc.rust-lang.org/std/primitive.slice.html#method.sort_unstable "method slice::sort_unstable"). The fallback algorithm is
Median of Medians using Tukey’s Ninther for pivot selection, which guarantees linear runtime
for all inputs.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-39)Panics

Panics when `index >= len()`, and so always panics on empty slices.

May panic if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `T` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order).

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-138)Examples

```
let mut v = [-5i32, 4, 2, -3, 1];

// Find the items `<=` to the median, the median itself, and the items `>=` to it.
let (lesser, median, greater) = v.select_nth_unstable(2);

assert!(lesser == [-3, -5] || lesser == [-5, -3]);
assert_eq!(median, &mut 1);
assert!(greater == [4, 2] || greater == [2, 4]);

// We are only guaranteed the slice will be one of the following, based on the way we sort
// about the specified index.
assert!(v == [-3, -5, 1, 2, 4] ||
        v == [-5, -3, 1, 2, 4] ||
        v == [-3, -5, 1, 4, 2] ||
        v == [-5, -3, 1, 4, 2]);
```

1.49.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3330-3336)

#### pub fn [select\_nth\_unstable\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.select_nth_unstable_by)<F>( &mut self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html), compare: F, ) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), [&mut T](https://doc.rust-lang.org/std/primitive.reference.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html), [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering"),

Reorders the slice with a comparator function such that the element at `index` is at a
sort-order position. All elements before `index` will be `<=` to this value, and all
elements after will be `>=` to it, according to the comparator function.

This reordering is unstable (i.e. any element that compares equal to the nth element may end
up at that position), in-place (i.e. does not allocate), and runs in *O*(*n*) time. This
function is also known as “kth element” in other libraries.

Returns a triple partitioning the reordered slice:

* The unsorted subslice before `index`, whose elements all satisfy
  `compare(x, self[index]).is_le()`.
* The element at `index`.
* The unsorted subslice after `index`, whose elements all satisfy
  `compare(x, self[index]).is_ge()`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-4)Current implementation

The current algorithm is an introselect implementation based on [ipnsort](https://github.com/Voultapher/sort-research-rs/tree/main/ipnsort) by Lukas Bergdoll
and Orson Peters, which is also the basis for [`sort_unstable`](https://doc.rust-lang.org/std/primitive.slice.html#method.sort_unstable "method slice::sort_unstable"). The fallback algorithm is
Median of Medians using Tukey’s Ninther for pivot selection, which guarantees linear runtime
for all inputs.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-40)Panics

Panics when `index >= len()`, and so always panics on empty slices.

May panic if `compare` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order).

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-139)Examples

```
let mut v = [-5i32, 4, 2, -3, 1];

// Find the items `>=` to the median, the median itself, and the items `<=` to it, by using
// a reversed comparator.
let (before, median, after) = v.select_nth_unstable_by(2, |a, b| b.cmp(a));

assert!(before == [4, 2] || before == [2, 4]);
assert_eq!(median, &mut 1);
assert!(after == [-3, -5] || after == [-5, -3]);

// We are only guaranteed the slice will be one of the following, based on the way we sort
// about the specified index.
assert!(v == [2, 4, 1, -5, -3] ||
        v == [2, 4, 1, -3, -5] ||
        v == [4, 2, 1, -5, -3] ||
        v == [4, 2, 1, -3, -5]);
```

1.49.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3397-3404)

#### pub fn [select\_nth\_unstable\_by\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.select_nth_unstable_by_key)<K, F>( &mut self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html), f: F, ) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), [&mut T](https://doc.rust-lang.org/std/primitive.reference.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> K, K: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Reorders the slice with a key extraction function such that the element at `index` is at a
sort-order position. All elements before `index` will have keys `<=` to the key at `index`,
and all elements after will have keys `>=` to it.

This reordering is unstable (i.e. any element that compares equal to the nth element may end
up at that position), in-place (i.e. does not allocate), and runs in *O*(*n*) time. This
function is also known as “kth element” in other libraries.

Returns a triple partitioning the reordered slice:

* The unsorted subslice before `index`, whose elements all satisfy `f(x) <= f(self[index])`.
* The element at `index`.
* The unsorted subslice after `index`, whose elements all satisfy `f(x) >= f(self[index])`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-5)Current implementation

The current algorithm is an introselect implementation based on [ipnsort](https://github.com/Voultapher/sort-research-rs/tree/main/ipnsort) by Lukas Bergdoll
and Orson Peters, which is also the basis for [`sort_unstable`](https://doc.rust-lang.org/std/primitive.slice.html#method.sort_unstable "method slice::sort_unstable"). The fallback algorithm is
Median of Medians using Tukey’s Ninther for pivot selection, which guarantees linear runtime
for all inputs.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-41)Panics

Panics when `index >= len()`, meaning it always panics on empty slices.

May panic if `K: Ord` does not implement a total order.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-140)Examples

```
let mut v = [-5i32, 4, 1, -3, 2];

// Find the items `<=` to the absolute median, the absolute median itself, and the items
// `>=` to it.
let (lesser, median, greater) = v.select_nth_unstable_by_key(2, |a| a.abs());

assert!(lesser == [1, 2] || lesser == [2, 1]);
assert_eq!(median, &mut -3);
assert!(greater == [4, -5] || greater == [-5, 4]);

// We are only guaranteed the slice will be one of the following, based on the way we sort
// about the specified index.
assert!(v == [1, 2, -3, 4, -5] ||
        v == [1, 2, -3, -5, 4] ||
        v == [2, 1, -3, 4, -5] ||
        v == [2, 1, -3, -5, 4]);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3431-3433)

#### pub fn [partition\_dedup](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.partition_dedup)(&mut self) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

🔬This is a nightly-only experimental API. (`slice_partition_dedup` [#54279](https://github.com/rust-lang/rust/issues/54279))

Moves all consecutive repeated elements to the end of the slice according to the
[`PartialEq`](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq") trait implementation.

Returns two slices. The first contains no consecutive repeated elements.
The second contains all the duplicates in no specified order.

If the slice is sorted, the first returned slice contains no duplicates.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-141)Examples

```
#![feature(slice_partition_dedup)]

let mut slice = [1, 2, 2, 3, 3, 2, 1, 1];

let (dedup, duplicates) = slice.partition_dedup();

assert_eq!(dedup, [1, 2, 3, 2, 1]);
assert_eq!(duplicates, [2, 3, 1]);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3465-3467)

#### pub fn [partition\_dedup\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.partition_dedup_by)<F>(&mut self, same\_bucket: F) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html), [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

🔬This is a nightly-only experimental API. (`slice_partition_dedup` [#54279](https://github.com/rust-lang/rust/issues/54279))

Moves all but the first of consecutive elements to the end of the slice satisfying
a given equality relation.

Returns two slices. The first contains no consecutive repeated elements.
The second contains all the duplicates in no specified order.

The `same_bucket` function is passed references to two elements from the slice and
must determine if the elements compare equal. The elements are passed in opposite order
from their order in the slice, so if `same_bucket(a, b)` returns `true`, `a` is moved
at the end of the slice.

If the slice is sorted, the first returned slice contains no duplicates.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-142)Examples

```
#![feature(slice_partition_dedup)]

let mut slice = ["foo", "Foo", "BAZ", "Bar", "bar", "baz", "BAZ"];

let (dedup, duplicates) = slice.partition_dedup_by(|a, b| a.eq_ignore_ascii_case(b));

assert_eq!(dedup, ["foo", "BAZ", "Bar", "baz"]);
assert_eq!(duplicates, ["bar", "Foo", "BAZ"]);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3591-3594)

#### pub fn [partition\_dedup\_by\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.partition_dedup_by_key)<K, F>(&mut self, key: F) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> K, K: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

🔬This is a nightly-only experimental API. (`slice_partition_dedup` [#54279](https://github.com/rust-lang/rust/issues/54279))

Moves all but the first of consecutive elements to the end of the slice that resolve
to the same key.

Returns two slices. The first contains no consecutive repeated elements.
The second contains all the duplicates in no specified order.

If the slice is sorted, the first returned slice contains no duplicates.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-143)Examples

```
#![feature(slice_partition_dedup)]

let mut slice = [10, 20, 21, 30, 30, 20, 11, 13];

let (dedup, duplicates) = slice.partition_dedup_by_key(|i| *i / 10);

assert_eq!(dedup, [10, 20, 30, 20, 11]);
assert_eq!(duplicates, [21, 30, 13]);
```

1.26.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3633)

#### pub fn [rotate\_left](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rotate_left)(&mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Rotates the slice in-place such that the first `mid` elements of the
slice move to the end while the last `self.len() - mid` elements move to
the front.

After calling `rotate_left`, the element previously at index `mid` will
become the first element in the slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-42)Panics

This function will panic if `mid` is greater than the length of the
slice. Note that `mid == self.len()` does *not* panic and is a no-op
rotation.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#complexity)Complexity

Takes linear (in `self.len()`) time.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-144)Examples

```
let mut a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.rotate_left(2);
assert_eq!(a, ['c', 'd', 'e', 'f', 'a', 'b']);
```

Rotating a subslice:

```
let mut a = ['a', 'b', 'c', 'd', 'e', 'f'];
a[1..5].rotate_left(1);
assert_eq!(a, ['a', 'c', 'd', 'e', 'b', 'f']);
```

1.26.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3679)

#### pub fn [rotate\_right](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.rotate_right)(&mut self, k: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Rotates the slice in-place such that the first `self.len() - k`
elements of the slice move to the end while the last `k` elements move
to the front.

After calling `rotate_right`, the element previously at index
`self.len() - k` will become the first element in the slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-43)Panics

This function will panic if `k` is greater than the length of the
slice. Note that `k == self.len()` does *not* panic and is a no-op
rotation.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#complexity-1)Complexity

Takes linear (in `self.len()`) time.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-145)Examples

```
let mut a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.rotate_right(2);
assert_eq!(a, ['e', 'f', 'a', 'b', 'c', 'd']);
```

Rotating a subslice:

```
let mut a = ['a', 'b', 'c', 'd', 'e', 'f'];
a[1..5].rotate_right(1);
assert_eq!(a, ['a', 'e', 'b', 'c', 'd', 'f']);
```

1.50.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3702-3704)

#### pub fn [fill](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.fill)(&mut self, value: T) where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Fills `self` with elements by cloning `value`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-146)Examples

```
let mut buf = vec![0; 10];
buf.fill(1);
assert_eq!(buf, vec![1; 10]);
```

1.51.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3726-3728)

#### pub fn [fill\_with](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.fill_with)<F>(&mut self, f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")() -> T,

Fills `self` with elements returned by calling a closure repeatedly.

This method uses a closure to create new values. If you’d rather
[`Clone`](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") a given value, use [`fill`](https://doc.rust-lang.org/std/primitive.slice.html#method.fill "method slice::fill"). If you want to use the [`Default`](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default")
trait to generate values, you can pass [`Default::default`](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default "associated function std::default::Default::default") as the
argument.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-147)Examples

```
let mut buf = vec![1; 10];
buf.fill_with(Default::default);
assert_eq!(buf, vec![0; 10]);
```

1.7.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3789-3791)

#### pub fn [clone\_from\_slice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clone_from_slice)(&mut self, src: &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Copies the elements from `src` into `self`.

The length of `src` must be the same as `self`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-44)Panics

This function will panic if the two slices have different lengths.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-148)Examples

Cloning two elements from a slice into another:

```
let src = [1, 2, 3, 4];
let mut dst = [0, 0];

// Because the slices have to be the same length,
// we slice the source slice from four elements
// to two. It will panic if we don't do this.
dst.clone_from_slice(&src[2..]);

assert_eq!(src, [1, 2, 3, 4]);
assert_eq!(dst, [3, 4]);
```

Rust enforces that there can only be one mutable reference with no
immutable references to a particular piece of data in a particular
scope. Because of this, attempting to use `clone_from_slice` on a
single slice will result in a compile failure:

[ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html "This example deliberately fails to compile")

```
let mut slice = [1, 2, 3, 4, 5];

slice[..2].clone_from_slice(&slice[3..]); // compile fail!
```

To work around this, we can use [`split_at_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.split_at_mut "method slice::split_at_mut") to create two distinct
sub-slices from a slice:

```
let mut slice = [1, 2, 3, 4, 5];

{
    let (left, right) = slice.split_at_mut(2);
    left.clone_from_slice(&right[1..]);
}

assert_eq!(slice, [4, 5, 3, 4, 5]);
```

1.9.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3855-3857)

#### pub fn [copy\_from\_slice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.copy_from_slice)(&mut self, src: &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

Copies all elements from `src` into `self`, using a memcpy.

The length of `src` must be the same as `self`.

If `T` does not implement `Copy`, use [`clone_from_slice`](https://doc.rust-lang.org/std/primitive.slice.html#method.clone_from_slice "method slice::clone_from_slice").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-45)Panics

This function will panic if the two slices have different lengths.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-149)Examples

Copying two elements from a slice into another:

```
let src = [1, 2, 3, 4];
let mut dst = [0, 0];

// Because the slices have to be the same length,
// we slice the source slice from four elements
// to two. It will panic if we don't do this.
dst.copy_from_slice(&src[2..]);

assert_eq!(src, [1, 2, 3, 4]);
assert_eq!(dst, [3, 4]);
```

Rust enforces that there can only be one mutable reference with no
immutable references to a particular piece of data in a particular
scope. Because of this, attempting to use `copy_from_slice` on a
single slice will result in a compile failure:

[ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html "This example deliberately fails to compile")

```
let mut slice = [1, 2, 3, 4, 5];

slice[..2].copy_from_slice(&slice[3..]); // compile fail!
```

To work around this, we can use [`split_at_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.split_at_mut "method slice::split_at_mut") to create two distinct
sub-slices from a slice:

```
let mut slice = [1, 2, 3, 4, 5];

{
    let (left, right) = slice.split_at_mut(2);
    left.copy_from_slice(&right[1..]);
}

assert_eq!(slice, [4, 5, 3, 4, 5]);
```

1.37.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3911-3913)

#### pub fn [copy\_within](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.copy_within)<R>(&mut self, src: R, dest: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) where R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>, T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

Copies elements from one part of the slice to another part of itself,
using a memmove.

`src` is the range within `self` to copy from. `dest` is the starting
index of the range within `self` to copy to, which will have the same
length as `src`. The two ranges may overlap. The ends of the two ranges
must be less than or equal to `self.len()`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-46)Panics

This function will panic if either range exceeds the end of the slice,
or if the end of `src` is before the start.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-150)Examples

Copying four bytes within a slice:

```
let mut bytes = *b"Hello, World!";

bytes.copy_within(1..5, 8);

assert_eq!(&bytes, b"Hello, Wello!");
```

1.27.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#3979)

#### pub fn [swap\_with\_slice](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.swap_with_slice)(&mut self, other: &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Swaps all elements in `self` with those in `other`.

The length of `other` must be the same as `self`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-47)Panics

This function will panic if the two slices have different lengths.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#example)Example

Swapping two elements across slices:

```
let mut slice1 = [0, 0];
let mut slice2 = [1, 2, 3, 4];

slice1.swap_with_slice(&mut slice2[2..]);

assert_eq!(slice1, [3, 4]);
assert_eq!(slice2, [1, 2, 0, 0]);
```

Rust enforces that there can only be one mutable reference to a
particular piece of data in a particular scope. Because of this,
attempting to use `swap_with_slice` on a single slice will result in
a compile failure:

[ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html "This example deliberately fails to compile")

```
let mut slice = [1, 2, 3, 4, 5];
slice[..2].swap_with_slice(&mut slice[3..]); // compile fail!
```

To work around this, we can use [`split_at_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.split_at_mut "method slice::split_at_mut") to create two distinct
mutable sub-slices from a slice:

```
let mut slice = [1, 2, 3, 4, 5];

{
    let (left, right) = slice.split_at_mut(2);
    left.swap_with_slice(&mut right[1..]);
}

assert_eq!(slice, [4, 5, 3, 1, 2]);
```

1.30.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4056)

#### pub unsafe fn [align\_to](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.align_to)<U>(&self) -> (&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[U]](https://doc.rust-lang.org/std/primitive.slice.html), &[[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Transmutes the slice to a slice of another type, ensuring alignment of the types is
maintained.

This method splits the slice into three distinct slices: prefix, correctly aligned middle
slice of a new type, and the suffix slice. The middle part will be as big as possible under
the given alignment constraint and element size.

This method has no purpose when either input element `T` or output element `U` are
zero-sized and will return the original slice without splitting anything.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-12)Safety

This method is essentially a `transmute` with respect to the elements in the returned
middle slice, so all the usual caveats pertaining to `transmute::<T, U>` also apply here.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-151)Examples

Basic usage:

```
unsafe {
    let bytes: [u8; 7] = [1, 2, 3, 4, 5, 6, 7];
    let (prefix, shorts, suffix) = bytes.align_to::<u16>();
    // less_efficient_algorithm_for_bytes(prefix);
    // more_efficient_algorithm_for_aligned_shorts(shorts);
    // less_efficient_algorithm_for_bytes(suffix);
}
```

1.30.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4121)

#### pub unsafe fn [align\_to\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.align_to_mut)<U>(&mut self) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[U]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html))

Transmutes the mutable slice to a mutable slice of another type, ensuring alignment of the
types is maintained.

This method splits the slice into three distinct slices: prefix, correctly aligned middle
slice of a new type, and the suffix slice. The middle part will be as big as possible under
the given alignment constraint and element size.

This method has no purpose when either input element `T` or output element `U` are
zero-sized and will return the original slice without splitting anything.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-13)Safety

This method is essentially a `transmute` with respect to the elements in the returned
middle slice, so all the usual caveats pertaining to `transmute::<T, U>` also apply here.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-152)Examples

Basic usage:

```
unsafe {
    let mut bytes: [u8; 7] = [1, 2, 3, 4, 5, 6, 7];
    let (prefix, shorts, suffix) = bytes.align_to_mut::<u16>();
    // less_efficient_algorithm_for_bytes(prefix);
    // more_efficient_algorithm_for_aligned_shorts(shorts);
    // less_efficient_algorithm_for_bytes(suffix);
}
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4212-4216)

#### pub fn [as\_simd](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_simd)<const LANES: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>(&self) -> (&[[T]](https://doc.rust-lang.org/std/primitive.slice.html), &[[Simd](https://doc.rust-lang.org/std/simd/struct.Simd.html "struct std::simd::Simd")<T, LANES>], &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where [Simd](https://doc.rust-lang.org/std/simd/struct.Simd.html "struct std::simd::Simd")<T, LANES>: [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[[T; LANES]](https://doc.rust-lang.org/std/primitive.array.html)>, T: [SimdElement](https://doc.rust-lang.org/std/simd/trait.SimdElement.html "trait std::simd::SimdElement"), [LaneCount](https://doc.rust-lang.org/std/simd/struct.LaneCount.html "struct std::simd::LaneCount")<LANES>: [SupportedLaneCount](https://doc.rust-lang.org/std/simd/trait.SupportedLaneCount.html "trait std::simd::SupportedLaneCount"),

🔬This is a nightly-only experimental API. (`portable_simd` [#86656](https://github.com/rust-lang/rust/issues/86656))

Splits a slice into a prefix, a middle of aligned SIMD types, and a suffix.

This is a safe wrapper around [`slice::align_to`](https://doc.rust-lang.org/std/primitive.slice.html#method.align_to "method slice::align_to"), so inherits the same
guarantees as that method.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-48)Panics

This will panic if the size of the SIMD type is different from
`LANES` times that of the scalar.

At the time of writing, the trait restrictions on `Simd<T, LANES>` keeps
that from ever happening, as only power-of-two numbers of lanes are
supported. It’s possible that, in the future, those restrictions might
be lifted in a way that would make it possible to see panics from this
method for something like `LANES == 3`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-153)Examples

```
#![feature(portable_simd)]
use core::simd::prelude::*;

let short = &[1, 2, 3];
let (prefix, middle, suffix) = short.as_simd::<4>();
assert_eq!(middle, []); // Not enough elements for anything in the middle

// They might be split in any possible way between prefix and suffix
let it = prefix.iter().chain(suffix).copied();
assert_eq!(it.collect::<Vec<_>>(), vec![1, 2, 3]);

fn basic_simd_sum(x: &[f32]) -> f32 {
    use std::ops::Add;
    let (prefix, middle, suffix) = x.as_simd();
    let sums = f32x4::from_array([
        prefix.iter().copied().sum(),
        0.0,
        0.0,
        suffix.iter().copied().sum(),
    ]);
    let sums = middle.iter().copied().fold(sums, f32x4::add);
    sums.reduce_sum()
}

let numbers: Vec<f32> = (1..101).map(|x| x as _).collect();
assert_eq!(basic_simd_sum(&numbers[1..99]), 4949.0);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4248-4252)

#### pub fn [as\_simd\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_simd_mut)<const LANES: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>( &mut self, ) -> (&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), &mut [[Simd](https://doc.rust-lang.org/std/simd/struct.Simd.html "struct std::simd::Simd")<T, LANES>], &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) where [Simd](https://doc.rust-lang.org/std/simd/struct.Simd.html "struct std::simd::Simd")<T, LANES>: [AsMut](https://doc.rust-lang.org/std/convert/trait.AsMut.html "trait std::convert::AsMut")<[[T; LANES]](https://doc.rust-lang.org/std/primitive.array.html)>, T: [SimdElement](https://doc.rust-lang.org/std/simd/trait.SimdElement.html "trait std::simd::SimdElement"), [LaneCount](https://doc.rust-lang.org/std/simd/struct.LaneCount.html "struct std::simd::LaneCount")<LANES>: [SupportedLaneCount](https://doc.rust-lang.org/std/simd/trait.SupportedLaneCount.html "trait std::simd::SupportedLaneCount"),

🔬This is a nightly-only experimental API. (`portable_simd` [#86656](https://github.com/rust-lang/rust/issues/86656))

Splits a mutable slice into a mutable prefix, a middle of aligned SIMD types,
and a mutable suffix.

This is a safe wrapper around [`slice::align_to_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.align_to_mut "method slice::align_to_mut"), so inherits the same
guarantees as that method.

This is the mutable version of [`slice::as_simd`](https://doc.rust-lang.org/std/primitive.slice.html#method.as_simd "method slice::as_simd"); see that for examples.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-49)Panics

This will panic if the size of the SIMD type is different from
`LANES` times that of the scalar.

At the time of writing, the trait restrictions on `Simd<T, LANES>` keeps
that from ever happening, as only power-of-two numbers of lanes are
supported. It’s possible that, in the future, those restrictions might
be lifted in a way that would make it possible to see panics from this
method for something like `LANES == 3`.

1.82.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4287-4289)

#### pub fn [is\_sorted](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.is_sorted)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where T: [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd"),

Checks if the elements of this slice are sorted.

That is, for each element `a` and its following element `b`, `a <= b` must hold. If the
slice yields exactly zero or one element, `true` is returned.

Note that if `Self::Item` is only `PartialOrd`, but not `Ord`, the above definition
implies that this function returns `false` if any two consecutive items are not
comparable.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-154)Examples

```
let empty: [i32; 0] = [];

assert!([1, 2, 2, 9].is_sorted());
assert!(![1, 3, 2, 4].is_sorted());
assert!([0].is_sorted());
assert!(empty.is_sorted());
assert!(![0.0, 1.0, f32::NAN].is_sorted());
```

1.82.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4330-4332)

#### pub fn [is\_sorted\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.is_sorted_by)<'a, F>(&'a self, compare: F) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&'a T](https://doc.rust-lang.org/std/primitive.reference.html), [&'a T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Checks if the elements of this slice are sorted using the given comparator function.

Instead of using `PartialOrd::partial_cmp`, this function uses the given `compare`
function to determine whether two elements are to be considered in sorted order.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-155)Examples

```
assert!([1, 2, 2, 9].is_sorted_by(|a, b| a <= b));
assert!(![1, 2, 2, 9].is_sorted_by(|a, b| a < b));

assert!([0].is_sorted_by(|a, b| true));
assert!([0].is_sorted_by(|a, b| false));

let empty: [i32; 0] = [];
assert!(empty.is_sorted_by(|a, b| false));
assert!(empty.is_sorted_by(|a, b| true));
```

1.82.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4354-4357)

#### pub fn [is\_sorted\_by\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.is_sorted_by_key)<'a, F, K>(&'a self, f: F) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&'a T](https://doc.rust-lang.org/std/primitive.reference.html)) -> K, K: [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd"),

Checks if the elements of this slice are sorted using the given key extraction function.

Instead of comparing the slice’s elements directly, this function compares the keys of the
elements, as determined by `f`. Apart from that, it’s equivalent to [`is_sorted`](https://doc.rust-lang.org/std/primitive.slice.html#method.is_sorted "method slice::is_sorted"); see its
documentation for more information.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-156)Examples

```
assert!(["c", "bb", "aaa"].is_sorted_by_key(|s| s.len()));
assert!(![-2i32, -1, 0, 3].is_sorted_by_key(|n| n.abs()));
```

1.52.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4413-4415)

#### pub fn [partition\_point](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.partition_point)<P>(&self, pred: P) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html) where P: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns the index of the partition point according to the given predicate
(the index of the first element of the second partition).

The slice is assumed to be partitioned according to the given predicate.
This means that all elements for which the predicate returns true are at the start of the slice
and all elements for which the predicate returns false are at the end.
For example, `[7, 15, 3, 5, 4, 12, 6]` is partitioned under the predicate `x % 2 != 0`
(all odd numbers are at the start, all even at the end).

If this slice is not partitioned, the returned result is unspecified and meaningless,
as this method performs a kind of binary search.

See also [`binary_search`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search "method slice::binary_search"), [`binary_search_by`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search_by "method slice::binary_search_by"), and [`binary_search_by_key`](https://doc.rust-lang.org/std/primitive.slice.html#method.binary_search_by_key "method slice::binary_search_by_key").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-157)Examples

```
let v = [1, 2, 3, 3, 5, 6, 7];
let i = v.partition_point(|&x| x < 5);

assert_eq!(i, 4);
assert!(v[..i].iter().all(|&x| x < 5));
assert!(v[i..].iter().all(|&x| !(x < 5)));
```

If all elements of the slice match the predicate, including if the slice
is empty, then the length of the slice will be returned:

```
let a = [2, 4, 8];
assert_eq!(a.partition_point(|x| x < &100), a.len());
let a: [i32; 0] = [];
assert_eq!(a.partition_point(|x| x < &100), 0);
```

If you want to insert an item to a sorted vector, while maintaining
sort order:

```
let mut s = vec![0, 1, 1, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
let num = 42;
let idx = s.partition_point(|&x| x <= num);
s.insert(idx, num);
assert_eq!(s, [0, 1, 1, 1, 1, 2, 3, 5, 8, 13, 21, 34, 42, 55]);
```

1.87.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4465-4468)

#### pub fn [split\_off](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_off-1)<'a, R>(self: &mut &'a [[T]](https://doc.rust-lang.org/std/primitive.slice.html), range: R) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&'a [[T]](https://doc.rust-lang.org/std/primitive.slice.html)> where R: [OneSidedRange](https://doc.rust-lang.org/std/ops/trait.OneSidedRange.html "trait std::ops::OneSidedRange")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Removes the subslice corresponding to the given range
and returns a reference to it.

Returns `None` and does not modify the slice if the given
range is out of bounds.

Note that this method only accepts one-sided ranges such as
`2..` or `..6`, but not `2..6`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-158)Examples

Splitting off the first three elements of a slice:

```
let mut slice: &[_] = &['a', 'b', 'c', 'd'];
let mut first_three = slice.split_off(..3).unwrap();

assert_eq!(slice, &['d']);
assert_eq!(first_three, &['a', 'b', 'c']);
```

Splitting off a slice starting with the third element:

```
let mut slice: &[_] = &['a', 'b', 'c', 'd'];
let mut tail = slice.split_off(2..).unwrap();

assert_eq!(slice, &['a', 'b']);
assert_eq!(tail, &['c', 'd']);
```

Getting `None` when `range` is out of bounds:

```
let mut slice: &[_] = &['a', 'b', 'c', 'd'];

assert_eq!(None, slice.split_off(5..));
assert_eq!(None, slice.split_off(..5));
assert_eq!(None, slice.split_off(..=4));
let expected: &[char] = &['a', 'b', 'c', 'd'];
assert_eq!(Some(expected), slice.split_off(..4));
```

1.87.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4531-4534)

#### pub fn [split\_off\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_off_mut)<'a, R>( self: &mut &'a mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html), range: R, ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&'a mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)> where R: [OneSidedRange](https://doc.rust-lang.org/std/ops/trait.OneSidedRange.html "trait std::ops::OneSidedRange")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Removes the subslice corresponding to the given range
and returns a mutable reference to it.

Returns `None` and does not modify the slice if the given
range is out of bounds.

Note that this method only accepts one-sided ranges such as
`2..` or `..6`, but not `2..6`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-159)Examples

Splitting off the first three elements of a slice:

```
let mut slice: &mut [_] = &mut ['a', 'b', 'c', 'd'];
let mut first_three = slice.split_off_mut(..3).unwrap();

assert_eq!(slice, &mut ['d']);
assert_eq!(first_three, &mut ['a', 'b', 'c']);
```

Splitting off a slice starting with the third element:

```
let mut slice: &mut [_] = &mut ['a', 'b', 'c', 'd'];
let mut tail = slice.split_off_mut(2..).unwrap();

assert_eq!(slice, &mut ['a', 'b']);
assert_eq!(tail, &mut ['c', 'd']);
```

Getting `None` when `range` is out of bounds:

```
let mut slice: &mut [_] = &mut ['a', 'b', 'c', 'd'];

assert_eq!(None, slice.split_off_mut(5..));
assert_eq!(None, slice.split_off_mut(..5));
assert_eq!(None, slice.split_off_mut(..=4));
let expected: &mut [_] = &mut ['a', 'b', 'c', 'd'];
assert_eq!(Some(expected), slice.split_off_mut(..4));
```

1.87.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4569)

#### pub fn [split\_off\_first](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_off_first)<'a>(self: &mut &'a [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a T](https://doc.rust-lang.org/std/primitive.reference.html)>

Removes the first element of the slice and returns a reference
to it.

Returns `None` if the slice is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-160)Examples

```
let mut slice: &[_] = &['a', 'b', 'c'];
let first = slice.split_off_first().unwrap();

assert_eq!(slice, &['b', 'c']);
assert_eq!(first, &'a');
```

1.87.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4594)

#### pub fn [split\_off\_first\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_off_first_mut)<'a>(self: &mut &'a mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

Removes the first element of the slice and returns a mutable
reference to it.

Returns `None` if the slice is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-161)Examples

```
let mut slice: &mut [_] = &mut ['a', 'b', 'c'];
let first = slice.split_off_first_mut().unwrap();
*first = 'd';

assert_eq!(slice, &['b', 'c']);
assert_eq!(first, &'d');
```

1.87.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4619)

#### pub fn [split\_off\_last](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_off_last)<'a>(self: &mut &'a [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a T](https://doc.rust-lang.org/std/primitive.reference.html)>

Removes the last element of the slice and returns a reference
to it.

Returns `None` if the slice is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-162)Examples

```
let mut slice: &[_] = &['a', 'b', 'c'];
let last = slice.split_off_last().unwrap();

assert_eq!(slice, &['a', 'b']);
assert_eq!(last, &'c');
```

1.87.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4644)

#### pub fn [split\_off\_last\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.split_off_last_mut)<'a>(self: &mut &'a mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

Removes the last element of the slice and returns a mutable
reference to it.

Returns `None` if the slice is empty.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-163)Examples

```
let mut slice: &mut [_] = &mut ['a', 'b', 'c'];
let last = slice.split_off_last_mut().unwrap();
*last = 'd';

assert_eq!(slice, &['a', 'b']);
assert_eq!(last, &'d');
```

1.86.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4701-4706)

#### pub unsafe fn [get\_disjoint\_unchecked\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.get_disjoint_unchecked_mut)<I, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>( &mut self, indices: [[I; N]](https://doc.rust-lang.org/std/primitive.array.html), ) -> [&mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output"); [N](https://doc.rust-lang.org/std/primitive.array.html)] where I: [GetDisjointMutIndex](https://doc.rust-lang.org/core/slice/trait.GetDisjointMutIndex.html "trait core::slice::GetDisjointMutIndex") + [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>,

Returns mutable references to many indices at once, without doing any checks.

An index can be either a `usize`, a [`Range`](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range") or a [`RangeInclusive`](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive"). Note
that this method takes an array, so all indices must be of the same type.
If passed an array of `usize`s this method gives back an array of mutable references
to single elements, while if passed an array of ranges it gives back an array of
mutable references to slices.

For a safe alternative see [`get_disjoint_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.get_disjoint_mut "method slice::get_disjoint_mut").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#safety-14)Safety

Calling this method with overlapping or out-of-bounds indices is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*
even if the resulting references are not used.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-164)Examples

```
let x = &mut [1, 2, 4];

unsafe {
    let [a, b] = x.get_disjoint_unchecked_mut([0, 2]);
    *a *= 10;
    *b *= 100;
}
assert_eq!(x, &[10, 2, 400]);

unsafe {
    let [a, b] = x.get_disjoint_unchecked_mut([0..1, 1..3]);
    a[0] = 8;
    b[0] = 88;
    b[1] = 888;
}
assert_eq!(x, &[8, 88, 888]);

unsafe {
    let [a, b] = x.get_disjoint_unchecked_mut([1..=2, 0..=0]);
    a[0] = 11;
    a[1] = 111;
    b[0] = 1;
}
assert_eq!(x, &[1, 11, 111]);
```

1.86.0 · [Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4768-4773)

#### pub fn [get\_disjoint\_mut](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.get_disjoint_mut)<I, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)>( &mut self, indices: [[I; N]](https://doc.rust-lang.org/std/primitive.array.html), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[&mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output"); [N](https://doc.rust-lang.org/std/primitive.array.html)], [GetDisjointMutError](https://doc.rust-lang.org/std/slice/enum.GetDisjointMutError.html "enum std::slice::GetDisjointMutError")> where I: [GetDisjointMutIndex](https://doc.rust-lang.org/core/slice/trait.GetDisjointMutIndex.html "trait core::slice::GetDisjointMutIndex") + [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>,

Returns mutable references to many indices at once.

An index can be either a `usize`, a [`Range`](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range") or a [`RangeInclusive`](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive"). Note
that this method takes an array, so all indices must be of the same type.
If passed an array of `usize`s this method gives back an array of mutable references
to single elements, while if passed an array of ranges it gives back an array of
mutable references to slices.

Returns an error if any index is out-of-bounds, or if there are overlapping indices.
An empty range is not considered to overlap if it is located at the beginning or at
the end of another range, but is considered to overlap if it is located in the middle.

This method does a O(n^2) check to check that there are no overlapping indices, so be careful
when passing many indices.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-165)Examples

```
let v = &mut [1, 2, 3];
if let Ok([a, b]) = v.get_disjoint_mut([0, 2]) {
    *a = 413;
    *b = 612;
}
assert_eq!(v, &[413, 2, 612]);

if let Ok([a, b]) = v.get_disjoint_mut([0..1, 1..3]) {
    a[0] = 8;
    b[0] = 88;
    b[1] = 888;
}
assert_eq!(v, &[8, 88, 888]);

if let Ok([a, b]) = v.get_disjoint_mut([1..=2, 0..=0]) {
    a[0] = 11;
    a[1] = 111;
    b[0] = 1;
}
assert_eq!(v, &[1, 11, 111]);
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4823)

#### pub fn [element\_offset](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.element_offset)(&self, element: [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

🔬This is a nightly-only experimental API. (`substr_range` [#126769](https://github.com/rust-lang/rust/issues/126769))

Returns the index that an element reference points to.

Returns `None` if `element` does not point to the start of an element within the slice.

This method is useful for extending slice iterators like [`slice::split`](https://doc.rust-lang.org/std/primitive.slice.html#method.split "method slice::split").

Note that this uses pointer arithmetic and **does not compare elements**.
To find the index of an element via comparison, use
[`.iter().position()`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.position "method std::iter::Iterator::position") instead.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-50)Panics

Panics if `T` is zero-sized.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-166)Examples

Basic usage:

```
#![feature(substr_range)]

let nums: &[u32] = &[1, 7, 1, 1];
let num = &nums[2];

assert_eq!(num, &1);
assert_eq!(nums.element_offset(num), Some(2));
```

Returning `None` with an unaligned element:

```
#![feature(substr_range)]

let arr: &[[u32; 2]] = &[[0, 1], [2, 3]];
let flat_arr: &[u32] = arr.as_flattened();

let ok_elm: &[u32; 2] = flat_arr[0..2].try_into().unwrap();
let weird_elm: &[u32; 2] = flat_arr[1..3].try_into().unwrap();

assert_eq!(ok_elm, &[0, 1]);
assert_eq!(weird_elm, &[1, 2]);

assert_eq!(arr.element_offset(ok_elm), Some(0)); // Points to element 0
assert_eq!(arr.element_offset(weird_elm), None); // Points between element 0 and 1
```

[Source](https://doc.rust-lang.org/src/core/slice/mod.rs.html#4877)

#### pub fn [subslice\_range](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.subslice_range)(&self, subslice: &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>>

🔬This is a nightly-only experimental API. (`substr_range` [#126769](https://github.com/rust-lang/rust/issues/126769))

Returns the range of indices that a subslice points to.

Returns `None` if `subslice` does not point within the slice or if it is not aligned with the
elements in the slice.

This method **does not compare elements**. Instead, this method finds the location in the slice that
`subslice` was obtained from. To find the index of a subslice via comparison, instead use
[`.windows()`](https://doc.rust-lang.org/std/primitive.slice.html#method.windows "method slice::windows")[`.position()`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.position "method std::iter::Iterator::position").

This method is useful for extending slice iterators like [`slice::split`](https://doc.rust-lang.org/std/primitive.slice.html#method.split "method slice::split").

Note that this may return a false positive (either `Some(0..0)` or `Some(self.len()..self.len())`)
if `subslice` has a length of zero and points to the beginning or end of another, separate, slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-51)Panics

Panics if `T` is zero-sized.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-167)Examples

Basic usage:

```
#![feature(substr_range)]

let nums = &[0, 5, 10, 0, 0, 5];

let mut iter = nums
    .split(|t| *t == 0)
    .map(|n| nums.subslice_range(n).unwrap());

assert_eq!(iter.next(), Some(0..0));
assert_eq!(iter.next(), Some(1..3));
assert_eq!(iter.next(), Some(4..4));
assert_eq!(iter.next(), Some(5..6));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#129-131)

#### pub fn [sort](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort)(&mut self) where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Sorts the slice in ascending order, preserving initial order of equal elements.

This sort is stable (i.e., does not reorder equal elements) and *O*(*n* \* log(*n*))
worst-case.

If the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `T` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), the function
may panic; even if the function exits normally, the resulting order of elements in the slice
is unspecified. See also the note on panicking below.

When applicable, unstable sorting is preferred because it is generally faster than stable
sorting and it doesn’t allocate auxiliary memory. See
[`sort_unstable`](https://doc.rust-lang.org/std/primitive.slice.html#method.sort_unstable "method slice::sort_unstable"). The exception are partially sorted slices, which
may be better served with `slice::sort`.

Sorting types that only implement [`PartialOrd`](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd") such as [`f32`](https://doc.rust-lang.org/std/primitive.f32.html "primitive f32") and [`f64`](https://doc.rust-lang.org/std/primitive.f64.html "primitive f64") require
additional precautions. For example, `f32::NAN != f32::NAN`, which doesn’t fulfill the
reflexivity requirement of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"). By using an alternative comparison function with
`slice::sort_by` such as [`f32::total_cmp`](https://doc.rust-lang.org/std/primitive.f32.html#method.total_cmp "method f32::total_cmp") or [`f64::total_cmp`](https://doc.rust-lang.org/std/primitive.f64.html#method.total_cmp "method f64::total_cmp") that defines a [total
order](https://en.wikipedia.org/wiki/Total_order) users can sort slices containing floating-point values. Alternatively, if all values
in the slice are guaranteed to be in a subset for which [`PartialOrd::partial_cmp`](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp "method std::cmp::PartialOrd::partial_cmp") forms a
[total order](https://en.wikipedia.org/wiki/Total_order), it’s possible to sort the slice with `sort_by(|a, b| a.partial_cmp(b).unwrap())`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-6)Current implementation

The current implementation is based on [driftsort](https://github.com/Voultapher/driftsort) by Orson Peters and Lukas Bergdoll, which
combines the fast average case of quicksort with the fast worst case and partial run
detection of mergesort, achieving linear time on fully sorted and reversed inputs. On inputs
with k distinct elements, the expected time to sort the data is *O*(*n* \* log(*k*)).

The auxiliary memory allocation behavior depends on the input length. Short slices are
handled without allocation, medium sized slices allocate `self.len()` and beyond that it
clamps at `self.len() / 2`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-52)Panics

May panic if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `T` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), or if
the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") implementation itself panics.

All safe functions on slices preserve the invariant that even if the function panics, all
original elements will remain in the slice and any possible modifications via interior
mutability are observed in the input. This ensures that recovery code (for instance inside
of a `Drop` or following a `catch_unwind`) will still have access to all the original
elements. For instance, if the slice belongs to a `Vec`, the `Vec::drop` method will be able
to dispose of all contained elements.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-168)Examples

```
let mut v = [4, -5, 1, -3, 2];

v.sort();
assert_eq!(v, [-5, -3, 1, 2, 4]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#190-192)

#### pub fn [sort\_by](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_by)<F>(&mut self, compare: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html), [&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering"),

Sorts the slice in ascending order with a comparison function, preserving initial order of
equal elements.

This sort is stable (i.e., does not reorder equal elements) and *O*(*n* \* log(*n*))
worst-case.

If the comparison function `compare` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), the function may
panic; even if the function exits normally, the resulting order of elements in the slice is
unspecified. See also the note on panicking below.

For example `|a, b| (a - b).cmp(a)` is a comparison function that is neither transitive nor
reflexive nor total, `a < b < c < a` with `a = 1, b = 2, c = 3`. For more information and
examples see the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") documentation.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-7)Current implementation

The current implementation is based on [driftsort](https://github.com/Voultapher/driftsort) by Orson Peters and Lukas Bergdoll, which
combines the fast average case of quicksort with the fast worst case and partial run
detection of mergesort, achieving linear time on fully sorted and reversed inputs. On inputs
with k distinct elements, the expected time to sort the data is *O*(*n* \* log(*k*)).

The auxiliary memory allocation behavior depends on the input length. Short slices are
handled without allocation, medium sized slices allocate `self.len()` and beyond that it
clamps at `self.len() / 2`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-53)Panics

May panic if `compare` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), or if `compare` itself panics.

All safe functions on slices preserve the invariant that even if the function panics, all
original elements will remain in the slice and any possible modifications via interior
mutability are observed in the input. This ensures that recovery code (for instance inside
of a `Drop` or following a `catch_unwind`) will still have access to all the original
elements. For instance, if the slice belongs to a `Vec`, the `Vec::drop` method will be able
to dispose of all contained elements.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-169)Examples

```
let mut v = [4, -5, 1, -3, 2];
v.sort_by(|a, b| a.cmp(b));
assert_eq!(v, [-5, -3, 1, 2, 4]);

// reverse sorting
v.sort_by(|a, b| b.cmp(a));
assert_eq!(v, [4, 2, 1, -3, -5]);
```

1.7.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#245-248)

#### pub fn [sort\_by\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_by_key)<K, F>(&mut self, f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> K, K: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Sorts the slice in ascending order with a key extraction function, preserving initial order
of equal elements.

This sort is stable (i.e., does not reorder equal elements) and *O*(*m* \* *n* \* log(*n*))
worst-case, where the key function is *O*(*m*).

If the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `K` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), the function
may panic; even if the function exits normally, the resulting order of elements in the slice
is unspecified. See also the note on panicking below.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-8)Current implementation

The current implementation is based on [driftsort](https://github.com/Voultapher/driftsort) by Orson Peters and Lukas Bergdoll, which
combines the fast average case of quicksort with the fast worst case and partial run
detection of mergesort, achieving linear time on fully sorted and reversed inputs. On inputs
with k distinct elements, the expected time to sort the data is *O*(*n* \* log(*k*)).

The auxiliary memory allocation behavior depends on the input length. Short slices are
handled without allocation, medium sized slices allocate `self.len()` and beyond that it
clamps at `self.len() / 2`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-54)Panics

May panic if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `K` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), or if
the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") implementation or the key-function `f` panics.

All safe functions on slices preserve the invariant that even if the function panics, all
original elements will remain in the slice and any possible modifications via interior
mutability are observed in the input. This ensures that recovery code (for instance inside
of a `Drop` or following a `catch_unwind`) will still have access to all the original
elements. For instance, if the slice belongs to a `Vec`, the `Vec::drop` method will be able
to dispose of all contained elements.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-170)Examples

```
let mut v = [4i32, -5, 1, -3, 2];

v.sort_by_key(|k| k.abs());
assert_eq!(v, [1, 2, -3, 4, -5]);
```

1.34.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#310-313)

#### pub fn [sort\_by\_cached\_key](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.sort_by_cached_key)<K, F>(&mut self, f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> K, K: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

Sorts the slice in ascending order with a key extraction function, preserving initial order
of equal elements.

This sort is stable (i.e., does not reorder equal elements) and *O*(*m* \* *n* + *n* \*
log(*n*)) worst-case, where the key function is *O*(*m*).

During sorting, the key function is called at most once per element, by using temporary
storage to remember the results of key evaluation. The order of calls to the key function is
unspecified and may change in future versions of the standard library.

If the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `K` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), the function
may panic; even if the function exits normally, the resulting order of elements in the slice
is unspecified. See also the note on panicking below.

For simple key functions (e.g., functions that are property accesses or basic operations),
[`sort_by_key`](https://doc.rust-lang.org/std/primitive.slice.html#method.sort_by_key "method slice::sort_by_key") is likely to be faster.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#current-implementation-9)Current implementation

The current implementation is based on [instruction-parallel-network sort](https://github.com/Voultapher/sort-research-rs/tree/main/ipnsort) by Lukas
Bergdoll, which combines the fast average case of randomized quicksort with the fast worst
case of heapsort, while achieving linear time on fully sorted and reversed inputs. And
*O*(*k* \* log(*n*)) where *k* is the number of distinct elements in the input. It leverages
superscalar out-of-order execution capabilities commonly found in CPUs, to efficiently
perform the operation.

In the worst case, the algorithm allocates temporary storage in a `Vec<(K, usize)>` the
length of the slice.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-55)Panics

May panic if the implementation of [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for `K` does not implement a [total order](https://en.wikipedia.org/wiki/Total_order), or if
the [`Ord`](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") implementation panics.

All safe functions on slices preserve the invariant that even if the function panics, all
original elements will remain in the slice and any possible modifications via interior
mutability are observed in the input. This ensures that recovery code (for instance inside
of a `Drop` or following a `catch_unwind`) will still have access to all the original
elements. For instance, if the slice belongs to a `Vec`, the `Vec::drop` method will be able
to dispose of all contained elements.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-171)Examples

```
let mut v = [4i32, -5, 1, -3, 2, 10];

// Strings are sorted by lexicographical order.
v.sort_by_cached_key(|k| k.to_string());
assert_eq!(v, [-3, -5, 1, 10, 2, 4]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#370-372)

#### pub fn [to\_vec](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.to_vec)(&self) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Copies `self` into a new `Vec`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-172)Examples

```
let s = [10, 40, 30];
let x = s.to_vec();
// Here, `s` and `x` can be modified independently.
```

[Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#394-396)

#### pub fn [to\_vec\_in](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.to_vec_in)<A>(&self, alloc: A) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

🔬This is a nightly-only experimental API. (`allocator_api` [#32838](https://github.com/rust-lang/rust/issues/32838))

Copies `self` into a new `Vec` with an allocator.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-173)Examples

```
#![feature(allocator_api)]

use std::alloc::System;

let s = [10, 40, 30];
let x = s.to_vec_in(System);
// Here, `s` and `x` can be modified independently.
```

1.40.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#505-507)

#### pub fn [repeat](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.repeat)(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

Creates a vector by copying a slice `n` times.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#panics-56)Panics

This function will panic if the capacity would overflow.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-174)Examples

```
assert_eq!([1, 2].repeat(3), vec![1, 2, 1, 2, 1, 2]);
```

A panic upon overflow:

[ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html "This example panics")

```
// this will panic at runtime
b"0123456789abcdef".repeat(usize::MAX);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#573-575)

#### pub fn [concat](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.concat)<Item>(&self) -> <[[T]](https://doc.rust-lang.org/std/primitive.slice.html) as [Concat](https://doc.rust-lang.org/std/slice/trait.Concat.html "trait std::slice::Concat")<Item>>::[Output](https://doc.rust-lang.org/std/slice/trait.Concat.html#associatedtype.Output "type std::slice::Concat::Output") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where [[T]](https://doc.rust-lang.org/std/primitive.slice.html): [Concat](https://doc.rust-lang.org/std/slice/trait.Concat.html "trait std::slice::Concat")<Item>, Item: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Flattens a slice of `T` into a single value `Self::Output`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-175)Examples

```
assert_eq!(["hello", "world"].concat(), "helloworld");
assert_eq!([[1, 2], [3, 4]].concat(), [1, 2, 3, 4]);
```

1.3.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#592-594)

#### pub fn [join](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.join)<Separator>( &self, sep: Separator, ) -> <[[T]](https://doc.rust-lang.org/std/primitive.slice.html) as [Join](https://doc.rust-lang.org/std/slice/trait.Join.html "trait std::slice::Join")<Separator>>::[Output](https://doc.rust-lang.org/std/slice/trait.Join.html#associatedtype.Output "type std::slice::Join::Output") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where [[T]](https://doc.rust-lang.org/std/primitive.slice.html): [Join](https://doc.rust-lang.org/std/slice/trait.Join.html "trait std::slice::Join")<Separator>,

Flattens a slice of `T` into a single value `Self::Output`, placing a
given separator between each.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-176)Examples

```
assert_eq!(["hello", "world"].join(" "), "hello world");
assert_eq!([[1, 2], [3, 4]].join(&0), [1, 2, 0, 3, 4]);
assert_eq!([[1, 2], [3, 4]].join(&[0, 0][..]), [1, 2, 0, 0, 3, 4]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#612-614)

#### pub fn [connect](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.connect)<Separator>( &self, sep: Separator, ) -> <[[T]](https://doc.rust-lang.org/std/primitive.slice.html) as [Join](https://doc.rust-lang.org/std/slice/trait.Join.html "trait std::slice::Join")<Separator>>::[Output](https://doc.rust-lang.org/std/slice/trait.Join.html#associatedtype.Output "type std::slice::Join::Output") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html) where [[T]](https://doc.rust-lang.org/std/primitive.slice.html): [Join](https://doc.rust-lang.org/std/slice/trait.Join.html "trait std::slice::Join")<Separator>,

👎Deprecated since 1.3.0: renamed to join

Flattens a slice of `T` into a single value `Self::Output`, placing a
given separator between each.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-177)Examples

```
assert_eq!(["hello", "world"].connect(" "), "hello world");
assert_eq!([[1, 2], [3, 4]].connect(&0), [1, 2, 0, 3, 4]);
```

## Trait Implementations[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#trait-implementations)

1.5.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4095)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-AsMut%3C%5BT%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [AsMut](https://doc.rust-lang.org/std/convert/trait.AsMut.html "trait std::convert::AsMut")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4096)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut-1)

#### fn [as\_mut](https://doc.rust-lang.org/std/convert/trait.AsMut.html#tymethod.as_mut)(&mut self) -> &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Converts this type into a mutable reference of the (usually inferred) input type.

1.5.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4081)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-AsMut%3CVec%3CT,+A%3E%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [AsMut](https://doc.rust-lang.org/std/convert/trait.AsMut.html "trait std::convert::AsMut")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4082)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_mut)

#### fn [as\_mut](https://doc.rust-lang.org/std/convert/trait.AsMut.html#tymethod.as_mut)(&mut self) -> &mut [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

Converts this type into a mutable reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4088)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-AsRef%3C%5BT%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4089)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ref-1)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4074)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-AsRef%3CVec%3CT,+A%3E%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4075)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.as_ref)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#787)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Borrow%3C%5BT%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#788)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#794)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-BorrowMut%3C%5BT%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/slice.rs.html#795)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3561)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Clone-for-Vec%3CT,+A%3E)

### impl<T, A> [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator") + [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3591)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clone_from)

#### fn [clone\_from](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)(&mut self, source: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>)

Overwrites the contents of `self` with a clone of the contents of `source`.

This method is preferred over simply assigning `source.clone()` to `self`,
as it avoids reallocation if possible. Additionally, if the element type
`T` overrides `clone_from()`, this will reuse the resources of `self`’s
elements as well.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-178)Examples

```
let x = vec![5, 6, 7];
let mut y = vec![8, 9, 10];
let yp: *const i32 = y.as_ptr();

y.clone_from(&x);

// The value is the same
assert_eq!(x, y);

// And no reallocation occurred
assert_eq!(yp, y.as_ptr());
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3563)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clone)

#### fn [clone](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)(&self) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

Returns a duplicate of the value. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4067)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Debug-for-Vec%3CT,+A%3E)

### impl<T, A> [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4068)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143894 "Tracking issue for const_default")) · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4057)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Default-for-Vec%3CT%3E)

### impl<T> [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4061)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.default)

#### fn [default](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default)() -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Creates an empty `Vec<T>`.

The vector will not allocate until elements are pushed onto it.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3539)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Deref-for-Vec%3CT,+A%3E)

### impl<T, A> [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3540)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Target)

#### type [Target](https://doc.rust-lang.org/std/ops/trait.Deref.html#associatedtype.Target) = [[T]](https://doc.rust-lang.org/std/primitive.slice.html)

The resulting type after dereferencing.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3543)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.deref)

#### fn [deref](https://doc.rust-lang.org/std/ops/trait.Deref.html#tymethod.deref)(&self) -> &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Dereferences the value.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3549)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-DerefMut-for-Vec%3CT,+A%3E)

### impl<T, A> [DerefMut](https://doc.rust-lang.org/std/ops/trait.DerefMut.html "trait std::ops::DerefMut") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3551)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.deref_mut)

#### fn [deref\_mut](https://doc.rust-lang.org/std/ops/trait.DerefMut.html#tymethod.deref_mut)(&mut self) -> &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Mutably dereferences the value.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4043)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Drop-for-Vec%3CT,+A%3E)

### impl<T, A> [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html "trait std::ops::Drop") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4044)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.drop)

#### fn [drop](https://doc.rust-lang.org/std/ops/trait.Drop.html#tymethod.drop)(&mut self)

Executes the destructor for this type. [Read more](https://doc.rust-lang.org/std/ops/trait.Drop.html#tymethod.drop)

1.2.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3987)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Extend%3C%26T%3E-for-Vec%3CT,+A%3E)

### impl<'a, T, A> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<[&'a T](https://doc.rust-lang.org/std/primitive.reference.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy") + 'a, A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

Extend implementation that copies elements out of references before pushing them onto the Vec.

This implementation is specialized for slice iterators, where it uses [`copy_from_slice`](https://doc.rust-lang.org/std/primitive.slice.html#method.copy_from_slice "method slice::copy_from_slice") to
append the entire slice at once.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3989)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend-1)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [&'a T](https://doc.rust-lang.org/std/primitive.reference.html)>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3995)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_one-1)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, \_: [&'a T](https://doc.rust-lang.org/std/primitive.reference.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4001)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_reserve-1)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3748)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Extend%3CT%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<T> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3751)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = T>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3757)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_one)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, item: T)

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3763)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.extend_reserve)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4103)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3C%26%5BT%5D%3E-for-Vec%3CT%3E)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[[T]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4112)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-12)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Allocates a `Vec<T>` and fills it by cloning `s`’s items.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-181)Examples

```
assert_eq!(Vec::from(&[1, 2, 3][..]), vec![1, 2, 3]);
```

1.74.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4135)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3C%26%5BT;+N%5D%3E-for-Vec%3CT%3E)

### impl<T, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4144)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-14)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Allocates a `Vec<T>` and fills it by cloning `s`’s items.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-183)Examples

```
assert_eq!(Vec::from(&[1, 2, 3]), vec![1, 2, 3]);
```

1.28.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/cow.rs.html#44)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3C%26Vec%3CT%3E%3E-for-Cow%3C'a,+%5BT%5D%3E)

### impl<'a, T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&'a [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [[T]](https://doc.rust-lang.org/std/primitive.slice.html)> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/cow.rs.html#51)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-11)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: &'a [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [[T]](https://doc.rust-lang.org/std/primitive.slice.html)>

Creates a [`Borrowed`](https://doc.rust-lang.org/std/borrow/enum.Cow.html#variant.Borrowed "variant std::borrow::Cow::Borrowed") variant of [`Cow`](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")
from a reference to [`Vec`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec").

This conversion does not allocate or clone the data.

1.19.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4119)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3C%26mut+%5BT%5D%3E-for-Vec%3CT%3E)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4128)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-13)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Allocates a `Vec<T>` and fills it by cloning `s`’s items.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-182)Examples

```
assert_eq!(Vec::from(&mut [1, 2, 3][..]), vec![1, 2, 3]);
```

1.74.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4151)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3C%26mut+%5BT;+N%5D%3E-for-Vec%3CT%3E)

### impl<T, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&mut [[T; N]](https://doc.rust-lang.org/std/primitive.array.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4160)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-15)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &mut [[T; N]](https://doc.rust-lang.org/std/primitive.array.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Allocates a `Vec<T>` and fills it by cloning `s`’s items.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-184)Examples

```
assert_eq!(Vec::from(&mut [1, 2, 3]), vec![1, 2, 3]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4255)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3C%26str%3E-for-Vec%3Cu8%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4264)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-20)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Allocates a `Vec<u8>` and fills it with a UTF-8 string.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-189)Examples

```
assert_eq!(Vec::from("123"), vec![b'1', b'2', b'3']);
```

1.44.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4167)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3C%5BT;+N%5D%3E-for-Vec%3CT%3E)

### impl<T, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4176)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-16)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [[T; N]](https://doc.rust-lang.org/std/primitive.array.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Allocates a `Vec<T>` and moves `s`’s items into it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-185)Examples

```
assert_eq!(Vec::from([1, 2, 3]), vec![1, 2, 3]);
```

1.5.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/binary_heap/mod.rs.html#1886)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CBinaryHeap%3CT,+A%3E%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[BinaryHeap](https://doc.rust-lang.org/std/collections/struct.BinaryHeap.html "struct std::collections::BinaryHeap")<T, A>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/collections/binary_heap/mod.rs.html#1891)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-2)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(heap: [BinaryHeap](https://doc.rust-lang.org/std/collections/struct.BinaryHeap.html "struct std::collections::BinaryHeap")<T, A>) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

Converts a `BinaryHeap<T>` into a `Vec<T>`.

This conversion requires no data movement or allocation, and has
constant time complexity.

1.18.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4208)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CBox%3C%5BT%5D,+A%3E%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4218)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-18)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A>) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

Converts a boxed slice into a vector by transferring ownership of
the existing heap allocation.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-187)Examples

```
let b: Box<[i32]> = vec![1, 2, 3].into_boxed_slice();
assert_eq!(Vec::from(b), vec![1, 2, 3]);
```

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#214)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CByteString%3E-for-Vec%3Cu8%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#216)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Converts to this type from the input type.

1.7.0 · [Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#727)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CCString%3E-for-Vec%3Cu8%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString")> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#732)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-5)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString")) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Converts a [`CString`](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString") into a `Vec<u8>`.

The conversion consumes the [`CString`](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString"), and removes the terminating NUL byte.

1.14.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4182-4184)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CCow%3C'a,+%5BT%5D%3E%3E-for-Vec%3CT%3E)

### impl<'a, T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [[T]](https://doc.rust-lang.org/std/primitive.slice.html)>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where [[T]](https://doc.rust-lang.org/std/primitive.slice.html): [ToOwned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html "trait std::borrow::ToOwned")<Owned = [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>>,

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4201)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-17)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [[T]](https://doc.rust-lang.org/std/primitive.slice.html)>) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Converts a clone-on-write slice into a vector.

If `s` already owns a `Vec<T>`, it will be returned directly.
If `s` is borrowing a slice, a new `Vec<T>` will be allocated and
filled by cloning `s`’s items into it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-186)Examples

```
let o: Cow<'_, [i32]> = Cow::Owned(vec![1, 2, 3]);
let b: Cow<'_, [i32]> = Cow::Borrowed(&[1, 2, 3]);
assert_eq!(Vec::from(o), Vec::from(b));
```

1.14.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3201)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CString%3E-for-Vec%3Cu8%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3214)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-8)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(string: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Converts the given [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") to a vector [`Vec`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec") that holds values of type [`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-180)Examples

```
let s1 = String::from("hello world");
let v1 = Vec::from(s1);

for b in v1 {
    println!("{b}");
}
```

1.43.0 · [Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#807)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVec%3CNonZero%3Cu8%3E%3E%3E-for-CString)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[NonZero](https://doc.rust-lang.org/std/num/struct.NonZero.html "struct std::num::NonZero")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>>> for [CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString")

[Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#811)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-6)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[NonZero](https://doc.rust-lang.org/std/num/struct.NonZero.html "struct std::num::NonZero")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>>) -> [CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString")

Converts a `Vec<NonZero<u8>>` into a [`CString`](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString") without
copying nor checking for inner nul bytes.

1.8.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/cow.rs.html#31)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVec%3CT%3E%3E-for-Cow%3C'a,+%5BT%5D%3E)

### impl<'a, T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [[T]](https://doc.rust-lang.org/std/primitive.slice.html)> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/cow.rs.html#38)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-10)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [[T]](https://doc.rust-lang.org/std/primitive.slice.html)>

Creates an [`Owned`](https://doc.rust-lang.org/std/borrow/enum.Cow.html#variant.Owned "variant std::borrow::Cow::Owned") variant of [`Cow`](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")
from an owned instance of [`Vec`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec").

This conversion does not allocate or clone the data.

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3838)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVec%3CT,+A%3E%3E-for-Arc%3C%5BT%5D,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator") + [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3850)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-9)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>) -> [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A>

Allocates a reference-counted slice and moves `v`’s items into it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#example-2)Example

```
let unique: Vec<i32> = vec![1, 2, 3];
let shared: Arc<[i32]> = Arc::from(unique);
assert_eq!(&[1, 2, 3], &shared[..]);
```

1.5.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/binary_heap/mod.rs.html#1858)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVec%3CT,+A%3E%3E-for-BinaryHeap%3CT,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [BinaryHeap](https://doc.rust-lang.org/std/collections/struct.BinaryHeap.html "struct std::collections::BinaryHeap")<T, A> where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/collections/binary_heap/mod.rs.html#1862)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-1)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(vec: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>) -> [BinaryHeap](https://doc.rust-lang.org/std/collections/struct.BinaryHeap.html "struct std::collections::BinaryHeap")<T, A>

Converts a `Vec<T>` into a `BinaryHeap<T>`.

This conversion happens in-place, and has *O*(*n*) time complexity.

1.20.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4226)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVec%3CT,+A%3E%3E-for-Box%3C%5BT%5D,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4248)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-19)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A>

Converts a vector into a boxed slice.

Before doing the conversion, this method discards excess capacity like [`Vec::shrink_to_fit`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to_fit "method std::vec::Vec::shrink_to_fit").

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-188)Examples

```
assert_eq!(Box::from(vec![1, 2, 3]), vec![1, 2, 3].into_boxed_slice());
```

Any excess capacity is removed:

```
let mut vec = Vec::with_capacity(10);
vec.extend([1, 2, 3]);

assert_eq!(Box::from(vec), vec![1, 2, 3].into_boxed_slice());
```

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2813)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVec%3CT,+A%3E%3E-for-Rc%3C%5BT%5D,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2825)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-7)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>) -> [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html), A>

Allocates a reference-counted slice and moves `v`’s items into it.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#example-1)Example

```
let unique: Vec<i32> = vec![1, 2, 3];
let shared: Rc<[i32]> = Rc::from(unique);
assert_eq!(&[1, 2, 3], &shared[..]);
```

1.10.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/mod.rs.html#3206)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVec%3CT,+A%3E%3E-for-VecDeque%3CT,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [VecDeque](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/mod.rs.html#3216)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-3)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(other: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>) -> [VecDeque](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque")<T, A>

Turn a [`Vec<T>`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec") into a [`VecDeque<T>`](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque").

This conversion is guaranteed to run in *O*(1) time
and to not re-allocate the `Vec`’s buffer or allocate
any additional memory.

1.10.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/mod.rs.html#3223)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CVecDeque%3CT,+A%3E%3E-for-Vec%3CT,+A%3E)

### impl<T, A> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[VecDeque](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque")<T, A>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/mod.rs.html#3253)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-4)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(other: [VecDeque](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque")<T, A>) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

Turn a [`VecDeque<T>`](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque") into a [`Vec<T>`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec").

This never needs to re-allocate, but does need to do *O*(*n*) data movement if
the circular buffer doesn’t happen to be at the beginning of the allocation.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-179)Examples

```
use std::collections::VecDeque;

// This one is *O*(1).
let deque: VecDeque<_> = (1..5).collect();
let ptr = deque.as_slices().0.as_ptr();
let vec = Vec::from(deque);
assert_eq!(vec, [1, 2, 3, 4]);
assert_eq!(vec.as_ptr(), ptr);

// This one needs data rearranging.
let mut deque: VecDeque<_> = (1..5).collect();
deque.push_front(9);
deque.push_front(8);
let ptr = deque.as_slices().1.as_ptr();
let vec = Vec::from(deque);
assert_eq!(vec, [8, 9, 1, 2, 3, 4]);
assert_eq!(vec.as_ptr(), ptr);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3679)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-FromIterator%3CT%3E-for-Vec%3CT%3E)

### impl<T> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<T> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

Collects an iterator into a Vec, commonly called via [`Iterator::collect()`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.collect "method std::iter::Iterator::collect")

#### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#allocation-behavior)Allocation behavior

In general `Vec` does not guarantee any particular growth or allocation strategy.
That also applies to this trait impl.

**Note:** This section covers implementation details and is therefore exempt from
stability guarantees.

Vec may use any or none of the following strategies,
depending on the supplied iterator:

* preallocate based on [`Iterator::size_hint()`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.size_hint "method std::iter::Iterator::size_hint")
  + and panic if the number of items is outside the provided lower/upper bounds
* use an amortized growth strategy similar to `pushing` one item at a time
* perform the iteration in-place on the original allocation backing the iterator

The last case warrants some attention. It is an optimization that in many cases reduces peak memory
consumption and improves cache locality. But when big, short-lived allocations are created,
only a small fraction of their items get collected, no further use is made of the spare capacity
and the resulting `Vec` is moved into a longer-lived structure, then this can lead to the large
allocations having their lifetimes unnecessarily extended which can result in increased memory
footprint.

In cases where this is an issue, the excess capacity can be discarded with [`Vec::shrink_to()`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to "method std::vec::Vec::shrink_to"),
[`Vec::shrink_to_fit()`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.shrink_to_fit "method std::vec::Vec::shrink_to_fit") or by collecting into [`Box<[T]>`](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box") instead, which additionally reduces
the size of the long-lived struct.

```
static LONG_LIVED: Mutex<Vec<Vec<u16>>> = Mutex::new(Vec::new());

for i in 0..10 {
    let big_temporary: Vec<u16> = (0..1024).collect();
    // discard most items
    let mut result: Vec<_> = big_temporary.into_iter().filter(|i| i % 100 == 0).collect();
    // without this a lot of unused capacity might be moved into the global
    result.shrink_to_fit();
    LONG_LIVED.lock().unwrap().push(result);
}
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3682)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_iter)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T> where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = T>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3608)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Hash-for-Vec%3CT,+A%3E)

### impl<T, A> [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

The hash of a vector is the same as that of the corresponding slice,
as required by the `core::borrow::Borrow` implementation.

```
use std::hash::BuildHasher;

let b = std::hash::RandomState::new();
let v: Vec<u8> = vec![0xa8, 0x3c, 0x09];
let s: &[u8] = &[0xa8, 0x3c, 0x09];
assert_eq!(b.hash_one(v), b.hash_one(s));
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3610)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.hash)

#### fn [hash](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)<H>(&self, state: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"),

Feeds this value into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)

1.3.0 · [Source](https://doc.rust-lang.org/src/core/hash/mod.rs.html#235-237)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.hash_slice)

#### fn [hash\_slice](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)<H>(data: &[Self], state: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"), Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Feeds a slice of this type into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3616)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Index%3CI%3E-for-Vec%3CT,+A%3E)

### impl<T, I, A> [Index](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index")<I> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>, A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3617)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Output)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Index.html#associatedtype.Output) = <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

The returned type after indexing.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3620)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.index)

#### fn [index](https://doc.rust-lang.org/std/ops/trait.Index.html#tymethod.index)(&self, index: I) -> &<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> as [Index](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index")<I>>::[Output](https://doc.rust-lang.org/std/ops/trait.Index.html#associatedtype.Output "type std::ops::Index::Output") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Performs the indexing (`container[index]`) operation. [Read more](https://doc.rust-lang.org/std/ops/trait.Index.html#tymethod.index)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3626)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-IndexMut%3CI%3E-for-Vec%3CT,+A%3E)

### impl<T, I, A> [IndexMut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html "trait std::ops::IndexMut")<I> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[[T]](https://doc.rust-lang.org/std/primitive.slice.html)>, A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3628)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.index_mut)

#### fn [index\_mut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html#tymethod.index_mut)(&mut self, index: I) -> &mut <[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> as [Index](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index")<I>>::[Output](https://doc.rust-lang.org/std/ops/trait.Index.html#associatedtype.Output "type std::ops::Index::Output") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Performs the mutable indexing (`container[index]`) operation. [Read more](https://doc.rust-lang.org/std/ops/trait.IndexMut.html#tymethod.index_mut)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3727)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-IntoIterator-for-%26Vec%3CT,+A%3E)

### impl<'a, T, A> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for &'a [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3728)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Item-1)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = [&'a T](https://doc.rust-lang.org/std/primitive.reference.html)

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3729)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.IntoIter-1)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [Iter](https://doc.rust-lang.org/std/slice/struct.Iter.html "struct std::slice::Iter")<'a, T>

Which kind of iterator are we turning this into?

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3731)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_iter-1)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> <&'a [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> as [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")>::[IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter "type std::iter::IntoIterator::IntoIter") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Creates an iterator from a value. [Read more](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3737)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-IntoIterator-for-%26mut+Vec%3CT,+A%3E)

### impl<'a, T, A> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for &'a mut [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3738)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Item-2)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = [&'a mut T](https://doc.rust-lang.org/std/primitive.reference.html)

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3739)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.IntoIter-2)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [IterMut](https://doc.rust-lang.org/std/slice/struct.IterMut.html "struct std::slice::IterMut")<'a, T>

Which kind of iterator are we turning this into?

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3741)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_iter-2)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> <&'a mut [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> as [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")>::[IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter "type std::iter::IntoIterator::IntoIter") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Creates an iterator from a value. [Read more](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3688)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-IntoIterator-for-Vec%3CT,+A%3E)

### impl<T, A> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3709)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_iter)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> <[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> as [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")>::[IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter "type std::iter::IntoIterator::IntoIter") [ⓘ](https://doc.rust-lang.org/std/vec/struct.Vec.html)

Creates a consuming iterator, that is, one that moves each value out of
the vector (from start to end). The vector cannot be used after calling
this.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-193)Examples

```
let v = vec!["a".to_string(), "b".to_string()];
let mut v_iter = v.into_iter();

let first_element: Option<String> = v_iter.next();

assert_eq!(first_element, Some("a".to_string()));
assert_eq!(v_iter.next(), Some("b".to_string()));
assert_eq!(v_iter.next(), None);
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3689)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Item)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = T

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3690)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.IntoIter)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [IntoIter](https://doc.rust-lang.org/std/vec/struct.IntoIter.html "struct std::vec::IntoIter")<T, A>

Which kind of iterator are we turning this into?

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4035)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Ord-for-Vec%3CT,+A%3E)

### impl<T, A> [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

Implements ordering of vectors, [lexicographically](https://doc.rust-lang.org/std/cmp/trait.Ord.html#lexicographical-comparison "trait std::cmp::Ord").

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4037)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.cmp)

#### fn [cmp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")

This method returns an [`Ordering`](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering") between `self` and `other`. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1023-1025)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.max)

#### fn [max](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the maximum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1062-1064)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.min)

#### fn [min](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the minimum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)

1.50.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1088-1090)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clamp)

#### fn [clamp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)(self, min: Self, max: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Restrict a value to a certain interval. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#23)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3C%26%5BU%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&[[U]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#23)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-6)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&[[U]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#23)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-6)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &&[[U]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#36)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3C%26%5BU;+N%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, U, A, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&[[U; N]](https://doc.rust-lang.org/std/primitive.array.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#36)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-14)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&[[U; N]](https://doc.rust-lang.org/std/primitive.array.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#36)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-14)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &&[[U; N]](https://doc.rust-lang.org/std/primitive.array.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#24)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3C%26mut+%5BU%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&mut [[U]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#24)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-7)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&mut [[U]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#24)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-7)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &&mut [[U]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.48.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#27)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3C%5BU%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[[U]](https://doc.rust-lang.org/std/primitive.slice.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#27)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-10)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[[U]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#27)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-10)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[[U]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#35)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3C%5BU;+N%5D%3E-for-Vec%3CT,+A%3E)

### impl<T, U, A, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[[U; N]](https://doc.rust-lang.org/std/primitive.array.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#35)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-13)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[[U; N]](https://doc.rust-lang.org/std/primitive.array.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#35)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-13)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[[U; N]](https://doc.rust-lang.org/std/primitive.array.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#667)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CByteStr%3E-for-Vec%3Cu8%3E)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#667)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-3)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-3)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#523)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CByteString%3E-for-Vec%3Cu8%3E)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#523)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-1)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-1)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.46.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#25)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3CU,+A%3E%3E-for-%26%5BT%5D)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>> for &[[T]](https://doc.rust-lang.org/std/primitive.slice.html) where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#25)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-8)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#25)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-8)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.46.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#26)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3CU,+A%3E%3E-for-%26mut+%5BT%5D)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>> for &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html) where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#26)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-9)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#26)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-9)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.48.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#28)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3CU,+A%3E%3E-for-%5BT%5D)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>> for [[T]](https://doc.rust-lang.org/std/primitive.slice.html) where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#28)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-11)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#28)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-11)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#30)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3CU,+A%3E%3E-for-Cow%3C'_,+%5BT%5D%3E)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'\_, [[T]](https://doc.rust-lang.org/std/primitive.slice.html)> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U> + [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#30)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-12)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#30)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-12)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.17.0 · [Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/mod.rs.html#3048)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3CU,+A%3E%3E-for-VecDeque%3CT,+A%3E)

### impl<T, U, A> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>> for [VecDeque](https://doc.rust-lang.org/std/collections/struct.VecDeque.html "struct std::collections::VecDeque")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/collections/vec_deque/mod.rs.html#3048)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-4)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-4)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#22)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3CU,+A2%3E%3E-for-Vec%3CT,+A1%3E)

### impl<T, U, A1, A2> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A2>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A1> where A1: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), A2: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<U>,

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#22)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-5)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A2>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/vec/partial_eq.rs.html#22)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-5)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<U, A2>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#667)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3Cu8%3E%3E-for-ByteStr)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>> for [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#667)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq-2)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne-2)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#523)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialEq%3CVec%3Cu8%3E%3E-for-ByteString)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>> for [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#523)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.eq)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ne)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4018-4022)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-PartialOrd%3CVec%3CT,+A2%3E%3E-for-Vec%3CT,+A1%3E)

### impl<T, A1, A2> [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A2>> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A1> where T: [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd"), A1: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"), A2: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

Implements comparison of vectors, [lexicographically](https://doc.rust-lang.org/std/cmp/trait.Ord.html#lexicographical-comparison "trait std::cmp::Ord").

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4025)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.partial_cmp)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A2>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.lt)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.le)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.gt)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.ge)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.66.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#313)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-TryFrom%3CVec%3CT%3E%3E-for-Box%3C%5BT;+N%5D%3E)

### impl<T, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#334)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( vec: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>, ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)>, <[Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[T; N]](https://doc.rust-lang.org/std/primitive.array.html)> as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Attempts to convert a `Vec<T>` into a `Box<[T; N]>`.

Like [`Vec::into_boxed_slice`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into_boxed_slice "method std::vec::Vec::into_boxed_slice"), this is in-place if `vec.capacity() == N`,
but will require a reallocation otherwise.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#errors-4)Errors

Returns the original `Vec<T>` in the `Err` variant if
`boxed_slice.len()` does not equal `N`.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-190)Examples

This can be used with [`vec!`](https://doc.rust-lang.org/std/macro.vec.html "macro std::vec") to create an array on the heap:

```
let state: Box<[f32; 100]> = vec![1.0; 100].try_into().unwrap();
assert_eq!(state.len(), 100);
```

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#314)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T>

The type returned in the event of a conversion error.

1.48.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4270)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-TryFrom%3CVec%3CT,+A%3E%3E-for-%5BT;+N%5D)

### impl<T, A, const N: [usize](https://doc.rust-lang.org/std/primitive.usize.html)> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>> for [[T; N]](https://doc.rust-lang.org/std/primitive.array.html) where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4299)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_from-2)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(vec: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[[T; N]](https://doc.rust-lang.org/std/primitive.array.html), [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>>

Gets the entire contents of the `Vec<T>` as an array,
if its size exactly matches that of the requested array.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-192)Examples

```
assert_eq!(vec![1, 2, 3].try_into(), Ok([1, 2, 3]));
assert_eq!(<Vec<i32>>::new().try_into(), Ok([]));
```

If the length doesn’t match, the input comes back in `Err`:

```
let r: Result<[i32; 4], _> = (0..10).collect::<Vec<_>>().try_into();
assert_eq!(r, Err(vec![0, 1, 2, 3, 4, 5, 6, 7, 8, 9]));
```

If you’re fine with just getting a prefix of the `Vec<T>`,
you can call [`.truncate(N)`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.truncate "method std::vec::Vec::truncate") first.

```
let mut v = String::from("hello world").into_bytes();
v.sort();
v.truncate(2);
let [a, b]: [_; 2] = v.try_into().unwrap();
assert_eq!(a, b' ');
assert_eq!(b, b'd');
```

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4271)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Error-2)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A>

The type returned in the event of a conversion error.

1.87.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3220)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-TryFrom%3CVec%3Cu8%3E%3E-for-String)

### impl [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3232)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_from-1)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( bytes: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>, ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), <[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Converts the given [`Vec<u8>`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec") into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") if it contains valid UTF-8 data.

##### [§](https://doc.rust-lang.org/std/vec/struct.Vec.html#examples-191)Examples

```
let s1 = b"hello world".to_vec();
let v1 = String::try_from(s1).unwrap();
assert_eq!(v1, "hello world");
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3221)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [FromUtf8Error](https://doc.rust-lang.org/std/string/struct.FromUtf8Error.html "struct std::string::FromUtf8Error")

The type returned in the event of a conversion error.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/impls.rs.html#480-518)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Write-for-Vec%3Cu8,+A%3E)

### impl<A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator")> [Write](https://doc.rust-lang.org/std/io/trait.Write.html "trait std::io::Write") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html), A>

Write is implemented for `Vec<u8>` by appending to the vector.
The vector will grow as needed.

[Source](https://doc.rust-lang.org/src/std/io/impls.rs.html#482-485)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.write)

#### fn [write](https://doc.rust-lang.org/std/io/trait.Write.html#tymethod.write)(&mut self, buf: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Writes a buffer into this writer, returning how many bytes were written. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#tymethod.write)

[Source](https://doc.rust-lang.org/src/std/io/impls.rs.html#488-495)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.write_vectored)

#### fn [write\_vectored](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_vectored)(&mut self, bufs: &[[IoSlice](https://doc.rust-lang.org/std/io/struct.IoSlice.html "struct std::io::IoSlice")<'\_>]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Like [`write`](https://doc.rust-lang.org/std/io/trait.Write.html#tymethod.write "method std::io::Write::write"), except that it writes from a slice of buffers. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_vectored)

[Source](https://doc.rust-lang.org/src/std/io/impls.rs.html#498-500)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.is_write_vectored)

#### fn [is\_write\_vectored](https://doc.rust-lang.org/std/io/trait.Write.html#method.is_write_vectored)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`can_vector` [#69941](https://github.com/rust-lang/rust/issues/69941))

Determines if this `Write`r has an efficient [`write_vectored`](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_vectored "method std::io::Write::write_vectored")
implementation. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#method.is_write_vectored)

[Source](https://doc.rust-lang.org/src/std/io/impls.rs.html#503-506)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.write_all)

#### fn [write\_all](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_all)(&mut self, buf: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

Attempts to write an entire buffer into this writer. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_all)

[Source](https://doc.rust-lang.org/src/std/io/impls.rs.html#509-512)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.write_all_vectored)

#### fn [write\_all\_vectored](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_all_vectored)(&mut self, bufs: &mut [[IoSlice](https://doc.rust-lang.org/std/io/struct.IoSlice.html "struct std::io::IoSlice")<'\_>]) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

🔬This is a nightly-only experimental API. (`write_all_vectored` [#70436](https://github.com/rust-lang/rust/issues/70436))

Attempts to write multiple buffers into this writer. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_all_vectored)

[Source](https://doc.rust-lang.org/src/std/io/impls.rs.html#515-517)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.flush)

#### fn [flush](https://doc.rust-lang.org/std/io/trait.Write.html#tymethod.flush)(&mut self) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

Flushes this output stream, ensuring that all intermediately buffered
contents reach their destination. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#tymethod.flush)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1950-1956)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.write_fmt)

#### fn [write\_fmt](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_fmt)(&mut self, args: [Arguments](https://doc.rust-lang.org/std/fmt/struct.Arguments.html "struct std::fmt::Arguments")<'\_>) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>

Writes a formatted string into this writer, returning any error
encountered. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#method.write_fmt)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/io/mod.rs.html#1980-1985)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.by_ref)

#### fn [by\_ref](https://doc.rust-lang.org/std/io/trait.Write.html#method.by_ref)(&mut self) -> &mut Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Creates a “by reference” adapter for this instance of `Write`. [Read more](https://doc.rust-lang.org/std/io/trait.Write.html#method.by_ref)

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#3557)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-DerefPure-for-Vec%3CT,+A%3E)

### impl<T, A> [DerefPure](https://doc.rust-lang.org/std/ops/trait.DerefPure.html "trait std::ops::DerefPure") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4031)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Eq-for-Vec%3CT,+A%3E)

### impl<T, A> [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where T: [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq"), A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Freeze-for-Vec%3CT,+A%3E)

### impl<T, A> [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze"),

[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-RefUnwindSafe-for-Vec%3CT,+A%3E)

### impl<T, A> [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe"), T: [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe"),

[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Send-for-Vec%3CT,+A%3E)

### impl<T, A> [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send"), T: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send"),

[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Sync-for-Vec%3CT,+A%3E)

### impl<T, A> [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync"), T: [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync"),

[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Unpin-for-Vec%3CT,+A%3E)

### impl<T, A> [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin"), T: [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin"),

[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-UnwindSafe-for-Vec%3CT,+A%3E)

### impl<T, A> [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<T, A> where A: [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe"), T: [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe"),

## Blanket Implementations[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.borrow-1)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.borrow_mut-1)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#515)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-CloneToUninit-for-T)

### impl<T> [CloneToUninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html "trait std::clone::CloneToUninit") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#517)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clone_to_uninit)

#### unsafe fn [clone\_to\_uninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)(&self, dest: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html))

🔬This is a nightly-only experimental API. (`clone_to_uninit` [#126799](https://github.com/rust-lang/rust/issues/126799))

Performs copy-assignment from `self` to `dest`. [Read more](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#785)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-From%3CT%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#788)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from-21)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: T) -> T

Returns the argument unchanged.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#767-769)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Into%3CU%3E-for-T)

### impl<T, U> [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<U> for T where U: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#777)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.into)

#### fn [into](https://doc.rust-lang.org/std/convert/trait.Into.html#tymethod.into)(self) -> U

Calls `U::from(self)`.

That is, this conversion is whatever the implementation of
`From<T> for U` chooses to do.

[Source](https://doc.rust-lang.org/src/core/ops/deref.rs.html#378-380)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-Receiver-for-P)

### impl<P, T> [Receiver](https://doc.rust-lang.org/std/ops/trait.Receiver.html "trait std::ops::Receiver") for P where P: [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")<Target = T> + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/ops/deref.rs.html#382)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Target-1)

#### type [Target](https://doc.rust-lang.org/std/ops/trait.Receiver.html#associatedtype.Target) = T

🔬This is a nightly-only experimental API. (`arbitrary_self_types` [#44874](https://github.com/rust-lang/rust/issues/44874))

The target type on which the method may be called.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#85-87)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-ToOwned-for-T)

### impl<T> [ToOwned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html "trait std::borrow::ToOwned") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#89)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Owned)

#### type [Owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#associatedtype.Owned) = T

The resulting type after obtaining ownership.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#90)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.to_owned)

#### fn [to\_owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)(&self) -> T

Creates owned data from borrowed data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#94)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.clone_into)

#### fn [clone\_into](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)(&self, target: [&mut T](https://doc.rust-lang.org/std/primitive.reference.html))

Uses borrowed data to replace owned data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#827-829)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-TryFrom%3CU%3E-for-T)

### impl<T, U> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U> for T where U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#831)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Error-4)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#834)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_from-3)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: U) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, <T as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#811-813)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#impl-TryInto%3CU%3E-for-T)

### impl<T, U> [TryInto](https://doc.rust-lang.org/std/convert/trait.TryInto.html "trait std::convert::TryInto")<U> for T where U: [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#815)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#associatedtype.Error-3)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryInto.html#associatedtype.Error) = <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#818)[§](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.try_into)

#### fn [try\_into](https://doc.rust-lang.org/std/convert/trait.TryInto.html#tymethod.try_into)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.