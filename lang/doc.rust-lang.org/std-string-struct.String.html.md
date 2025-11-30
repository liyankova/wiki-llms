---
url: https://doc.rust-lang.org/std/string/struct.String.html
title: String in std::string - Rust
source_domain: doc.rust-lang.org
---

# String in std::string - Rust

## [String](https://doc.rust-lang.org/std/string/struct.String.html)

[std](https://doc.rust-lang.org/std/index.html)::[string](https://doc.rust-lang.org/std/string/index.html)

# Struct String

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#360)

```
pub struct String { /* private fields */ }
```

Expand description

A UTF-8–encoded, growable string.

`String` is the most common string type. It has ownership over the contents
of the string, stored in a heap-allocated buffer (see [Representation](https://doc.rust-lang.org/std/string/struct.String.html#representation)).
It is closely related to its borrowed counterpart, the primitive [`str`](https://doc.rust-lang.org/std/primitive.str.html "str").

## [§](https://doc.rust-lang.org/std/string/struct.String.html#examples)Examples

You can create a `String` from [a literal string](https://doc.rust-lang.org/std/primitive.str.html "&str") with [`String::from`](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from "associated function std::convert::From::from"):

```
let hello = String::from("Hello, world!");
```

You can append a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") to a `String` with the [`push`](https://doc.rust-lang.org/std/string/struct.String.html#method.push "method std::string::String::push") method, and
append a [`&str`](https://doc.rust-lang.org/std/primitive.str.html "&str") with the [`push_str`](https://doc.rust-lang.org/std/string/struct.String.html#method.push_str "method std::string::String::push_str") method:

```
let mut hello = String::from("Hello, ");

hello.push('w');
hello.push_str("orld!");
```

If you have a vector of UTF-8 bytes, you can create a `String` from it with
the [`from_utf8`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8 "associated function std::string::String::from_utf8") method:

```
// some bytes, in a vector
let sparkle_heart = vec![240, 159, 146, 150];

// We know these bytes are valid, so we'll use `unwrap()`.
let sparkle_heart = String::from_utf8(sparkle_heart).unwrap();

assert_eq!("💖", sparkle_heart);
```

## [§](https://doc.rust-lang.org/std/string/struct.String.html#utf-8)UTF-8

`String`s are always valid UTF-8. If you need a non-UTF-8 string, consider
[`OsString`](https://doc.rust-lang.org/std/ffi/struct.OsString.html "ffi::OsString"). It is similar, but without the UTF-8 constraint. Because UTF-8
is a variable width encoding, `String`s are typically smaller than an array of
the same `char`s:

```
// `s` is ASCII which represents each `char` as one byte
let s = "hello";
assert_eq!(s.len(), 5);

// A `char` array with the same contents would be longer because
// every `char` is four bytes
let s = ['h', 'e', 'l', 'l', 'o'];
let size: usize = s.into_iter().map(|c| size_of_val(&c)).sum();
assert_eq!(size, 20);

// However, for non-ASCII strings, the difference will be smaller
// and sometimes they are the same
let s = "💖💖💖💖💖";
assert_eq!(s.len(), 20);

let s = ['💖', '💖', '💖', '💖', '💖'];
let size: usize = s.into_iter().map(|c| size_of_val(&c)).sum();
assert_eq!(size, 20);
```

This raises interesting questions as to how `s[i]` should work.
What should `i` be here? Several options include byte indices and
`char` indices but, because of UTF-8 encoding, only byte indices
would provide constant time indexing. Getting the `i`th `char`, for
example, is available using [`chars`](https://doc.rust-lang.org/std/primitive.str.html#method.chars "method str::chars"):

```
let s = "hello";
let third_character = s.chars().nth(2);
assert_eq!(third_character, Some('l'));

let s = "💖💖💖💖💖";
let third_character = s.chars().nth(2);
assert_eq!(third_character, Some('💖'));
```

Next, what should `s[i]` return? Because indexing returns a reference
to underlying data it could be `&u8`, `&[u8]`, or something similar.
Since we’re only providing one index, `&u8` makes the most sense but that
might not be what the user expects and can be explicitly achieved with
[`as_bytes()`](https://doc.rust-lang.org/std/primitive.str.html#method.as_bytes "method str::as_bytes"):

```
// The first byte is 104 - the byte value of `'h'`
let s = "hello";
assert_eq!(s.as_bytes()[0], 104);
// or
assert_eq!(s.as_bytes()[0], b'h');

// The first byte is 240 which isn't obviously useful
let s = "💖💖💖💖💖";
assert_eq!(s.as_bytes()[0], 240);
```

Due to these ambiguities/restrictions, indexing with a `usize` is simply
forbidden:

[ⓘ](https://doc.rust-lang.org/std/string/struct.String.html "This example deliberately fails to compile")

```
let s = "hello";

// The following will not compile!
println!("The first letter of s is {}", s[0]);
```

It is more clear, however, how `&s[i..j]` should work (that is,
indexing with a range). It should accept byte indices (to be constant-time)
and return a `&str` which is UTF-8 encoded. This is also called “string slicing”.
Note this will panic if the byte indices provided are not character
boundaries - see [`is_char_boundary`](https://doc.rust-lang.org/std/primitive.str.html#method.is_char_boundary "method str::is_char_boundary") for more details. See the implementations
for [`SliceIndex<str>`](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex") for more details on string slicing. For a non-panicking
version of string slicing, see [`get`](https://doc.rust-lang.org/std/primitive.str.html#method.get "method str::get").

The [`bytes`](https://doc.rust-lang.org/std/primitive.str.html#method.bytes "method str::bytes") and [`chars`](https://doc.rust-lang.org/std/primitive.str.html#method.chars "method str::chars") methods return iterators over the bytes and
codepoints of the string, respectively. To iterate over codepoints along
with byte indices, use [`char_indices`](https://doc.rust-lang.org/std/primitive.str.html#method.char_indices "method str::char_indices").

## [§](https://doc.rust-lang.org/std/string/struct.String.html#deref)Deref

`String` implements `Deref<Target = str>`, and so inherits all of [`str`](https://doc.rust-lang.org/std/primitive.str.html "str")’s
methods. In addition, this means that you can pass a `String` to a
function which takes a [`&str`](https://doc.rust-lang.org/std/primitive.str.html "&str") by using an ampersand (`&`):

```
fn takes_str(s: &str) { }

let s = String::from("Hello");

takes_str(&s);
```

This will create a [`&str`](https://doc.rust-lang.org/std/primitive.str.html "&str") from the `String` and pass it in. This
conversion is very inexpensive, and so generally, functions will accept
[`&str`](https://doc.rust-lang.org/std/primitive.str.html "&str")s as arguments unless they need a `String` for some specific
reason.

In certain cases Rust doesn’t have enough information to make this
conversion, known as [`Deref`](https://doc.rust-lang.org/std/ops/trait.Deref.html "ops::Deref") coercion. In the following example a string
slice [`&'a str`](https://doc.rust-lang.org/std/primitive.str.html "&str") implements the trait `TraitExample`, and the function
`example_func` takes anything that implements the trait. In this case Rust
would need to make two implicit conversions, which Rust doesn’t have the
means to do. For that reason, the following example will not compile.

[ⓘ](https://doc.rust-lang.org/std/string/struct.String.html "This example deliberately fails to compile")

```
trait TraitExample {}

impl<'a> TraitExample for &'a str {}

fn example_func<A: TraitExample>(example_arg: A) {}

let example_string = String::from("example_string");
example_func(&example_string);
```

There are two options that would work instead. The first would be to
change the line `example_func(&example_string);` to
`example_func(example_string.as_str());`, using the method [`as_str()`](https://doc.rust-lang.org/std/string/struct.String.html#method.as_str "method std::string::String::as_str")
to explicitly extract the string slice containing the string. The second
way changes `example_func(&example_string);` to
`example_func(&*example_string);`. In this case we are dereferencing a
`String` to a [`str`](https://doc.rust-lang.org/std/primitive.str.html "str"), then referencing the [`str`](https://doc.rust-lang.org/std/primitive.str.html "str") back to
[`&str`](https://doc.rust-lang.org/std/primitive.str.html "&str"). The second way is more idiomatic, however both work to do the
conversion explicitly rather than relying on the implicit conversion.

## [§](https://doc.rust-lang.org/std/string/struct.String.html#representation)Representation

A `String` is made up of three components: a pointer to some bytes, a
length, and a capacity. The pointer points to the internal buffer which `String`
uses to store its data. The length is the number of bytes currently stored
in the buffer, and the capacity is the size of the buffer in bytes. As such,
the length will always be less than or equal to the capacity.

This buffer is always stored on the heap.

You can look at these with the [`as_ptr`](https://doc.rust-lang.org/std/primitive.str.html#method.as_ptr "method str::as_ptr"), [`len`](https://doc.rust-lang.org/std/string/struct.String.html#method.len "method std::string::String::len"), and [`capacity`](https://doc.rust-lang.org/std/string/struct.String.html#method.capacity "method std::string::String::capacity")
methods:

```
use std::mem;

let story = String::from("Once upon a time...");

// Prevent automatically dropping the String's data
let mut story = mem::ManuallyDrop::new(story);

let ptr = story.as_mut_ptr();
let len = story.len();
let capacity = story.capacity();

// story has nineteen bytes
assert_eq!(19, len);

// We can re-build a String out of ptr, len, and capacity. This is all
// unsafe because we are responsible for making sure the components are
// valid:
let s = unsafe { String::from_raw_parts(ptr, len, capacity) } ;

assert_eq!(String::from("Once upon a time..."), s);
```

If a `String` has enough capacity, adding elements to it will not
re-allocate. For example, consider this program:

```
let mut s = String::new();

println!("{}", s.capacity());

for _ in 0..5 {
    s.push_str("hello");
    println!("{}", s.capacity());
}
```

This will output the following:

```
0
8
16
16
32
32
```

At first, we have no memory allocated at all, but as we append to the
string, it increases its capacity appropriately. If we instead use the
[`with_capacity`](https://doc.rust-lang.org/std/string/struct.String.html#method.with_capacity "associated function std::string::String::with_capacity") method to allocate the correct capacity initially:

```
let mut s = String::with_capacity(25);

println!("{}", s.capacity());

for _ in 0..5 {
    s.push_str("hello");
    println!("{}", s.capacity());
}
```

We end up with a different output:

```
25
25
25
25
25
25
```

Here, there’s no need to allocate more memory inside the loop.

## Implementations[§](https://doc.rust-lang.org/std/string/struct.String.html#implementations)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#422)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-String)

### impl [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

1.0.0 (const: 1.39.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#444)

#### pub const fn [new](https://doc.rust-lang.org/std/string/struct.String.html#method.new)() -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Creates a new empty `String`.

Given that the `String` is empty, this will not allocate any initial
buffer. While that means that this initial operation is very
inexpensive, it may cause excessive allocation later when you add
data. If you have an idea of how much data the `String` will hold,
consider the [`with_capacity`](https://doc.rust-lang.org/std/string/struct.String.html#method.with_capacity "associated function std::string::String::with_capacity") method to prevent excessive
re-allocation.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-1)Examples

```
let s = String::new();
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#487)

#### pub fn [with\_capacity](https://doc.rust-lang.org/std/string/struct.String.html#method.with_capacity)(capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Creates a new empty `String` with at least the specified capacity.

`String`s have an internal buffer to hold their data. The capacity is
the length of that buffer, and can be queried with the [`capacity`](https://doc.rust-lang.org/std/string/struct.String.html#method.capacity "method std::string::String::capacity")
method. This method creates an empty `String`, but one with an initial
buffer that can hold at least `capacity` bytes. This is useful when you
may be appending a bunch of data to the `String`, reducing the number of
reallocations it needs to do.

If the given capacity is `0`, no allocation will occur, and this method
is identical to the [`new`](https://doc.rust-lang.org/std/string/struct.String.html#method.new "associated function std::string::String::new") method.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-2)Examples

```
let mut s = String::with_capacity(10);

// The String contains no chars, even though it has capacity for more
assert_eq!(s.len(), 0);

// These are all done without reallocating...
let cap = s.capacity();
for _ in 0..10 {
    s.push('a');
}

assert_eq!(s.capacity(), cap);

// ...but this may make the string reallocate
s.push('a');
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#500)

#### pub fn [try\_with\_capacity](https://doc.rust-lang.org/std/string/struct.String.html#method.try_with_capacity)(capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), [TryReserveError](https://doc.rust-lang.org/std/collections/struct.TryReserveError.html "struct std::collections::TryReserveError")>

🔬This is a nightly-only experimental API. (`try_with_capacity` [#91913](https://github.com/rust-lang/rust/issues/91913))

Creates a new empty `String` with at least the specified capacity.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#errors)Errors

Returns [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") if the capacity exceeds `isize::MAX` bytes,
or if the memory allocator reports failure.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#563)

#### pub fn [from\_utf8](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8)(vec: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), [FromUtf8Error](https://doc.rust-lang.org/std/string/struct.FromUtf8Error.html "struct std::string::FromUtf8Error")>

Converts a vector of bytes to a `String`.

A string ([`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) is made of bytes ([`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8")), and a vector of bytes
([`Vec<u8>`](https://doc.rust-lang.org/std/vec/struct.Vec.html "Vec")) is made of bytes, so this function converts between the
two. Not all byte slices are valid `String`s, however: `String`
requires that it is valid UTF-8. `from_utf8()` checks to ensure that
the bytes are valid UTF-8, and then does the conversion.

If you are sure that the byte slice is valid UTF-8, and you don’t want
to incur the overhead of the validity check, there is an unsafe version
of this function, [`from_utf8_unchecked`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_unchecked "associated function std::string::String::from_utf8_unchecked"), which has the same behavior
but skips the check.

This method will take care to not copy the vector, for efficiency’s
sake.

If you need a [`&str`](https://doc.rust-lang.org/std/primitive.str.html "&str") instead of a `String`, consider
[`str::from_utf8`](https://doc.rust-lang.org/std/str/fn.from_utf8.html "fn std::str::from_utf8").

The inverse of this method is [`into_bytes`](https://doc.rust-lang.org/std/string/struct.String.html#method.into_bytes "method std::string::String::into_bytes").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#errors-1)Errors

Returns [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") if the slice is not UTF-8 with a description as to why the
provided bytes are not UTF-8. The vector you moved in is also included.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-3)Examples

Basic usage:

```
// some bytes, in a vector
let sparkle_heart = vec![240, 159, 146, 150];

// We know these bytes are valid, so we'll use `unwrap()`.
let sparkle_heart = String::from_utf8(sparkle_heart).unwrap();

assert_eq!("💖", sparkle_heart);
```

Incorrect bytes:

```
// some invalid bytes, in a vector
let sparkle_heart = vec![0, 159, 146, 150];

assert!(String::from_utf8(sparkle_heart).is_err());
```

See the docs for [`FromUtf8Error`](https://doc.rust-lang.org/std/string/struct.FromUtf8Error.html "struct std::string::FromUtf8Error") for more details on what you can do
with this error.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#622)

#### pub fn [from\_utf8\_lossy](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_lossy)(v: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'\_, [str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts a slice of bytes to a string, including invalid characters.

Strings are made of bytes ([`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8")), and a slice of bytes
([`&[u8]`](https://doc.rust-lang.org/std/primitive.slice.html "primitive slice")) is made of bytes, so this function converts
between the two. Not all byte slices are valid strings, however: strings
are required to be valid UTF-8. During this conversion,
`from_utf8_lossy()` will replace any invalid UTF-8 sequences with
[`U+FFFD REPLACEMENT CHARACTER`](https://doc.rust-lang.org/std/char/constant.REPLACEMENT_CHARACTER.html "constant std::char::REPLACEMENT_CHARACTER"), which looks like this: �

If you are sure that the byte slice is valid UTF-8, and you don’t want
to incur the overhead of the conversion, there is an unsafe version
of this function, [`from_utf8_unchecked`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_unchecked "associated function std::string::String::from_utf8_unchecked"), which has the same behavior
but skips the checks.

This function returns a [`Cow<'a, str>`](https://doc.rust-lang.org/std/borrow/enum.Cow.html "borrow::Cow"). If our byte slice is invalid
UTF-8, then we need to insert the replacement characters, which will
change the size of the string, and hence, require a `String`. But if
it’s already valid UTF-8, we don’t need a new allocation. This return
type allows us to handle both cases.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-4)Examples

Basic usage:

```
// some bytes, in a vector
let sparkle_heart = vec![240, 159, 146, 150];

let sparkle_heart = String::from_utf8_lossy(&sparkle_heart);

assert_eq!("💖", sparkle_heart);
```

Incorrect bytes:

```
// some invalid bytes
let input = b"Hello \xF0\x90\x80World";
let output = String::from_utf8_lossy(input);

assert_eq!("Hello �World", output);
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#689)

#### pub fn [from\_utf8\_lossy\_owned](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_lossy_owned)(v: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

🔬This is a nightly-only experimental API. (`string_from_utf8_lossy_owned` [#129436](https://github.com/rust-lang/rust/issues/129436))

Converts a [`Vec<u8>`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec") to a `String`, substituting invalid UTF-8
sequences with replacement characters.

See [`from_utf8_lossy`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_lossy "associated function std::string::String::from_utf8_lossy") for more details.

Note that this function does not guarantee reuse of the original `Vec`
allocation.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-5)Examples

Basic usage:

```
#![feature(string_from_utf8_lossy_owned)]
// some bytes, in a vector
let sparkle_heart = vec![240, 159, 146, 150];

let sparkle_heart = String::from_utf8_lossy_owned(sparkle_heart);

assert_eq!(String::from("💖"), sparkle_heart);
```

Incorrect bytes:

```
#![feature(string_from_utf8_lossy_owned)]
// some invalid bytes
let input: Vec<u8> = b"Hello \xF0\x90\x80World".into();
let output = String::from_utf8_lossy_owned(input);

assert_eq!(String::from("Hello �World"), output);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#721)

#### pub fn [from\_utf16](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf16)(v: &[[u16](https://doc.rust-lang.org/std/primitive.u16.html)]) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), [FromUtf16Error](https://doc.rust-lang.org/std/string/struct.FromUtf16Error.html "struct std::string::FromUtf16Error")>

Decode a native endian UTF-16–encoded vector `v` into a `String`,
returning [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") if `v` contains any invalid data.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-6)Examples

```
// 𝄞music
let v = &[0xD834, 0xDD1E, 0x006d, 0x0075,
          0x0073, 0x0069, 0x0063];
assert_eq!(String::from("𝄞music"),
           String::from_utf16(v).unwrap());

// 𝄞mu<invalid>ic
let v = &[0xD834, 0xDD1E, 0x006d, 0x0075,
          0xD800, 0x0069, 0x0063];
assert!(String::from_utf16(v).is_err());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#761)

#### pub fn [from\_utf16\_lossy](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf16_lossy)(v: &[[u16](https://doc.rust-lang.org/std/primitive.u16.html)]) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Decode a native endian UTF-16–encoded slice `v` into a `String`,
replacing invalid data with [the replacement character (`U+FFFD`)](https://doc.rust-lang.org/std/char/constant.REPLACEMENT_CHARACTER.html "constant std::char::REPLACEMENT_CHARACTER").

Unlike [`from_utf8_lossy`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_lossy "associated function std::string::String::from_utf8_lossy") which returns a [`Cow<'a, str>`](https://doc.rust-lang.org/std/borrow/enum.Cow.html "borrow::Cow"),
`from_utf16_lossy` returns a `String` since the UTF-16 to UTF-8
conversion requires a memory allocation.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-7)Examples

```
// 𝄞mus<invalid>ic<invalid>
let v = &[0xD834, 0xDD1E, 0x006d, 0x0075,
          0x0073, 0xDD1E, 0x0069, 0x0063,
          0xD834];

assert_eq!(String::from("𝄞mus\u{FFFD}ic\u{FFFD}"),
           String::from_utf16_lossy(v));
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#789)

#### pub fn [from\_utf16le](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf16le)(v: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), [FromUtf16Error](https://doc.rust-lang.org/std/string/struct.FromUtf16Error.html "struct std::string::FromUtf16Error")>

🔬This is a nightly-only experimental API. (`str_from_utf16_endian` [#116258](https://github.com/rust-lang/rust/issues/116258))

Decode a UTF-16LE–encoded vector `v` into a `String`,
returning [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") if `v` contains any invalid data.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-8)Examples

Basic usage:

```
#![feature(str_from_utf16_endian)]
// 𝄞music
let v = &[0x34, 0xD8, 0x1E, 0xDD, 0x6d, 0x00, 0x75, 0x00,
          0x73, 0x00, 0x69, 0x00, 0x63, 0x00];
assert_eq!(String::from("𝄞music"),
           String::from_utf16le(v).unwrap());

// 𝄞mu<invalid>ic
let v = &[0x34, 0xD8, 0x1E, 0xDD, 0x6d, 0x00, 0x75, 0x00,
          0x00, 0xD8, 0x69, 0x00, 0x63, 0x00];
assert!(String::from_utf16le(v).is_err());
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#828)

#### pub fn [from\_utf16le\_lossy](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf16le_lossy)(v: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

🔬This is a nightly-only experimental API. (`str_from_utf16_endian` [#116258](https://github.com/rust-lang/rust/issues/116258))

Decode a UTF-16LE–encoded slice `v` into a `String`, replacing
invalid data with [the replacement character (`U+FFFD`)](https://doc.rust-lang.org/std/char/constant.REPLACEMENT_CHARACTER.html "constant std::char::REPLACEMENT_CHARACTER").

Unlike [`from_utf8_lossy`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_lossy "associated function std::string::String::from_utf8_lossy") which returns a [`Cow<'a, str>`](https://doc.rust-lang.org/std/borrow/enum.Cow.html "borrow::Cow"),
`from_utf16le_lossy` returns a `String` since the UTF-16 to UTF-8
conversion requires a memory allocation.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-9)Examples

Basic usage:

```
#![feature(str_from_utf16_endian)]
// 𝄞mus<invalid>ic<invalid>
let v = &[0x34, 0xD8, 0x1E, 0xDD, 0x6d, 0x00, 0x75, 0x00,
          0x73, 0x00, 0x1E, 0xDD, 0x69, 0x00, 0x63, 0x00,
          0x34, 0xD8];

assert_eq!(String::from("𝄞mus\u{FFFD}ic\u{FFFD}"),
           String::from_utf16le_lossy(v));
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#864)

#### pub fn [from\_utf16be](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf16be)(v: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), [FromUtf16Error](https://doc.rust-lang.org/std/string/struct.FromUtf16Error.html "struct std::string::FromUtf16Error")>

🔬This is a nightly-only experimental API. (`str_from_utf16_endian` [#116258](https://github.com/rust-lang/rust/issues/116258))

Decode a UTF-16BE–encoded vector `v` into a `String`,
returning [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") if `v` contains any invalid data.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-10)Examples

Basic usage:

```
#![feature(str_from_utf16_endian)]
// 𝄞music
let v = &[0xD8, 0x34, 0xDD, 0x1E, 0x00, 0x6d, 0x00, 0x75,
          0x00, 0x73, 0x00, 0x69, 0x00, 0x63];
assert_eq!(String::from("𝄞music"),
           String::from_utf16be(v).unwrap());

// 𝄞mu<invalid>ic
let v = &[0xD8, 0x34, 0xDD, 0x1E, 0x00, 0x6d, 0x00, 0x75,
          0xD8, 0x00, 0x00, 0x69, 0x00, 0x63];
assert!(String::from_utf16be(v).is_err());
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#903)

#### pub fn [from\_utf16be\_lossy](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf16be_lossy)(v: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

🔬This is a nightly-only experimental API. (`str_from_utf16_endian` [#116258](https://github.com/rust-lang/rust/issues/116258))

Decode a UTF-16BE–encoded slice `v` into a `String`, replacing
invalid data with [the replacement character (`U+FFFD`)](https://doc.rust-lang.org/std/char/constant.REPLACEMENT_CHARACTER.html "constant std::char::REPLACEMENT_CHARACTER").

Unlike [`from_utf8_lossy`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_lossy "associated function std::string::String::from_utf8_lossy") which returns a [`Cow<'a, str>`](https://doc.rust-lang.org/std/borrow/enum.Cow.html "borrow::Cow"),
`from_utf16le_lossy` returns a `String` since the UTF-16 to UTF-8
conversion requires a memory allocation.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-11)Examples

Basic usage:

```
#![feature(str_from_utf16_endian)]
// 𝄞mus<invalid>ic<invalid>
let v = &[0xD8, 0x34, 0xDD, 0x1E, 0x00, 0x6d, 0x00, 0x75,
          0x00, 0x73, 0xDD, 0x1E, 0x00, 0x69, 0x00, 0x63,
          0xD8, 0x34];

assert_eq!(String::from("𝄞mus\u{FFFD}ic\u{FFFD}"),
           String::from_utf16be_lossy(v));
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#945)

#### pub fn [into\_raw\_parts](https://doc.rust-lang.org/std/string/struct.String.html#method.into_raw_parts)(self) -> ([\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html), [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`vec_into_raw_parts` [#65816](https://github.com/rust-lang/rust/issues/65816))

Decomposes a `String` into its raw components: `(pointer, length, capacity)`.

Returns the raw pointer to the underlying data, the length of
the string (in bytes), and the allocated capacity of the data
(in bytes). These are the same arguments in the same order as
the arguments to [`from_raw_parts`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_raw_parts "associated function std::string::String::from_raw_parts").

After calling this function, the caller is responsible for the
memory previously managed by the `String`. The only way to do
this is to convert the raw pointer, length, and capacity back
into a `String` with the [`from_raw_parts`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_raw_parts "associated function std::string::String::from_raw_parts") function, allowing
the destructor to perform the cleanup.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-12)Examples

```
#![feature(vec_into_raw_parts)]
let s = String::from("hello");

let (ptr, len, cap) = s.into_raw_parts();

let rebuilt = unsafe { String::from_raw_parts(ptr, len, cap) };
assert_eq!(rebuilt, "hello");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#994)

#### pub unsafe fn [from\_raw\_parts](https://doc.rust-lang.org/std/string/struct.String.html#method.from_raw_parts)( buf: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html), length: [usize](https://doc.rust-lang.org/std/primitive.usize.html), capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Creates a new `String` from a pointer, a length and a capacity.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety)Safety

This is highly unsafe, due to the number of invariants that aren’t
checked:

* all safety requirements for [`Vec::<u8>::from_raw_parts`](https://doc.rust-lang.org/std/vec/struct.Vec.html#method.from_raw_parts "associated function std::vec::Vec::from_raw_parts").
* all safety requirements for [`String::from_utf8_unchecked`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_unchecked "associated function std::string::String::from_utf8_unchecked").

Violating these may cause problems like corrupting the allocator’s
internal data structures. For example, it is normally **not** safe to
build a `String` from a pointer to a C `char` array containing UTF-8
*unless* you are certain that array was originally allocated by the
Rust standard library’s allocator.

The ownership of `buf` is effectively transferred to the
`String` which may then deallocate, reallocate or change the
contents of memory pointed to by the pointer at will. Ensure
that nothing else uses the pointer after calling this
function.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-13)Examples

```
use std::mem;

unsafe {
    let s = String::from("hello");

    // Prevent automatically dropping the String's data
    let mut s = mem::ManuallyDrop::new(s);

    let ptr = s.as_mut_ptr();
    let len = s.len();
    let capacity = s.capacity();

    let s = String::from_raw_parts(ptr, len, capacity);

    assert_eq!(String::from("hello"), s);
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1027)

#### pub unsafe fn [from\_utf8\_unchecked](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8_unchecked)(bytes: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a vector of bytes to a `String` without checking that the
string contains valid UTF-8.

See the safe version, [`from_utf8`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8 "associated function std::string::String::from_utf8"), for more details.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-1)Safety

This function is unsafe because it does not check that the bytes passed
to it are valid UTF-8. If this constraint is violated, it may cause
memory unsafety issues with future users of the `String`, as the rest of
the standard library assumes that `String`s are valid UTF-8.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-14)Examples

```
// some bytes, in a vector
let sparkle_heart = vec![240, 159, 146, 150];

let sparkle_heart = unsafe {
    String::from_utf8_unchecked(sparkle_heart)
};

assert_eq!("💖", sparkle_heart);
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1048)

#### pub const fn [into\_bytes](https://doc.rust-lang.org/std/string/struct.String.html#method.into_bytes)(self) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Converts a `String` into a byte vector.

This consumes the `String`, so we do not need to copy its contents.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-15)Examples

```
let s = String::from("hello");
let bytes = s.into_bytes();

assert_eq!(&[104, 101, 108, 108, 111][..], &bytes[..]);
```

1.7.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1066)

#### pub const fn [as\_str](https://doc.rust-lang.org/std/string/struct.String.html#method.as_str)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Extracts a string slice containing the entire `String`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-16)Examples

```
let s = String::from("foo");

assert_eq!("foo", s.as_str());
```

1.7.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1089)

#### pub const fn [as\_mut\_str](https://doc.rust-lang.org/std/string/struct.String.html#method.as_mut_str)(&mut self) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Converts a `String` into a mutable string slice.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-17)Examples

```
let mut s = String::from("foobar");
let s_mut_str = s.as_mut_str();

s_mut_str.make_ascii_uppercase();

assert_eq!("FOOBAR", s_mut_str);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1112)

#### pub fn [push\_str](https://doc.rust-lang.org/std/string/struct.String.html#method.push_str)(&mut self, string: &[str](https://doc.rust-lang.org/std/primitive.str.html))

Appends a given string slice onto the end of this `String`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-18)Examples

```
let mut s = String::from("foo");

s.push_str("bar");

assert_eq!("foobar", s);
```

1.87.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1140-1142)

#### pub fn [extend\_from\_within](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_from_within)<R>(&mut self, src: R) where R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Copies elements from `src` range to the end of the string.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics)Panics

Panics if the starting point or end point do not lie on a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")
boundary, or if they’re out of bounds.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-19)Examples

```
let mut string = String::from("abcde");

string.extend_from_within(2..);
assert_eq!(string, "abcdecde");

string.extend_from_within(..2);
assert_eq!(string, "abcdecdeab");

string.extend_from_within(4..8);
assert_eq!(string, "abcdecdeabecde");
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1165)

#### pub const fn [capacity](https://doc.rust-lang.org/std/string/struct.String.html#method.capacity)(&self) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Returns this `String`’s capacity, in bytes.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-20)Examples

```
let s = String::with_capacity(10);

assert!(s.capacity() >= 10);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1213)

#### pub fn [reserve](https://doc.rust-lang.org/std/string/struct.String.html#method.reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Reserves capacity for at least `additional` bytes more than the
current length. The allocator may reserve more space to speculatively
avoid frequent allocations. After calling `reserve`,
capacity will be greater than or equal to `self.len() + additional`.
Does nothing if capacity is already sufficient.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-1)Panics

Panics if the new capacity overflows [`usize`](https://doc.rust-lang.org/std/primitive.usize.html "primitive usize").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-21)Examples

Basic usage:

```
let mut s = String::new();

s.reserve(10);

assert!(s.capacity() >= 10);
```

This might not actually increase the capacity:

```
let mut s = String::with_capacity(10);
s.push('a');
s.push('b');

// s now has a length of 2 and a capacity of at least 10
let capacity = s.capacity();
assert_eq!(2, s.len());
assert!(capacity >= 10);

// Since we already have at least an extra 8 capacity, calling this...
s.reserve(8);

// ... doesn't actually increase.
assert_eq!(capacity, s.capacity());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1264)

#### pub fn [reserve\_exact](https://doc.rust-lang.org/std/string/struct.String.html#method.reserve_exact)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Reserves the minimum capacity for at least `additional` bytes more than
the current length. Unlike [`reserve`](https://doc.rust-lang.org/std/string/struct.String.html#method.reserve "method std::string::String::reserve"), this will not
deliberately over-allocate to speculatively avoid frequent allocations.
After calling `reserve_exact`, capacity will be greater than or equal to
`self.len() + additional`. Does nothing if the capacity is already
sufficient.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-2)Panics

Panics if the new capacity overflows [`usize`](https://doc.rust-lang.org/std/primitive.usize.html "primitive usize").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-22)Examples

Basic usage:

```
let mut s = String::new();

s.reserve_exact(10);

assert!(s.capacity() >= 10);
```

This might not actually increase the capacity:

```
let mut s = String::with_capacity(10);
s.push('a');
s.push('b');

// s now has a length of 2 and a capacity of at least 10
let capacity = s.capacity();
assert_eq!(2, s.len());
assert!(capacity >= 10);

// Since we already have at least an extra 8 capacity, calling this...
s.reserve_exact(8);

// ... doesn't actually increase.
assert_eq!(capacity, s.capacity());
```

1.57.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1299)

#### pub fn [try\_reserve](https://doc.rust-lang.org/std/string/struct.String.html#method.try_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [TryReserveError](https://doc.rust-lang.org/std/collections/struct.TryReserveError.html "struct std::collections::TryReserveError")>

Tries to reserve capacity for at least `additional` bytes more than the
current length. The allocator may reserve more space to speculatively
avoid frequent allocations. After calling `try_reserve`, capacity will be
greater than or equal to `self.len() + additional` if it returns
`Ok(())`. Does nothing if capacity is already sufficient. This method
preserves the contents even if an error occurs.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#errors-2)Errors

If the capacity overflows, or the allocator reports a failure, then an error
is returned.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-23)Examples

```
use std::collections::TryReserveError;

fn process_data(data: &str) -> Result<String, TryReserveError> {
    let mut output = String::new();

    // Pre-reserve the memory, exiting if we can't
    output.try_reserve(data.len())?;

    // Now we know this can't OOM in the middle of our complex work
    output.push_str(data);

    Ok(output)
}
```

1.57.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1340)

#### pub fn [try\_reserve\_exact](https://doc.rust-lang.org/std/string/struct.String.html#method.try_reserve_exact)( &mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [TryReserveError](https://doc.rust-lang.org/std/collections/struct.TryReserveError.html "struct std::collections::TryReserveError")>

Tries to reserve the minimum capacity for at least `additional` bytes
more than the current length. Unlike [`try_reserve`](https://doc.rust-lang.org/std/string/struct.String.html#method.try_reserve "method std::string::String::try_reserve"), this will not
deliberately over-allocate to speculatively avoid frequent allocations.
After calling `try_reserve_exact`, capacity will be greater than or
equal to `self.len() + additional` if it returns `Ok(())`.
Does nothing if the capacity is already sufficient.

Note that the allocator may give the collection more space than it
requests. Therefore, capacity can not be relied upon to be precisely
minimal. Prefer [`try_reserve`](https://doc.rust-lang.org/std/string/struct.String.html#method.try_reserve "method std::string::String::try_reserve") if future insertions are expected.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#errors-3)Errors

If the capacity overflows, or the allocator reports a failure, then an error
is returned.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-24)Examples

```
use std::collections::TryReserveError;

fn process_data(data: &str) -> Result<String, TryReserveError> {
    let mut output = String::new();

    // Pre-reserve the memory, exiting if we can't
    output.try_reserve_exact(data.len())?;

    // Now we know this can't OOM in the middle of our complex work
    output.push_str(data);

    Ok(output)
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1361)

#### pub fn [shrink\_to\_fit](https://doc.rust-lang.org/std/string/struct.String.html#method.shrink_to_fit)(&mut self)

Shrinks the capacity of this `String` to match its length.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-25)Examples

```
let mut s = String::from("foo");

s.reserve(100);
assert!(s.capacity() >= 100);

s.shrink_to_fit();
assert_eq!(3, s.capacity());
```

1.56.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1389)

#### pub fn [shrink\_to](https://doc.rust-lang.org/std/string/struct.String.html#method.shrink_to)(&mut self, min\_capacity: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Shrinks the capacity of this `String` with a lower bound.

The capacity will remain at least as large as both the length
and the supplied value.

If the current capacity is less than the lower limit, this is a no-op.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-26)Examples

```
let mut s = String::from("foo");

s.reserve(100);
assert!(s.capacity() >= 100);

s.shrink_to(10);
assert!(s.capacity() >= 10);
s.shrink_to(0);
assert!(s.capacity() >= 3);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1410)

#### pub fn [push](https://doc.rust-lang.org/std/string/struct.String.html#method.push)(&mut self, ch: [char](https://doc.rust-lang.org/std/primitive.char.html))

Appends the given [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") to the end of this `String`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-27)Examples

```
let mut s = String::from("abc");

s.push('1');
s.push('2');
s.push('3');

assert_eq!("abc123", s);
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1439)

#### pub const fn [as\_bytes](https://doc.rust-lang.org/std/string/struct.String.html#method.as_bytes)(&self) -> &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns a byte slice of this `String`’s contents.

The inverse of this method is [`from_utf8`](https://doc.rust-lang.org/std/string/struct.String.html#method.from_utf8 "associated function std::string::String::from_utf8").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-28)Examples

```
let s = String::from("hello");

assert_eq!(&[104, 101, 108, 108, 111], s.as_bytes());
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1467)

#### pub fn [truncate](https://doc.rust-lang.org/std/string/struct.String.html#method.truncate)(&mut self, new\_len: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

Shortens this `String` to the specified length.

If `new_len` is greater than or equal to the string’s current length, this has no
effect.

Note that this method has no effect on the allocated capacity
of the string

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-3)Panics

Panics if `new_len` does not lie on a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") boundary.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-29)Examples

```
let mut s = String::from("hello");

s.truncate(2);

assert_eq!("he", s);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1491)

#### pub fn [pop](https://doc.rust-lang.org/std/string/struct.String.html#method.pop)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[char](https://doc.rust-lang.org/std/primitive.char.html)>

Removes the last character from the string buffer and returns it.

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if this `String` is empty.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-30)Examples

```
let mut s = String::from("abč");

assert_eq!(s.pop(), Some('č'));
assert_eq!(s.pop(), Some('b'));
assert_eq!(s.pop(), Some('a'));

assert_eq!(s.pop(), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1524)

#### pub fn [remove](https://doc.rust-lang.org/std/string/struct.String.html#method.remove)(&mut self, idx: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [char](https://doc.rust-lang.org/std/primitive.char.html)

Removes a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") from this `String` at byte position `idx` and returns it.

Copies all bytes after the removed char to new positions.

Note that calling this in a loop can result in quadratic behavior.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-4)Panics

Panics if `idx` is larger than or equal to the `String`’s length,
or if it does not lie on a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") boundary.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-31)Examples

```
let mut s = String::from("abç");

assert_eq!(s.remove(0), 'a');
assert_eq!(s.remove(1), 'ç');
assert_eq!(s.remove(0), 'b');
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1561)

#### pub fn [remove\_matches](https://doc.rust-lang.org/std/string/struct.String.html#method.remove_matches)<P>(&mut self, pat: P) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

🔬This is a nightly-only experimental API. (`string_remove_matches` [#72826](https://github.com/rust-lang/rust/issues/72826))

Remove all matches of pattern `pat` in the `String`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-32)Examples

```
#![feature(string_remove_matches)]
let mut s = String::from("Trees are not green, the sky is not blue.");
s.remove_matches("not ");
assert_eq!("Trees are green, the sky is blue.", s);
```

Matches will be detected and removed iteratively, so in cases where
patterns overlap, only the first pattern will be removed:

```
#![feature(string_remove_matches)]
let mut s = String::from("banana");
s.remove_matches("ana");
assert_eq!("bna", s);
```

1.26.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1638-1640)

#### pub fn [retain](https://doc.rust-lang.org/std/string/struct.String.html#method.retain)<F>(&mut self, f: F) where F: [FnMut](https://doc.rust-lang.org/std/ops/trait.FnMut.html "trait std::ops::FnMut")([char](https://doc.rust-lang.org/std/primitive.char.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Retains only the characters specified by the predicate.

In other words, remove all characters `c` such that `f(c)` returns `false`.
This method operates in place, visiting each character exactly once in the
original order, and preserves the order of the retained characters.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-33)Examples

```
let mut s = String::from("f_o_ob_ar");

s.retain(|c| c != '_');

assert_eq!(s, "foobar");
```

Because the elements are visited exactly once in the original order,
external state may be used to decide which elements to keep.

```
let mut s = String::from("abcde");
let keep = [false, true, true, false, true];
let mut iter = keep.iter();
s.retain(|_| *iter.next().unwrap());
assert_eq!(s, "bce");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1720)

#### pub fn [insert](https://doc.rust-lang.org/std/string/struct.String.html#method.insert)(&mut self, idx: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ch: [char](https://doc.rust-lang.org/std/primitive.char.html))

Inserts a character into this `String` at byte position `idx`.

Reallocates if `self.capacity()` is insufficient, which may involve copying all
`self.capacity()` bytes. Makes space for the insertion by copying all bytes of
`&self[idx..]` to new positions.

Note that calling this in a loop can result in quadratic behavior.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-5)Panics

Panics if `idx` is larger than the `String`’s length, or if it does not
lie on a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") boundary.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-34)Examples

```
let mut s = String::with_capacity(3);

s.insert(0, 'f');
s.insert(1, 'o');
s.insert(2, 'o');

assert_eq!("foo", s);
```

1.16.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1777)

#### pub fn [insert\_str](https://doc.rust-lang.org/std/string/struct.String.html#method.insert_str)(&mut self, idx: [usize](https://doc.rust-lang.org/std/primitive.usize.html), string: &[str](https://doc.rust-lang.org/std/primitive.str.html))

Inserts a string slice into this `String` at byte position `idx`.

Reallocates if `self.capacity()` is insufficient, which may involve copying all
`self.capacity()` bytes. Makes space for the insertion by copying all bytes of
`&self[idx..]` to new positions.

Note that calling this in a loop can result in quadratic behavior.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-6)Panics

Panics if `idx` is larger than the `String`’s length, or if it does not
lie on a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") boundary.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-35)Examples

```
let mut s = String::from("bar");

s.insert_str(0, "foo");

assert_eq!("foobar", s);
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1830)

#### pub const unsafe fn [as\_mut\_vec](https://doc.rust-lang.org/std/string/struct.String.html#method.as_mut_vec)(&mut self) -> &mut [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns a mutable reference to the contents of this `String`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-2)Safety

This function is unsafe because the returned `&mut Vec` allows writing
bytes which are not valid UTF-8. If this constraint is violated, using
the original `String` after dropping the `&mut Vec` may violate memory
safety, as the rest of the standard library assumes that `String`s are
valid UTF-8.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-36)Examples

```
let mut s = String::from("hello");

unsafe {
    let vec = s.as_mut_vec();
    assert_eq!(&[104, 101, 108, 108, 111][..], &vec[..]);

    vec.reverse();
}
assert_eq!(s, "olleh");
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1854)

#### pub const fn [len](https://doc.rust-lang.org/std/string/struct.String.html#method.len)(&self) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Returns the length of this `String`, in bytes, not [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s or
graphemes. In other words, it might not be what a human considers the
length of the string.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-37)Examples

```
let a = String::from("foo");
assert_eq!(a.len(), 3);

let fancy_f = String::from("ƒoo");
assert_eq!(fancy_f.len(), 4);
assert_eq!(fancy_f.chars().count(), 3);
```

1.0.0 (const: 1.87.0) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1874)

#### pub const fn [is\_empty](https://doc.rust-lang.org/std/string/struct.String.html#method.is_empty)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if this `String` has a length of zero, and `false` otherwise.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-38)Examples

```
let mut v = String::new();
assert!(v.is_empty());

v.push('a');
assert!(!v.is_empty());
```

1.16.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1906)

#### pub fn [split\_off](https://doc.rust-lang.org/std/string/struct.String.html#method.split_off)(&mut self, at: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Splits the string into two at the given byte index.

Returns a newly allocated `String`. `self` contains bytes `[0, at)`, and
the returned `String` contains bytes `[at, len)`. `at` must be on the
boundary of a UTF-8 code point.

Note that the capacity of `self` does not change.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-7)Panics

Panics if `at` is not on a `UTF-8` code point boundary, or if it is beyond the last
code point of the string.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-39)Examples

```
let mut hello = String::from("Hello, World!");
let world = hello.split_off(7);
assert_eq!(hello, "Hello, ");
assert_eq!(world, "World!");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1930)

#### pub fn [clear](https://doc.rust-lang.org/std/string/struct.String.html#method.clear)(&mut self)

Truncates this `String`, removing all contents.

While this means the `String` will have a length of zero, it does not
touch its capacity.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-40)Examples

```
let mut s = String::from("foo");

s.clear();

assert!(s.is_empty());
assert_eq!(0, s.len());
assert_eq!(3, s.capacity());
```

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#1969-1971)

#### pub fn [drain](https://doc.rust-lang.org/std/string/struct.String.html#method.drain)<R>(&mut self, range: R) -> [Drain](https://doc.rust-lang.org/std/string/struct.Drain.html "struct std::string::Drain")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Removes the specified range from the string in bulk, returning all
removed characters as an iterator.

The returned iterator keeps a mutable borrow on the string to optimize
its implementation.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-8)Panics

Panics if the starting point or end point do not lie on a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")
boundary, or if they’re out of bounds.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#leaking)Leaking

If the returned iterator goes out of scope without being dropped (due to
[`core::mem::forget`](https://doc.rust-lang.org/std/mem/fn.forget.html "fn std::mem::forget"), for example), the string may still contain a copy
of any drained characters, or may have lost characters arbitrarily,
including characters outside the range.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-41)Examples

```
let mut s = String::from("α is alpha, β is beta");
let beta_offset = s.find('β').unwrap_or(s.len());

// Remove the range up until the β from the string
let t: String = s.drain(..beta_offset).collect();
assert_eq!(t, "α is alpha, ");
assert_eq!(s, "β is beta");

// A full range clears the string, like `clear()` does
s.drain(..);
assert_eq!(s, "");
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2043)

#### pub fn [into\_chars](https://doc.rust-lang.org/std/string/struct.String.html#method.into_chars)(self) -> [IntoChars](https://doc.rust-lang.org/std/string/struct.IntoChars.html "struct std::string::IntoChars") [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

🔬This is a nightly-only experimental API. (`string_into_chars` [#133125](https://github.com/rust-lang/rust/issues/133125))

Converts a `String` into an iterator over the [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s of the string.

As a string consists of valid UTF-8, we can iterate through a string
by [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"). This method returns such an iterator.

It’s important to remember that [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") represents a Unicode Scalar
Value, and might not match your idea of what a ‘character’ is. Iteration
over grapheme clusters may be what you actually want. That functionality
is not provided by Rust’s standard library, check crates.io instead.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-42)Examples

Basic usage:

```
#![feature(string_into_chars)]

let word = String::from("goodbye");

let mut chars = word.into_chars();

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
#![feature(string_into_chars)]

let y = String::from("y̆");

let mut chars = y.into_chars();

assert_eq!(Some('y'), chars.next()); // not 'y̆'
assert_eq!(Some('\u{0306}'), chars.next());

assert_eq!(None, chars.next());
```

1.27.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2069-2071)

#### pub fn [replace\_range](https://doc.rust-lang.org/std/string/struct.String.html#method.replace_range)<R>(&mut self, range: R, replace\_with: &[str](https://doc.rust-lang.org/std/primitive.str.html)) where R: [RangeBounds](https://doc.rust-lang.org/std/ops/trait.RangeBounds.html "trait std::ops::RangeBounds")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>,

Removes the specified range in the string,
and replaces it with the given string.
The given string doesn’t need to be the same length as the range.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-9)Panics

Panics if the starting point or end point do not lie on a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")
boundary, or if they’re out of bounds.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-43)Examples

```
let mut s = String::from("α is alpha, β is beta");
let beta_offset = s.find('β').unwrap_or(s.len());

// Replace the range up until the β from the string
s.replace_range(..beta_offset, "Α is capital alpha; ");
assert_eq!(s, "Α is capital alpha; β is beta");
```

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2119)

#### pub fn [into\_boxed\_str](https://doc.rust-lang.org/std/string/struct.String.html#method.into_boxed_str)(self) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts this `String` into a `Box<str>`.

Before doing the conversion, this method discards excess capacity like [`shrink_to_fit`](https://doc.rust-lang.org/std/string/struct.String.html#method.shrink_to_fit "method std::string::String::shrink_to_fit").
Note that this call may reallocate and copy the bytes of the string.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-44)Examples

```
let s = String::from("hello");

let b = s.into_boxed_str();
```

1.72.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2150)

#### pub fn [leak](https://doc.rust-lang.org/std/string/struct.String.html#method.leak)<'a>(self) -> &'a mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Consumes and leaks the `String`, returning a mutable reference to the contents,
`&'a mut str`.

The caller has free choice over the returned lifetime, including `'static`. Indeed,
this function is ideally used for data that lives for the remainder of the program’s life,
as dropping the returned reference will cause a memory leak.

It does not reallocate or shrink the `String`, so the leaked allocation may include unused
capacity that is not part of the returned slice. If you want to discard excess capacity,
call [`into_boxed_str`](https://doc.rust-lang.org/std/string/struct.String.html#method.into_boxed_str "method std::string::String::into_boxed_str"), and then [`Box::leak`](https://doc.rust-lang.org/std/boxed/struct.Box.html#method.leak "associated function std::boxed::Box::leak") instead. However, keep in mind that
trimming the capacity may result in a reallocation and copy.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-45)Examples

```
let x = String::from("bucket");
let static_ref: &'static mut str = x.leak();
assert_eq!(static_ref, "bucket");
```

## Methods from [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")<Target = [str](https://doc.rust-lang.org/std/primitive.str.html)>[§](https://doc.rust-lang.org/std/string/struct.String.html#deref-methods-str)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#141)

#### pub fn [len](https://doc.rust-lang.org/std/string/struct.String.html#method.len-1)(&self) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Returns the length of `self`.

This length is in bytes, not [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s or graphemes. In other words,
it might not be what a human considers the length of the string.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-46)Examples

```
let len = "foo".len();
assert_eq!(3, len);

assert_eq!("ƒoo".len(), 4); // fancy f!
assert_eq!("ƒoo".chars().count(), 3);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#161)

#### pub fn [is\_empty](https://doc.rust-lang.org/std/string/struct.String.html#method.is_empty-1)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if `self` has a length of zero bytes.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-47)Examples

```
let s = "";
assert!(s.is_empty());

let s = "not empty";
assert!(!s.is_empty());
```

1.9.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#361)

#### pub fn [is\_char\_boundary](https://doc.rust-lang.org/std/string/struct.String.html#method.is_char_boundary)(&self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Checks that `index`-th byte is the first byte in a UTF-8 code point
sequence or the end of the string.

The start and end of the string (when `index == self.len()`) are
considered to be boundaries.

Returns `false` if `index` is greater than `self.len()`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-48)Examples

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

1.91.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#410)

#### pub fn [floor\_char\_boundary](https://doc.rust-lang.org/std/string/struct.String.html#method.floor_char_boundary)(&self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Finds the closest `x` not exceeding `index` where [`is_char_boundary(x)`](https://doc.rust-lang.org/std/primitive.str.html#method.is_char_boundary "method str::is_char_boundary") is `true`.

This method can help you truncate a string so that it’s still valid UTF-8, but doesn’t
exceed a given number of bytes. Note that this is done purely at the character level
and can still visually split graphemes, even though the underlying characters aren’t
split. For example, the emoji 🧑‍🔬 (scientist) could be split so that the string only
includes 🧑 (person) instead.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-49)Examples

```
let s = "❤️🧡💛💚💙💜";
assert_eq!(s.len(), 26);
assert!(!s.is_char_boundary(13));

let closest = s.floor_char_boundary(13);
assert_eq!(closest, 10);
assert_eq!(&s[..closest], "❤️🧡");
```

1.91.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#453)

#### pub fn [ceil\_char\_boundary](https://doc.rust-lang.org/std/string/struct.String.html#method.ceil_char_boundary)(&self, index: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [usize](https://doc.rust-lang.org/std/primitive.usize.html)

Finds the closest `x` not below `index` where [`is_char_boundary(x)`](https://doc.rust-lang.org/std/primitive.str.html#method.is_char_boundary "method str::is_char_boundary") is `true`.

If `index` is greater than the length of the string, this returns the length of the string.

This method is the natural complement to [`floor_char_boundary`](https://doc.rust-lang.org/std/primitive.str.html#method.floor_char_boundary "method str::floor_char_boundary"). See that method
for more details.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-50)Examples

```
let s = "❤️🧡💛💚💙💜";
assert_eq!(s.len(), 26);
assert!(!s.is_char_boundary(13));

let closest = s.ceil_char_boundary(13);
assert_eq!(closest, 14);
assert_eq!(&s[..closest], "❤️🧡💛");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#486)

#### pub fn [as\_bytes](https://doc.rust-lang.org/std/string/struct.String.html#method.as_bytes-1)(&self) -> &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Converts a string slice to a byte slice. To convert the byte slice back
into a string slice, use the [`from_utf8`](https://doc.rust-lang.org/std/str/fn.from_utf8.html "fn std::str::from_utf8") function.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-51)Examples

```
let bytes = "bors".as_bytes();
assert_eq!(b"bors", bytes);
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#531)

#### pub unsafe fn [as\_bytes\_mut](https://doc.rust-lang.org/std/string/struct.String.html#method.as_bytes_mut)(&mut self) -> &mut [[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Converts a mutable string slice to a mutable byte slice.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-3)Safety

The caller must ensure that the content of the slice is valid UTF-8
before the borrow ends and the underlying `str` is used.

Use of a `str` whose contents are not valid UTF-8 is undefined behavior.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-52)Examples

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

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#562)

#### pub fn [as\_ptr](https://doc.rust-lang.org/std/string/struct.String.html#method.as_ptr)(&self) -> [\*const](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html)

Converts a string slice to a raw pointer.

As string slices are a slice of bytes, the raw pointer points to a
[`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8"). This pointer will be pointing to the first byte of the string
slice.

The caller must ensure that the returned pointer is never written to.
If you need to mutate the contents of the string slice, use [`as_mut_ptr`](https://doc.rust-lang.org/std/primitive.str.html#method.as_mut_ptr "method str::as_mut_ptr").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-53)Examples

```
let s = "Hello";
let ptr = s.as_ptr();
```

1.36.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#580)

#### pub fn [as\_mut\_ptr](https://doc.rust-lang.org/std/string/struct.String.html#method.as_mut_ptr)(&mut self) -> [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html)

Converts a mutable string slice to a raw pointer.

As string slices are a slice of bytes, the raw pointer points to a
[`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8"). This pointer will be pointing to the first byte of the string
slice.

It is your responsibility to make sure that the string slice only gets
modified in a way that it remains valid UTF-8.

1.20.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#606)

#### pub fn [get](https://doc.rust-lang.org/std/string/struct.String.html#method.get)<I>(&self, i: I) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns a subslice of `str`.

This is the non-panicking alternative to indexing the `str`. Returns
[`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") whenever equivalent indexing operation would panic.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-54)Examples

```
let v = String::from("🗻∈🌏");

assert_eq!(Some("🗻"), v.get(0..4));

// indices not on UTF-8 sequence boundaries
assert!(v.get(1..).is_none());
assert!(v.get(..8).is_none());

// out of bounds
assert!(v.get(..42).is_none());
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#639)

#### pub fn [get\_mut](https://doc.rust-lang.org/std/string/struct.String.html#method.get_mut)<I>( &mut self, i: I, ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")> where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns a mutable subslice of `str`.

This is the non-panicking alternative to indexing the `str`. Returns
[`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") whenever equivalent indexing operation would panic.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-55)Examples

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

#### pub unsafe fn [get\_unchecked](https://doc.rust-lang.org/std/string/struct.String.html#method.get_unchecked)<I>(&self, i: I) -> &<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns an unchecked subslice of `str`.

This is the unchecked alternative to indexing the `str`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-4)Safety

Callers of this function are responsible that these preconditions are
satisfied:

* The starting index must not exceed the ending index;
* Indexes must be within bounds of the original slice;
* Indexes must lie on UTF-8 sequence boundaries.

Failing that, the returned string slice may reference invalid memory or
violate the invariants communicated by the `str` type.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-56)Examples

```
let v = "🗻∈🌏";
unsafe {
    assert_eq!("🗻", v.get_unchecked(0..4));
    assert_eq!("∈", v.get_unchecked(4..7));
    assert_eq!("🌏", v.get_unchecked(7..11));
}
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#706)

#### pub unsafe fn [get\_unchecked\_mut](https://doc.rust-lang.org/std/string/struct.String.html#method.get_unchecked_mut)<I>( &mut self, i: I, ) -> &mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

Returns a mutable, unchecked subslice of `str`.

This is the unchecked alternative to indexing the `str`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-5)Safety

Callers of this function are responsible that these preconditions are
satisfied:

* The starting index must not exceed the ending index;
* Indexes must be within bounds of the original slice;
* Indexes must lie on UTF-8 sequence boundaries.

Failing that, the returned string slice may reference invalid memory or
violate the invariants communicated by the `str` type.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-57)Examples

```
let mut v = String::from("🗻∈🌏");
unsafe {
    assert_eq!("🗻", v.get_unchecked_mut(0..4));
    assert_eq!("∈", v.get_unchecked_mut(4..7));
    assert_eq!("🌏", v.get_unchecked_mut(7..11));
}
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#757)

#### pub unsafe fn [slice\_unchecked](https://doc.rust-lang.org/std/string/struct.String.html#method.slice_unchecked)(&self, begin: [usize](https://doc.rust-lang.org/std/primitive.usize.html), end: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.29.0: use `get_unchecked(begin..end)` instead

Creates a string slice from another string slice, bypassing safety
checks.

This is generally not recommended, use with caution! For a safe
alternative see [`str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str") and [`Index`](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index").

This new slice goes from `begin` to `end`, including `begin` but
excluding `end`.

To get a mutable string slice instead, see the
[`slice_mut_unchecked`](https://doc.rust-lang.org/std/primitive.str.html#method.slice_mut_unchecked "method str::slice_mut_unchecked") method.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-6)Safety

Callers of this function are responsible that three preconditions are
satisfied:

* `begin` must not exceed `end`.
* `begin` and `end` must be byte positions within the string slice.
* `begin` and `end` must lie on UTF-8 sequence boundaries.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-58)Examples

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

#### pub unsafe fn [slice\_mut\_unchecked](https://doc.rust-lang.org/std/string/struct.String.html#method.slice_mut_unchecked)( &mut self, begin: [usize](https://doc.rust-lang.org/std/primitive.usize.html), end: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.29.0: use `get_unchecked_mut(begin..end)` instead

Creates a string slice from another string slice, bypassing safety
checks.

This is generally not recommended, use with caution! For a safe
alternative see [`str`](https://doc.rust-lang.org/std/primitive.str.html "primitive str") and [`IndexMut`](https://doc.rust-lang.org/std/ops/trait.IndexMut.html "trait std::ops::IndexMut").

This new slice goes from `begin` to `end`, including `begin` but
excluding `end`.

To get an immutable string slice instead, see the
[`slice_unchecked`](https://doc.rust-lang.org/std/primitive.str.html#method.slice_unchecked "method str::slice_unchecked") method.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-7)Safety

Callers of this function are responsible that three preconditions are
satisfied:

* `begin` must not exceed `end`.
* `begin` and `end` must be byte positions within the string slice.
* `begin` and `end` must lie on UTF-8 sequence boundaries.

1.4.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#831)

#### pub fn [split\_at](https://doc.rust-lang.org/std/string/struct.String.html#method.split_at)(&self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> (&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))

Divides one string slice into two at an index.

The argument, `mid`, should be a byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get mutable string slices instead, see the [`split_at_mut`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut "method str::split_at_mut")
method.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-10)Panics

Panics if `mid` is not on a UTF-8 code point boundary, or if it is past
the end of the last code point of the string slice. For a non-panicking
alternative see [`split_at_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_checked "method str::split_at_checked").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-59)Examples

```
let s = "Per Martin-Löf";

let (first, last) = s.split_at(3);

assert_eq!("Per", first);
assert_eq!(" Martin-Löf", last);
```

1.4.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#872)

#### pub fn [split\_at\_mut](https://doc.rust-lang.org/std/string/struct.String.html#method.split_at_mut)(&mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> (&mut [str](https://doc.rust-lang.org/std/primitive.str.html), &mut [str](https://doc.rust-lang.org/std/primitive.str.html))

Divides one mutable string slice into two at an index.

The argument, `mid`, should be a byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get immutable string slices instead, see the [`split_at`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at "method str::split_at") method.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-11)Panics

Panics if `mid` is not on a UTF-8 code point boundary, or if it is past
the end of the last code point of the string slice. For a non-panicking
alternative see [`split_at_mut_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut_checked "method str::split_at_mut_checked").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-60)Examples

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

1.80.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#912)

#### pub fn [split\_at\_checked](https://doc.rust-lang.org/std/string/struct.String.html#method.split_at_checked)(&self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))>

Divides one string slice into two at an index.

The argument, `mid`, should be a valid byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point. The
method returns `None` if that’s not the case.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get mutable string slices instead, see the [`split_at_mut_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_mut_checked "method str::split_at_mut_checked")
method.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-61)Examples

```
let s = "Per Martin-Löf";

let (first, last) = s.split_at_checked(3).unwrap();
assert_eq!("Per", first);
assert_eq!(" Martin-Löf", last);

assert_eq!(None, s.split_at_checked(13));  // Inside “ö”
assert_eq!(None, s.split_at_checked(16));  // Beyond the string length
```

1.80.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#953)

#### pub fn [split\_at\_mut\_checked](https://doc.rust-lang.org/std/string/struct.String.html#method.split_at_mut_checked)( &mut self, mid: [usize](https://doc.rust-lang.org/std/primitive.usize.html), ) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&mut [str](https://doc.rust-lang.org/std/primitive.str.html), &mut [str](https://doc.rust-lang.org/std/primitive.str.html))>

Divides one mutable string slice into two at an index.

The argument, `mid`, should be a valid byte offset from the start of the
string. It must also be on the boundary of a UTF-8 code point. The
method returns `None` if that’s not the case.

The two slices returned go from the start of the string slice to `mid`,
and from `mid` to the end of the string slice.

To get immutable string slices instead, see the [`split_at_checked`](https://doc.rust-lang.org/std/primitive.str.html#method.split_at_checked "method str::split_at_checked") method.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-62)Examples

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

#### pub fn [chars](https://doc.rust-lang.org/std/string/struct.String.html#method.chars)(&self) -> [Chars](https://doc.rust-lang.org/std/str/struct.Chars.html "struct std::str::Chars")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns an iterator over the [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s of a string slice.

As a string slice consists of valid UTF-8, we can iterate through a
string slice by [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"). This method returns such an iterator.

It’s important to remember that [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") represents a Unicode Scalar
Value, and might not match your idea of what a ‘character’ is. Iteration
over grapheme clusters may be what you actually want. This functionality
is not provided by Rust’s standard library, check crates.io instead.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-63)Examples

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

#### pub fn [char\_indices](https://doc.rust-lang.org/std/string/struct.String.html#method.char_indices)(&self) -> [CharIndices](https://doc.rust-lang.org/std/str/struct.CharIndices.html "struct std::str::CharIndices")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns an iterator over the [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s of a string slice, and their
positions.

As a string slice consists of valid UTF-8, we can iterate through a
string slice by [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"). This method returns an iterator of both
these [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, as well as their byte positions.

The iterator yields tuples. The position is first, the [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") is
second.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-64)Examples

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

#### pub fn [bytes](https://doc.rust-lang.org/std/string/struct.String.html#method.bytes)(&self) -> [Bytes](https://doc.rust-lang.org/std/str/struct.Bytes.html "struct std::str::Bytes")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns an iterator over the bytes of a string slice.

As a string slice consists of a sequence of bytes, we can iterate
through a string slice by byte. This method returns such an iterator.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-65)Examples

```
let mut bytes = "bors".bytes();

assert_eq!(Some(b'b'), bytes.next());
assert_eq!(Some(b'o'), bytes.next());
assert_eq!(Some(b'r'), bytes.next());
assert_eq!(Some(b's'), bytes.next());

assert_eq!(None, bytes.next());
```

1.1.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1182)

#### pub fn [split\_whitespace](https://doc.rust-lang.org/std/string/struct.String.html#method.split_whitespace)(&self) -> [SplitWhitespace](https://doc.rust-lang.org/std/str/struct.SplitWhitespace.html "struct std::str::SplitWhitespace")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Splits a string slice by whitespace.

The iterator returned will return string slices that are sub-slices of
the original string slice, separated by any amount of whitespace.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`. If you only want to split on ASCII whitespace
instead, use [`split_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.str.html#method.split_ascii_whitespace "method str::split_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-66)Examples

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

#### pub fn [split\_ascii\_whitespace](https://doc.rust-lang.org/std/string/struct.String.html#method.split_ascii_whitespace)(&self) -> [SplitAsciiWhitespace](https://doc.rust-lang.org/std/str/struct.SplitAsciiWhitespace.html "struct std::str::SplitAsciiWhitespace")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Splits a string slice by ASCII whitespace.

The iterator returned will return string slices that are sub-slices of
the original string slice, separated by any amount of ASCII whitespace.

This uses the same definition as [`char::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.char.html#method.is_ascii_whitespace "method char::is_ascii_whitespace").
To split by Unicode `Whitespace` instead, use [`split_whitespace`](https://doc.rust-lang.org/std/primitive.str.html#method.split_whitespace "method str::split_whitespace").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-67)Examples

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

#### pub fn [lines](https://doc.rust-lang.org/std/string/struct.String.html#method.lines)(&self) -> [Lines](https://doc.rust-lang.org/std/str/struct.Lines.html "struct std::str::Lines")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

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

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-68)Examples

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

#### pub fn [lines\_any](https://doc.rust-lang.org/std/string/struct.String.html#method.lines_any)(&self) -> [LinesAny](https://doc.rust-lang.org/std/str/struct.LinesAny.html "struct std::str::LinesAny")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

👎Deprecated since 1.4.0: use lines() instead now

Returns an iterator over the lines of a string.

1.8.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1315)

#### pub fn [encode\_utf16](https://doc.rust-lang.org/std/string/struct.String.html#method.encode_utf16)(&self) -> [EncodeUtf16](https://doc.rust-lang.org/std/str/struct.EncodeUtf16.html "struct std::str::EncodeUtf16")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns an iterator of `u16` over the string encoded
as native endian UTF-16 (without byte-order mark).

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-69)Examples

```
let text = "Zażółć gęślą jaźń";

let utf8_len = text.len();
let utf16_len = text.encode_utf16().count();

assert!(utf16_len <= utf8_len);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1340)

#### pub fn [contains](https://doc.rust-lang.org/std/string/struct.String.html#method.contains)<P>(&self, pat: P) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns `true` if the given pattern matches a sub-slice of
this string slice.

Returns `false` if it does not.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-70)Examples

```
let bananas = "bananas";

assert!(bananas.contains("nana"));
assert!(!bananas.contains("apples"));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1378)

#### pub fn [starts\_with](https://doc.rust-lang.org/std/string/struct.String.html#method.starts_with)<P>(&self, pat: P) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns `true` if the given pattern matches a prefix of this
string slice.

Returns `false` if it does not.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, in which case this function will return true if
the `&str` is a prefix of this string slice.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can also be a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.
These will only be checked against the first character of this string slice.
Look at the second example below regarding behavior for slices of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-71)Examples

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

#### pub fn [ends\_with](https://doc.rust-lang.org/std/string/struct.String.html#method.ends_with)<P>(&self, pat: P) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns `true` if the given pattern matches a suffix of this
string slice.

Returns `false` if it does not.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-72)Examples

```
let bananas = "bananas";

assert!(bananas.ends_with("anas"));
assert!(!bananas.ends_with("nana"));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1454)

#### pub fn [find](https://doc.rust-lang.org/std/string/struct.String.html#method.find)<P>(&self, pat: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns the byte index of the first character of this string slice that
matches the pattern.

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the pattern doesn’t match.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-73)Examples

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

#### pub fn [rfind](https://doc.rust-lang.org/std/string/struct.String.html#method.rfind)<P>(&self, pat: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns the byte index for the first character of the last match of the pattern in
this string slice.

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the pattern doesn’t match.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-74)Examples

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

#### pub fn [split](https://doc.rust-lang.org/std/string/struct.String.html#method.split)<P>(&self, pat: P) -> [Split](https://doc.rust-lang.org/std/str/struct.Split.html "struct std::str::Split")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of this string slice, separated by
characters matched by a pattern.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

If there are no matches the full string slice is returned as the only
item in the iterator.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rsplit`](https://doc.rust-lang.org/std/primitive.str.html#method.rsplit "method str::rsplit") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-75)Examples

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

[ⓘ](https://doc.rust-lang.org/std/string/struct.String.html "This example is not tested")

```
assert_eq!(d, &["a", "b", "c"]);
```

Use [`split_whitespace`](https://doc.rust-lang.org/std/primitive.str.html#method.split_whitespace "method str::split_whitespace") for this behavior.

1.51.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1669)

#### pub fn [split\_inclusive](https://doc.rust-lang.org/std/string/struct.String.html#method.split_inclusive)<P>(&self, pat: P) -> [SplitInclusive](https://doc.rust-lang.org/std/str/struct.SplitInclusive.html "struct std::str::SplitInclusive")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of this string slice, separated by
characters matched by a pattern.

Differs from the iterator produced by `split` in that `split_inclusive`
leaves the matched part as the terminator of the substring.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-76)Examples

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

#### pub fn [rsplit](https://doc.rust-lang.org/std/string/struct.String.html#method.rsplit)<P>(&self, pat: P) -> [RSplit](https://doc.rust-lang.org/std/str/struct.RSplit.html "struct std::str::RSplit")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over substrings of the given string slice, separated
by characters matched by a pattern and yielded in reverse order.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-1)Iterator behavior

The returned iterator requires that the pattern supports a reverse
search, and it will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if a forward/reverse
search yields the same elements.

For iterating from the front, the [`split`](https://doc.rust-lang.org/std/primitive.str.html#method.split "method str::split") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-77)Examples

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

#### pub fn [split\_terminator](https://doc.rust-lang.org/std/string/struct.String.html#method.split_terminator)<P>(&self, pat: P) -> [SplitTerminator](https://doc.rust-lang.org/std/str/struct.SplitTerminator.html "struct std::str::SplitTerminator")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of the given string slice, separated
by characters matched by a pattern.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

Equivalent to [`split`](https://doc.rust-lang.org/std/primitive.str.html#method.split "method str::split"), except that the trailing substring
is skipped if empty.

This method can be used for string data that is *terminated*,
rather than *separated* by a pattern.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-2)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rsplit_terminator`](https://doc.rust-lang.org/std/primitive.str.html#method.rsplit_terminator "method str::rsplit_terminator") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-78)Examples

```
let v: Vec<&str> = "A.B.".split_terminator('.').collect();
assert_eq!(v, ["A", "B"]);

let v: Vec<&str> = "A..B..".split_terminator(".").collect();
assert_eq!(v, ["A", "", "B", ""]);

let v: Vec<&str> = "A.B:C.D".split_terminator(&['.', ':'][..]).collect();
assert_eq!(v, ["A", "B", "C", "D"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1819-1821)

#### pub fn [rsplit\_terminator](https://doc.rust-lang.org/std/string/struct.String.html#method.rsplit_terminator)<P>(&self, pat: P) -> [RSplitTerminator](https://doc.rust-lang.org/std/str/struct.RSplitTerminator.html "struct std::str::RSplitTerminator")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over substrings of `self`, separated by characters
matched by a pattern and yielded in reverse order.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

Equivalent to [`split`](https://doc.rust-lang.org/std/primitive.str.html#method.split "method str::split"), except that the trailing substring is
skipped if empty.

This method can be used for string data that is *terminated*,
rather than *separated* by a pattern.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-3)Iterator behavior

The returned iterator requires that the pattern supports a
reverse search, and it will be double ended if a forward/reverse
search yields the same elements.

For iterating from the front, the [`split_terminator`](https://doc.rust-lang.org/std/primitive.str.html#method.split_terminator "method str::split_terminator") method can be
used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-79)Examples

```
let v: Vec<&str> = "A.B.".rsplit_terminator('.').collect();
assert_eq!(v, ["B", "A"]);

let v: Vec<&str> = "A..B..".rsplit_terminator(".").collect();
assert_eq!(v, ["", "B", "", "A"]);

let v: Vec<&str> = "A.B:C.D".rsplit_terminator(&['.', ':'][..]).collect();
assert_eq!(v, ["D", "C", "B", "A"]);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1874)

#### pub fn [splitn](https://doc.rust-lang.org/std/string/struct.String.html#method.splitn)<P>(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pat: P) -> [SplitN](https://doc.rust-lang.org/std/str/struct.SplitN.html "struct std::str::SplitN")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over substrings of the given string slice, separated
by a pattern, restricted to returning at most `n` items.

If `n` substrings are returned, the last substring (the `n`th substring)
will contain the remainder of the string.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-4)Iterator behavior

The returned iterator will not be double ended, because it is
not efficient to support.

If the pattern allows a reverse search, the [`rsplitn`](https://doc.rust-lang.org/std/primitive.str.html#method.rsplitn "method str::rsplitn") method can be
used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-80)Examples

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

#### pub fn [rsplitn](https://doc.rust-lang.org/std/string/struct.String.html#method.rsplitn)<P>(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html), pat: P) -> [RSplitN](https://doc.rust-lang.org/std/str/struct.RSplitN.html "struct std::str::RSplitN")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over substrings of this string slice, separated by a
pattern, starting from the end of the string, restricted to returning at
most `n` items.

If `n` substrings are returned, the last substring (the `n`th substring)
will contain the remainder of the string.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-5)Iterator behavior

The returned iterator will not be double ended, because it is not
efficient to support.

For splitting from the front, the [`splitn`](https://doc.rust-lang.org/std/primitive.str.html#method.splitn "method str::splitn") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-81)Examples

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

#### pub fn [split\_once](https://doc.rust-lang.org/std/string/struct.String.html#method.split_once)<P>(&self, delimiter: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Splits the string on the first occurrence of the specified delimiter and
returns prefix before delimiter and suffix after delimiter.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-82)Examples

```
assert_eq!("cfg".split_once('='), None);
assert_eq!("cfg=".split_once('='), Some(("cfg", "")));
assert_eq!("cfg=foo".split_once('='), Some(("cfg", "foo")));
assert_eq!("cfg=foo=bar".split_once('='), Some(("cfg", "foo=bar")));
```

1.52.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#1961-1963)

#### pub fn [rsplit\_once](https://doc.rust-lang.org/std/string/struct.String.html#method.rsplit_once)<P>(&self, delimiter: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<(&[str](https://doc.rust-lang.org/std/primitive.str.html), &[str](https://doc.rust-lang.org/std/primitive.str.html))> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Splits the string on the last occurrence of the specified delimiter and
returns prefix before delimiter and suffix after delimiter.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-83)Examples

```
assert_eq!("cfg".rsplit_once('='), None);
assert_eq!("cfg=foo".rsplit_once('='), Some(("cfg", "foo")));
assert_eq!("cfg=foo=bar".rsplit_once('='), Some(("cfg=foo", "bar")));
```

1.2.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2001)

#### pub fn [matches](https://doc.rust-lang.org/std/string/struct.String.html#method.matches)<P>(&self, pat: P) -> [Matches](https://doc.rust-lang.org/std/str/struct.Matches.html "struct std::str::Matches")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over the disjoint matches of a pattern within the
given string slice.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-6)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rmatches`](https://doc.rust-lang.org/std/primitive.str.html#method.rmatches "method str::rmatches") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-84)Examples

```
let v: Vec<&str> = "abcXXXabcYYYabc".matches("abc").collect();
assert_eq!(v, ["abc", "abc", "abc"]);

let v: Vec<&str> = "1abc2abc3".matches(char::is_numeric).collect();
assert_eq!(v, ["1", "2", "3"]);
```

1.2.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2035-2037)

#### pub fn [rmatches](https://doc.rust-lang.org/std/string/struct.String.html#method.rmatches)<P>(&self, pat: P) -> [RMatches](https://doc.rust-lang.org/std/str/struct.RMatches.html "struct std::str::RMatches")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over the disjoint matches of a pattern within this
string slice, yielded in reverse order.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-7)Iterator behavior

The returned iterator requires that the pattern supports a reverse
search, and it will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if a forward/reverse
search yields the same elements.

For iterating from the front, the [`matches`](https://doc.rust-lang.org/std/primitive.str.html#method.matches "method str::matches") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-85)Examples

```
let v: Vec<&str> = "abcXXXabcYYYabc".rmatches("abc").collect();
assert_eq!(v, ["abc", "abc", "abc"]);

let v: Vec<&str> = "1abc2abc3".rmatches(char::is_numeric).collect();
assert_eq!(v, ["3", "2", "1"]);
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2079)

#### pub fn [match\_indices](https://doc.rust-lang.org/std/string/struct.String.html#method.match_indices)<P>(&self, pat: P) -> [MatchIndices](https://doc.rust-lang.org/std/str/struct.MatchIndices.html "struct std::str::MatchIndices")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns an iterator over the disjoint matches of a pattern within this string
slice as well as the index that the match starts at.

For matches of `pat` within `self` that overlap, only the indices
corresponding to the first match are returned.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-8)Iterator behavior

The returned iterator will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if the pattern
allows a reverse search and forward/reverse search yields the same
elements. This is true for, e.g., [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), but not for `&str`.

If the pattern allows a reverse search but its results might differ
from a forward search, the [`rmatch_indices`](https://doc.rust-lang.org/std/primitive.str.html#method.rmatch_indices "method str::rmatch_indices") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-86)Examples

```
let v: Vec<_> = "abcXXXabcYYYabc".match_indices("abc").collect();
assert_eq!(v, [(0, "abc"), (6, "abc"), (12, "abc")]);

let v: Vec<_> = "1abcabc2".match_indices("abc").collect();
assert_eq!(v, [(1, "abc"), (4, "abc")]);

let v: Vec<_> = "ababa".match_indices("aba").collect();
assert_eq!(v, [(0, "aba")]); // only the first `aba`
```

1.5.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2119-2121)

#### pub fn [rmatch\_indices](https://doc.rust-lang.org/std/string/struct.String.html#method.rmatch_indices)<P>(&self, pat: P) -> [RMatchIndices](https://doc.rust-lang.org/std/str/struct.RMatchIndices.html "struct std::str::RMatchIndices")<'\_, P> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns an iterator over the disjoint matches of a pattern within `self`,
yielded in reverse order along with the index of the match.

For matches of `pat` within `self` that overlap, only the indices
corresponding to the last match are returned.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#iterator-behavior-9)Iterator behavior

The returned iterator requires that the pattern supports a reverse
search, and it will be a [`DoubleEndedIterator`](https://doc.rust-lang.org/std/iter/trait.DoubleEndedIterator.html "trait std::iter::DoubleEndedIterator") if a forward/reverse
search yields the same elements.

For iterating from the front, the [`match_indices`](https://doc.rust-lang.org/std/primitive.str.html#method.match_indices "method str::match_indices") method can be used.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-87)Examples

```
let v: Vec<_> = "abcXXXabcYYYabc".rmatch_indices("abc").collect();
assert_eq!(v, [(12, "abc"), (6, "abc"), (0, "abc")]);

let v: Vec<_> = "1abcabc2".rmatch_indices("abc").collect();
assert_eq!(v, [(4, "abc"), (1, "abc")]);

let v: Vec<_> = "ababa".rmatch_indices("aba").collect();
assert_eq!(v, [(2, "aba")]); // only the last `aba`
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2143)

#### pub fn [trim](https://doc.rust-lang.org/std/string/struct.String.html#method.trim)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading and trailing whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`, which includes newlines.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-88)Examples

```
let s = "\n Hello\tworld\t\n";

assert_eq!("Hello\tworld", s.trim());
```

1.30.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2182)

#### pub fn [trim\_start](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_start)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`, which includes newlines.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality)Text directionality

A string is a sequence of bytes. `start` in this context means the first
position of that byte string; for a left-to-right language like English or
Russian, this will be left side, and for right-to-left languages like
Arabic or Hebrew, this will be the right side.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-89)Examples

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

#### pub fn [trim\_end](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_end)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with trailing whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`, which includes newlines.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality-1)Text directionality

A string is a sequence of bytes. `end` in this context means the last
position of that byte string; for a left-to-right language like English or
Russian, this will be right side, and for right-to-left languages like
Arabic or Hebrew, this will be the left side.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-90)Examples

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

#### pub fn [trim\_left](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_left)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.33.0: superseded by `trim_start`

Returns a string slice with leading whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality-2)Text directionality

A string is a sequence of bytes. ‘Left’ in this context means the first
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *right* side, not the left.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-91)Examples

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

#### pub fn [trim\_right](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_right)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

👎Deprecated since 1.33.0: superseded by `trim_end`

Returns a string slice with trailing whitespace removed.

‘Whitespace’ is defined according to the terms of the Unicode Derived
Core Property `White_Space`.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality-3)Text directionality

A string is a sequence of bytes. ‘Right’ in this context means the last
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *left* side, not the right.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-92)Examples

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

#### pub fn [trim\_matches](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [DoubleEndedSearcher](https://doc.rust-lang.org/std/str/pattern/trait.DoubleEndedSearcher.html "trait std::str::pattern::DoubleEndedSearcher")<'a>,

Returns a string slice with all prefixes and suffixes that match a
pattern repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a function
or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-93)Examples

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

#### pub fn [trim\_start\_matches](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_start_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns a string slice with all prefixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality-4)Text directionality

A string is a sequence of bytes. `start` in this context means the first
position of that byte string; for a left-to-right language like English or
Russian, this will be left side, and for right-to-left languages like
Arabic or Hebrew, this will be the right side.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-94)Examples

```
assert_eq!("11foo1bar11".trim_start_matches('1'), "foo1bar11");
assert_eq!("123foo1bar123".trim_start_matches(char::is_numeric), "foo1bar123");

let x: &[_] = &['1', '2'];
assert_eq!("12foo1bar12".trim_start_matches(x), "foo1bar12");
```

1.45.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2415)

#### pub fn [strip\_prefix](https://doc.rust-lang.org/std/string/struct.String.html#method.strip_prefix)<P>(&self, prefix: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Returns a string slice with the prefix removed.

If the string starts with the pattern `prefix`, returns the substring after the prefix,
wrapped in `Some`. Unlike [`trim_start_matches`](https://doc.rust-lang.org/std/primitive.str.html#method.trim_start_matches "method str::trim_start_matches"), this method removes the prefix exactly once.

If the string does not start with `prefix`, returns `None`.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-95)Examples

```
assert_eq!("foo:bar".strip_prefix("foo:"), Some("bar"));
assert_eq!("foo:bar".strip_prefix("bar"), None);
assert_eq!("foofoo".strip_prefix("foo"), Some("foo"));
```

1.45.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2443-2445)

#### pub fn [strip\_suffix](https://doc.rust-lang.org/std/string/struct.String.html#method.strip_suffix)<P>(&self, suffix: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns a string slice with the suffix removed.

If the string ends with the pattern `suffix`, returns the substring before the suffix,
wrapped in `Some`. Unlike [`trim_end_matches`](https://doc.rust-lang.org/std/primitive.str.html#method.trim_end_matches "method str::trim_end_matches"), this method removes the suffix exactly once.

If the string does not end with `suffix`, returns `None`.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-96)Examples

```
assert_eq!("bar:foo".strip_suffix(":foo"), Some("bar"));
assert_eq!("bar:foo".strip_suffix("bar"), None);
assert_eq!("foofoo".strip_suffix("foo"), Some("foo"));
```

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2483)

#### pub fn [trim\_prefix](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_prefix)<P>(&self, prefix: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

🔬This is a nightly-only experimental API. (`trim_prefix_suffix` [#142312](https://github.com/rust-lang/rust/issues/142312))

Returns a string slice with the optional prefix removed.

If the string starts with the pattern `prefix`, returns the substring after the prefix.
Unlike [`strip_prefix`](https://doc.rust-lang.org/std/primitive.str.html#method.strip_prefix "method str::strip_prefix"), this method always returns `&str` for easy method chaining,
instead of returning [`Option<&str>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option").

If the string does not start with `prefix`, returns the original string unchanged.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-97)Examples

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

#### pub fn [trim\_suffix](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_suffix)<P>(&self, suffix: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

🔬This is a nightly-only experimental API. (`trim_prefix_suffix` [#142312](https://github.com/rust-lang/rust/issues/142312))

Returns a string slice with the optional suffix removed.

If the string ends with the pattern `suffix`, returns the substring before the suffix.
Unlike [`strip_suffix`](https://doc.rust-lang.org/std/primitive.str.html#method.strip_suffix "method str::strip_suffix"), this method always returns `&str` for easy method chaining,
instead of returning [`Option<&str>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option").

If the string does not end with `suffix`, returns the original string unchanged.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-98)Examples

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

#### pub fn [trim\_end\_matches](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_end_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

Returns a string slice with all suffixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality-5)Text directionality

A string is a sequence of bytes. `end` in this context means the last
position of that byte string; for a left-to-right language like English or
Russian, this will be right side, and for right-to-left languages like
Arabic or Hebrew, this will be the left side.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-99)Examples

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

#### pub fn [trim\_left\_matches](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_left_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

👎Deprecated since 1.33.0: superseded by `trim_start_matches`

Returns a string slice with all prefixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality-6)Text directionality

A string is a sequence of bytes. ‘Left’ in this context means the first
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *right* side, not the left.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-100)Examples

