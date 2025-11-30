---
url: https://doc.rust-lang.org/std/primitive.str.html
title: str - Rust
source_domain: doc.rust-lang.org
---

# str - Rust

## [str](https://doc.rust-lang.org/std/primitive.str.html)

# Primitive Type str

1.0.0

Expand description

String slices.

*[See also the `std::str` module](https://doc.rust-lang.org/std/str/index.html "mod std::str").*

The `str` type, also called a ‘string slice’, is the most primitive string
type. It is usually seen in its borrowed form, `&str`. It is also the type
of string literals, `&'static str`.

## [§](https://doc.rust-lang.org/std/primitive.str.html#basic-usage)Basic Usage

String literals are string slices:

```
let hello_world = "Hello, World!";
```

Here we have declared a string slice initialized with a string literal.
String literals have a static lifetime, which means the string `hello_world`
is guaranteed to be valid for the duration of the entire program.
We can explicitly specify `hello_world`’s lifetime as well:

```
let hello_world: &'static str = "Hello, world!";
```

## [§](https://doc.rust-lang.org/std/primitive.str.html#representation)Representation

A `&str` is made up of two components: a pointer to some bytes, and a
length. You can look at these with the [`as_ptr`](https://doc.rust-lang.org/std/primitive.str.html#method.as_ptr "method str::as_ptr") and [`len`](https://doc.rust-lang.org/std/primitive.str.html#method.len "method str::len") methods:

```
use std::slice;
use std::str;

let story = "Once upon a time...";

let ptr = story.as_ptr();
let len = story.len();

// story has nineteen bytes
assert_eq!(19, len);

// We can re-build a str out of ptr and len. This is all unsafe because
// we are responsible for making sure the two components are valid:
let s = unsafe {
    // First, we build a &[u8]...
    let slice = slice::from_raw_parts(ptr, len);

    // ... and then convert that slice into a string slice
    str::from_utf8(slice)
};

assert_eq!(s, Ok(story));
```

Note: This example shows the internals of `&str`. `unsafe` should not be
used to get a string slice under normal circumstances. Use `as_str`
instead.

## [§](https://doc.rust-lang.org/std/primitive.str.html#invariant)Invariant

Rust libraries may assume that string slices are always valid UTF-8.

Constructing a non-UTF-8 string slice is not immediate undefined behavior, but any function
called on a string slice may assume that it is valid UTF-8, which means that a non-UTF-8 string
slice can lead to undefined behavior down the road.

## Implementations[§](https://doc.rust-lang.org/std/primitive.str.html#implementations)

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#118)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-str)

### impl [str](https://doc.rust-lang.org/std/primitive.str.html)

1.0.0 (const: 1.39.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#141)

#### pub const fn [len](https://doc.rust-lang.org/std/primitive.str.html#method.len)(&self) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Returns the length of `self`.

This length is in bytes, not [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s or graphemes. In other words,
it might not be what a human considers the length of the string.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples)Examples

```
let len = "foo".len();
assert_eq!(3, len);

assert_eq!("ƒoo".len(), 4); // fancy f!
assert_eq!("ƒoo".chars().count(), 3);
```

1.0.0 (const: 1.39.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#161)

#### pub const fn [is\_empty](https://doc.rust-lang.org/std/primitive.str.html#method.is_empty)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if `self` has a length of zero bytes.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-1)Examples

```
let s = "";
assert!(s.is_empty());

let s = "not empty";
assert!(!s.is_empty());
```

1.87.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#239)

#### pub const fn [from\_utf8](https://doc.rust-lang.org/std/primitive.str.html#method.from_utf8)(v: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<&[str](https://doc.rust-lang.org/std/primitive.str.html), [Utf8Error](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error")>

Converts a slice of bytes to a string slice.

A string slice ([`&str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str")) is made of bytes ([`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8")), and a byte slice
([`&[u8]`](https://doc.rust-lang.org/std/primitive.slice.html "primitive slice")) is made of bytes, so this function converts between
the two. Not all byte slices are valid string slices, however: [`&str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str") requires
that it is valid UTF-8. `from_utf8()` checks to ensure that the bytes are valid
UTF-8, and then does the conversion.

If you are sure that the byte slice is valid UTF-8, and you don’t want to
incur the overhead of the validity check, there is an unsafe version of
this function, [`from_utf8_unchecked`](https://doc.rust-lang.org/std/str/fn.from_utf8_unchecked.html "fn std::str::from_utf8_unchecked"), which has the same
behavior but skips the check.

If you need a `String` instead of a `&str`, consider
[`String::from_utf8`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8).

Because you can stack-allocate a `[u8; N]`, and you can take a
[`&[u8]`](https://doc.rust-lang.org/std/primitive.slice.html "primitive slice") of it, this function is one way to have a
stack-allocated string. There is an example of this in the
examples section below.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#errors)Errors

Returns `Err` if the slice is not UTF-8 with a description as to why the
provided slice is not UTF-8.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-2)Examples

Basic usage:

```
// some bytes, in a vector
let sparkle_heart = vec![240, 159, 146, 150];

// We can use the ? (try) operator to check if the bytes are valid
let sparkle_heart = str::from_utf8(&sparkle_heart)?;

assert_eq!("💖", sparkle_heart);
```

Incorrect bytes:

```
// some invalid bytes, in a vector
let sparkle_heart = vec![0, 159, 146, 150];

assert!(str::from_utf8(&sparkle_heart).is_err());
```

See the docs for [`Utf8Error`](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error") for more details on the kinds of
errors that can be returned.

A “stack allocated string”:

```
// some bytes, in a stack-allocated array
let sparkle_heart = [240, 159, 146, 150];

// We know these bytes are valid, so just use `unwrap()`.
let sparkle_heart: &str = str::from_utf8(&sparkle_heart).unwrap();

assert_eq!("💖", sparkle_heart);
```

1.87.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#272)

#### pub const fn [from\_utf8\_mut](https://doc.rust-lang.org/std/primitive.str.html#method.from_utf8_mut)(v: &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<&mut [str](https://doc.rust-lang.org/std/primitive.str.html), [Utf8Error](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error")>

Converts a mutable slice of bytes to a mutable string slice.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-3)Examples

Basic usage:

```
// "Hello, Rust!" as a mutable vector
let mut hellorust = vec![72, 101, 108, 108, 111, 44, 32, 82, 117, 115, 116, 33];

// As we know these bytes are valid, we can use `unwrap()`
let outstr = str::from_utf8_mut(&mut hellorust).unwrap();

assert_eq!("Hello, Rust!", outstr);
```

Incorrect bytes:

```
// Some invalid bytes in a mutable vector
let mut invalid = vec![128, 223];

assert!(str::from_utf8_mut(&mut invalid).is_err());
```

See the docs for [`Utf8Error`](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error") for more details on the kinds of
errors that can be returned.

1.87.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#304)

#### pub const unsafe fn [from\_utf8\_unchecked](https://doc.rust-lang.org/std/primitive.str.html#method.from_utf8_unchecked)(v: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Converts a slice of bytes to a string slice without checking
that the string contains valid UTF-8.

See the safe version, [`from_utf8`](https://doc.rust-lang.org/std/str/fn.from_utf8.html "fn std::str::from_utf8"), for more information.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#safety)Safety

The bytes passed in must be valid UTF-8.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-4)Examples

Basic usage:

```
// some bytes, in a vector
let sparkle_heart = vec![240, 159, 146, 150];

let sparkle_heart = unsafe {
    str::from_utf8_unchecked(&sparkle_heart)
};

assert_eq!("💖", sparkle_heart);
```

1.87.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#329)

#### pub const unsafe fn [from\_utf8\_unchecked\_mut](https://doc.rust-lang.org/std/primitive.str.html#method.from_utf8_unchecked_mut)(v: &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Converts a slice of bytes to a string slice without checking
that the string contains valid UTF-8; mutable version.

See the immutable version, [`from_utf8_unchecked()`](https://doc.rust-lang.org/std/str/fn.from_utf8_unchecked.html "fn std::str::from_utf8_unchecked") for documentation and safety requirements.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-5)Examples

Basic usage:

```
let mut heart = vec![240, 159, 146, 150];
let heart = unsafe { str::from_utf8_unchecked_mut(&mut heart) };

assert_eq!("💖", heart);
```

1.9.0 (const: 1.86.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#361)

#### pub const fn [is\_char\_boundary](https://doc.rust-lang.org/std/primitive.str.html#method.is_char_boundary)(&self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Checks that `index`-th byte is the first byte in a UTF-8 code point
sequence or the end of the string.

The start and end of the string (when `index == self.len()`) are
considered to be boundaries.

Returns `false` if `index` is greater than `self.len()`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-6)Examples

```
let s = "Löwe 老虎 Léopard";
assert!(s.is_char_boundary(0));
// start of `老`
assert!(s.is_char_boundary(6));
assert!(s.is_char_boundary(s.len()));

// second byte of `ö`
assert!(!s.is_char_boundary(2));

// third byte of `老`
assert!(!s.is_char_boundary(8));
```

1.91.0 (const: 1.91.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#410)

#### pub const fn [floor\_char\_boundary](https://doc.rust-lang.org/std/primitive.str.html#method.floor_char_boundary)(&self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Finds the closest `x` not exceeding `index` where [`is_char_boundary(x)`](https://doc.rust-lang.org/std/primitive.str.html#method.is_char_boundary "method str::is_char_boundary") is `true`.

This method can help you truncate a string so that it’s still valid UTF-8, but doesn’t
exceed a given number of bytes. Note that this is done purely at the character level
and can still visually split graphemes, even though the underlying characters aren’t
split. For example, the emoji 🧑‍🔬 (scientist) could be split so that the string only
includes 🧑 (person) instead.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-7)Examples

```
let s = "❤️🧡💛💚💙💜";
assert_eq!(s.len(), 26);
assert!(!s.is_char_boundary(13));

let closest = s.floor_char_boundary(13);
assert_eq!(closest, 10);
assert_eq!(&s[..closest], "❤️🧡");
```

1.91.0 (const: 1.91.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#453)

#### pub const fn [ceil\_char\_boundary](https://doc.rust-lang.org/std/primitive.str.html#method.ceil_char_boundary)(&self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Finds the closest `x` not below `index` where [`is_char_boundary(x)`](https://doc.rust-lang.org/std/primitive.str.html#method.is_char_boundary "method str::is_char_boundary") is `true`.

If `index` is greater than the length of the string, this returns the length of the string.

This method is the natural complement to [`floor_char_boundary`](https://doc.rust-lang.org/std/primitive.str.html#method.floor_char_boundary "method str::floor_char_boundary"). See that method
for more details.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-8)Examples

```
let s = "❤️🧡💛💚💙💜";
assert_eq!(s.len(), 26);
assert!(!s.is_char_boundary(13));

let closest = s.ceil_char_boundary(13);
assert_eq!(closest, 14);
assert_eq!(&s[..closest], "❤️🧡💛");
```

1.0.0 (const: 1.39.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#486)

#### pub const fn [as\_bytes](https://doc.rust-lang.org/std/primitive.str.html#method.as_bytes)(&self) -> &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Converts a string slice to a byte slice. To convert the byte slice back
into a string slice, use the [`from_utf8`](https://doc.rust-lang.org/std/str/fn.from_utf8.html "fn std::str::from_utf8") function.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-9)Examples

```
let bytes = "bors".as_bytes();
assert_eq!(b"bors", bytes);
```

1.20.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#531)

#### pub const unsafe fn [as\_bytes\_mut](https://doc.rust-lang.org/std/primitive.str.html#method.as_bytes_mut)(&mut self) -> &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Converts a mutable string slice to a mutable byte slice.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#safety-1)Safety

The caller must ensure that the content of the slice is valid UTF-8
before the borrow ends and the underlying `str` is used.

Use of a `str` whose contents are not valid UTF-8 is undefined behavior.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-10)Examples

Basic usage:

```
let mut s = String::from("Hello");
let bytes = unsafe { s.as_bytes_mut() };

assert_eq!(b"Hello", bytes);
```

Mutability:

```
let mut s = String::from("🗻∈🌏");

unsafe {
    let bytes = s.as_bytes_mut();

    bytes[0] = 0xF0;
    bytes[1] = 0x9F;
    bytes[2] = 0x8D;
    bytes[3] = 0x94;
}

assert_eq!("🍔∈🌏", s);
```

1.0.0 (const: 1.32.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#562)

#### pub const fn [as\_ptr](https://doc.rust-lang.org/std/primitive.str.html#method.as_ptr)(&self) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html)

Converts a string slice to a raw pointer.

As string slices are a slice of bytes, the raw pointer points to a
[`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8"). This pointer will be pointing to the first byte of the string
slice.

The caller must ensure that the returned pointer is never written to.
If you need to mutate the contents of the string slice, use [`as_mut_ptr`](https://doc.rust-lang.org/std/primitive.str.html#method.as_mut_ptr "method str::as_mut_ptr").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-11)Examples

```
let s = "Hello";
let ptr = s.as_ptr();
```

1.36.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#580)

#### pub const fn [as\_mut\_ptr](https://doc.rust-lang.org/std/primitive.str.html#method.as_mut_ptr)(&mut self) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html)

Converts a mutable string slice to a raw pointer.

As string slices are a slice of bytes, the raw pointer points to a
[`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8"). This pointer will be pointing to the first byte of the string
slice.

It is your responsibility to make sure that the string slice only gets
modified in a way that it remains valid UTF-8.

1.20.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#606)

#### pub fn [get](https://doc.rust-lang.org/std/primitive.str.html#method.get)<I>(&self, i: I) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns a subslice of `str`.

This is the non-panicking alternative to indexing the `str`. Returns
[`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") whenever equivalent indexing operation would panic.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-12)Examples

```
let v = String::from("🗻∈🌏");

assert_eq!(Some("🗻"), v.get(0..4));

// indices not on UTF-8 sequence boundaries
assert!(v.get(1..).is_none());
assert!(v.get(..8).is_none());

// out of bounds
assert!(v.get(..42).is_none());
```

1.20.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#639)

#### pub fn [get\_mut](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut)<I>( &mut self, i: I, ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns a mutable subslice of `str`.

This is the non-panicking alternative to indexing the `str`. Returns
[`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") whenever equivalent indexing operation would panic.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-13)Examples

```
let mut v = String::from("hello");
// correct length
assert!(v.get_mut(0..5).is_some());
// out of bounds
assert!(v.get_mut(..42).is_none());
assert_eq!(Some("he"), v.get_mut(0..2).map(|v| &*v));

assert_eq!("hello", v);
{
    let s = v.get_mut(0..2);
    let s = s.map(|s| {
        s.make_ascii_uppercase();
        &*s
    });
    assert_eq!(Some("HE"), s);
}
assert_eq!("HEllo", v);
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#671)

#### pub unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked)<I>(&self, i: I) -> &<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns an unchecked subslice of `str`.

This is the unchecked alternative to indexing the `str`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#safety-2)Safety

Callers of this function are responsible that these preconditions are
satisfied:

* The starting index must not exceed the ending index;
* Indexes must be within bounds of the original slice;
* Indexes must lie on UTF-8 sequence boundaries.

Failing that, the returned string slice may reference invalid memory or
violate the invariants communicated by the `str` type.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-14)Examples

```
let v = "🗻∈🌏";
unsafe {
    assert_eq!("🗻", v.get_unchecked(0..4));
    assert_eq!("∈", v.get_unchecked(4..7));
    assert_eq!("🌏", v.get_unchecked(7..11));
}
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#706)

#### pub unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut)<I>( &mut self, i: I, ) -> &mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns a mutable, unchecked subslice of `str`.

This is the unchecked alternative to indexing the `str`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#safety-3)Safety

Callers of this function are responsible that these preconditions are
satisfied:

* The starting index must not exceed the ending index;
* Indexes must be within bounds of the original slice;
* Indexes must lie on UTF-8 sequence boundaries.

Failing that, the returned string slice may reference invalid memory or
violate the invariants communicated by the `str` type.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-15)Examples

```
let mut v = String::from("🗻∈🌏");
unsafe {
    assert_eq!("🗻", v.get_unchecked_mut(0..4));
    assert_eq!("∈", v.get_unchecked_mut(4..7));
    assert_eq!("🌏", v.get_unchecked_mut(7..11));
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#757)

#### pub unsafe fn [slice\_unchecked](https://doc.rust-lang.org/std/primitive.str.html#method.slice_unchecked)(&self, begin: [usize](https://doc.rust-lang.org/std/primitive.usize.html), end: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.29.0: use `get_unchecked(begin..end)` instead

Creates a string slice from another string slice, bypassing safety
checks.

This is generally not recommended, use with caution! For a safe
alternative see [`str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str") and [`Index`](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index").

This new slice goes from `begin` to `end`, including `begin` but
excluding `end`.

To get a mutable string slice instead, see the
[`slice_mut_unchecked`](https://doc.rust-lang.org/std/primitive.str.html#method.slice_mut_unchecked "method str::slice_mut_unchecked") method.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#safety-4)Safety

Callers of this function are responsible that three preconditions are
satisfied:

* `begin` must not exceed `end`.
* `begin` and `end` must be byte positions within the string slice.
* `begin` and `end` must lie on UTF-8 sequence boundaries.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-16)Examples

```
let s = "Löwe 老虎 Léopard";

unsafe {
    assert_eq!("Löwe 老虎 Léopard", s.slice_unchecked(0, 21));
}

let s = "Hello, world!";

unsafe {
    assert_eq!("world", s.slice_unchecked(7, 12));
}
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#791)

#### pub unsafe fn [slice\_mut\_unchecked](https://doc.rust-lang.org/std/primitive.str.html#method.slice_mut_unchecked)( &mut self, begin: [usize](https://doc.rust-lang.org/std/primitive.usize.html), end: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.29.0: use `get_unchecked_mut(begin..end)` instead

Creates a string slice from another string slice, bypassing safety
checks.

This is generally not recommended, use with caution! For a safe
alternative see [`str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str") and [`IndexMut`](https://doc.rust-lang.org/std/ops/trait.IndexMut.html "trait std::ops::IndexMut").

This new slice goes from `begin` to `end`, including `begin` but
excluding `end`.

To get an immutable string slice instead, see the
[`slice_unchecked`](https://doc.rust-lang.org/std/primitive.str.html#method.slice_unchecked "method str::slice_unchecked") method.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#safety-5)Safety

Callers of this function are responsible that three preconditions are
satisfied:

* `begin` must not exceed `end`.
* `begin` and `end` must be byte positions within the string slice.
* `begin` and `end` must lie on UTF-8 sequence boundaries.

1.4.0 (const: 1.86.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#831)

#### pub const fn [split\_at](https://doc.rust-lang.org/std/primitive.str.html#method.split_at)(&self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> (&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))

Divides one string slice into two at an index.

The argument, `mid`, should be a byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get mutable string slices instead, see the [`split_at_mut`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut "method str::split_at_mut")
method.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#panics)Panics

Panics if `mid` is not on a UTF-8 code point boundary, or if it is past
the end of the last code point of the string slice. For a non-panicking
alternative see [`split_at_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_checked "method str::split_at_checked").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-17)Examples

```
let s = "Per Martin-Löf";

let (first, last) = s.split_at(3);

assert_eq!("Per", first);
assert_eq!(" Martin-Löf", last);
```

1.4.0 (const: 1.86.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#872)

#### pub const fn [split\_at\_mut](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut)(&mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> (&mut [str](https://doc.rust-lang.org/std/primitive.str.html), &mut [str](https://doc.rust-lang.org/std/primitive.str.html))

Divides one mutable string slice into two at an index.

The argument, `mid`, should be a byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get immutable string slices instead, see the [`split_at`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at "method str::split_at") method.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-1)Panics

Panics if `mid` is not on a UTF-8 code point boundary, or if it is past
the end of the last code point of the string slice. For a non-panicking
alternative see [`split_at_mut_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut_checked "method str::split_at_mut_checked").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-18)Examples

```
let mut s = "Per Martin-Löf".to_string();
{
    let (first, last) = s.split_at_mut(3);
    first.make_ascii_uppercase();
    assert_eq!("PER", first);
    assert_eq!(" Martin-Löf", last);
}
assert_eq!("PER Martin-Löf", s);
```

1.80.0 (const: 1.86.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#912)

#### pub const fn [split\_at\_checked](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_checked)(&self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))>

Divides one string slice into two at an index.

The argument, `mid`, should be a valid byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point. The
method returns `None` if that’s not the case.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get mutable string slices instead, see the [`split_at_mut_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut_checked "method str::split_at_mut_checked")
method.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-19)Examples

```
let s = "Per Martin-Löf";

let (first, last) = s.split_at_checked(3).unwrap();
assert_eq!("Per", first);
assert_eq!(" Martin-Löf", last);

assert_eq!(None, s.split_at_checked(13));  // Inside “ö”
assert_eq!(None, s.split_at_checked(16));  // Beyond the string length
```

1.80.0 (const: 1.86.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#953)

#### pub const fn [split\_at\_mut\_checked](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut_checked)( &mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&mut [str](https://doc.rust-lang.org/std/primitive.str.html), &mut [str](https://doc.rust-lang.org/std/primitive.str.html))>

Divides one mutable string slice into two at an index.

The argument, `mid`, should be a valid byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point. The
method returns `None` if that’s not the case.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get immutable string slices instead, see the [`split_at_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_checked "method str::split_at_checked") method.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-20)Examples

```
let mut s = "Per Martin-Löf".to_string();
if let Some((first, last)) = s.split_at_mut_checked(3) {
    first.make_ascii_uppercase();
    assert_eq!("PER", first);
    assert_eq!(" Martin-Löf", last);
}
assert_eq!("PER Martin-Löf", s);

assert_eq!(None, s.split_at_mut_checked(13));  // Inside “ö”
assert_eq!(None, s.split_at_mut_checked(16));  // Beyond the string length
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1050)

#### pub fn [chars](https://doc.rust-lang.org/std/primitive.str.html#method.chars)(&self) -> [Chars](https://doc.rust-lang.org/std/str/struct.Chars.html "struct std::str::Chars")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator over the [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s of a string slice.

As a string slice consists of valid UTF-8, we can iterate through a
string slice by [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"). This method returns such an iterator.

It’s important to remember that [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") represents a Unicode Scalar
Value, and might not match your idea of what a ‘character’ is. Iteration
over grapheme clusters may be what you actually want. This functionality
is not provided by Rust’s standard library, check crates.io instead.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-21)Examples

Basic usage:

```
let word = "goodbye";

let count = word.chars().count();
assert_eq!(7, count);

let mut chars = word.chars();

assert_eq!(Some('g'), chars.next());
assert_eq!(Some('o'), chars.next());
assert_eq!(Some('o'), chars.next());
assert_eq!(Some('d'), chars.next());
assert_eq!(Some('b'), chars.next());
assert_eq!(Some('y'), chars.next());
assert_eq!(Some('e'), chars.next());

assert_eq!(None, chars.next());
```

Remember, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s might not match your intuition about characters:

```
let y = "y̆";

let mut chars = y.chars();

assert_eq!(Some('y'), chars.next()); // not 'y̆'
assert_eq!(Some('\u{0306}'), chars.next());

assert_eq!(None, chars.next());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1107)

#### pub fn [char\_indices](https://doc.rust-lang.org/std/primitive.str.html#method.char_indices)(&self) -> [CharIndices](https://doc.rust-lang.org/std/str/struct.CharIndices.html "struct std::str::CharIndices")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator over the [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s of a string slice, and their
positions.

As a string slice consists of valid UTF-8, we can iterate through a
string slice by [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"). This method returns an iterator of both
these [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, as well as their byte positions.

The iterator yields tuples. The position is first, the [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") is
second.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-22)Examples

Basic usage:

```
let word = "goodbye";

let count = word.char_indices().count();
assert_eq!(7, count);

let mut char_indices = word.char_indices();

assert_eq!(Some((0, 'g')), char_indices.next());
assert_eq!(Some((1, 'o')), char_indices.next());
assert_eq!(Some((2, 'o')), char_indices.next());
assert_eq!(Some((3, 'd')), char_indices.next());
assert_eq!(Some((4, 'b')), char_indices.next());
assert_eq!(Some((5, 'y')), char_indices.next());
assert_eq!(Some((6, 'e')), char_indices.next());

assert_eq!(None, char_indices.next());
```

Remember, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s might not match your intuition about characters:

```
let yes = "y̆es";

let mut char_indices = yes.char_indices();

assert_eq!(Some((0, 'y')), char_indices.next()); // not (0, 'y̆')
assert_eq!(Some((1, '\u{0306}')), char_indices.next());

// note the 3 here - the previous character took up two bytes
assert_eq!(Some((3, 'e')), char_indices.next());
assert_eq!(Some((4, 's')), char_indices.next());

assert_eq!(None, char_indices.next());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1130)

#### pub fn [bytes](https://doc.rust-lang.org/std/primitive.str.html#method.bytes)(&self) -> [Bytes](https://doc.rust-lang.org/std/str/struct.Bytes.html "struct std::str::Bytes")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator over the bytes of a string slice.

As a string slice consists of a sequence of bytes, we can iterate
through a string slice by byte. This method returns such an iterator.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-23)Examples

```
let mut bytes = "bors".bytes();

assert_eq!(Some(b'b'), bytes.next());
assert_eq!(Some(b'o'), bytes.next());
assert_eq!(Some(b'r'), bytes.next());
assert_eq!(Some(b's'), bytes.next());

assert_eq!(None, bytes.next());
```

1.1.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1182)

#### pub fn [split\_whitespace](https://doc.rust-lang.org/std/primitive.str.html#method.split_whitespace)(&self) -> [SplitWhitespace](https://doc.rust-lang.org/std/str/struct.SplitWhitespace.html "struct std::str::SplitWhitespace")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Splits a string slice by whitespace.

The iterator returned will return string slices that are sub-slices of
the original string slice, separated by any amount of whitespace.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`. If you only want to split on ASCII whitespace
instead, use [`split_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.str.html#method.split_ascii_whitespace "method str::split_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-24)Examples

Basic usage:

```
let mut iter = "A few words".split_whitespace();

assert_eq!(Some("A"), iter.next());
assert_eq!(Some("few"), iter.next());
assert_eq!(Some("words"), iter.next());

assert_eq!(None, iter.next());
```

All kinds of whitespace are considered:

```
let mut iter = " Mary   had\ta\u{2009}little  \n\t lamb".split_whitespace();
assert_eq!(Some("Mary"), iter.next());
assert_eq!(Some("had"), iter.next());
assert_eq!(Some("a"), iter.next());
assert_eq!(Some("little"), iter.next());
assert_eq!(Some("lamb"), iter.next());

assert_eq!(None, iter.next());
```

If the string is empty or all whitespace, the iterator yields no string slices:

```
assert_eq!("".split_whitespace().next(), None);
assert_eq!("   ".split_whitespace().next(), None);
```

1.34.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1233)

#### pub fn [split\_ascii\_whitespace](https://doc.rust-lang.org/std/primitive.str.html#method.split_ascii_whitespace)(&self) -> [SplitAsciiWhitespace](https://doc.rust-lang.org/std/str/struct.SplitAsciiWhitespace.html "struct std::str::SplitAsciiWhitespace")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Splits a string slice by ASCII whitespace.

The iterator returned will return string slices that are sub-slices of
the original string slice, separated by any amount of ASCII whitespace.

This uses the same definition as [`char::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.char.html#method.is_ascii_whitespace "method char::is_ascii_whitespace").
To split by Unicode `Whitespace` instead, use [`split_whitespace`](https://doc.rust-lang.org/std/primitive.str.html#method.split_whitespace "method str::split_whitespace").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-25)Examples

Basic usage:

```
let mut iter = "A few words".split_ascii_whitespace();

assert_eq!(Some("A"), iter.next());
assert_eq!(Some("few"), iter.next());
assert_eq!(Some("words"), iter.next());

assert_eq!(None, iter.next());
```

Various kinds of ASCII whitespace are considered
(see [`char::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.char.html#method.is_ascii_whitespace "method char::is_ascii_whitespace")):

```
let mut iter = " Mary   had\ta little  \n\t lamb".split_ascii_whitespace();
assert_eq!(Some("Mary"), iter.next());
assert_eq!(Some("had"), iter.next());
assert_eq!(Some("a"), iter.next());
assert_eq!(Some("little"), iter.next());
assert_eq!(Some("lamb"), iter.next());

assert_eq!(None, iter.next());
```

If the string is empty or all ASCII whitespace, the iterator yields no string slices:

```
assert_eq!("".split_ascii_whitespace().next(), None);
assert_eq!("   ".split_ascii_whitespace().next(), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1286)

#### pub fn [lines](https://doc.rust-lang.org/std/primitive.str.html#method.lines)(&self) -> [Lines](https://doc.rust-lang.org/std/str/struct.Lines.html "struct std::str::Lines")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator over the lines of a string, as string slices.

Lines are split at line endings that are either newlines (`\n`) or
sequences of a carriage return followed by a line feed (`\r\n`).

Line terminators are not included in the lines returned by the iterator.

Note that any carriage return (`\r`) not immediately followed by a
line feed (`\n`) does not split a line. These carriage returns are
thereby included in the produced lines.

The final line ending is optional. A string that ends with a final line
ending will return the same lines as an otherwise identical string
without a final line ending.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-26)Examples

Basic usage:

```
let text = "foo\r\nbar\n\nbaz\r";
let mut lines = text.lines();

assert_eq!(Some("foo"), lines.next());
assert_eq!(Some("bar"), lines.next());
assert_eq!(Some(""), lines.next());
// Trailing carriage return is included in the last line
assert_eq!(Some("baz\r"), lines.next());

assert_eq!(None, lines.next());
```

The final line does not require any ending:

```
let text = "foo\nbar\n\r\nbaz";
let mut lines = text.lines();

assert_eq!(Some("foo"), lines.next());
assert_eq!(Some("bar"), lines.next());
assert_eq!(Some(""), lines.next());
assert_eq!(Some("baz"), lines.next());

assert_eq!(None, lines.next());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1295)

#### pub fn [lines\_any](https://doc.rust-lang.org/std/primitive.str.html#method.lines_any)(&self) -> [LinesAny](https://doc.rust-lang.org/std/str/struct.LinesAny.html "struct std::str::LinesAny")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.4.0: use lines() instead now

Returns an iterator over the lines of a string.

1.8.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1315)

#### pub fn [encode\_utf16](https://doc.rust-lang.org/std/primitive.str.html#method.encode_utf16)(&self) -> [EncodeUtf16](https://doc.rust-lang.org/std/str/struct.EncodeUtf16.html "struct std::str::EncodeUtf16")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator of `u16` over the string encoded
as native endian UTF-16 (without byte-order mark).

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-27)Examples

```
let text = "Zażółć gęślą jaźń";

let utf8_len = text.len();
let utf16_len = text.encode_utf16().count();

assert!(utf16_len <= utf8_len);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1340)

#### pub fn [contains](https://doc.rust-lang.org/std/primitive.str.html#method.contains)<P>(&self, pat: P) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns `true` if the given pattern matches a sub-slice of
this string slice.

Returns `false` if it does not.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-28)Examples

```
let bananas = "bananas";

assert!(bananas.contains("nana"));
assert!(!bananas.contains("apples"));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1378)

#### pub fn [starts\_with](https://doc.rust-lang.org/std/primitive.str.html#method.starts_with)<P>(&self, pat: P) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns `true` if the given pattern matches a prefix of this
string slice.

Returns `false` if it does not.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, in which case this function will return true if
the `&str` is a prefix of this string slice.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can also be a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.
These will only be checked against the first character of this string slice.
Look at the second example below regarding behavior for slices of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-29)Examples

```
let bananas = "bananas";

assert!(bananas.starts_with("bana"));
assert!(!bananas.starts_with("nana"));
```

```
let bananas = "bananas";

// Note that both of these assert successfully.
assert!(bananas.starts_with(&['b', 'a', 'n', 'a']));
assert!(bananas.starts_with(&['a', 'b', 'c', 'd']));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1403-1405)

#### pub fn [ends\_with](https://doc.rust-lang.org/std/primitive.str.html#method.ends_with)<P>(&self, pat: P) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns `true` if the given pattern matches a suffix of this
string slice.

Returns `false` if it does not.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-30)Examples

```
let bananas = "bananas";

assert!(bananas.ends_with("anas"));
assert!(!bananas.ends_with("nana"));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1454)

#### pub fn [find](https://doc.rust-lang.org/std/primitive.str.html#method.find)<P>(&self, pat: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns the byte index of the first character of this string slice that
matches the pattern.

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the pattern doesn’t match.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-31)Examples

Simple patterns:

```
let s = "Löwe 老虎 Léopard Gepardi";

assert_eq!(s.find('L'), Some(0));
assert_eq!(s.find('é'), Some(14));
assert_eq!(s.find("pard"), Some(17));
```

More complex patterns using point-free style and closures:

```
let s = "Löwe 老虎 Léopard";

assert_eq!(s.find(char::is_whitespace), Some(5));
assert_eq!(s.find(char::is_lowercase), Some(1));
assert_eq!(s.find(|c: char| c.is_whitespace() || c.is_lowercase()), Some(1));
assert_eq!(s.find(|c: char| (c < 'o') && (c > 'a')), Some(4));
```

Not finding the pattern:

```
let s = "Löwe 老虎 Léopard";
let x: &[_] = &['1', '2'];

assert_eq!(s.find(x), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1500-1502)

#### pub fn [rfind](https://doc.rust-lang.org/std/primitive.str.html#method.rfind)<P>(&self, pat: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns the byte index for the first character of the last match of the pattern in
this string slice.

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the pattern doesn’t match.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-32)Examples

Simple patterns:

```
let s = "Löwe 老虎 Léopard Gepardi";

assert_eq!(s.rfind('L'), Some(13));
assert_eq!(s.rfind('é'), Some(14));
assert_eq!(s.rfind("pard"), Some(24));
```

More complex patterns with closures:

```
let s = "Löwe 老虎 Léopard";

assert_eq!(s.rfind(char::is_whitespace), Some(12));
assert_eq!(s.rfind(char::is_lowercase), Some(20));
```

Not finding the pattern:

```
let s = "Löwe 老虎 Léopard";
let x: &[_] = &['1', '2'];

assert_eq!(s.rfind(x), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1628)

#### pub fn [split](https://doc.rust-lang.org/std/primitive.str.html#method.split)<P>(&self, pat: P) -> [Split](https://doc.rust-lang.org/std/str/struct.Split.html "struct std::str::Split")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of this string slice, separated by
characters matched by a pattern.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

If there are no matches the full string slice is returned as the only
item in the iterator.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rsplit`](https://doc.rust-lang.org/std/primitive.str.html#method.rsplit "method str::rsplit") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-33)Examples

Simple patterns:

```
let v: Vec<&str> = "Mary had a little lamb".split(' ').collect();
assert_eq!(v, ["Mary", "had", "a", "little", "lamb"]);

let v: Vec<&str> = "".split('X').collect();
assert_eq!(v, [""]);

let v: Vec<&str> = "lionXXtigerXleopard".split('X').collect();
assert_eq!(v, ["lion", "", "tiger", "leopard"]);

let v: Vec<&str> = "lion::tiger::leopard".split("::").collect();
assert_eq!(v, ["lion", "tiger", "leopard"]);

let v: Vec<&str> = "AABBCC".split("DD").collect();
assert_eq!(v, ["AABBCC"]);

let v: Vec<&str> = "abc1def2ghi".split(char::is_numeric).collect();
assert_eq!(v, ["abc", "def", "ghi"]);

let v: Vec<&str> = "lionXtigerXleopard".split(char::is_uppercase).collect();
assert_eq!(v, ["lion", "tiger", "leopard"]);
```

If the pattern is a slice of chars, split on each occurrence of any of the characters:

```
let v: Vec<&str> = "2020-11-03 23:59".split(&['-', ' ', ':', '@'][..]).collect();
assert_eq!(v, ["2020", "11", "03", "23", "59"]);
```

A more complex pattern, using a closure:

```
let v: Vec<&str> = "abc1defXghi".split(|c| c == '1' || c == 'X').collect();
assert_eq!(v, ["abc", "def", "ghi"]);
```

If a string contains multiple contiguous separators, you will end up
with empty strings in the output:

```
let x = "||||a||b|c".to_string();
let d: Vec<_> = x.split('|').collect();

assert_eq!(d, &["", "", "", "", "a", "", "b", "c"]);
```

Contiguous separators are separated by the empty string.

```
let x = "(///)".to_string();
let d: Vec<_> = x.split('/').collect();

assert_eq!(d, &["(", "", "", ")"]);
```

Separators at the start or end of a string are neighbored
by empty strings.

```
let d: Vec<_> = "010".split("0").collect();
assert_eq!(d, &["", "1", ""]);
```

When the empty string is used as a separator, it separates
every character in the string, along with the beginning
and end of the string.

```
let f: Vec<_> = "rust".split("").collect();
assert_eq!(f, &["", "r", "u", "s", "t", ""]);
```

Contiguous separators can lead to possibly surprising behavior
when whitespace is used as the separator. This code is correct:

```
let x = "    a  b c".to_string();
let d: Vec<_> = x.split(' ').collect();

assert_eq!(d, &["", "", "", "", "a", "", "b", "c"]);
```

It does *not* give you:

[ⓘ](https://doc.rust-lang.org/std/primitive.str.html "This example is not tested")

```
assert_eq!(d, &["a", "b", "c"]);
```

Use [`split_whitespace`](https://doc.rust-lang.org/std/primitive.str.html#method.split_whitespace "method str::split_whitespace") for this behavior.

1.51.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1669)

#### pub fn [split\_inclusive](https://doc.rust-lang.org/std/primitive.str.html#method.split_inclusive)<P>(&self, pat: P) -> [SplitInclusive](https://doc.rust-lang.org/std/str/struct.SplitInclusive.html "struct std::str::SplitInclusive")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of this string slice, separated by
characters matched by a pattern.

Differs from the iterator produced by `split` in that `split_inclusive`
leaves the matched part as the terminator of the substring.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-34)Examples

```
let v: Vec<&str> = "Mary had a little lamb\nlittle lamb\nlittle lamb."
    .split_inclusive('\n').collect();
assert_eq!(v, ["Mary had a little lamb\n", "little lamb\n", "little lamb."]);
```

If the last element of the string is matched,
that element will be considered the terminator of the preceding substring.
That substring will be the last item returned by the iterator.

```
let v: Vec<&str> = "Mary had a little lamb\nlittle lamb\nlittle lamb.\n"
    .split_inclusive('\n').collect();
assert_eq!(v, ["Mary had a little lamb\n", "little lamb\n", "little lamb.\n"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1724-1726)

#### pub fn [rsplit](https://doc.rust-lang.org/std/primitive.str.html#method.rsplit)<P>(&self, pat: P) -> [RSplit](https://doc.rust-lang.org/std/str/struct.RSplit.html "struct std::str::RSplit")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over substrings of the given string slice, separated
by characters matched by a pattern and yielded in reverse order.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-1)Iterator behavior

The returned iterator requires that the pattern supports a reverse
search, and it will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if a forward/reverse
search yields the same elements.

For iterating from the front, the [`split`](https://doc.rust-lang.org/std/primitive.str.html#method.split "method str::split") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-35)Examples

Simple patterns:

```
let v: Vec<&str> = "Mary had a little lamb".rsplit(' ').collect();
assert_eq!(v, ["lamb", "little", "a", "had", "Mary"]);

let v: Vec<&str> = "".rsplit('X').collect();
assert_eq!(v, [""]);

let v: Vec<&str> = "lionXXtigerXleopard".rsplit('X').collect();
assert_eq!(v, ["leopard", "tiger", "", "lion"]);

let v: Vec<&str> = "lion::tiger::leopard".rsplit("::").collect();
assert_eq!(v, ["leopard", "tiger", "lion"]);
```

A more complex pattern, using a closure:

```
let v: Vec<&str> = "abc1defXghi".rsplit(|c| c == '1' || c == 'X').collect();
assert_eq!(v, ["ghi", "def", "abc"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1773)

#### pub fn [split\_terminator](https://doc.rust-lang.org/std/primitive.str.html#method.split_terminator)<P>(&self, pat: P) -> [SplitTerminator](https://doc.rust-lang.org/std/str/struct.SplitTerminator.html "struct std::str::SplitTerminator")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of the given string slice, separated
by characters matched by a pattern.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

Equivalent to [`split`](https://doc.rust-lang.org/std/primitive.str.html#method.split "method str::split"), except that the trailing substring
is skipped if empty.

This method can be used for string data that is *terminated*,
rather than *separated* by a pattern.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-2)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rsplit_terminator`](https://doc.rust-lang.org/std/primitive.str.html#method.rsplit_terminator "method str::rsplit_terminator") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-36)Examples

```
let v: Vec<&str> = "A.B.".split_terminator('.').collect();
assert_eq!(v, ["A", "B"]);

let v: Vec<&str> = "A..B..".split_terminator(".").collect();
assert_eq!(v, ["A", "", "B", ""]);

let v: Vec<&str> = "A.B:C.D".split_terminator(&['.', ':'][..]).collect();
assert_eq!(v, ["A", "B", "C", "D"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1819-1821)

#### pub fn [rsplit\_terminator](https://doc.rust-lang.org/std/primitive.str.html#method.rsplit_terminator)<P>(&self, pat: P) -> [RSplitTerminator](https://doc.rust-lang.org/std/str/struct.RSplitTerminator.html "struct std::str::RSplitTerminator")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over substrings of `self`, separated by characters
matched by a pattern and yielded in reverse order.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

Equivalent to [`split`](https://doc.rust-lang.org/std/primitive.str.html#method.split "method str::split"), except that the trailing substring is
skipped if empty.

This method can be used for string data that is *terminated*,
rather than *separated* by a pattern.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-3)Iterator behavior

The returned iterator requires that the pattern supports a
reverse search, and it will be double ended if a forward/reverse
search yields the same elements.

For iterating from the front, the [`split_terminator`](https://doc.rust-lang.org/std/primitive.str.html#method.split_terminator "method str::split_terminator") method can be
used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-37)Examples

```
let v: Vec<&str> = "A.B.".rsplit_terminator('.').collect();
assert_eq!(v, ["B", "A"]);

let v: Vec<&str> = "A..B..".rsplit_terminator(".").collect();
assert_eq!(v, ["", "B", "", "A"]);

let v: Vec<&str> = "A.B:C.D".rsplit_terminator(&['.', ':'][..]).collect();
assert_eq!(v, ["D", "C", "B", "A"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1874)

#### pub fn [splitn](https://doc.rust-lang.org/std/primitive.str.html#method.splitn)<P>(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pat: P) -> [SplitN](https://doc.rust-lang.org/std/str/struct.SplitN.html "struct std::str::SplitN")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of the given string slice, separated
by a pattern, restricted to returning at most `n` items.

If `n` substrings are returned, the last substring (the `n`th substring)
will contain the remainder of the string.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-4)Iterator behavior

The returned iterator will not be double ended, because it is
not efficient to support.

If the pattern allows a reverse search, the [`rsplitn`](https://doc.rust-lang.org/std/primitive.str.html#method.rsplitn "method str::rsplitn") method can be
used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-38)Examples

Simple patterns:

```
let v: Vec<&str> = "Mary had a little lambda".splitn(3, ' ').collect();
assert_eq!(v, ["Mary", "had", "a little lambda"]);

let v: Vec<&str> = "lionXXtigerXleopard".splitn(3, "X").collect();
assert_eq!(v, ["lion", "", "tigerXleopard"]);

let v: Vec<&str> = "abcXdef".splitn(1, 'X').collect();
assert_eq!(v, ["abcXdef"]);

let v: Vec<&str> = "".splitn(1, 'X').collect();
assert_eq!(v, [""]);
```

A more complex pattern, using a closure:

```
let v: Vec<&str> = "abc1defXghi".splitn(2, |c| c == '1' || c == 'X').collect();
assert_eq!(v, ["abc", "defXghi"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1923-1925)

#### pub fn [rsplitn](https://doc.rust-lang.org/std/primitive.str.html#method.rsplitn)<P>(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pat: P) -> [RSplitN](https://doc.rust-lang.org/std/str/struct.RSplitN.html "struct std::str::RSplitN")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over substrings of this string slice, separated by a
pattern, starting from the end of the string, restricted to returning at
most `n` items.

If `n` substrings are returned, the last substring (the `n`th substring)
will contain the remainder of the string.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-5)Iterator behavior

The returned iterator will not be double ended, because it is not
efficient to support.

For splitting from the front, the [`splitn`](https://doc.rust-lang.org/std/primitive.str.html#method.splitn "method str::splitn") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-39)Examples

Simple patterns:

```
let v: Vec<&str> = "Mary had a little lamb".rsplitn(3, ' ').collect();
assert_eq!(v, ["lamb", "little", "Mary had a"]);

let v: Vec<&str> = "lionXXtigerXleopard".rsplitn(3, 'X').collect();
assert_eq!(v, ["leopard", "tiger", "lionX"]);

let v: Vec<&str> = "lion::tiger::leopard".rsplitn(2, "::").collect();
assert_eq!(v, ["leopard", "lion::tiger"]);
```

A more complex pattern, using a closure:

```
let v: Vec<&str> = "abc1defXghi".rsplitn(2, |c| c == '1' || c == 'X').collect();
assert_eq!(v, ["ghi", "abc1def"]);
```

1.52.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1943)

#### pub fn [split\_once](https://doc.rust-lang.org/std/primitive.str.html#method.split_once)<P>(&self, delimiter: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Splits the string on the first occurrence of the specified delimiter and
returns prefix before delimiter and suffix after delimiter.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-40)Examples

```
assert_eq!("cfg".split_once('='), None);
assert_eq!("cfg=".split_once('='), Some(("cfg", "")));
assert_eq!("cfg=foo".split_once('='), Some(("cfg", "foo")));
assert_eq!("cfg=foo=bar".split_once('='), Some(("cfg", "foo=bar")));
```

1.52.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1961-1963)

#### pub fn [rsplit\_once](https://doc.rust-lang.org/std/primitive.str.html#method.rsplit_once)<P>(&self, delimiter: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Splits the string on the last occurrence of the specified delimiter and
returns prefix before delimiter and suffix after delimiter.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-41)Examples

```
assert_eq!("cfg".rsplit_once('='), None);
assert_eq!("cfg=foo".rsplit_once('='), Some(("cfg", "foo")));
assert_eq!("cfg=foo=bar".rsplit_once('='), Some(("cfg=foo", "bar")));
```

1.2.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2001)

#### pub fn [matches](https://doc.rust-lang.org/std/primitive.str.html#method.matches)<P>(&self, pat: P) -> [Matches](https://doc.rust-lang.org/std/str/struct.Matches.html "struct std::str::Matches")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over the disjoint matches of a pattern within the
given string slice.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-6)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rmatches`](https://doc.rust-lang.org/std/primitive.str.html#method.rmatches "method str::rmatches") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-42)Examples

```
let v: Vec<&str> = "abcXXXabcYYYabc".matches("abc").collect();
assert_eq!(v, ["abc", "abc", "abc"]);

let v: Vec<&str> = "1abc2abc3".matches(char::is_numeric).collect();
assert_eq!(v, ["1", "2", "3"]);
```

1.2.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2035-2037)

#### pub fn [rmatches](https://doc.rust-lang.org/std/primitive.str.html#method.rmatches)<P>(&self, pat: P) -> [RMatches](https://doc.rust-lang.org/std/str/struct.RMatches.html "struct std::str::RMatches")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over the disjoint matches of a pattern within this
string slice, yielded in reverse order.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-7)Iterator behavior

The returned iterator requires that the pattern supports a reverse
search, and it will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if a forward/reverse
search yields the same elements.

For iterating from the front, the [`matches`](https://doc.rust-lang.org/std/primitive.str.html#method.matches "method str::matches") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-43)Examples

```
let v: Vec<&str> = "abcXXXabcYYYabc".rmatches("abc").collect();
assert_eq!(v, ["abc", "abc", "abc"]);

let v: Vec<&str> = "1abc2abc3".rmatches(char::is_numeric).collect();
assert_eq!(v, ["3", "2", "1"]);
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2079)

#### pub fn [match\_indices](https://doc.rust-lang.org/std/primitive.str.html#method.match_indices)<P>(&self, pat: P) -> [MatchIndices](https://doc.rust-lang.org/std/str/struct.MatchIndices.html "struct std::str::MatchIndices")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over the disjoint matches of a pattern within this string
slice as well as the index that the match starts at.

For matches of `pat` within `self` that overlap, only the indices
corresponding to the first match are returned.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-8)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rmatch_indices`](https://doc.rust-lang.org/std/primitive.str.html#method.rmatch_indices "method str::rmatch_indices") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-44)Examples

```
let v: Vec<_> = "abcXXXabcYYYabc".match_indices("abc").collect();
assert_eq!(v, [(0, "abc"), (6, "abc"), (12, "abc")]);

let v: Vec<_> = "1abcabc2".match_indices("abc").collect();
assert_eq!(v, [(1, "abc"), (4, "abc")]);

let v: Vec<_> = "ababa".match_indices("aba").collect();
assert_eq!(v, [(0, "aba")]); // only the first `aba`
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2119-2121)

#### pub fn [rmatch\_indices](https://doc.rust-lang.org/std/primitive.str.html#method.rmatch_indices)<P>(&self, pat: P) -> [RMatchIndices](https://doc.rust-lang.org/std/str/struct.RMatchIndices.html "struct std::str::RMatchIndices")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over the disjoint matches of a pattern within `self`,
yielded in reverse order along with the index of the match.

For matches of `pat` within `self` that overlap, only the indices
corresponding to the last match are returned.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#iterator-behavior-9)Iterator behavior

The returned iterator requires that the pattern supports a reverse
search, and it will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if a forward/reverse
search yields the same elements.

For iterating from the front, the [`match_indices`](https://doc.rust-lang.org/std/primitive.str.html#method.match_indices "method str::match_indices") method can be used.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-45)Examples

```
let v: Vec<_> = "abcXXXabcYYYabc".rmatch_indices("abc").collect();
assert_eq!(v, [(12, "abc"), (6, "abc"), (0, "abc")]);

let v: Vec<_> = "1abcabc2".rmatch_indices("abc").collect();
assert_eq!(v, [(4, "abc"), (1, "abc")]);

let v: Vec<_> = "ababa".rmatch_indices("aba").collect();
assert_eq!(v, [(2, "aba")]); // only the last `aba`
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2143)

#### pub fn [trim](https://doc.rust-lang.org/std/primitive.str.html#method.trim)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading and trailing whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`, which includes newlines.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-46)Examples

```
let s = "\n Hello\tworld\t\n";

assert_eq!("Hello\tworld", s.trim());
```

1.30.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2182)

#### pub fn [trim\_start](https://doc.rust-lang.org/std/primitive.str.html#method.trim_start)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`, which includes newlines.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality)Text directionality

A string is a sequence of bytes. `start` in this context means the first
position of that byte string; for a left-to-right language like English or
Russian, this will be left side, and for right-to-left languages like
Arabic or Hebrew, this will be the right side.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-47)Examples