```
assert_eq!("11foo1bar11".trim_left_matches('1'), "foo1bar11");
assert_eq!("123foo1bar123".trim_left_matches(char::is_numeric), "foo1bar123");

let x: &[_] = &['1', '2'];
assert_eq!("12foo1bar12".trim_left_matches(x), "foo1bar12");
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2650-2652)

#### pub fn [trim\_right\_matches](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_right_matches)<P>(&self, pat: P) -> &[str](https://doc.rust-lang.org/std/primitive.str.html) where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"), <P as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: for<'a> [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

👎Deprecated since 1.33.0: superseded by `trim_end_matches`

Returns a string slice with all suffixes that match a pattern
repeatedly removed.

The [pattern](https://doc.rust-lang.org/std/str/pattern/index.html "mod std::str::pattern") can be a `&str`, [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char"), a slice of [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char")s, or a
function or closure that determines if a character matches.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#text-directionality-7)Text directionality

A string is a sequence of bytes. ‘Right’ in this context means the last
position of that byte string; for a language like Arabic or Hebrew
which are ‘right to left’ rather than ‘left to right’, this will be
the *left* side, not the right.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-101)Examples

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

#### pub fn [parse](https://doc.rust-lang.org/std/string/struct.String.html#method.parse)<F>(&self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<F, <F as [FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr")>::[Err](https://doc.rust-lang.org/std/str/trait.FromStr.html#associatedtype.Err "type std::str::FromStr::Err")> where F: [FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr"),

Parses this string slice into another type.

Because `parse` is so general, it can cause problems with type
inference. As such, `parse` is one of the few times you’ll see
the syntax affectionately known as the ‘turbofish’: `::<>`. This
helps the inference algorithm understand specifically which type
you’re trying to parse into.

`parse` can parse into any type that implements the [`FromStr`](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr") trait.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#errors-4)Errors

Will return [`Err`](https://doc.rust-lang.org/std/str/trait.FromStr.html#associatedtype.Err "associated type std::str::FromStr::Err") if it’s not possible to parse this string slice into
the desired type.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-102)Examples

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

1.23.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2720)

#### pub fn [is\_ascii](https://doc.rust-lang.org/std/string/struct.String.html#method.is_ascii)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Checks if all characters in this string are within the ASCII range.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-103)Examples

```
let ascii = "hello!\n";
let non_ascii = "Grüße, Jürgen ❤";