Basic usage:

```
let s = "\n Hello\tworld\t\n";
assert_eq!("Hello\tworld\t\n", s.trim_start());
```

Directionality:

```
let s = "  English  ";
assert!(Some('E') == s.trim_start().chars().next());

let s = "  עברית  ";
assert!(Some('ע') == s.trim_start().chars().next());
```

1.30.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2221)

#### pub fn [trim\_end](https://doc.rust-lang.org/std/primitive.str.html#method.trim_end)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with trailing whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`, which includes newlines.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality-1)Text directionality

A string is a sequence of bytes. `end` in this context means the last
position of that byte string; for a left-to-right language like English or
Russian, this will be right side, and for right-to-left languages like
Arabic or Hebrew, this will be the left side.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-48)Examples

Basic usage:

```
let s = "\n Hello\tworld\t\n";
assert_eq!("\n Hello\tworld", s.trim_end());
```

Directionality:

```
let s = "  English  ";
assert!(Some('h') == s.trim_end().chars().rev().next());

let s = "  עברית  ";
assert!(Some('ת') == s.trim_end().chars().rev().next());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2261)

#### pub fn [trim\_left](https://doc.rust-lang.org/std/primitive.str.html#method.trim_left)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.33.0: superseded by `trim_start`

Returns a string slice with leading whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality-2)Text directionality

A string is a sequence of bytes. ‘Left’ in this context means the first
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *right* side, not the left.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-49)Examples

Basic usage:

```
let s = " Hello\tworld\t";