assert!(ascii.is_ascii());
assert!(!non_ascii.is_ascii());
```

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2732)

#### pub fn [as\_ascii](https://doc.rust-lang.org/std/string/struct.String.html#method.as_ascii)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[[AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")]>

🔬This is a nightly-only experimental API. (`ascii_char` [#110998](https://github.com/rust-lang/rust/issues/110998))

If this string slice [`is_ascii`](https://doc.rust-lang.org/std/primitive.str.html#method.is_ascii "method str::is_ascii"), returns it as a slice
of [ASCII characters](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char"), otherwise returns `None`.

[Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2746)

#### pub unsafe fn [as\_ascii\_unchecked](https://doc.rust-lang.org/std/string/struct.String.html#method.as_ascii_unchecked)(&self) -> &[[AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")]

🔬This is a nightly-only experimental API. (`ascii_char` [#110998](https://github.com/rust-lang/rust/issues/110998))

Converts this string slice into a slice of [ASCII characters](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char"),
without checking whether they are valid.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#safety-8)Safety

Every character in this string must be ASCII, or else this is UB.

1.23.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2774)

#### pub fn [eq\_ignore\_ascii\_case](https://doc.rust-lang.org/std/string/struct.String.html#method.eq_ignore_ascii_case)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Checks that two strings are an ASCII case-insensitive match.

Same as `to_ascii_lowercase(a) == to_ascii_lowercase(b)`,
but without allocating and copying temporaries.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-104)Examples

```
assert!("Ferris".eq_ignore_ascii_case("FERRIS"));
assert!("Ferrös".eq_ignore_ascii_case("FERRöS"));
assert!(!"Ferrös".eq_ignore_ascii_case("FERRÖS"));
```

1.23.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2800)

#### pub fn [make\_ascii\_uppercase](https://doc.rust-lang.org/std/string/struct.String.html#method.make_ascii_uppercase)(&mut self)

Converts this string to its ASCII upper case equivalent in-place.

ASCII letters ‘a’ to ‘z’ are mapped to ‘A’ to ‘Z’,
but non-ASCII letters are unchanged.

To return a new uppercased value without modifying the existing one, use
[`to_ascii_uppercase()`](https://doc.rust-lang.org/std/string/struct.String.html#method.to_ascii_uppercase).

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-105)Examples

```
let mut s = String::from("Grüße, Jürgen ❤");