assert_eq!("Hello\tworld\t", s.trim_left());
```

Directionality:

```
let s = "  English";
assert!(Some('E') == s.trim_left().chars().next());

let s = "  עברית";
assert!(Some('ע') == s.trim_left().chars().next());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2301)

#### pub fn [trim\_right](https://doc.rust-lang.org/std/primitive.str.html#method.trim_right)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.33.0: superseded by `trim_end`

Returns a string slice with trailing whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality-3)Text directionality

A string is a sequence of bytes. ‘Right’ in this context means the last
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *left* side, not the right.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-50)Examples

Basic usage:

```
let s = " Hello\tworld\t";

assert_eq!(" Hello\tworld", s.trim_right());
```

Directionality:

```
let s = "English  ";
assert!(Some('h') == s.trim_right().chars().rev().next());

let s = "עברית  ";
assert!(Some('ת') == s.trim_right().chars().rev().next());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2334-2336)

#### pub fn [trim\_matches](https://doc.rust-lang.org/std/primitive.str.html#method.trim_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [DoubleEndedSearcher](https://doc.rust-lang.org/std/str/pattern/trait.DoubleEndedSearcher.html "trait std::str::pattern::DoubleEndedSearcher")<'a>,

Returns a string slice with all prefixes and suffixes that match a
pattern repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a function
or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-51)Examples

Simple patterns:

```
assert_eq!("11foo1bar11".trim_matches('1'), "foo1bar");
assert_eq!("123foo1bar123".trim_matches(char::is_numeric), "foo1bar");