s.make_ascii_uppercase();

assert_eq!("GRüßE, JüRGEN ❤", s);
```

1.23.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2828)

#### pub fn [make\_ascii\_lowercase](https://doc.rust-lang.org/std/string/struct.String.html#method.make_ascii_lowercase)(&mut self)

Converts this string to its ASCII lower case equivalent in-place.

ASCII letters ‘A’ to ‘Z’ are mapped to ‘a’ to ‘z’,
but non-ASCII letters are unchanged.

To return a new lowercased value without modifying the existing one, use
[`to_ascii_lowercase()`](https://doc.rust-lang.org/std/string/struct.String.html#method.to_ascii_lowercase).

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-106)Examples

```
let mut s = String::from("GRÜßE, JÜRGEN ❤");

s.make_ascii_lowercase();

assert_eq!("grÜße, jÜrgen ❤", s);
```

1.80.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2853)

#### pub fn [trim\_ascii\_start](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_ascii_start)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading ASCII whitespace removed.

‘Whitespace’ refers to the definition used by
[`u8::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.u8.html#method.is_ascii_whitespace "method u8::is_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-107)Examples

```
assert_eq!(" \t \u{3000}hello world\n".trim_ascii_start(), "\u{3000}hello world\n");
assert_eq!("  ".trim_ascii_start(), "");
assert_eq!("".trim_ascii_start(), "");
```