let x: &[_] = &['1', '2'];
assert_eq!("12foo1bar12".trim_matches(x), "foo1bar");
```

A more complex pattern, using a closure:

```
assert_eq!("1foo1barXX".trim_matches(|c| c == '1' || c == 'X'), "foo1bar");
```

1.30.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2381)

#### pub fn [trim\_start\_matches](https://doc.rust-lang.org/std/primitive.str.html#method.trim_start_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns a string slice with all prefixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality-4)Text directionality

A string is a sequence of bytes. `start` in this context means the first
position of that byte string; for a left-to-right language like English or
Russian, this will be left side, and for right-to-left languages like
Arabic or Hebrew, this will be the right side.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-52)Examples

```
assert_eq!("11foo1bar11".trim_start_matches('1'), "foo1bar11");
assert_eq!("123foo1bar123".trim_start_matches(char::is_numeric), "foo1bar123");

let x: &[_] = &['1', '2'];
assert_eq!("12foo1bar12".trim_start_matches(x), "foo1bar12");
```

1.45.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2415)

#### pub fn [strip\_prefix](https://doc.rust-lang.org/std/primitive.str.html#method.strip_prefix)<P>(&self, prefix: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns a string slice with the prefix removed.

If the string starts with the pattern `prefix`, returns the substring after the prefix,
wrapped in `Some`. Unlike [`trim_start_matches`](https://doc.rust-lang.org/std/primitive.str.html#method.trim_start_matches "method str::trim_start_matches"), this method removes the prefix exactly once.

If the string does not start with `prefix`, returns `None`.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-53)Examples

```
assert_eq!("foo:bar".strip_prefix("foo:"), Some("bar"));
assert_eq!("foo:bar".strip_prefix("bar"), None);
assert_eq!("foofoo".strip_prefix("foo"), Some("foo"));
```

1.45.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2443-2445)

#### pub fn [strip\_suffix](https://doc.rust-lang.org/std/primitive.str.html#method.strip_suffix)<P>(&self, suffix: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns a string slice with the suffix removed.

If the string ends with the pattern `suffix`, returns the substring before the suffix,
wrapped in `Some`. Unlike [`trim_end_matches`](https://doc.rust-lang.org/std/primitive.str.html#method.trim_end_matches "method str::trim_end_matches"), this method removes the suffix exactly once.

If the string does not end with `suffix`, returns `None`.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-54)Examples

```
assert_eq!("bar:foo".strip_suffix(":foo"), Some("bar"));
assert_eq!("bar:foo".strip_suffix("bar"), None);
assert_eq!("foofoo".strip_suffix("foo"), Some("foo"));
```

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2483)

#### pub fn [trim\_prefix](https://doc.rust-lang.org/std/primitive.str.html#method.trim_prefix)<P>(&self, prefix: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

🔬This is a nightly-only experimental API. (`trim_prefix_suffix` [#142312](https://github.com/rust-lang/rust/issues/142312))

Returns a string slice with the optional prefix removed.

If the string starts with the pattern `prefix`, returns the substring after the prefix.
Unlike [`strip_prefix`](https://doc.rust-lang.org/std/primitive.str.html#method.strip_prefix "method str::strip_prefix"), this method always returns `&str` for easy method chaining,
instead of returning [`Option<&str>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option").

If the string does not start with `prefix`, returns the original string unchanged.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-55)Examples

```
#![feature(trim_prefix_suffix)]

// Prefix present - removes it
assert_eq!("foo:bar".trim_prefix("foo:"), "bar");
assert_eq!("foofoo".trim_prefix("foo"), "foo");

// Prefix absent - returns original string
assert_eq!("foo:bar".trim_prefix("bar"), "foo:bar");

// Method chaining example
assert_eq!("<https://example.com/>".trim_prefix('<').trim_suffix('>'), "https://example.com/");
```

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2520-2522)

#### pub fn [trim\_suffix](https://doc.rust-lang.org/std/primitive.str.html#method.trim_suffix)<P>(&self, suffix: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

🔬This is a nightly-only experimental API. (`trim_prefix_suffix` [#142312](https://github.com/rust-lang/rust/issues/142312))

Returns a string slice with the optional suffix removed.

If the string ends with the pattern `suffix`, returns the substring before the suffix.
Unlike [`strip_suffix`](https://doc.rust-lang.org/std/primitive.str.html#method.strip_suffix "method str::strip_suffix"), this method always returns `&str` for easy method chaining,
instead of returning [`Option<&str>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option").

If the string does not end with `suffix`, returns the original string unchanged.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-56)Examples

```
#![feature(trim_prefix_suffix)]

// Suffix present - removes it
assert_eq!("bar:foo".trim_suffix(":foo"), "bar");
assert_eq!("foofoo".trim_suffix("foo"), "foo");

// Suffix absent - returns original string
assert_eq!("bar:foo".trim_suffix("bar"), "bar:foo");

// Method chaining example
assert_eq!("<https://example.com/>".trim_prefix('<').trim_suffix('>'), "https://example.com/");
```

1.30.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2563-2565)

#### pub fn [trim\_end\_matches](https://doc.rust-lang.org/std/primitive.str.html#method.trim_end_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns a string slice with all suffixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality-5)Text directionality

A string is a sequence of bytes. `end` in this context means the last
position of that byte string; for a left-to-right language like English or
Russian, this will be right side, and for right-to-left languages like
Arabic or Hebrew, this will be the left side.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-57)Examples

Simple patterns:

```
assert_eq!("11foo1bar11".trim_end_matches('1'), "11foo1bar");
assert_eq!("123foo1bar123".trim_end_matches(char::is_numeric), "123foo1bar");

let x: &[_] = &['1', '2'];
assert_eq!("12foo1bar12".trim_end_matches(x), "12foo1bar");
```

A more complex pattern, using a closure:

```
assert_eq!("1fooX".trim_end_matches(|c| c == '1' || c == 'X'), "1foo");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2607)

#### pub fn [trim\_left\_matches](https://doc.rust-lang.org/std/primitive.str.html#method.trim_left_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

👎Deprecated since 1.33.0: superseded by `trim_start_matches`

Returns a string slice with all prefixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality-6)Text directionality

A string is a sequence of bytes. ‘Left’ in this context means the first
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *right* side, not the left.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-58)Examples

```
assert_eq!("11foo1bar11".trim_left_matches('1'), "foo1bar11");
assert_eq!("123foo1bar123".trim_left_matches(char::is_numeric), "foo1bar123");

let x: &[_] = &['1', '2'];
assert_eq!("12foo1bar12".trim_left_matches(x), "foo1bar12");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2650-2652)

#### pub fn [trim\_right\_matches](https://doc.rust-lang.org/std/primitive.str.html#method.trim_right_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

👎Deprecated since 1.33.0: superseded by `trim_end_matches`

Returns a string slice with all suffixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#text-directionality-7)Text directionality

A string is a sequence of bytes. ‘Right’ in this context means the last
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *left* side, not the right.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-59)Examples

Simple patterns:

```
assert_eq!("11foo1bar11".trim_right_matches('1'), "11foo1bar");
assert_eq!("123foo1bar123".trim_right_matches(char::is_numeric), "123foo1bar");

let x: &[_] = &['1', '2'];
assert_eq!("12foo1bar12".trim_right_matches(x), "12foo1bar");
```

A more complex pattern, using a closure:

```
assert_eq!("1fooX".trim_right_matches(|c| c == '1' || c == 'X'), "1foo");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2701)

#### pub fn [parse](https://doc.rust-lang.org/std/primitive.str.html#method.parse)<F>(&self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<F, <F as [FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr")>::[Err](https://doc.rust-lang.org/std/str/trait.FromStr.html#associatedtype.Err "type std::str::FromStr::Err")> where F: [FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr"),

Parses this string slice into another type.

Because `parse` is so general, it can cause problems with type
inference. As such, `parse` is one of the few times you’ll see
the syntax affectionately known as the ‘turbofish’: `::<>`. This
helps the inference algorithm understand specifically which type
you’re trying to parse into.

`parse` can parse into any type that implements the [`FromStr`](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr") trait.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#errors-1)Errors

Will return [`Err`](https://doc.rust-lang.org/std/str/trait.FromStr.html#associatedtype.Err "associated type std::str::FromStr::Err") if it’s not possible to parse this string slice into
the desired type.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-60)Examples

Basic usage:

```
let four: u32 = "4".parse().unwrap();

assert_eq!(4, four);
```

Using the ‘turbofish’ instead of annotating `four`:

```
let four = "4".parse::<u32>();

assert_eq!(Ok(4), four);
```

Failing to parse:

```
let nope = "j".parse::<u32>();

assert!(nope.is_err());
```

1.23.0 (const: 1.74.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2720)

#### pub const fn [is\_ascii](https://doc.rust-lang.org/std/primitive.str.html#method.is_ascii)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Checks if all characters in this string are within the ASCII range.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-61)Examples

```
let ascii = "hello!\n";
let non_ascii = "Grüße, Jürgen ❤";

assert!(ascii.is_ascii());
assert!(!non_ascii.is_ascii());
```

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2732)

#### pub const fn [as\_ascii](https://doc.rust-lang.org/std/primitive.str.html#method.as_ascii)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[[AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")]>

🔬This is a nightly-only experimental API. (`ascii_char` [#110998](https://github.com/rust-lang/rust/issues/110998))

If this string slice [`is_ascii`](https://doc.rust-lang.org/std/primitive.str.html#method.is_ascii "method str::is_ascii"), returns it as a slice
of [ASCII characters](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char"), otherwise returns `None`.

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2746)

#### pub const unsafe fn [as\_ascii\_unchecked](https://doc.rust-lang.org/std/primitive.str.html#method.as_ascii_unchecked)(&self) -> &[[AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")]

🔬This is a nightly-only experimental API. (`ascii_char` [#110998](https://github.com/rust-lang/rust/issues/110998))

Converts this string slice into a slice of [ASCII characters](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char"),
without checking whether they are valid.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#safety-6)Safety

Every character in this string must be ASCII, or else this is UB.

1.23.0 (const: 1.89.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2774)

#### pub const fn [eq\_ignore\_ascii\_case](https://doc.rust-lang.org/std/primitive.str.html#method.eq_ignore_ascii_case)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Checks that two strings are an ASCII case-insensitive match.

Same as `to_ascii_lowercase(a) == to_ascii_lowercase(b)`,
but without allocating and copying temporaries.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-62)Examples

```
assert!("Ferris".eq_ignore_ascii_case("FERRIS"));
assert!("Ferrös".eq_ignore_ascii_case("FERRöS"));
assert!(!"Ferrös".eq_ignore_ascii_case("FERRÖS"));
```

1.23.0 (const: 1.84.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2800)

#### pub const fn [make\_ascii\_uppercase](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_uppercase)(&mut self)

Converts this string to its ASCII upper case equivalent in-place.

ASCII letters ‘a’ to ‘z’ are mapped to ‘A’ to ‘Z’,
but non-ASCII letters are unchanged.

To return a new uppercased value without modifying the existing one, use
[`to_ascii_uppercase()`](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_uppercase).

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-63)Examples

```
let mut s = String::from("Grüße, Jürgen ❤");

s.make_ascii_uppercase();

assert_eq!("GRüßE, JüRGEN ❤", s);
```

1.23.0 (const: 1.84.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2828)

#### pub const fn [make\_ascii\_lowercase](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_lowercase)(&mut self)

Converts this string to its ASCII lower case equivalent in-place.

ASCII letters ‘A’ to ‘Z’ are mapped to ‘a’ to ‘z’,
but non-ASCII letters are unchanged.

To return a new lowercased value without modifying the existing one, use
[`to_ascii_lowercase()`](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_lowercase).

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-64)Examples

```
let mut s = String::from("GRÜßE, JÜRGEN ❤");

s.make_ascii_lowercase();

assert_eq!("grÜße, jÜrgen ❤", s);
```

1.80.0 (const: 1.80.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2853)

#### pub const fn [trim\_ascii\_start](https://doc.rust-lang.org/std/primitive.str.html#method.trim_ascii_start)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading ASCII whitespace removed.

‘Whitespace’ refers to the definition used by
[`u8::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.u8.html#method.is_ascii_whitespace "method u8::is_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-65)Examples

```
assert_eq!(" \t \u{3000}hello world\n".trim_ascii_start(), "\u{3000}hello world\n");
assert_eq!("  ".trim_ascii_start(), "");
assert_eq!("".trim_ascii_start(), "");
```

1.80.0 (const: 1.80.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2878)

#### pub const fn [trim\_ascii\_end](https://doc.rust-lang.org/std/primitive.str.html#method.trim_ascii_end)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with trailing ASCII whitespace removed.

‘Whitespace’ refers to the definition used by
[`u8::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.u8.html#method.is_ascii_whitespace "method u8::is_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-66)Examples

```
assert_eq!("\r hello world\u{3000}\n ".trim_ascii_end(), "\r hello world\u{3000}");
assert_eq!("  ".trim_ascii_end(), "");
assert_eq!("".trim_ascii_end(), "");
```

1.80.0 (const: 1.80.0) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2904)

#### pub const fn [trim\_ascii](https://doc.rust-lang.org/std/primitive.str.html#method.trim_ascii)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading and trailing ASCII whitespace
removed.

‘Whitespace’ refers to the definition used by
[`u8::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.u8.html#method.is_ascii_whitespace "method u8::is_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-67)Examples

```
assert_eq!("\r hello world\n ".trim_ascii(), "hello world");
assert_eq!("  ".trim_ascii(), "");
assert_eq!("".trim_ascii(), "");
```

1.34.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2947)

#### pub fn [escape\_debug](https://doc.rust-lang.org/std/primitive.str.html#method.escape_debug)(&self) -> [EscapeDebug](https://doc.rust-lang.org/std/str/struct.EscapeDebug.html "struct std::str::EscapeDebug")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator that escapes each char in `self` with [`char::escape_debug`](https://doc.rust-lang.org/std/primitive.char.html#method.escape_debug "method char::escape_debug").

Note: only extended grapheme codepoints that begin the string will be
escaped.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-68)Examples

As an iterator:

```
for c in "❤\n!".escape_debug() {
    print!("{c}");
}
println!();
```

Using `println!` directly:

```
println!("{}", "❤\n!".escape_debug());
```

Both are equivalent to:

```
println!("❤\\n!");
```

Using `to_string`:

```
assert_eq!("❤\n!".escape_debug().to_string(), "❤\\n!");
```

1.34.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2993)

#### pub fn [escape\_default](https://doc.rust-lang.org/std/primitive.str.html#method.escape_default)(&self) -> [EscapeDefault](https://doc.rust-lang.org/std/str/struct.EscapeDefault.html "struct std::str::EscapeDefault")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator that escapes each char in `self` with [`char::escape_default`](https://doc.rust-lang.org/std/primitive.char.html#method.escape_default "method char::escape_default").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-69)Examples

As an iterator:

```
for c in "❤\n!".escape_default() {
    print!("{c}");
}
println!();
```

Using `println!` directly:

```
println!("{}", "❤\n!".escape_default());
```

Both are equivalent to:

```
println!("\\u{{2764}}\\n!");
```

Using `to_string`:

```
assert_eq!("❤\n!".escape_default().to_string(), "\\u{2764}\\n!");
```

1.34.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3031)

#### pub fn [escape\_unicode](https://doc.rust-lang.org/std/primitive.str.html#method.escape_unicode)(&self) -> [EscapeUnicode](https://doc.rust-lang.org/std/str/struct.EscapeUnicode.html "struct std::str::EscapeUnicode")<'\_> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Returns an iterator that escapes each char in `self` with [`char::escape_unicode`](https://doc.rust-lang.org/std/primitive.char.html#method.escape_unicode "method char::escape_unicode").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-70)Examples

As an iterator:

```
for c in "❤\n!".escape_unicode() {
    print!("{c}");
}
println!();
```

Using `println!` directly:

```
println!("{}", "❤\n!".escape_unicode());
```

Both are equivalent to:

```
println!("\\u{{2764}}\\u{{a}}\\u{{21}}");
```

Using `to_string`:

```
assert_eq!("❤\n!".escape_unicode().to_string(), "\\u{2764}\\u{a}\\u{21}");
```

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3064)

#### pub fn [substr\_range](https://doc.rust-lang.org/std/primitive.str.html#method.substr_range)(&self, substr: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>>

🔬This is a nightly-only experimental API. (`substr_range` [#126769](https://github.com/rust-lang/rust/issues/126769))

Returns the range that a substring points to.

Returns `None` if `substr` does not point within `self`.

Unlike [`str::find`](https://doc.rust-lang.org/std/primitive.str.html#method.find "method str::find"), **this does not search through the string**.
Instead, it uses pointer arithmetic to find where in the string
`substr` is derived from.

This is useful for extending [`str::split`](https://doc.rust-lang.org/std/primitive.str.html#method.split "method str::split") and similar methods.

Note that this method may return false positives (typically either
`Some(0..0)` or `Some(self.len()..self.len())`) if `substr` is a
zero-length `str` that points at the beginning or end of another,
independent, `str`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-71)Examples

```
#![feature(substr_range)]

let data = "a, b, b, a";
let mut iter = data.split(", ").map(|s| data.substr_range(s).unwrap());

assert_eq!(iter.next(), Some(0..1));
assert_eq!(iter.next(), Some(3..4));
assert_eq!(iter.next(), Some(6..7));
assert_eq!(iter.next(), Some(9..10));
```

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3075)

#### pub const fn [as\_str](https://doc.rust-lang.org/std/primitive.str.html#method.as_str)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`str_as_str` [#130366](https://github.com/rust-lang/rust/issues/130366))

Returns the same string as a string slice `&str`.

This method is redundant when used directly on `&str`, but
it helps dereferencing other string-like types to string slices,
for example references to `Box<str>` or `Arc<str>`.

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#222)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-str-1)

### impl [str](https://doc.rust-lang.org/std/primitive.str.html)

Methods for string slices.

1.20.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#237)

#### pub fn [into\_boxed\_bytes](https://doc.rust-lang.org/std/primitive.str.html#method.into_boxed_bytes)(self: [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]>

Converts a `Box<str>` into a `Box<[u8]>` without copying or allocating.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-72)Examples

```
let s = "this is a string";
let boxed_str = s.to_owned().into_boxed_str();
let boxed_bytes = boxed_str.into_boxed_bytes();
assert_eq!(*boxed_bytes, *s.as_bytes());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#268)

#### pub fn [replace](https://doc.rust-lang.org/std/primitive.str.html#method.replace)<P>(&self, from: P, to: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Replaces all matches of a pattern with another string.

`replace` creates a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), and copies the data from this string slice into it.
While doing so, it attempts to find matches of a pattern. If it finds any, it
replaces them with the replacement string slice.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-73)Examples

```
let s = "this is old";

assert_eq!("this is new", s.replace("old", "new"));
assert_eq!("than an old", s.replace("is", "an"));
```

When the pattern doesn’t match, it returns this string slice as [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"):

```
let s = "this is old";
assert_eq!(s, s.replace("cookie monster", "little lamb"));
```

1.16.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#323)

#### pub fn [replacen](https://doc.rust-lang.org/std/primitive.str.html#method.replacen)<P>(&self, pat: P, to: &[str](https://doc.rust-lang.org/std/primitive.str.html), count: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Replaces first N matches of a pattern with another string.

`replacen` creates a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), and copies the data from this string slice into it.
While doing so, it attempts to find matches of a pattern. If it finds any, it
replaces them with the replacement string slice at most `count` times.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-74)Examples

```
let s = "foo foo 123 foo";
assert_eq!("new new 123 foo", s.replacen("foo", "new", 2));
assert_eq!("faa fao 123 foo", s.replacen('o', "a", 3));
assert_eq!("foo foo new23 foo", s.replacen(char::is_numeric, "new", 1));
```

When the pattern doesn’t match, it returns this string slice as [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"):

```
let s = "this is old";
assert_eq!(s, s.replacen("cookie monster", "little lamb", 10));
```

1.2.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#380)

#### pub fn [to\_lowercase](https://doc.rust-lang.org/std/primitive.str.html#method.to_lowercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns the lowercase equivalent of this string slice, as a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

‘Lowercase’ is defined according to the terms of the Unicode Derived Core Property
`Lowercase`.

Since some characters can expand into multiple characters when changing
the case, this function returns a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") instead of modifying the
parameter in-place.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-75)Examples

Basic usage:

```
let s = "HELLO";

assert_eq!("hello", s.to_lowercase());
```

A tricky example, with sigma:

```
let sigma = "Σ";

assert_eq!("σ", sigma.to_lowercase());

// but at the end of a word, it's ς, not σ:
let odysseus = "ὈΔΥΣΣΕΎΣ";

assert_eq!("ὀδυσσεύς", odysseus.to_lowercase());
```

Languages without case are not changed:

```
let new_year = "农历新年";

assert_eq!(new_year, new_year.to_lowercase());
```

1.2.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#466)

#### pub fn [to\_uppercase](https://doc.rust-lang.org/std/primitive.str.html#method.to_uppercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns the uppercase equivalent of this string slice, as a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

‘Uppercase’ is defined according to the terms of the Unicode Derived Core Property
`Uppercase`.

Since some characters can expand into multiple characters when changing
the case, this function returns a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") instead of modifying the
parameter in-place.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-76)Examples

Basic usage:

```
let s = "hello";

assert_eq!("HELLO", s.to_uppercase());
```

Scripts without case are not changed:

```
let new_year = "农历新年";

assert_eq!(new_year, new_year.to_uppercase());
```

One character can become multiple:

```
let s = "tschüß";

assert_eq!("TSCHÜSS", s.to_uppercase());
```

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#500)

#### pub fn [into\_string](https://doc.rust-lang.org/std/primitive.str.html#method.into_string)(self: [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a [`Box<str>`](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box") into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") without copying or allocating.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-77)Examples

```
let string = String::from("birthday gift");
let boxed_str = string.clone().into_boxed_str();

assert_eq!(boxed_str.into_string(), string);
```

1.16.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#530)

#### pub fn [repeat](https://doc.rust-lang.org/std/primitive.str.html#method.repeat)(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Creates a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") by repeating a string `n` times.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-2)Panics

This function will panic if the capacity would overflow.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-78)Examples

Basic usage:

```
assert_eq!("abc".repeat(4), String::from("abcabcabcabc"));
```

A panic upon overflow:

[ⓘ](https://doc.rust-lang.org/std/primitive.str.html "This example panics")

```
// this will panic at runtime
let huge = "0123456789abcdef".repeat(usize::MAX);
```

1.23.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#560)

#### pub fn [to\_ascii\_uppercase](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_uppercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns a copy of this string where each character is mapped to its
ASCII upper case equivalent.

ASCII letters ‘a’ to ‘z’ are mapped to ‘A’ to ‘Z’,
but non-ASCII letters are unchanged.

To uppercase the value in-place, use [`make_ascii_uppercase`](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_uppercase "method str::make_ascii_uppercase").

To uppercase ASCII characters in addition to non-ASCII characters, use
[`to_uppercase`](https://doc.rust-lang.org/std/primitive.str.html#method.to_uppercase).

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-79)Examples

```
let s = "Grüße, Jürgen ❤";

assert_eq!("GRüßE, JüRGEN ❤", s.to_ascii_uppercase());
```

1.23.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#592)

#### pub fn [to\_ascii\_lowercase](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_lowercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns a copy of this string where each character is mapped to its
ASCII lower case equivalent.

ASCII letters ‘A’ to ‘Z’ are mapped to ‘a’ to ‘z’,
but non-ASCII letters are unchanged.

To lowercase the value in-place, use [`make_ascii_lowercase`](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_lowercase "method str::make_ascii_lowercase").

To lowercase ASCII characters in addition to non-ASCII characters, use
[`to_lowercase`](https://doc.rust-lang.org/std/primitive.str.html#method.to_lowercase).

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-80)Examples

```
let s = "Grüße, Jürgen ❤";

assert_eq!("grüße, jürgen ❤", s.to_ascii_lowercase());
```

## Trait Implementations[§](https://doc.rust-lang.org/std/primitive.str.html#trait-implementations)

1.14.0 · [Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#463)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Add%3C%26str%3E-for-Cow%3C'a,+str%3E)

### impl<'a> [Add](https://doc.rust-lang.org/std/ops/trait.Add.html "trait std::ops::Add")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#464)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-11)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Add.html#associatedtype.Output) = [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

The resulting type after applying the `+` operator.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#467)[§](https://doc.rust-lang.org/std/primitive.str.html#method.add)

#### fn [add](https://doc.rust-lang.org/std/ops/trait.Add.html#tymethod.add)(self, rhs: &'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> <[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)> as [Add](https://doc.rust-lang.org/std/ops/trait.Add.html "trait std::ops::Add")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/ops/trait.Add.html#associatedtype.Output "type std::ops::Add::Output")

Performs the `+` operation. [Read more](https://doc.rust-lang.org/std/ops/trait.Add.html#tymethod.add)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2676)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Add%3C%26str%3E-for-String)

### impl [Add](https://doc.rust-lang.org/std/ops/trait.Add.html "trait std::ops::Add")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Implements the `+` operator for concatenating two strings.

This consumes the `String` on the left-hand side and re-uses its buffer (growing it if
necessary). This is done to avoid allocating a new `String` and copying the entire contents on
every operation, which would lead to *O*(*n*^2) running time when building an *n*-byte string by
repeated concatenation.

The string on the right-hand side is only borrowed; its contents are copied into the returned
`String`.

#### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-83)Examples

Concatenating two `String`s takes the first by value and borrows the second:

```
let a = String::from("hello");
let b = String::from(" world");
let c = a + &b;
// `a` is moved and can no longer be used here.
```

If you want to keep using the first `String`, you can clone it and append to the clone instead:

```
let a = String::from("hello");
let b = String::from(" world");
let c = a.clone() + &b;
// `a` is still valid here.
```

Concatenating `&str` slices can be done by converting the first to a `String`:

```
let a = "hello";
let b = " world";
let c = a.to_string() + b;
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2677)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-12)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Add.html#associatedtype.Output) = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

The resulting type after applying the `+` operator.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2680)[§](https://doc.rust-lang.org/std/primitive.str.html#method.add-1)

#### fn [add](https://doc.rust-lang.org/std/ops/trait.Add.html#tymethod.add)(self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Performs the `+` operation. [Read more](https://doc.rust-lang.org/std/ops/trait.Add.html#tymethod.add)

1.14.0 · [Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#487)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AddAssign%3C%26str%3E-for-Cow%3C'a,+str%3E)

### impl<'a> [AddAssign](https://doc.rust-lang.org/std/ops/trait.AddAssign.html "trait std::ops::AddAssign")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#488)[§](https://doc.rust-lang.org/std/primitive.str.html#method.add_assign)

#### fn [add\_assign](https://doc.rust-lang.org/std/ops/trait.AddAssign.html#tymethod.add_assign)(&mut self, rhs: &'a [str](https://doc.rust-lang.org/std/primitive.str.html))

Performs the `+=` operation. [Read more](https://doc.rust-lang.org/std/ops/trait.AddAssign.html#tymethod.add_assign)

1.12.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2691)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AddAssign%3C%26str%3E-for-String)

### impl [AddAssign](https://doc.rust-lang.org/std/ops/trait.AddAssign.html "trait std::ops::AddAssign")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Implements the `+=` operator for appending to a `String`.

This has the same behavior as the [`push_str`](https://doc.rust-lang.org/std/string/struct.String.html#method.push_str "method std::string::String::push_str") method.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2693)[§](https://doc.rust-lang.org/std/primitive.str.html#method.add_assign-1)

#### fn [add\_assign](https://doc.rust-lang.org/std/ops/trait.AddAssign.html#tymethod.add_assign)(&mut self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html))

Performs the `+=` operation. [Read more](https://doc.rust-lang.org/std/ops/trait.AddAssign.html#tymethod.add_assign)

1.43.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2996)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsMut%3Cstr%3E-for-String)

### impl [AsMut](https://doc.rust-lang.org/std/convert/trait.AsMut.html "trait std::convert::AsMut")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2998)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_mut-1)

#### fn [as\_mut](https://doc.rust-lang.org/std/convert/trait.AsMut.html#tymethod.as_mut)(&mut self) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a mutable reference of the (usually inferred) input type.

1.51.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#872)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsMut%3Cstr%3E-for-str)

### impl [AsMut](https://doc.rust-lang.org/std/convert/trait.AsMut.html "trait std::convert::AsMut")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#874)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_mut)

#### fn [as\_mut](https://doc.rust-lang.org/std/convert/trait.AsMut.html#tymethod.as_mut)(&mut self) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a mutable reference of the (usually inferred) input type.

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3082)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsRef%3C%5Bu8%5D%3E-for-str)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3084)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_ref-2)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a shared reference of the (usually inferred) input type.

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#216)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsRef%3CByteStr%3E-for-str)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#218)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_ref-1)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1704-1709)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsRef%3COsStr%3E-for-str)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1706-1708)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_ref-5)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#3551-3556)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsRef%3CPath%3E-for-str)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/path.rs.html#3553-3555)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_ref-6)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")

Converts this type into a shared reference of the (usually inferred) input type.

1.55.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3445)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsRef%3Cstr%3E-for-Drain%3C'a%3E)

### impl<'a> [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Drain](https://doc.rust-lang.org/std/string/struct.Drain.html "struct std::string::Drain")<'a>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3446)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_ref-4)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2988)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsRef%3Cstr%3E-for-String)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2990)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_ref-3)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#863)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsRef%3Cstr%3E-for-str)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#865)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_ref)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ascii.rs.html#206-210)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-AsciiExt-for-str)

### impl [AsciiExt](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html "trait std::ascii::AsciiExt") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/ascii.rs.html#207)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Owned-1)

#### type [Owned](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#associatedtype.Owned) = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

👎Deprecated since 1.26.0: use inherent methods instead

Container type for copied ASCII characters.

[Source](https://doc.rust-lang.org/src/std/ascii.rs.html#209)[§](https://doc.rust-lang.org/std/primitive.str.html#method.is_ascii-1)

#### fn [is\_ascii](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.is_ascii)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

👎Deprecated since 1.26.0: use inherent methods instead

Checks if the value is within the ASCII range. [Read more](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.is_ascii)

[Source](https://doc.rust-lang.org/src/std/ascii.rs.html#209)[§](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_uppercase-1)

#### fn [to\_ascii\_uppercase](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.to_ascii_uppercase)(&self) -> Self::[Owned](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#associatedtype.Owned "type std::ascii::AsciiExt::Owned")

👎Deprecated since 1.26.0: use inherent methods instead

Makes a copy of the value in its ASCII upper case equivalent. [Read more](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.to_ascii_uppercase)

[Source](https://doc.rust-lang.org/src/std/ascii.rs.html#209)[§](https://doc.rust-lang.org/std/primitive.str.html#method.to_ascii_lowercase-1)

#### fn [to\_ascii\_lowercase](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.to_ascii_lowercase)(&self) -> Self::[Owned](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#associatedtype.Owned "type std::ascii::AsciiExt::Owned")

👎Deprecated since 1.26.0: use inherent methods instead

Makes a copy of the value in its ASCII lower case equivalent. [Read more](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.to_ascii_lowercase)

[Source](https://doc.rust-lang.org/src/std/ascii.rs.html#209)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq_ignore_ascii_case-1)

#### fn [eq\_ignore\_ascii\_case](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.eq_ignore_ascii_case)(&self, o: &Self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

👎Deprecated since 1.26.0: use inherent methods instead

Checks that two values are an ASCII case-insensitive match. [Read more](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.eq_ignore_ascii_case)

[Source](https://doc.rust-lang.org/src/std/ascii.rs.html#209)[§](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_uppercase-1)

#### fn [make\_ascii\_uppercase](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.make_ascii_uppercase)(&mut self)

👎Deprecated since 1.26.0: use inherent methods instead

Converts this type to its ASCII upper case equivalent in-place. [Read more](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.make_ascii_uppercase)

[Source](https://doc.rust-lang.org/src/std/ascii.rs.html#209)[§](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_lowercase-1)

#### fn [make\_ascii\_lowercase](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.make_ascii_lowercase)(&mut self)

👎Deprecated since 1.26.0: use inherent methods instead

Converts this type to its ASCII lower case equivalent in-place. [Read more](https://doc.rust-lang.org/std/ascii/trait.AsciiExt.html#tymethod.make_ascii_lowercase)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#189)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Borrow%3Cstr%3E-for-String)

### impl [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#191)[§](https://doc.rust-lang.org/std/primitive.str.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

1.36.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#197)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-BorrowMut%3Cstr%3E-for-String)

### impl [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#199)[§](https://doc.rust-lang.org/std/primitive.str.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

1.3.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed.rs.html#1820)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Clone-for-Box%3Cstr%3E)

### impl [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed.rs.html#1821)[§](https://doc.rust-lang.org/std/primitive.str.html#method.clone)

#### fn [clone](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)(&self) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Returns a duplicate of the value. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/clone.rs.html#245-247)[§](https://doc.rust-lang.org/std/primitive.str.html#method.clone_from)

#### fn [clone\_from](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)(&mut self, source: &Self)

Performs copy-assignment from `source`. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#535)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-CloneToUninit-for-str)

### impl [CloneToUninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html "trait std::clone::CloneToUninit") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#538)[§](https://doc.rust-lang.org/std/primitive.str.html#method.clone_to_uninit)

#### unsafe fn [clone\_to\_uninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)(&self, dest: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html))

🔬This is a nightly-only experimental API. (`clone_to_uninit` [#126799](https://github.com/rust-lang/rust/issues/126799))

Performs copy-assignment from `self` to `dest`. [Read more](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#62)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Concat%3Cstr%3E-for-%5BS%5D)

### impl<S> [Concat](https://doc.rust-lang.org/std/slice/trait.Concat.html "trait std::slice::Concat")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [[S]](https://doc.rust-lang.org/std/primitive.slice.html) where S: [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Note: `str` in `Concat<str>` is not meaningful here.
This type parameter of the trait only exists to enable another impl.

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#63)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-13)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.Concat.html#associatedtype.Output) = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

🔬This is a nightly-only experimental API. (`slice_concat_trait` [#27747](https://github.com/rust-lang/rust/issues/27747))

The resulting type after concatenation

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#65)[§](https://doc.rust-lang.org/std/primitive.str.html#method.concat)

#### fn [concat](https://doc.rust-lang.org/std/slice/trait.Concat.html#tymethod.concat)(slice: &[[S]](https://doc.rust-lang.org/std/primitive.slice.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

🔬This is a nightly-only experimental API. (`slice_concat_trait` [#27747](https://github.com/rust-lang/rust/issues/27747))

Implementation of [`[T]::concat`](https://doc.rust-lang.org/std/primitive.slice.html#method.concat "method slice::concat")

1.0.0 · [Source](https://doc.rust-lang.org/src/core/fmt/mod.rs.html#2702)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Debug-for-str)

### impl [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/fmt/mod.rs.html#2703)[§](https://doc.rust-lang.org/std/primitive.str.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

1.28.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143894 "Tracking issue for const_default")) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3101)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Default-for-%26mut+str)

### impl [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") for &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3104)[§](https://doc.rust-lang.org/std/primitive.str.html#method.default-1)

#### fn [default](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default)() -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Creates an empty mutable str

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143894 "Tracking issue for const_default")) · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3091)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Default-for-%26str)

### impl [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") for &[str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3094)[§](https://doc.rust-lang.org/std/primitive.str.html#method.default)

#### fn [default](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default)() -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Creates an empty str

1.17.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed.rs.html#1708)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Default-for-Box%3Cstr%3E)

### impl [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed.rs.html#1710)[§](https://doc.rust-lang.org/std/primitive.str.html#method.default-2)

#### fn [default](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default)() -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Returns the “default value” for a type. [Read more](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/fmt/mod.rs.html#2751)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Display-for-str)

### impl [Display](https://doc.rust-lang.org/std/fmt/trait.Display.html "trait std::fmt::Display") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/fmt/mod.rs.html#2752)[§](https://doc.rust-lang.org/std/primitive.str.html#method.fmt-1)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Display.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Display.html#tymethod.fmt)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2431)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Extend%3C%26str%3E-for-String)

### impl<'a> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2432)[§](https://doc.rust-lang.org/std/primitive.str.html#method.extend)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [str](https://doc.rust-lang.org/std/primitive.str.html)>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2437)[§](https://doc.rust-lang.org/std/primitive.str.html#method.extend_one)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, s: &'a [str](https://doc.rust-lang.org/std/primitive.str.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#425)[§](https://doc.rust-lang.org/std/primitive.str.html#method.extend_reserve)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.84.0 · [Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3780)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26mut+str%3E-for-Arc%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&mut [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3793)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-12)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: &mut [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Allocates a reference-counted `str` and copies `v` into it.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#example-4)Example

```
let mut original = String::from("eggplant");
let original: &mut str = &mut original;
let shared: Arc<str> = Arc::from(original);
assert_eq!("eggplant", &shared[..]);
```

1.84.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#175)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26mut+str%3E-for-Box%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&mut [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#190)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-1)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &mut [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts a `&mut str` into a `Box<str>`

This conversion allocates on the heap
and performs a copy of `s`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-85)Examples

```
let mut original = String::from("hello");
let original: &mut str = &mut original;
let boxed: Box<str> = Box::from(original);
println!("{boxed}");
```

1.84.0 · [Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2755)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26mut+str%3E-for-Rc%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&mut [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2768)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-6)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: &mut [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Allocates a reference-counted string slice and copies `v` into it.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#example-1)Example

```
let mut original = String::from("statue");
let original: &mut str = &mut original;
let shared: Rc<str> = Rc::from(original);
assert_eq!("statue", &shared[..]);
```

1.44.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3025)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26mut+str%3E-for-String)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&mut [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3030)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-8)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &mut [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a `&mut str` into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

The result is allocated on the heap.

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3761)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-Arc%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3772)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-11)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Allocates a reference-counted `str` and copies `v` into it.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#example-3)Example

```
let shared: Arc<str> = Arc::from("eggplant");
assert_eq!("eggplant", &shared[..]);
```

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#676)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-Box%3Cdyn+Error%3E)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + 'a>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#690)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-4)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(err: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + 'a>

Converts a [`str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str") into a box of dyn [`Error`](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-88)Examples

```
use std::error::Error;

let a_str_error = "a str error";
let a_boxed_error = Box::<dyn Error>::from(a_str_error);
assert!(size_of::<Box<dyn Error>>() == size_of_val(&a_boxed_error))
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#653)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-Box%3Cdyn+Error+%2B+Send+%2B+Sync%3E)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") + 'a>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#669)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-3)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(err: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") + 'a>

Converts a [`str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str") into a box of dyn [`Error`](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + [`Send`](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + [`Sync`](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync").

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-87)Examples

```
use std::error::Error;

let a_str_error = "a str error";
let a_boxed_error = Box::<dyn Error + Send + Sync>::from(a_str_error);
assert!(
    size_of::<Box<dyn Error + Send + Sync>>() == size_of_val(&a_boxed_error))
```

1.17.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#155)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-Box%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#168)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts a `&str` into a `Box<str>`

This conversion allocates on the heap
and performs a copy of `s`.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-84)Examples