1.80.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2878)

#### pub fn [trim\_ascii\_end](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_ascii_end)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with trailing ASCII whitespace removed.

‘Whitespace’ refers to the definition used by
[`u8::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.u8.html#method.is_ascii_whitespace "method u8::is_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-108)Examples

```
assert_eq!("\r hello world\u{3000}\n ".trim_ascii_end(), "\r hello world\u{3000}");
assert_eq!("  ".trim_ascii_end(), "");
assert_eq!("".trim_ascii_end(), "");
```

1.80.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2904)

#### pub fn [trim\_ascii](https://doc.rust-lang.org/std/string/struct.String.html#method.trim_ascii)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Returns a string slice with leading and trailing ASCII whitespace
removed.

‘Whitespace’ refers to the definition used by
[`u8::is_ascii_whitespace`](https://doc.rust-lang.org/std/primitive.u8.html#method.is_ascii_whitespace "method u8::is_ascii_whitespace").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-109)Examples

```
assert_eq!("\r hello world\n ".trim_ascii(), "hello world");
assert_eq!("  ".trim_ascii(), "");
assert_eq!("".trim_ascii(), "");
```

1.34.0 · [Source](https://doc.rust-lang.org/src/core/str/mod.rs.html#2947)

#### pub fn [escape\_debug](https://doc.rust-lang.org/std/string/struct.String.html#method.escape_debug)(&self) -> [EscapeDebug](https://doc.rust-lang.org/std/str/struct.EscapeDebug.html "struct std::str::EscapeDebug")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns an iterator that escapes each char in `self` with [`char::escape_debug`](https://doc.rust-lang.org/std/primitive.char.html#method.escape_debug "method char::escape_debug").

Note: only extended grapheme codepoints that begin the string will be
escaped.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-110)Examples

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

#### pub fn [escape\_default](https://doc.rust-lang.org/std/string/struct.String.html#method.escape_default)(&self) -> [EscapeDefault](https://doc.rust-lang.org/std/str/struct.EscapeDefault.html "struct std::str::EscapeDefault")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns an iterator that escapes each char in `self` with [`char::escape_default`](https://doc.rust-lang.org/std/primitive.char.html#method.escape_default "method char::escape_default").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-111)Examples

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

#### pub fn [escape\_unicode](https://doc.rust-lang.org/std/string/struct.String.html#method.escape_unicode)(&self) -> [EscapeUnicode](https://doc.rust-lang.org/std/str/struct.EscapeUnicode.html "struct std::str::EscapeUnicode")<'\_> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Returns an iterator that escapes each char in `self` with [`char::escape_unicode`](https://doc.rust-lang.org/std/primitive.char.html#method.escape_unicode "method char::escape_unicode").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-112)Examples

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

#### pub fn [substr\_range](https://doc.rust-lang.org/std/string/struct.String.html#method.substr_range)(&self, substr: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Range](https://doc.rust-lang.org/std/ops/struct.Range.html "struct std::ops::Range")<[usize](https://doc.rust-lang.org/std/primitive.usize.html)>>

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

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-113)Examples

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

#### pub fn [as\_str](https://doc.rust-lang.org/std/string/struct.String.html#method.as_str-1)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

🔬This is a nightly-only experimental API. (`str_as_str` [#130366](https://github.com/rust-lang/rust/issues/130366))

Returns the same string as a string slice `&str`.

This method is redundant when used directly on `&str`, but
it helps dereferencing other string-like types to string slices,
for example references to `Box<str>` or `Arc<str>`.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#268)

#### pub fn [replace](https://doc.rust-lang.org/std/string/struct.String.html#method.replace)<P>(&self, from: P, to: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Replaces all matches of a pattern with another string.

`replace` creates a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), and copies the data from this string slice into it.
While doing so, it attempts to find matches of a pattern. If it finds any, it
replaces them with the replacement string slice.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-114)Examples

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

#### pub fn [replacen](https://doc.rust-lang.org/std/string/struct.String.html#method.replacen)<P>(&self, pat: P, to: &[str](https://doc.rust-lang.org/std/primitive.str.html), count: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where P: [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern"),

Replaces first N matches of a pattern with another string.

`replacen` creates a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), and copies the data from this string slice into it.
While doing so, it attempts to find matches of a pattern. If it finds any, it
replaces them with the replacement string slice at most `count` times.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-115)Examples

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

#### pub fn [to\_lowercase](https://doc.rust-lang.org/std/string/struct.String.html#method.to_lowercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns the lowercase equivalent of this string slice, as a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

‘Lowercase’ is defined according to the terms of the Unicode Derived Core Property
`Lowercase`.

Since some characters can expand into multiple characters when changing
the case, this function returns a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") instead of modifying the
parameter in-place.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-116)Examples

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

#### pub fn [to\_uppercase](https://doc.rust-lang.org/std/string/struct.String.html#method.to_uppercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns the uppercase equivalent of this string slice, as a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

‘Uppercase’ is defined according to the terms of the Unicode Derived Core Property
`Uppercase`.

Since some characters can expand into multiple characters when changing
the case, this function returns a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") instead of modifying the
parameter in-place.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-117)Examples

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

1.16.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#530)

#### pub fn [repeat](https://doc.rust-lang.org/std/string/struct.String.html#method.repeat)(&self, n: [usize](https://doc.rust-lang.org/std/primitive.usize.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Creates a new [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") by repeating a string `n` times.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#panics-12)Panics

This function will panic if the capacity would overflow.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-118)Examples

Basic usage:

```
assert_eq!("abc".repeat(4), String::from("abcabcabcabc"));
```

A panic upon overflow:

[ⓘ](https://doc.rust-lang.org/std/string/struct.String.html "This example panics")

```
// this will panic at runtime
let huge = "0123456789abcdef".repeat(usize::MAX);
```

1.23.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#560)

#### pub fn [to\_ascii\_uppercase](https://doc.rust-lang.org/std/string/struct.String.html#method.to_ascii_uppercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns a copy of this string where each character is mapped to its
ASCII upper case equivalent.

ASCII letters ‘a’ to ‘z’ are mapped to ‘A’ to ‘Z’,
but non-ASCII letters are unchanged.

To uppercase the value in-place, use [`make_ascii_uppercase`](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_uppercase "method str::make_ascii_uppercase").

To uppercase ASCII characters in addition to non-ASCII characters, use
[`to_uppercase`](https://doc.rust-lang.org/std/string/struct.String.html#method.to_uppercase).

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-119)Examples

```
let s = "Grüße, Jürgen ❤";

assert_eq!("GRüßE, JüRGEN ❤", s.to_ascii_uppercase());
```

1.23.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#592)

#### pub fn [to\_ascii\_lowercase](https://doc.rust-lang.org/std/string/struct.String.html#method.to_ascii_lowercase)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns a copy of this string where each character is mapped to its
ASCII lower case equivalent.

ASCII letters ‘A’ to ‘Z’ are mapped to ‘a’ to ‘z’,
but non-ASCII letters are unchanged.

To lowercase the value in-place, use [`make_ascii_lowercase`](https://doc.rust-lang.org/std/primitive.str.html#method.make_ascii_lowercase "method str::make_ascii_lowercase").

To lowercase ASCII characters in addition to non-ASCII characters, use
[`to_lowercase`](https://doc.rust-lang.org/std/string/struct.String.html#method.to_lowercase).

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-120)Examples

```
let s = "Grüße, Jürgen ❤";

assert_eq!("grüße, jürgen ❤", s.to_ascii_lowercase());
```

## Trait Implementations[§](https://doc.rust-lang.org/std/string/struct.String.html#trait-implementations)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2676)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Add%3C%26str%3E-for-String)

### impl [Add](https://doc.rust-lang.org/std/ops/trait.Add.html "trait std::ops::Add")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Implements the `+` operator for concatenating two strings.

This consumes the `String` on the left-hand side and re-uses its buffer (growing it if
necessary). This is done to avoid allocating a new `String` and copying the entire contents on
every operation, which would lead to *O*(*n*^2) running time when building an *n*-byte string by
repeated concatenation.

The string on the right-hand side is only borrowed; its contents are copied into the returned
`String`.

#### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-121)Examples

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

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2677)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Output)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Add.html#associatedtype.Output) = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

The resulting type after applying the `+` operator.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2680)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.add)

#### fn [add](https://doc.rust-lang.org/std/ops/trait.Add.html#tymethod.add)(self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Performs the `+` operation. [Read more](https://doc.rust-lang.org/std/ops/trait.Add.html#tymethod.add)

1.12.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2691)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-AddAssign%3C%26str%3E-for-String)

### impl [AddAssign](https://doc.rust-lang.org/std/ops/trait.AddAssign.html "trait std::ops::AddAssign")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Implements the `+=` operator for appending to a `String`.

This has the same behavior as the [`push_str`](https://doc.rust-lang.org/std/string/struct.String.html#method.push_str "method std::string::String::push_str") method.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2693)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.add_assign)

#### fn [add\_assign](https://doc.rust-lang.org/std/ops/trait.AddAssign.html#tymethod.add_assign)(&mut self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html))

Performs the `+=` operation. [Read more](https://doc.rust-lang.org/std/ops/trait.AddAssign.html#tymethod.add_assign)

1.43.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2996)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-AsMut%3Cstr%3E-for-String)

### impl [AsMut](https://doc.rust-lang.org/std/convert/trait.AsMut.html "trait std::convert::AsMut")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2998)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.as_mut)

#### fn [as\_mut](https://doc.rust-lang.org/std/convert/trait.AsMut.html#tymethod.as_mut)(&mut self) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a mutable reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3004)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-AsRef%3C%5Bu8%5D%3E-for-String)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3006)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.as_ref-1)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1712-1717)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-AsRef%3COsStr%3E-for-String)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#1714-1716)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.as_ref-2)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[OsStr](https://doc.rust-lang.org/std/ffi/struct.OsStr.html "struct std::ffi::OsStr")

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#3559-3564)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-AsRef%3CPath%3E-for-String)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#3561-3563)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.as_ref-3)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2988)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-AsRef%3Cstr%3E-for-String)

### impl [AsRef](https://doc.rust-lang.org/std/convert/trait.AsRef.html "trait std::convert::AsRef")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2990)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.as_ref)

#### fn [as\_ref](https://doc.rust-lang.org/std/convert/trait.AsRef.html#tymethod.as_ref)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Converts this type into a shared reference of the (usually inferred) input type.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#189)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Borrow%3Cstr%3E-for-String)

### impl [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#191)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

1.36.0 · [Source](https://doc.rust-lang.org/src/alloc/str.rs.html#197)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-BorrowMut%3Cstr%3E-for-String)

### impl [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/str.rs.html#199)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2295)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Clone-for-String)

### impl [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2306)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.clone_from)

#### fn [clone\_from](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)(&mut self, source: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"))

Clones the contents of `source` into `self`.

This method is preferred over simply assigning `source.clone()` to `self`,
as it avoids reallocation if possible.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2297)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.clone)

#### fn [clone](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Returns a duplicate of the value. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2622)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Debug-for-String)

### impl [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2624)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143894 "Tracking issue for const_default")) · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2605)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Default-for-String)

### impl [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2608)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.default)

#### fn [default](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default)() -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Creates an empty `String`.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2723)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Deref-for-String)

### impl [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2724)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Target)

#### type [Target](https://doc.rust-lang.org/std/ops/trait.Deref.html#associatedtype.Target) = [str](https://doc.rust-lang.org/std/primitive.str.html)

The resulting type after dereferencing.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2727)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.deref)

#### fn [deref](https://doc.rust-lang.org/std/ops/trait.Deref.html#tymethod.deref)(&self) -> &[str](https://doc.rust-lang.org/std/primitive.str.html)

Dereferences the value.

1.3.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2736)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-DerefMut-for-String)

### impl [DerefMut](https://doc.rust-lang.org/std/ops/trait.DerefMut.html "trait std::ops::DerefMut") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2738)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.deref_mut)

#### fn [deref\_mut](https://doc.rust-lang.org/std/ops/trait.DerefMut.html#tymethod.deref_mut)(&mut self) -> &mut [str](https://doc.rust-lang.org/std/primitive.str.html)

Mutably dereferences the value.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2614)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Display-for-String)

### impl [Display](https://doc.rust-lang.org/std/fmt/trait.Display.html "trait std::fmt::Display") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2616)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.fmt-1)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Display.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Display.html#tymethod.fmt)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2494)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3C%26Char%3E-for-String)

### impl<'a> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<&'a [AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2497)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend-7)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2503)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one-7)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, c: &'a [AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char"))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#425)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve-7)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.2.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2413)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3C%26char%3E-for-String)

### impl<'a> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<&'a [char](https://doc.rust-lang.org/std/primitive.char.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2414)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend-1)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [char](https://doc.rust-lang.org/std/primitive.char.html)>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2419)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one-1)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, \_: &'a [char](https://doc.rust-lang.org/std/primitive.char.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2424)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve-1)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2431)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3C%26str%3E-for-String)

### impl<'a> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2432)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend-2)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [str](https://doc.rust-lang.org/std/primitive.str.html)>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2437)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one-2)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, s: &'a [str](https://doc.rust-lang.org/std/primitive.str.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#425)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve-2)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.45.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2444)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3CBox%3Cstr,+A%3E%3E-for-String)

### impl<A> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<[Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html), A>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2445)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend-3)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html), A>>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#417)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one-3)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, item: A)

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#425)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve-3)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2478)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3CChar%3E-for-String)

### impl [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<[AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2481)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend-6)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char")>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2487)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one-6)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, c: [AsciiChar](https://doc.rust-lang.org/std/ascii/enum.Char.html "enum std::ascii::Char"))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#425)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve-6)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.19.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2465)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3CCow%3C'a,+str%3E%3E-for-String)

### impl<'a> [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2466)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend-5)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2471)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one-5)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, s: [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>)

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#425)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve-5)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2452)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3CString%3E-for-String)

### impl [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2453)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend-4)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2458)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one-4)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, s: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/core/iter/traits/collect.rs.html#425)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve-4)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2392)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Extend%3Cchar%3E-for-String)

### impl [Extend](https://doc.rust-lang.org/std/iter/trait.Extend.html "trait std::iter::Extend")<[char](https://doc.rust-lang.org/std/primitive.char.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2393)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend)

#### fn [extend](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)<I>(&mut self, iter: I) where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [char](https://doc.rust-lang.org/std/primitive.char.html)>,

Extends a collection with the contents of an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#tymethod.extend)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2401)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_one)

#### fn [extend\_one](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_one)(&mut self, c: [char](https://doc.rust-lang.org/std/primitive.char.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Extends a collection with exactly one element.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2406)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.extend_reserve)

#### fn [extend\_reserve](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)(&mut self, additional: [usize](https://doc.rust-lang.org/std/primitive.usize.html))

🔬This is a nightly-only experimental API. (`extend_one` [#72631](https://github.com/rust-lang/rust/issues/72631))

Reserves capacity in a collection for the given number of additional elements. [Read more](https://doc.rust-lang.org/std/iter/trait.Extend.html#method.extend_reserve)

1.28.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3156)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3C%26String%3E-for-Cow%3C'a,+str%3E)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&'a [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3171)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-10)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &'a [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") reference into a [`Borrowed`](https://doc.rust-lang.org/std/borrow/enum.Cow.html#variant.Borrowed "borrow::Cow::Borrowed") variant.
No heap allocation is performed, and the string
is not copied.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#example-3)Example

```
let s = "eggplant".to_string();
assert_eq!(Cow::from(&s), Cow::Borrowed("eggplant"));
```

1.35.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3037)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3C%26String%3E-for-String)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3042)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-5)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a `&String` into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

This clones `s` and returns the clone.

1.44.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3025)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3C%26mut+str%3E-for-String)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&mut [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3030)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-4)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &mut [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a `&mut str` into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

The result is allocated on the heap.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3013)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3C%26str%3E-for-String)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3018)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-3)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a `&str` into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

The result is allocated on the heap.

1.18.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3049)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CBox%3Cstr%3E%3E-for-String)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3062)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-6)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts the given boxed `str` slice to a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").
It is notable that the `str` slice is owned.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-124)Examples

```
let s1: String = String::from("hello world");
let s2: Box<str> = s1.into_boxed_str();
let s3: String = String::from(s2);

assert_eq!("hello world", s3)
```

1.14.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3088)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CCow%3C'a,+str%3E%3E-for-String)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3105)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-8)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts a clone-on-write string to an owned
instance of [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String").

This extracts the owned string,
clones the string if it is not already owned.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#example-1)Example

```
// If the string is not owned...
let cow: Cow<'_, str> = Cow::Borrowed("eggplant");
// It will allocate on the heap and copy the string.
let owned: String = String::from(cow);
assert_eq!(&owned[..], "eggplant");
```

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3800)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-Arc%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/sync.rs.html#3812)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-13)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html "struct std::sync::Arc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Allocates a reference-counted `str` and copies `v` into it.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#example-5)Example

```
let unique: String = "eggplant".to_owned();
let shared: Arc<str> = Arc::from(unique);
assert_eq!("eggplant", &shared[..]);
```

1.6.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#632)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-Box%3Cdyn+Error%3E)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + 'a>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#644)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-1)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(str\_err: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + 'a>

Converts a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") into a box of dyn [`Error`](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-123)Examples

```
use std::error::Error;

let a_string_error = "a string error".to_string();
let a_boxed_error = Box::<dyn Error>::from(a_string_error);
assert!(size_of::<Box<dyn Error>>() == size_of_val(&a_boxed_error))
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#594)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-Box%3Cdyn+Error+%2B+Send+%2B+Sync%3E)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") + 'a>

[Source](https://doc.rust-lang.org/src/alloc/boxed/convert.rs.html#608)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(err: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<dyn [Error](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") + 'a>

Converts a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") into a box of dyn [`Error`](https://doc.rust-lang.org/std/error/trait.Error.html "trait std::error::Error") + [`Send`](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") + [`Sync`](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-122)Examples

```
use std::error::Error;

let a_string_error = "a string error".to_string();
let a_boxed_error = Box::<dyn Error + Send + Sync>::from(a_string_error);
assert!(
    size_of::<Box<dyn Error + Send + Sync>>() == size_of_val(&a_boxed_error))
```

1.20.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3069)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-Box%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3081)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-7)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts the given [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") to a boxed `str` slice that is owned.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-125)Examples

```
let s1: String = String::from("hello world");
let s2: Box<str> = Box::from(s1);
let s3: String = String::from(s2);

assert_eq!("hello world", s3)
```

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3133)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-Cow%3C'a,+str%3E)

### impl<'a> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3149)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-9)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

Converts a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") into an [`Owned`](https://doc.rust-lang.org/std/borrow/enum.Cow.html#variant.Owned "borrow::Cow::Owned") variant.
No heap allocation is performed, and the string
is not copied.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#example-2)Example

```
let s = "eggplant".to_string();
let s2 = "eggplant".to_string();
assert_eq!(Cow::from(s), Cow::<'static, str>::Owned(s2));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#609-617)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-OsString)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")

[Source](https://doc.rust-lang.org/src/std/ffi/os_str.rs.html#614-616)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-14)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [OsString](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString")

Converts a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") into an [`OsString`](https://doc.rust-lang.org/std/ffi/struct.OsString.html "struct std::ffi::OsString").

This conversion does not allocate or copy memory.

1.0.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#1870-1878)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-PathBuf)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#1875-1877)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-15)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(s: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")

Converts a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") into a [`PathBuf`](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")

This conversion does not allocate or copy memory.

1.21.0 · [Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2775)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-Rc%3Cstr%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/rc.rs.html#2787)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-2)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(v: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html "struct std::rc::Rc")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

Allocates a reference-counted string slice and copies `v` into it.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#example)Example

```
let original: String = "statue".to_owned();
let shared: Rc<str> = Rc::from(original);
assert_eq!("statue", &shared[..]);
```

1.14.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3201)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CString%3E-for-Vec%3Cu8%3E)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3214)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-11)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(string: [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)> [ⓘ](https://doc.rust-lang.org/std/string/struct.String.html)

Converts the given [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") to a vector [`Vec`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec") that holds values of type [`u8`](https://doc.rust-lang.org/std/primitive.u8.html "primitive u8").

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-126)Examples

```
let s1 = String::from("hello world");
let v1 = Vec::from(s1);