```
let boxed: Box<str> = Box::from("hello");
println!("{boxed}");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3112)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-Cow%3C'a,+str%3E)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3126)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-10)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts a string slice into a [`Borrowed`](https://doc.rust-lang.org/std/borrow/enum.Cow.html#variant.Borrowed "borrow::Cow::Borrowed") variant.
No heap allocation is performed, and the string
is not copied.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#example-2)Example

```
assert_eq!(Cow::from("eggplant"), Cow::Borrowed("eggplant"));
```

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2736)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-Rc%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2747)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-5)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Allocates a reference-counted string slice and copies `v` into it.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#example)Example

```
let shared: Rc<str> = Rc::from("statue");
assert_eq!("statue", &shared[..]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3013)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-String)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3018)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-7)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a `&str` into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

The result is allocated on the heap.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4255)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3C%26str%3E-for-Vec%3Cu8%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/vec/mod.rs.html#4264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-13)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

Allocates a `Vec<u8>` and fills it with a UTF-8 string.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-90)Examples

```
assert_eq!(Vec::from("123"), vec![b'1', b'2', b'3']);
```

1.45.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#197)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3CCow%3C'_,+str%3E%3E-for-Box%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'\_, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#222)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-2)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(cow: [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'\_, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts a `Cow<'_, str>` into a `Box<str>`

When `cow` is the `Cow::Borrowed` variant, this
conversion allocates on the heap and copies the
underlying `str`. Otherwise, it will try to reuse the owned
`String`’s allocation.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-86)Examples

```
use std::borrow::Cow;

let unboxed = Cow::Borrowed("hello");
let boxed: Box<str> = Box::from(unboxed);
println!("{boxed}");
```

```
let unboxed = Cow::Owned("hello".to_string());
let boxed: Box<str> = Box::from(unboxed);
println!("{boxed}");
```