for b in v1 {
    println!("{b}");
}
```

1.46.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3490)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3Cchar%3E-for-String)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[char](https://doc.rust-lang.org/std/primitive.char.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3500)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-12)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(c: [char](https://doc.rust-lang.org/std/primitive.char.html)) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Allocates an owned [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") from a single character.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#example-4)Example

```
let c: char = 'a';
let s: String = String::from(c);
assert_eq!("a", &s[..]);
```

1.17.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2323)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3C%26char%3E-for-String)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<&'a [char](https://doc.rust-lang.org/std/primitive.char.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2324)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter-2)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [char](https://doc.rust-lang.org/std/primitive.char.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2333)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3C%26str%3E-for-String)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2334)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter-3)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = &'a [str](https://doc.rust-lang.org/std/primitive.str.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.45.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2362)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3CBox%3Cstr,+A%3E%3E-for-String)

### impl<A> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html), A>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where A: [Allocator](https://doc.rust-lang.org/std/alloc/trait.Allocator.html "trait std::alloc::Allocator"),

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2363)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter-5)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html), A>>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.19.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2372)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3CCow%3C'a,+str%3E%3E-for-String)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2373)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter-6)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.80.0 · [Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#174)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3CString%3E-for-Box%3Cstr%3E)

### impl [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/boxed/iter.rs.html#175)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<T>(iter: T) -> [Box](https://doc.rust-lang.org/std/boxed/struct.Box.html "struct std::boxed::Box")<[str](https://doc.rust-lang.org/std/primitive.str.html)> where T: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.12.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3194)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3CString%3E-for-Cow%3C'a,+str%3E)

### impl<'a> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3195)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter-7)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(it: I) -> [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)> where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.4.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2343)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3CString%3E-for-String)

### impl [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2344)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter-4)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2313)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromIterator%3Cchar%3E-for-String)

### impl [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[char](https://doc.rust-lang.org/std/primitive.char.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2314)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_iter-1)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [char](https://doc.rust-lang.org/std/primitive.char.html)>,

Creates a value from an iterator. [Read more](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2753)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-FromStr-for-String)

### impl [FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2754)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Err)

#### type [Err](https://doc.rust-lang.org/std/str/trait.FromStr.html#associatedtype.Err) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The associated error which can be returned from parsing.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2756)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from_str)

#### fn [from\_str](https://doc.rust-lang.org/std/str/trait.FromStr.html#tymethod.from_str)(s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), <[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr")>::[Err](https://doc.rust-lang.org/std/str/trait.FromStr.html#associatedtype.Err "type std::str::FromStr::Err")>

Parses a string `s` to return a value of this type. [Read more](https://doc.rust-lang.org/std/str/trait.FromStr.html#tymethod.from_str)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2630)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Hash-for-String)

### impl [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2632)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.hash)

#### fn [hash](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)<H>(&self, hasher: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"),

Feeds this value into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)

1.3.0 · [Source](https://doc.rust-lang.org/src/core/hash/mod.rs.html#235-237)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.hash_slice)

#### fn [hash\_slice](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)<H>(data: &[Self], state: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"), Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Feeds a slice of this type into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2699-2701)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Index%3CI%3E-for-String)

### impl<I> [Index](https://doc.rust-lang.org/std/ops/trait.Index.html "trait std::ops::Index")<I> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2703)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Output-1)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Index.html#associatedtype.Output) = <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

The returned type after indexing.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2706)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.index)

#### fn [index](https://doc.rust-lang.org/std/ops/trait.Index.html#tymethod.index)(&self, index: I) -> &<I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

Performs the indexing (`container[index]`) operation. [Read more](https://doc.rust-lang.org/std/ops/trait.Index.html#tymethod.index)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2712-2714)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-IndexMut%3CI%3E-for-String)

### impl<I> [IndexMut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html "trait std::ops::IndexMut")<I> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") where I: [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>,

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2717)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.index_mut)

#### fn [index\_mut](https://doc.rust-lang.org/std/ops/trait.IndexMut.html#tymethod.index_mut)(&mut self, index: I) -> &mut <I as [SliceIndex](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html "trait std::slice::SliceIndex")<[str](https://doc.rust-lang.org/std/primitive.str.html)>>::[Output](https://doc.rust-lang.org/std/slice/trait.SliceIndex.html#associatedtype.Output "type std::slice::SliceIndex::Output")

Performs the mutable indexing (`container[index]`) operation. [Read more](https://doc.rust-lang.org/std/ops/trait.IndexMut.html#tymethod.index_mut)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Ord-for-String)

### impl [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.cmp)

#### fn [cmp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")

This method returns an [`Ordering`](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering") between `self` and `other`. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1023-1025)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.max)

#### fn [max](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the maximum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1062-1064)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.min)

#### fn [min](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the minimum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)

1.50.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1088-1090)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.clamp)

#### fn [clamp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)(self, min: Self, max: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Restrict a value to a certain interval. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3C%26str%3E-for-String)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-7)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &&'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-7)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &&'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#669)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CByteStr%3E-for-String)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#669)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-3)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-3)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#529)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CByteString%3E-for-String)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#529)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-1)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-1)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2601)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CCow%3C'a,+str%3E%3E-for-String)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2601)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-10)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2601)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-10)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#3434-3439)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CPath%3E-for-String)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#3436-3438)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-14)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-14)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#2131-2136)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CPathBuf%3E-for-String)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#2133-2135)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-12)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-12)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CString%3E-for-%26str)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for &'a [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-8)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2595)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-8)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#669)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CString%3E-for-ByteStr)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#669)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-2)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-2)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#529)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CString%3E-for-ByteString)

### impl<'a> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#529)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2601)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CString%3E-for-Cow%3C'a,+str%3E)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Cow](https://doc.rust-lang.org/std/borrow/enum.Cow.html "enum std::borrow::Cow")<'a, [str](https://doc.rust-lang.org/std/primitive.str.html)>

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2601)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-9)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2601)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-9)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#3426-3431)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CString%3E-for-Path)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [Path](https://doc.rust-lang.org/std/path/struct.Path.html "struct std::path::Path")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#3428-3430)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-13)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-13)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.91.0 · [Source](https://doc.rust-lang.org/src/std/path.rs.html#2123-2128)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CString%3E-for-PathBuf)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [PathBuf](https://doc.rust-lang.org/std/path/struct.PathBuf.html "struct std::path::PathBuf")

[Source](https://doc.rust-lang.org/src/std/path.rs.html#2125-2127)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-11)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-11)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3CString%3E-for-str)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")> for [str](https://doc.rust-lang.org/std/primitive.str.html)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-6)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-6)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq%3Cstr%3E-for-String)

### impl<'a, 'b> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[str](https://doc.rust-lang.org/std/primitive.str.html)> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-5)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2594)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-5)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialEq-for-String)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.eq-4)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ne-4)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-PartialOrd-for-String)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.partial_cmp)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.lt)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.le)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.gt)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.ge)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2520)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Pattern-for-%26String)

### impl<'b> [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern") for &'b [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

A convenience impl that delegates to the impl for `&str`.

#### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-128)Examples

```
assert_eq!(String::from("Hello world").find("world"), Some(6));
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2521)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Searcher)

#### type [Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher)<'a> = <&'b [str](https://doc.rust-lang.org/std/primitive.str.html) as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Associated searcher for this pattern

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2523)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.into_searcher)

#### fn [into\_searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#tymethod.into_searcher)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> <&'b [str](https://doc.rust-lang.org/std/primitive.str.html) as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'\_>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Constructs the associated searcher from
`self` and the `haystack` to search in.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2528)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.is_contained_in)

#### fn [is\_contained\_in](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.is_contained_in)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Checks whether the pattern matches anywhere in the haystack

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2533)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.is_prefix_of)

#### fn [is\_prefix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.is_prefix_of)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Checks whether the pattern matches at the front of the haystack

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2538)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.strip_prefix_of)

#### fn [strip\_prefix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.strip_prefix_of)(self, haystack: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&[str](https://doc.rust-lang.org/std/primitive.str.html)>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Removes the pattern from the front of haystack, if it matches.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2543-2545)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.is_suffix_of)

#### fn [is\_suffix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.is_suffix_of)<'a>(self, haystack: &'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where <&'b [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Checks whether the pattern matches at the back of the haystack

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2551-2553)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.strip_suffix_of)

#### fn [strip\_suffix\_of](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.strip_suffix_of)<'a>(self, haystack: &'a [str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&'a [str](https://doc.rust-lang.org/std/primitive.str.html)> where <&'b [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [Pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html "trait std::str::pattern::Pattern")>::[Searcher](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#associatedtype.Searcher "type std::str::pattern::Pattern::Searcher")<'a>: [ReverseSearcher](https://doc.rust-lang.org/std/str/pattern/trait.ReverseSearcher.html "trait std::str::pattern::ReverseSearcher")<'a>,

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Removes the pattern from the back of haystack, if it matches.

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2559)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.as_utf8_pattern)

#### fn [as\_utf8\_pattern](https://doc.rust-lang.org/std/str/pattern/trait.Pattern.html#method.as_utf8_pattern)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Utf8Pattern](https://doc.rust-lang.org/std/str/pattern/enum.Utf8Pattern.html "enum std::str::pattern::Utf8Pattern")<'\_>>

🔬This is a nightly-only experimental API. (`pattern` [#27721](https://github.com/rust-lang/rust/issues/27721))

Returns the pattern as utf-8 bytes if possible.

1.16.0 · [Source](https://doc.rust-lang.org/src/std/net/socket_addr.rs.html#262-267)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-ToSocketAddrs-for-String)

### impl [ToSocketAddrs](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html "trait std::net::ToSocketAddrs") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/std/net/socket_addr.rs.html#263)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Iter)

#### type [Iter](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html#associatedtype.Iter) = [IntoIter](https://doc.rust-lang.org/std/vec/struct.IntoIter.html "struct std::vec::IntoIter")<[SocketAddr](https://doc.rust-lang.org/std/net/enum.SocketAddr.html "enum std::net::SocketAddr")>

Returned iterator over socket addresses which this type may correspond
to.

[Source](https://doc.rust-lang.org/src/std/net/socket_addr.rs.html#264-266)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.to_socket_addrs)

#### fn [to\_socket\_addrs](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html#tymethod.to_socket_addrs)(&self) -> [Result](https://doc.rust-lang.org/std/io/type.Result.html "type std::io::Result")<[IntoIter](https://doc.rust-lang.org/std/vec/struct.IntoIter.html "struct std::vec::IntoIter")<[SocketAddr](https://doc.rust-lang.org/std/net/enum.SocketAddr.html "enum std::net::SocketAddr")>>

Converts this object to an iterator of resolved [`SocketAddr`](https://doc.rust-lang.org/std/net/enum.SocketAddr.html "enum std::net::SocketAddr")s. [Read more](https://doc.rust-lang.org/std/net/trait.ToSocketAddrs.html#tymethod.to_socket_addrs)

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#675)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-TryFrom%3C%26ByteStr%3E-for-String)

### impl<'a> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#676)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Utf8Error](https://doc.rust-lang.org/std/str/struct.Utf8Error.html "struct std::str::Utf8Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#679)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.try_from-1)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( s: &'a [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr"), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), <[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<&'a [ByteStr](https://doc.rust-lang.org/std/bstr/struct.ByteStr.html "struct std::bstr::ByteStr")>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#571)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-TryFrom%3CByteString%3E-for-String)

### impl [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#572)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [FromUtf8Error](https://doc.rust-lang.org/std/string/struct.FromUtf8Error.html "struct std::string::FromUtf8Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/alloc/bstr.rs.html#575)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( s: [ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString"), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), <[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[ByteString](https://doc.rust-lang.org/std/bstr/struct.ByteString.html "struct std::bstr::ByteString")>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

1.85.0 · [Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#842)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-TryFrom%3CCString%3E-for-String)

### impl [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString")> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#849)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.try_from-2)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( value: [CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString"), ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), <[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[CString](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString")>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Converts a [`CString`](https://doc.rust-lang.org/std/ffi/struct.CString.html "struct std::ffi::CString") into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") if it contains valid UTF-8 data.

This method is equivalent to [`CString::into_string`](https://doc.rust-lang.org/std/ffi/struct.CString.html#method.into_string "method std::ffi::CString::into_string").

[Source](https://doc.rust-lang.org/src/alloc/ffi/c_str.rs.html#843)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Error-2)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [IntoStringError](https://doc.rust-lang.org/std/ffi/struct.IntoStringError.html "struct std::ffi::IntoStringError")

The type returned in the event of a conversion error.

1.87.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3220)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-TryFrom%3CVec%3Cu8%3E%3E-for-String)

### impl [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>> for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3232)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.try_from-3)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)( bytes: [Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>, ) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String"), <[String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<[Vec](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec")<[u8](https://doc.rust-lang.org/std/primitive.u8.html)>>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Converts the given [`Vec<u8>`](https://doc.rust-lang.org/std/vec/struct.Vec.html "struct std::vec::Vec") into a [`String`](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String") if it contains valid UTF-8 data.

##### [§](https://doc.rust-lang.org/std/string/struct.String.html#examples-127)Examples

```
let s1 = b"hello world".to_vec();
let v1 = String::try_from(s1).unwrap();
assert_eq!(v1, "hello world");
```

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3221)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Error-3)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [FromUtf8Error](https://doc.rust-lang.org/std/string/struct.FromUtf8Error.html "struct std::string::FromUtf8Error")

The type returned in the event of a conversion error.

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3239)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Write-for-String)

### impl [Write](https://doc.rust-lang.org/std/fmt/trait.Write.html "trait std::fmt::Write") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3241)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.write_str)

#### fn [write\_str](https://doc.rust-lang.org/std/fmt/trait.Write.html#tymethod.write_str)(&mut self, s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Writes a string slice into this writer, returning whether the write
succeeded. [Read more](https://doc.rust-lang.org/std/fmt/trait.Write.html#tymethod.write_str)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#3247)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.write_char)

#### fn [write\_char](https://doc.rust-lang.org/std/fmt/trait.Write.html#method.write_char)(&mut self, c: [char](https://doc.rust-lang.org/std/primitive.char.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Writes a [`char`](https://doc.rust-lang.org/std/primitive.char.html "primitive char") into this writer, returning whether the write succeeded. [Read more](https://doc.rust-lang.org/std/fmt/trait.Write.html#method.write_char)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/fmt/mod.rs.html#209)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.write_fmt)

#### fn [write\_fmt](https://doc.rust-lang.org/std/fmt/trait.Write.html#method.write_fmt)(&mut self, args: [Arguments](https://doc.rust-lang.org/std/fmt/struct.Arguments.html "struct std::fmt::Arguments")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Glue for usage of the [`write!`](https://doc.rust-lang.org/std/macro.write.html "macro std::write") macro with implementors of this trait. [Read more](https://doc.rust-lang.org/std/fmt/trait.Write.html#method.write_fmt)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2733)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-DerefPure-for-String)

### impl [DerefPure](https://doc.rust-lang.org/std/ops/trait.DerefPure.html "trait std::ops::DerefPure") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Eq-for-String)

### impl [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

1.0.0 · [Source](https://doc.rust-lang.org/src/alloc/string.rs.html#357)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-StructuralPartialEq-for-String)

### impl [StructuralPartialEq](https://doc.rust-lang.org/std/marker/trait.StructuralPartialEq.html "trait std::marker::StructuralPartialEq") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/string/struct.String.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Freeze-for-String)

### impl [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-RefUnwindSafe-for-String)

### impl [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Send-for-String)

### impl [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Sync-for-String)

### impl [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Unpin-for-String)

### impl [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-UnwindSafe-for-String)

### impl [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

## Blanket Implementations[§](https://doc.rust-lang.org/std/string/struct.String.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.borrow-1)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.borrow_mut-1)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#515)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-CloneToUninit-for-T)

### impl<T> [CloneToUninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html "trait std::clone::CloneToUninit") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#517)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.clone_to_uninit)

#### unsafe fn [clone\_to\_uninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)(&self, dest: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html))

🔬This is a nightly-only experimental API. (`clone_to_uninit` [#126799](https://github.com/rust-lang/rust/issues/126799))

Performs copy-assignment from `self` to `dest`. [Read more](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#785)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-From%3CT%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#788)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.from-16)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: T) -> T

Returns the argument unchanged.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#767-769)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Into%3CU%3E-for-T)

### impl<T, U> [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<U> for T where U: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#777)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.into)

#### fn [into](https://doc.rust-lang.org/std/convert/trait.Into.html#tymethod.into)(self) -> U

Calls `U::from(self)`.

That is, this conversion is whatever the implementation of
`From<T> for U` chooses to do.

[Source](https://doc.rust-lang.org/src/core/ops/deref.rs.html#378-380)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-Receiver-for-P)

### impl<P, T> [Receiver](https://doc.rust-lang.org/std/ops/trait.Receiver.html "trait std::ops::Receiver") for P where P: [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")<Target = T> + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"), T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/ops/deref.rs.html#382)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Target-1)

#### type [Target](https://doc.rust-lang.org/std/ops/trait.Receiver.html#associatedtype.Target) = T

🔬This is a nightly-only experimental API. (`arbitrary_self_types` [#44874](https://github.com/rust-lang/rust/issues/44874))

The target type on which the method may be called.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#85-87)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-ToOwned-for-T)

### impl<T> [ToOwned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html "trait std::borrow::ToOwned") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#89)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Owned)

#### type [Owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#associatedtype.Owned) = T

The resulting type after obtaining ownership.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#90)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.to_owned)

#### fn [to\_owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)(&self) -> T

Creates owned data from borrowed data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#94)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.clone_into)

#### fn [clone\_into](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)(&self, target: [&mut T](https://doc.rust-lang.org/std/primitive.reference.html))

Uses borrowed data to replace owned data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2796)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-ToString-for-T)

### impl<T> [ToString](https://doc.rust-lang.org/std/string/trait.ToString.html "trait std::string::ToString") for T where T: [Display](https://doc.rust-lang.org/std/fmt/trait.Display.html "trait std::fmt::Display") + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2798)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.to_string)

#### fn [to\_string](https://doc.rust-lang.org/std/string/trait.ToString.html#tymethod.to_string)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts the given value to a `String`. [Read more](https://doc.rust-lang.org/std/string/trait.ToString.html#tymethod.to_string)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#827-829)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-TryFrom%3CU%3E-for-T)

### impl<T, U> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U> for T where U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#831)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Error-5)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#834)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.try_from-4)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: U) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, <T as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#811-813)[§](https://doc.rust-lang.org/std/string/struct.String.html#impl-TryInto%3CU%3E-for-T)

### impl<T, U> [TryInto](https://doc.rust-lang.org/std/convert/trait.TryInto.html "trait std::convert::TryInto")<U> for T where U: [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#815)[§](https://doc.rust-lang.org/std/string/struct.String.html#associatedtype.Error-4)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryInto.html#associatedtype.Error) = <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#818)[§](https://doc.rust-lang.org/std/string/struct.String.html#method.try_into)

#### fn [try\_into](https://doc.rust-lang.org/std/convert/trait.TryInto.html#tymethod.try_into)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.