1.20.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3069)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-From%3CString%3E-for-Box%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3081)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from-9)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts the given [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") to a boxed `str` slice that is owned.

##### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-89)Examples

```
let s1: String = String::from("hello world");
let s2: Box<str> = Box::from(s1);
let s3: String = String::from(s2);

assert_eq!("hello world", s3)
```

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#158)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3C%26char%3E-for-Box%3Cstr%3E)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<&'a [char](https://doc.rust-lang.org/std/primitive.char.html)> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#159)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-1)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [char](https://doc.rust-lang.org/std/primitive.char.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#166)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3C%26str%3E-for-Box%3Cstr%3E)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#167)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-2)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [str](https://doc.rust-lang.org/std/primitive.str.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#280)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3C%26str%3E-for-ByteString)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#282)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-6)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString") where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [str](https://doc.rust-lang.org/std/primitive.str.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.12.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3186)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3C%26str%3E-for-Cow%3C'a,+str%3E)

### impl<'a, 'b> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<&'b [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3187)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-8)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(it: I) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)> where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'b [str](https://doc.rust-lang.org/std/primitive.str.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2333)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3C%26str%3E-for-String)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2334)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-7)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [str](https://doc.rust-lang.org/std/primitive.str.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#182)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3CBox%3Cstr,+A%3E%3E-for-Box%3Cstr%3E)

### impl<A> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html), A>> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#183)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-4)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html), A>>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#190)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3CCow%3C'a,+str%3E%3E-for-Box%3Cstr%3E)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#191)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-5)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#174)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3CString%3E-for-Box%3Cstr%3E)

### impl [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#175)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter-3)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#150)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-FromIterator%3Cchar%3E-for-Box%3Cstr%3E)

### impl [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[char](https://doc.rust-lang.org/std/primitive.char.html)> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#151)[§](https://doc.rust-lang.org/std/primitive.str.html#method.from_iter)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [char](https://doc.rust-lang.org/std/primitive.char.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/hash/mod.rs.html#861)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Hash-for-str)

### impl [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/hash/mod.rs.html#863)[§](https://doc.rust-lang.org/std/primitive.str.html#method.hash)

#### fn [hash](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)<H>(&self, state: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"),

Feeds this value into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#55-57)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Index%3CI%3E-for-str)

### impl<I> [Index](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index")<I> for [str](https://doc.rust-lang.org/std/primitive.str.html) where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#59)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Index.html#associatedtype.Output) = <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

The returned type after indexing.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#62)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index)

#### fn [index](https://doc.rust-lang.org/std/ops/trait.Index.html#tymethod.index)(&self, index: I) -> &<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

Performs the indexing (`container[index]`) operation. [Read more](https://doc.rust-lang.org/std/ops/trait.Index.html#tymethod.index)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#69-71)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-IndexMut%3CI%3E-for-str)

### impl<I> [IndexMut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html "trait std::ops::IndexMut")<I> for [str](https://doc.rust-lang.org/std/primitive.str.html) where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#74)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut)

#### fn [index\_mut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html#tymethod.index_mut)(&mut self, index: I) -> &mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

Performs the mutable indexing (`container[index]`) operation. [Read more](https://doc.rust-lang.org/std/ops/trait.IndexMut.html#tymethod.index_mut)

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#72)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Join%3C%26str%3E-for-%5BS%5D)

### impl<S> [Join](https://doc.rust-lang.org/std/slice/trait.Join.html "trait std::slice::Join")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [[S]](https://doc.rust-lang.org/std/primitive.slice.html) where S: [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#73)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-14)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.Join.html#associatedtype.Output) = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

🔬This is a nightly-only experimental API. (`slice_concat_trait` [#27747](https://github.com/rust-lang/rust/issues/27747))

The resulting type after concatenation

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#75)[§](https://doc.rust-lang.org/std/primitive.str.html#method.join)

#### fn [join](https://doc.rust-lang.org/std/slice/trait.Join.html#tymethod.join)(slice: &[[S]](https://doc.rust-lang.org/std/primitive.slice.html), sep: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

🔬This is a nightly-only experimental API. (`slice_concat_trait` [#27747](https://github.com/rust-lang/rust/issues/27747))

Implementation of [`[T]::join`](https://doc.rust-lang.org/std/primitive.slice.html#method.join "method slice::join")

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#18)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Ord-for-str)

### impl [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for [str](https://doc.rust-lang.org/std/primitive.str.html)

Implements ordering of strings.

Strings are ordered [lexicographically](https://doc.rust-lang.org/std/cmp/trait.Ord.html#lexicographical-comparison "trait std::cmp::Ord") by their byte values. This orders Unicode code
points based on their positions in the code charts. This is not necessarily the same as
“alphabetical” order, which varies by language and locale. Sorting strings according to
culturally-accepted standards requires locale-specific data that is outside the scope of
the `str` type.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#20)[§](https://doc.rust-lang.org/std/primitive.str.html#method.cmp)

#### fn [cmp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")

This method returns an [`Ordering`](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering") between `self` and `other`. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#143)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3C%26str%3E-for-ByteStr)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#143)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-2)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-2)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#533)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3C%26str%3E-for-ByteString)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#533)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-7)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-7)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2599)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3C%26str%3E-for-Cow%3C'a,+str%3E)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&'b [str](https://doc.rust-lang.org/std/primitive.str.html)> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2599)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-15)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&'b [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2599)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-15)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &&'b [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.29.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#745-750)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3C%26str%3E-for-OsString)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#747-749)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-19)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-19)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3C%26str%3E-for-String)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-11)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-11)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &&'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#143)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CByteStr%3E-for-%26str)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for &[str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#143)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-3)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-3)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#141)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CByteStr%3E-for-str)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#141)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-1)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-1)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#533)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CByteString%3E-for-%26str)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")> for &[str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#533)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-8)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-8)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#531)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CByteString%3E-for-str)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#531)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-6)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-6)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2599)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CCow%3C'a,+str%3E%3E-for-%26str)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for &'b [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2599)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-16)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2599)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-16)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2597)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CCow%3C'a,+str%3E%3E-for-str)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2597)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-14)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2597)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-14)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1500-1505)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3COsStr%3E-for-str)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1502-1504)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-22)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-22)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.29.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#753-758)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3COsString%3E-for-%26str)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")> for &'a [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#755-757)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-20)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-20)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#737-742)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3COsString%3E-for-str)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#739-741)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-18)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-18)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#3418-3423)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CPath%3E-for-str)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/path.rs.html#3420-3422)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-26)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-26)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#2115-2120)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CPathBuf%3E-for-str)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/path.rs.html#2117-2119)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-24)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-24)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CString%3E-for-%26str)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for &'a [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-12)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-12)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3CString%3E-for-str)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-10)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-10)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#141)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-ByteStr)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")

[Source](https://doc.rust-lang.org/src/core/bstr/traits.rs.html#141)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#531)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-ByteString)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#531)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-5)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-5)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2597)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-Cow%3C'a,+str%3E)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2597)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-13)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2597)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-13)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1492-1497)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-OsStr)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1494-1496)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-21)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-21)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#729-734)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-OsString)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#731-733)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-17)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-17)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#3409-3415)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-Path)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#3411-3414)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-25)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-25)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#2107-2112)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-PathBuf)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#2109-2111)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-23)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-23)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq%3Cstr%3E-for-String)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-9)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-9)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143800 "Tracking issue for const_cmp")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#27)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialEq-for-str)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#29)[§](https://doc.rust-lang.org/std/primitive.str.html#method.eq-4)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ne-4)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1535-1540)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialOrd%3Cstr%3E-for-OsStr)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1537-1539)[§](https://doc.rust-lang.org/std/primitive.str.html#method.partial_cmp-2)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/primitive.str.html#method.lt-2)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/primitive.str.html#method.le-2)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/primitive.str.html#method.gt-2)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ge-2)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#788-793)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialOrd%3Cstr%3E-for-OsString)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#790-792)[§](https://doc.rust-lang.org/std/primitive.str.html#method.partial_cmp-1)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/primitive.str.html#method.lt-1)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/primitive.str.html#method.le-1)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/primitive.str.html#method.gt-1)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ge-1)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#46)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-PartialOrd-for-str)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd") for [str](https://doc.rust-lang.org/std/primitive.str.html)

Implements comparison operations on strings.

Strings are compared [lexicographically](https://doc.rust-lang.org/std/cmp/trait.Ord.html#lexicographical-comparison "trait std::cmp::Ord") by their byte values. This compares Unicode code
points based on their positions in the code charts. This is not necessarily the same as
“alphabetical” order, which varies by language and locale. Comparing strings according to
culturally-accepted standards requires locale-specific data that is outside the scope of
the `str` type.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#48)[§](https://doc.rust-lang.org/std/primitive.str.html#method.partial_cmp)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/primitive.str.html#method.lt)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/primitive.str.html#method.le)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/primitive.str.html#method.gt)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/primitive.str.html#method.ge)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#972)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Pattern-for-%26str)

### impl<'b> [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern") for &'b [str](https://doc.rust-lang.org/std/primitive.str.html)

Non-allocating substring search.

Will handle the pattern `""` as returning empty matches at each character
boundary.

#### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-82)Examples

```
assert_eq!("Hello world".find("world"), Some(6));
```

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#982)[§](https://doc.rust-lang.org/std/primitive.str.html#method.is_prefix_of)

#### fn [is\_prefix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.is_prefix_of)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Checks whether the pattern matches at the front of the haystack.

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#988)[§](https://doc.rust-lang.org/std/primitive.str.html#method.is_contained_in)

#### fn [is\_contained\_in](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.is_contained_in)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Checks whether the pattern matches anywhere in the haystack

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#1017)[§](https://doc.rust-lang.org/std/primitive.str.html#method.strip_prefix_of)

#### fn [strip\_prefix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.strip_prefix_of)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[str](https://doc.rust-lang.org/std/primitive.str.html)>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Removes the pattern from the front of haystack, if it matches.

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#1028-1030)[§](https://doc.rust-lang.org/std/primitive.str.html#method.is_suffix_of)

#### fn [is\_suffix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.is_suffix_of)<'a>(self, haystack: &'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where <&'b [str](https://doc.rust-lang.org/std/primitive.str.html) as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Checks whether the pattern matches at the back of the haystack.

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#1037-1039)[§](https://doc.rust-lang.org/std/primitive.str.html#method.strip_suffix_of)

#### fn [strip\_suffix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.strip_suffix_of)<'a>(self, haystack: &'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> where <&'b [str](https://doc.rust-lang.org/std/primitive.str.html) as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Removes the pattern from the back of haystack, if it matches.

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#973)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Searcher)

#### type [Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher)<'a> = [StrSearcher](https://doc.rust-lang.org/std/str/pattern/struct.StrSearcher.html "struct std::str::pattern::StrSearcher")<'a, 'b>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Associated searcher for this pattern

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#976)[§](https://doc.rust-lang.org/std/primitive.str.html#method.into_searcher)

#### fn [into\_searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#tymethod.into_searcher)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [StrSearcher](https://doc.rust-lang.org/std/str/pattern/struct.StrSearcher.html "struct std::str::pattern::StrSearcher")<'\_, 'b>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Constructs the associated searcher from
`self` and the `haystack` to search in.

[Source](https://doc.rust-lang.org/src/core/str/pattern.rs.html#1051)[§](https://doc.rust-lang.org/std/primitive.str.html#method.as_utf8_pattern)

#### fn [as\_utf8\_pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.as_utf8_pattern)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Utf8Pattern](https://doc.rust-lang.org/std/str/pattern/enum.Utf8Pattern.html "enum std::str::pattern::Utf8Pattern")<'\_>>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Returns the pattern as utf-8 bytes if possible.

1.73.0 · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#387)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-(Bound%3Cusize%3E,+Bound%3Cusize%3E))

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for ([Bound](https://doc.rust-lang.org/std/ops/enum.Bound.html "enum std::ops::Bound")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>, [Bound](https://doc.rust-lang.org/std/ops/enum.Bound.html "enum std::ops::Bound")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>)

Implements substring slicing for arbitrary bounds.

Returns a slice of the given string bounded by the byte indices
provided by each bound.

This operation is *O*(1).

#### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-4)Panics

Panics if `begin` or `end` (if it exists and once adjusted for
inclusion/exclusion) does not point to the starting byte offset of
a character (as defined by `is_char_boundary`), if `begin > end`, or if
`end > len`.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#388)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-4)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#391)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-4)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[str](https://doc.rust-lang.org/std/primitive.str.html)>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#396)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-4)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)(self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut [str](https://doc.rust-lang.org/std/primitive.str.html)>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#401)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-4)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)(self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#408)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-4)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)(self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#415)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-4)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#420)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-4)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)(self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html)) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

1.20.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#165)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-Range%3Cusize%3E)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Implements substring slicing with syntax `&self[begin .. end]` or `&mut self[begin .. end]`.

Returns a slice of the given string from the byte range
[`begin`, `end`).

This operation is *O*(1).

Prior to 1.20.0, these indexing operations were still supported by
direct implementation of `Index` and `IndexMut`.

#### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-3)Panics

Panics if `begin` or `end` does not point to the starting byte offset of
a character (as defined by `is_char_boundary`), if `begin > end`, or if
`end > len`.

#### [§](https://doc.rust-lang.org/std/primitive.str.html#examples-81)Examples

```
let s = "Löwe 老虎 Léopard";
assert_eq!(&s[0 .. 1], "L");

assert_eq!(&s[1 .. 9], "öwe 老");

// these will panic:
// byte 2 lies within `ö`:
// &s[2 ..3];

// byte 8 lies within `老`
// &s[1 .. 8];

// byte 100 is outside the string
// &s[3 .. 100];
```

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#166)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-2)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#168)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-2)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#182)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-2)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#196)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-2)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#224)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-2)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#244)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-2)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> &<[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#252)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-2)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#270)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-Range%3Cusize%3E-1)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [Range](https://doc.rust-lang.org/std/range/struct.Range.html "struct std::range::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#271)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-3)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#273)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-3)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[Range](https://doc.rust-lang.org/std/range/struct.Range.html "struct std::range::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#287)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-3)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[Range](https://doc.rust-lang.org/std/range/struct.Range.html "struct std::range::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#301)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-3)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[Range](https://doc.rust-lang.org/std/range/struct.Range.html "struct std::range::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#329)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-3)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[Range](https://doc.rust-lang.org/std/range/struct.Range.html "struct std::range::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#349)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-3)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> &<[Range](https://doc.rust-lang.org/std/range/struct.Range.html "struct std::range::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#357)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-3)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[Range](https://doc.rust-lang.org/std/range/struct.Range.html "struct std::range::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

1.20.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#511)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-RangeFrom%3Cusize%3E)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html "struct std::ops::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Implements substring slicing with syntax `&self[begin ..]` or `&mut self[begin ..]`.

Returns a slice of the given string from the byte range [`begin`, `len`).
Equivalent to `&self[begin .. len]` or `&mut self[begin .. len]`.

This operation is *O*(1).

Prior to 1.20.0, these indexing operations were still supported by
direct implementation of `Index` and `IndexMut`.

#### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-6)Panics

Panics if `begin` does not point to the starting byte offset of
a character (as defined by `is_char_boundary`), or if `begin > len`.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#512)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-6)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#514)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-6)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html "struct std::ops::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#524)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-6)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html "struct std::ops::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#534)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-6)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html "struct std::ops::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#540)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-6)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html "struct std::ops::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#546)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-6)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> &<[RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html "struct std::ops::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#554)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-6)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[RangeFrom](https://doc.rust-lang.org/std/ops/struct.RangeFrom.html "struct std::ops::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#567)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-RangeFrom%3Cusize%3E-1)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [RangeFrom](https://doc.rust-lang.org/std/range/struct.RangeFrom.html "struct std::range::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#568)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-7)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#570)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-7)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[RangeFrom](https://doc.rust-lang.org/std/range/struct.RangeFrom.html "struct std::range::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#580)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-7)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[RangeFrom](https://doc.rust-lang.org/std/range/struct.RangeFrom.html "struct std::range::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#590)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-7)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeFrom](https://doc.rust-lang.org/std/range/struct.RangeFrom.html "struct std::range::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#596)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-7)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeFrom](https://doc.rust-lang.org/std/range/struct.RangeFrom.html "struct std::range::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#602)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-7)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> &<[RangeFrom](https://doc.rust-lang.org/std/range/struct.RangeFrom.html "struct std::range::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#610)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-7)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[RangeFrom](https://doc.rust-lang.org/std/range/struct.RangeFrom.html "struct std::range::RangeFrom")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

1.20.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#100)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-RangeFull)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html "struct std::ops::RangeFull")

Implements substring slicing with syntax `&self[..]` or `&mut self[..]`.

Returns a slice of the whole string, i.e., returns `&self` or `&mut self`. Equivalent to `&self[0 .. len]` or `&mut self[0 .. len]`. Unlike
other indexing operations, this can never panic.

This operation is *O*(1).

Prior to 1.20.0, these indexing operations were still supported by
direct implementation of `Index` and `IndexMut`.

Equivalent to `&self[0 .. len]` or `&mut self[0 .. len]`.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#101)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-1)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#103)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-1)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html "struct std::ops::RangeFull") as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#107)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-1)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html "struct std::ops::RangeFull") as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#111)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-1)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html "struct std::ops::RangeFull") as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#115)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-1)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html "struct std::ops::RangeFull") as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#119)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-1)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> &<[RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html "struct std::ops::RangeFull") as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#123)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-1)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[RangeFull](https://doc.rust-lang.org/std/ops/struct.RangeFull.html "struct std::ops::RangeFull") as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

1.26.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#639)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-RangeInclusive%3Cusize%3E)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [RangeInclusive](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Implements substring slicing with syntax `&self[begin ..= end]` or `&mut self[begin ..= end]`.

Returns a slice of the given string from the byte range
[`begin`, `end`]. Equivalent to `&self [begin .. end + 1]` or `&mut self[begin .. end + 1]`, except if `end` has the maximum value for
`usize`.

This operation is *O*(1).

#### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-7)Panics

Panics if `begin` does not point to the starting byte offset of
a character (as defined by `is_char_boundary`), if `end` does not point
to the ending byte offset of a character (`end + 1` is either a starting
byte offset or equal to `len`), if `begin > end`, or if `end >= len`.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#640)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-8)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#642)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-8)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[RangeInclusive](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#646)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-8)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[RangeInclusive](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#650)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-8)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeInclusive](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#655)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-8)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeInclusive](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#660)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-8)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &<[RangeInclusive](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#667)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-8)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[RangeInclusive](https://doc.rust-lang.org/std/ops/struct.RangeInclusive.html "struct std::ops::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") [ⓘ](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#677)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-RangeInclusive%3Cusize%3E-1)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [RangeInclusive](https://doc.rust-lang.org/std/range/struct.RangeInclusive.html "struct std::range::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#678)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-9)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#680)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-9)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[RangeInclusive](https://doc.rust-lang.org/std/range/struct.RangeInclusive.html "struct std::range::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#684)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-9)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[RangeInclusive](https://doc.rust-lang.org/std/range/struct.RangeInclusive.html "struct std::range::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#688)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-9)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeInclusive](https://doc.rust-lang.org/std/range/struct.RangeInclusive.html "struct std::range::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#693)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-9)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeInclusive](https://doc.rust-lang.org/std/range/struct.RangeInclusive.html "struct std::range::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#698)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-9)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &<[RangeInclusive](https://doc.rust-lang.org/std/range/struct.RangeInclusive.html "struct std::range::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#705)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-9)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[RangeInclusive](https://doc.rust-lang.org/std/range/struct.RangeInclusive.html "struct std::range::RangeInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

1.20.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#442)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-RangeTo%3Cusize%3E)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html "struct std::ops::RangeTo")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Implements substring slicing with syntax `&self[.. end]` or `&mut self[.. end]`.

Returns a slice of the given string from the byte range [0, `end`).
Equivalent to `&self[0 .. end]` or `&mut self[0 .. end]`.

This operation is *O*(1).

Prior to 1.20.0, these indexing operations were still supported by
direct implementation of `Index` and `IndexMut`.

#### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-5)Panics

Panics if `end` does not point to the starting byte offset of a
character (as defined by `is_char_boundary`), or if `end > len`.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#443)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-5)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#445)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-5)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html "struct std::ops::RangeTo")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#455)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-5)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html "struct std::ops::RangeTo")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#465)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-5)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html "struct std::ops::RangeTo")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#470)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-5)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html "struct std::ops::RangeTo")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#475)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-5)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)(self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> &<[RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html "struct std::ops::RangeTo")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#483)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-5)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[RangeTo](https://doc.rust-lang.org/std/ops/struct.RangeTo.html "struct std::ops::RangeTo")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

1.26.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143775 "Tracking issue for const_index")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#729)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-SliceIndex%3Cstr%3E-for-RangeToInclusive%3Cusize%3E)

### impl [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [RangeToInclusive](https://doc.rust-lang.org/std/ops/struct.RangeToInclusive.html "struct std::ops::RangeToInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>

Implements substring slicing with syntax `&self[..= end]` or `&mut self[..= end]`.

Returns a slice of the given string from the byte range [0, `end`].
Equivalent to `&self [0 .. end + 1]`, except if `end` has the maximum
value for `usize`.

This operation is *O*(1).

#### [§](https://doc.rust-lang.org/std/primitive.str.html#panics-8)Panics

Panics if `end` does not point to the ending byte offset of a character
(`end + 1` is either a starting byte offset as defined by
`is_char_boundary`, or equal to `len`), or if `end >= len`.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#730)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Output-10)

#### type [Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The output type returned by methods.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#732)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get-10)

#### fn [get](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<[RangeToInclusive](https://doc.rust-lang.org/std/ops/struct.RangeToInclusive.html "struct std::ops::RangeToInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#736)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_mut-10)

#### fn [get\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <[RangeToInclusive](https://doc.rust-lang.org/std/ops/struct.RangeToInclusive.html "struct std::ops::RangeToInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")>

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, if in
bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#740)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked-10)

#### unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)( self, slice: [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeToInclusive](https://doc.rust-lang.org/std/ops/struct.RangeToInclusive.html "struct std::ops::RangeToInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#745)[§](https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked_mut-10)

#### unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)( self, slice: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) <[RangeToInclusive](https://doc.rust-lang.org/std/ops/struct.RangeToInclusive.html "struct std::ops::RangeToInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable pointer to the output at this location, without
performing any bounds checking. [Read more](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.get_unchecked_mut)

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#750)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index-10)

#### fn [index](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index)( self, slice: &[str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &<[RangeToInclusive](https://doc.rust-lang.org/std/ops/struct.RangeToInclusive.html "struct std::ops::RangeToInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a shared reference to the output at this location, panicking
if out of bounds.

[Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#754)[§](https://doc.rust-lang.org/std/primitive.str.html#method.index_mut-10)

#### fn [index\_mut](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#tymethod.index_mut)( self, slice: &mut [str](https://doc.rust-lang.org/std/primitive.str.html), ) -> &mut <[RangeToInclusive](https://doc.rust-lang.org/std/ops/struct.RangeToInclusive.html "struct std::ops::RangeToInclusive")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

🔬This is a nightly-only experimental API. (`slice_index_methods`)

Returns a mutable reference to the output at this location, panicking
if out of bounds.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#206)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-ToOwned-for-str)

### impl [ToOwned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html "trait std::borrow::ToOwned") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#207)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Owned)

#### type [Owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#associatedtype.Owned) = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

The resulting type after obtaining ownership.

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#210)[§](https://doc.rust-lang.org/std/primitive.str.html#method.to_owned)

#### fn [to\_owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Creates owned data from borrowed data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#215)[§](https://doc.rust-lang.org/std/primitive.str.html#method.clone_into)

#### fn [clone\_into](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)(&self, target: &mut [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"))

Uses borrowed data to replace owned data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)

1.0.0 · [Source](https://doc.rust-lang.org/src/std/net/socket_addr.rs.html#232-242)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-ToSocketAddrs-for-str)

### impl [ToSocketAddrs](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html "trait std::net::ToSocketAddrs") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/net/socket_addr.rs.html#233)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Iter)

#### type [Iter](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html#associatedtype.Iter) = [IntoIter](https://doc.rust-lang.org/std/vec/struct.IntoIter.html "struct std::vec::IntoIter")<[SocketAddr](https://doc.rust-lang.org/std/net/enum.SocketAddr.html "enum std::net::SocketAddr")>

Returned iterator over socket addresses which this type may correspond
to.

[Source](https://doc.rust-lang.org/src/std/net/socket_addr.rs.html#234-241)[§](https://doc.rust-lang.org/std/primitive.str.html#method.to_socket_addrs)

#### fn [to\_socket\_addrs](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html#tymethod.to_socket_addrs)(&self) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[IntoIter](https://doc.rust-lang.org/std/vec/struct.IntoIter.html "struct std::vec::IntoIter")<[SocketAddr](https://doc.rust-lang.org/std/net/enum.SocketAddr.html "enum std::net::SocketAddr")>>

Converts this object to an iterator of resolved [`SocketAddr`](https://doc.rust-lang.org/std/net/enum.SocketAddr.html "enum std::net::SocketAddr")s. [Read more](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html#tymethod.to_socket_addrs)

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#320)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-TryFrom%3C%26ByteStr%3E-for-%26str)

### impl<'a> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for &'a [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#321)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Utf8Error](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#324)[§](https://doc.rust-lang.org/std/primitive.str.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( s: &'a [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr"), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html), <&'a [str](https://doc.rust-lang.org/std/primitive.str.html) as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#581)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-TryFrom%3C%26ByteString%3E-for-%26str)

### impl<'a> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")> for &'a [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#582)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Error-2)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Utf8Error](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#585)[§](https://doc.rust-lang.org/std/primitive.str.html#method.try_from-2)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( s: &'a [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString"), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html), <&'a [str](https://doc.rust-lang.org/std/primitive.str.html) as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

1.72.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1448-1463)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-TryFrom%3C%26OsStr%3E-for-%26str)

### impl<'a> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a [OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")> for &'a [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1460-1462)[§](https://doc.rust-lang.org/std/primitive.str.html#method.try_from-3)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: &'a [OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<Self, Self::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Tries to convert an `&OsStr` to a `&str`.

```
use std::ffi::OsStr;

let os_str = OsStr::new("foo");
let as_str = <&str>::try_from(os_str).unwrap();
assert_eq!(as_str, "foo");
```

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1449)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Error-3)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Utf8Error](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#331)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-TryFrom%3C%26mut+ByteStr%3E-for-%26mut+str)

### impl<'a> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a mut [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for &'a mut [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#332)[§](https://doc.rust-lang.org/std/primitive.str.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Utf8Error](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/bstr/mod.rs.html#335)[§](https://doc.rust-lang.org/std/primitive.str.html#method.try_from-1)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( s: &'a mut [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr"), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<&'a mut [str](https://doc.rust-lang.org/std/primitive.str.html), <&'a mut [str](https://doc.rust-lang.org/std/primitive.str.html) as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a mut [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143800 "Tracking issue for const_cmp")) · [Source](https://doc.rust-lang.org/src/core/str/traits.rs.html#36)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Eq-for-str)

### impl [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq") for [str](https://doc.rust-lang.org/std/primitive.str.html)

1.65.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#3166)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Error-for-%26str)

### impl ![Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") for &[str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/marker.rs.html#265-277)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-StructuralPartialEq-for-str)

### impl [StructuralPartialEq](https://doc.rust-lang.org/std/marker/trait.StructuralPartialEq.html "trait std::marker::StructuralPartialEq") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/core/marker.rs.html#1125-1138)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-UnsizedConstParamTy-for-str)

### impl [UnsizedConstParamTy](https://doc.rust-lang.org/std/marker/trait.UnsizedConstParamTy.html "trait std::marker::UnsizedConstParamTy") for [str](https://doc.rust-lang.org/std/primitive.str.html)

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/primitive.str.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Freeze-for-str)

### impl [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[§](https://doc.rust-lang.org/std/primitive.str.html#impl-RefUnwindSafe-for-str)

### impl [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Send-for-str)

### impl [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Sized-for-str)

### impl ![Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Sync-for-str)

### impl [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Unpin-for-str)

### impl [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [str](https://doc.rust-lang.org/std/primitive.str.html)

[§](https://doc.rust-lang.org/std/primitive.str.html#impl-UnwindSafe-for-str)

### impl [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [str](https://doc.rust-lang.org/std/primitive.str.html)

## Blanket Implementations[§](https://doc.rust-lang.org/std/primitive.str.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/primitive.str.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/primitive.str.html#method.borrow-1)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/primitive.str.html#method.borrow_mut-1)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2796)[§](https://doc.rust-lang.org/std/primitive.str.html#impl-ToString-for-T)

### impl<T> [ToString](https://doc.rust-lang.org/std/string/trait.ToString.html "trait std::string::ToString") for T where T: [Display](https://doc.rust-lang.org/std/fmt/trait.Display.html "trait std::fmt::Display") + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2798)[§](https://doc.rust-lang.org/std/primitive.str.html#method.to_string)

#### fn [to\_string](https://doc.rust-lang.org/std/string/trait.ToString.html#tymethod.to_string)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts the given value to a `String`. [Read more](https://doc.rust-lang.org/std/string/trait.ToString.html#tymethod.to_string)