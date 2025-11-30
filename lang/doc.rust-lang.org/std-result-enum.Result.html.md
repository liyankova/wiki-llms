---
url: https://doc.rust-lang.org/std/result/enum.Result.html
title: Result in std::result - Rust
source_domain: doc.rust-lang.org
---

# Result in std::result - Rust

## [Result](https://doc.rust-lang.org/std/result/enum.Result.html)

[std](https://doc.rust-lang.org/std/index.html)::[result](https://doc.rust-lang.org/std/result/index.html)

# Enum Result

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#550)

```
pub enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Expand description

`Result` is a type that represents either success ([`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok")) or failure ([`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err")).

See the [module documentation](https://doc.rust-lang.org/std/result/index.html "mod std::result") for details.

## Variants[§](https://doc.rust-lang.org/std/result/enum.Result.html#variants)

[§](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok)1.0.0

### Ok(T)

Contains the success value

[§](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err)1.0.0

### Err(E)

Contains the error value

## Implementations[§](https://doc.rust-lang.org/std/result/enum.Result.html#implementations)

[Source](https://doc.rust-lang.org/src/core/result.rs.html#566)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Result%3CT,+E%3E)

### impl<T, E> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

1.0.0 (const: 1.48.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#586)

#### pub const fn [is\_ok](https://doc.rust-lang.org/std/result/enum.Result.html#method.is_ok)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the result is [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples)Examples

```
let x: Result<i32, &str> = Ok(-3);
assert_eq!(x.is_ok(), true);

let x: Result<i32, &str> = Err("Some error message");
assert_eq!(x.is_ok(), false);
```

1.70.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#612-616)

#### pub fn [is\_ok\_and](https://doc.rust-lang.org/std/result/enum.Result.html#method.is_ok_and)<F>(self, f: F) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns `true` if the result is [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") and the value inside of it matches a predicate.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-1)Examples

```
let x: Result<u32, &str> = Ok(2);
assert_eq!(x.is_ok_and(|x| x > 1), true);

let x: Result<u32, &str> = Ok(0);
assert_eq!(x.is_ok_and(|x| x > 1), false);

let x: Result<u32, &str> = Err("hey");
assert_eq!(x.is_ok_and(|x| x > 1), false);

let x: Result<String, &str> = Ok("ownership".to_string());
assert_eq!(x.as_ref().is_ok_and(|x| x.len() > 1), true);
println!("still alive {:?}", x);
```

1.0.0 (const: 1.48.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#639)

#### pub const fn [is\_err](https://doc.rust-lang.org/std/result/enum.Result.html#method.is_err)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the result is [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-2)Examples

```
let x: Result<i32, &str> = Ok(-3);
assert_eq!(x.is_err(), false);

let x: Result<i32, &str> = Err("Some error message");
assert_eq!(x.is_err(), true);
```

1.70.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#667-671)

#### pub fn [is\_err\_and](https://doc.rust-lang.org/std/result/enum.Result.html#method.is_err_and)<F>(self, f: F) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html) where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(E) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns `true` if the result is [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") and the value inside of it matches a predicate.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-3)Examples

```
use std::io::{Error, ErrorKind};

let x: Result<u32, Error> = Err(Error::new(ErrorKind::NotFound, "!"));
assert_eq!(x.is_err_and(|x| x.kind() == ErrorKind::NotFound), true);

let x: Result<u32, Error> = Err(Error::new(ErrorKind::PermissionDenied, "!"));
assert_eq!(x.is_err_and(|x| x.kind() == ErrorKind::NotFound), false);

let x: Result<u32, Error> = Ok(123);
assert_eq!(x.is_err_and(|x| x.kind() == ErrorKind::NotFound), false);

let x: Result<u32, String> = Err("ownership".to_string());
assert_eq!(x.as_ref().is_err_and(|x| x.len() > 1), true);
println!("still alive {:?}", x);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#701-704)

#### pub fn [ok](https://doc.rust-lang.org/std/result/enum.Result.html#method.ok)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Converts from `Result<T, E>` to [`Option<T>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option").

Converts `self` into an [`Option<T>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option"), consuming `self`,
and discarding the error, if any.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-4)Examples

```
let x: Result<u32, &str> = Ok(2);
assert_eq!(x.ok(), Some(2));

let x: Result<u32, &str> = Err("Nothing here");
assert_eq!(x.ok(), None);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#729-732)

#### pub fn [err](https://doc.rust-lang.org/std/result/enum.Result.html#method.err)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<E>

Converts from `Result<T, E>` to [`Option<E>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option").

Converts `self` into an [`Option<E>`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option"), consuming `self`,
and discarding the success value, if any.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-5)Examples

```
let x: Result<u32, &str> = Ok(2);
assert_eq!(x.err(), None);

let x: Result<u32, &str> = Err("Nothing here");
assert_eq!(x.err(), Some("Nothing here"));
```

1.0.0 (const: 1.48.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#761)

#### pub const fn [as\_ref](https://doc.rust-lang.org/std/result/enum.Result.html#method.as_ref)(&self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[&T](https://doc.rust-lang.org/std/primitive.reference.html), [&E](https://doc.rust-lang.org/std/primitive.reference.html)>

Converts from `&Result<T, E>` to `Result<&T, &E>`.

Produces a new `Result`, containing a reference
into the original, leaving the original in place.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-6)Examples

```
let x: Result<u32, &str> = Ok(2);
assert_eq!(x.as_ref(), Ok(&2));

let x: Result<u32, &str> = Err("Error");
assert_eq!(x.as_ref(), Err(&"Error"));
```

1.0.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#791)

#### pub const fn [as\_mut](https://doc.rust-lang.org/std/result/enum.Result.html#method.as_mut)(&mut self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html), [&mut E](https://doc.rust-lang.org/std/primitive.reference.html)>

Converts from `&mut Result<T, E>` to `Result<&mut T, &mut E>`.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-7)Examples

```
fn mutate(r: &mut Result<i32, i32>) {
    match r.as_mut() {
        Ok(v) => *v = 42,
        Err(e) => *e = 0,
    }
}

let mut x: Result<i32, i32> = Ok(2);
mutate(&mut x);
assert_eq!(x.unwrap(), 42);

let mut x: Result<i32, i32> = Err(13);
mutate(&mut x);
assert_eq!(x.unwrap_err(), 0);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#824-826)

#### pub fn [map](https://doc.rust-lang.org/std/result/enum.Result.html#method.map)<U, F>(self, op: F) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U,

Maps a `Result<T, E>` to `Result<U, E>` by applying a function to a
contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value, leaving an [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value untouched.

This function can be used to compose the results of two functions.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-8)Examples

Print the numbers on each line of a string multiplied by two.

```
let line = "1\n2\n3\n4\n";

for num in line.lines() {
    match num.parse::<i32>().map(|i| i * 2) {
        Ok(n) => println!("{n}"),
        Err(..) => {}
    }
}
```

1.41.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#856-861)

#### pub fn [map\_or](https://doc.rust-lang.org/std/result/enum.Result.html#method.map_or)<U, F>(self, default: U, f: F) -> U where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U,

Returns the provided default (if [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err")), or
applies a function to the contained value (if [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok")).

Arguments passed to `map_or` are eagerly evaluated; if you are passing
the result of a function call, it is recommended to use [`map_or_else`](https://doc.rust-lang.org/std/result/enum.Result.html#method.map_or_else "method std::result::Result::map_or_else"),
which is lazily evaluated.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-9)Examples

```
let x: Result<_, &str> = Ok("foo");
assert_eq!(x.map_or(42, |v| v.len()), 3);

let x: Result<&str, _> = Err("bar");
assert_eq!(x.map_or(42, |v| v.len()), 42);
```

1.41.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#890-893)

#### pub fn [map\_or\_else](https://doc.rust-lang.org/std/result/enum.Result.html#method.map_or_else)<U, D, F>(self, default: D, f: F) -> U where D: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(E) -> U, F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U,

Maps a `Result<T, E>` to `U` by applying fallback function `default` to
a contained [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value, or function `f` to a contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value.

This function can be used to unpack a successful result
while handling an error.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-10)Examples

```
let k = 21;

let x : Result<_, &str> = Ok("foo");
assert_eq!(x.map_or_else(|e| k * 2, |v| v.len()), 3);

let x : Result<&str, _> = Err("bar");
assert_eq!(x.map_or_else(|e| k * 2, |v| v.len()), 42);
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#921-926)

#### pub const fn [map\_or\_default](https://doc.rust-lang.org/std/result/enum.Result.html#method.map_or_default)<U, F>(self, f: F) -> U where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U, U: [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default"),

🔬This is a nightly-only experimental API. (`result_option_map_or_default` [#138099](https://github.com/rust-lang/rust/issues/138099))

Maps a `Result<T, E>` to a `U` by applying function `f` to the contained
value if the result is [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), otherwise if [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), returns the
[default value](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default "associated function std::default::Default::default") for the type `U`.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-11)Examples

```
#![feature(result_option_map_or_default)]

let x: Result<_, &str> = Ok("foo");
let y: Result<&str, _> = Err("bar");

assert_eq!(x.map_or_default(|x| x.len()), 3);
assert_eq!(y.map_or_default(|y| y.len()), 0);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#955-957)

#### pub fn [map\_err](https://doc.rust-lang.org/std/result/enum.Result.html#method.map_err)<F, O>(self, op: O) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F> where O: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(E) -> F,

Maps a `Result<T, E>` to `Result<T, F>` by applying a function to a
contained [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value, leaving an [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value untouched.

This function can be used to pass through a successful result while handling
an error.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-12)Examples

```
fn stringify(x: u32) -> String { format!("error code: {x}") }

let x: Result<u32, u32> = Ok(2);
assert_eq!(x.map_err(stringify), Ok(2));

let x: Result<u32, u32> = Err(13);
assert_eq!(x.map_err(stringify), Err("error code: 13".to_string()));
```

1.76.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#981-983)

#### pub fn [inspect](https://doc.rust-lang.org/std/result/enum.Result.html#method.inspect)<F>(self, f: F) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")([&T](https://doc.rust-lang.org/std/primitive.reference.html)),

Calls a function with a reference to the contained value if [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok").

Returns the original result.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-13)Examples

```
let x: u8 = "4"
    .parse::<u8>()
    .inspect(|x| println!("original: {x}"))
    .map(|x| x.pow(3))
    .expect("failed to parse number");
```

1.76.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1009-1011)

#### pub fn [inspect\_err](https://doc.rust-lang.org/std/result/enum.Result.html#method.inspect_err)<F>(self, f: F) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")([&E](https://doc.rust-lang.org/std/primitive.reference.html)),

Calls a function with a reference to the contained value if [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err").

Returns the original result.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-14)Examples

```
use std::{fs, io};

fn read() -> io::Result<String> {
    fs::read_to_string("address.txt")
        .inspect_err(|e| eprintln!("failed to read file: {e}"))
}
```

1.47.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1039-1041)

#### pub fn [as\_deref](https://doc.rust-lang.org/std/result/enum.Result.html#method.as_deref)(&self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<&<T as [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")>::[Target](https://doc.rust-lang.org/std/ops/trait.Deref.html#associatedtype.Target "type std::ops::Deref::Target"), [&E](https://doc.rust-lang.org/std/primitive.reference.html)> where T: [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref"),

Converts from `Result<T, E>` (or `&Result<T, E>`) to `Result<&<T as Deref>::Target, &E>`.

Coerces the [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") variant of the original [`Result`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result") via [`Deref`](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")
and returns the new [`Result`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-15)Examples

```
let x: Result<String, u32> = Ok("hello".to_string());
let y: Result<&str, &u32> = Ok("hello");
assert_eq!(x.as_deref(), y);

let x: Result<String, u32> = Err(42);
let y: Result<&str, &u32> = Err(&42);
assert_eq!(x.as_deref(), y);
```

1.47.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1067-1069)

#### pub fn [as\_deref\_mut](https://doc.rust-lang.org/std/result/enum.Result.html#method.as_deref_mut)(&mut self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<&mut <T as [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")>::[Target](https://doc.rust-lang.org/std/ops/trait.Deref.html#associatedtype.Target "type std::ops::Deref::Target"), [&mut E](https://doc.rust-lang.org/std/primitive.reference.html)> where T: [DerefMut](https://doc.rust-lang.org/std/ops/trait.DerefMut.html "trait std::ops::DerefMut"),

Converts from `Result<T, E>` (or `&mut Result<T, E>`) to `Result<&mut <T as DerefMut>::Target, &mut E>`.

Coerces the [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") variant of the original [`Result`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result") via [`DerefMut`](https://doc.rust-lang.org/std/ops/trait.DerefMut.html "trait std::ops::DerefMut")
and returns the new [`Result`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-16)Examples

```
let mut s = "HELLO".to_string();
let mut x: Result<String, u32> = Ok("hello".to_string());
let y: Result<&mut str, &mut u32> = Ok(&mut s);
assert_eq!(x.as_deref_mut().map(|x| { x.make_ascii_uppercase(); x }), y);

let mut i = 42;
let mut x: Result<String, u32> = Err(42);
let y: Result<&mut str, &mut u32> = Err(&mut i);
assert_eq!(x.as_deref_mut().map(|x| { x.make_ascii_uppercase(); x }), y);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1094)

#### pub fn [iter](https://doc.rust-lang.org/std/result/enum.Result.html#method.iter)(&self) -> [Iter](https://doc.rust-lang.org/std/result/struct.Iter.html "struct std::result::Iter")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html)

Returns an iterator over the possibly contained value.

The iterator yields one value if the result is [`Result::Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), otherwise none.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-17)Examples

```
let x: Result<u32, &str> = Ok(7);
assert_eq!(x.iter().next(), Some(&7));

let x: Result<u32, &str> = Err("nothing!");
assert_eq!(x.iter().next(), None);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1118)

#### pub fn [iter\_mut](https://doc.rust-lang.org/std/result/enum.Result.html#method.iter_mut)(&mut self) -> [IterMut](https://doc.rust-lang.org/std/result/struct.IterMut.html "struct std::result::IterMut")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html)

Returns a mutable iterator over the possibly contained value.

The iterator yields one value if the result is [`Result::Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), otherwise none.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-18)Examples

```
let mut x: Result<u32, &str> = Ok(7);
match x.iter_mut().next() {
    Some(v) => *v = 40,
    None => {},
}
assert_eq!(x, Ok(40));

let mut x: Result<u32, &str> = Err("nothing!");
assert_eq!(x.iter_mut().next(), None);
```

1.4.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1172-1174)

#### pub fn [expect](https://doc.rust-lang.org/std/result/enum.Result.html#method.expect)(self, msg: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> T where E: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"),

Returns the contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value, consuming the `self` value.

Because this function may panic, its use is generally discouraged.
Instead, prefer to use pattern matching and handle the [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err")
case explicitly, or call [`unwrap_or`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or "method std::result::Result::unwrap_or"), [`unwrap_or_else`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or_else "method std::result::Result::unwrap_or_else"), or
[`unwrap_or_default`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or_default "method std::result::Result::unwrap_or_default").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#panics)Panics

Panics if the value is an [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), with a panic message including the
passed message, and the content of the [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-19)Examples

[ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html "This example panics")

```
let x: Result<u32, &str> = Err("emergency failure");
x.expect("Testing expect"); // panics with `Testing expect: emergency failure`
```

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#recommended-message-style)Recommended Message Style

We recommend that `expect` messages are used to describe the reason you
*expect* the `Result` should be `Ok`.

[ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html "This example panics")

```
let path = std::env::var("IMPORTANT_PATH")
    .expect("env variable `IMPORTANT_PATH` should be set by `wrapper_script.sh`");
```

**Hint**: If you’re having trouble remembering how to phrase expect
error messages remember to focus on the word “should” as in “env
variable should be set by blah” or “the given binary should be available
and executable by the current user”.

For more detail on expect message styles and the reasoning behind our recommendation please
refer to the section on [“Common Message
Styles”](https://doc.rust-lang.org/std/error/index.html#common-message-styles) in the
[`std::error`](https://doc.rust-lang.org/std/error/index.html) module docs.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1220-1222)

#### pub fn [unwrap](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap)(self) -> T where E: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"),

Returns the contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value, consuming the `self` value.

Because this function may panic, its use is generally discouraged.
Panics are meant for unrecoverable errors, and
[may abort the entire program](https://doc.rust-lang.org/book/ch09-01-unrecoverable-errors-with-panic.html).

Instead, prefer to use [the `?` (try) operator](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html#a-shortcut-for-propagating-errors-the--operator), or pattern matching
to handle the [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") case explicitly, or call [`unwrap_or`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or "method std::result::Result::unwrap_or"),
[`unwrap_or_else`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or_else "method std::result::Result::unwrap_or_else"), or [`unwrap_or_default`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or_default "method std::result::Result::unwrap_or_default").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#panics-1)Panics

Panics if the value is an [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), with a panic message provided by the
[`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err")’s value.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-20)Examples

Basic usage:

```
let x: Result<u32, &str> = Ok(2);
assert_eq!(x.unwrap(), 2);
```

[ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html "This example panics")

```
let x: Result<u32, &str> = Err("emergency failure");
x.unwrap(); // panics with `emergency failure`
```

1.16.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1258-1261)

#### pub fn [unwrap\_or\_default](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or_default)(self) -> T where T: [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default"),

Returns the contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value or a default

Consumes the `self` argument then, if [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), returns the contained
value, otherwise if [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), returns the default value for that
type.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-21)Examples

Converts a string to an integer, turning poorly-formed strings
into 0 (the default value for integers). [`parse`](https://doc.rust-lang.org/std/primitive.str.html#method.parse "method str::parse") converts
a string to any other type that implements [`FromStr`](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr"), returning an
[`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") on error.

```
let good_year_from_input = "1909";
let bad_year_from_input = "190blarg";
let good_year = good_year_from_input.parse().unwrap_or_default();
let bad_year = bad_year_from_input.parse().unwrap_or_default();

assert_eq!(1909, good_year);
assert_eq!(0, bad_year);
```

1.17.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1286-1288)

#### pub fn [expect\_err](https://doc.rust-lang.org/std/result/enum.Result.html#method.expect_err)(self, msg: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> E where T: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"),

Returns the contained [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value, consuming the `self` value.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#panics-2)Panics

Panics if the value is an [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), with a panic message including the
passed message, and the content of the [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-22)Examples

[ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html "This example panics")

```
let x: Result<u32, &str> = Ok(10);
x.expect_err("Testing expect_err"); // panics with `Testing expect_err: 10`
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1317-1319)

#### pub fn [unwrap\_err](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_err)(self) -> E where T: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"),

Returns the contained [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value, consuming the `self` value.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#panics-3)Panics

Panics if the value is an [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), with a custom panic message provided
by the [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok")’s value.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-23)Examples

[ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html "This example panics")

```
let x: Result<u32, &str> = Ok(2);
x.unwrap_err(); // panics with `2`
```

```
let x: Result<u32, &str> = Err("emergency failure");
assert_eq!(x.unwrap_err(), "emergency failure");
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1354-1356)

#### pub const fn [into\_ok](https://doc.rust-lang.org/std/result/enum.Result.html#method.into_ok)(self) -> T where E: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<[!](https://doc.rust-lang.org/std/primitive.never.html)>,

🔬This is a nightly-only experimental API. (`unwrap_infallible` [#61695](https://github.com/rust-lang/rust/issues/61695))

Returns the contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value, but never panics.

Unlike [`unwrap`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap "method std::result::Result::unwrap"), this method is known to never panic on the
result types it is implemented for. Therefore, it can be used
instead of `unwrap` as a maintainability safeguard that will fail
to compile if the error type of the `Result` is later changed
to an error that can actually occur.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-24)Examples

```
fn only_good_news() -> Result<String, !> {
    Ok("this is fine".into())
}

let s: String = only_good_news().into_ok();
println!("{s}");
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1391-1393)

#### pub const fn [into\_err](https://doc.rust-lang.org/std/result/enum.Result.html#method.into_err)(self) -> E where T: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<[!](https://doc.rust-lang.org/std/primitive.never.html)>,

🔬This is a nightly-only experimental API. (`unwrap_infallible` [#61695](https://github.com/rust-lang/rust/issues/61695))

Returns the contained [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value, but never panics.

Unlike [`unwrap_err`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_err "method std::result::Result::unwrap_err"), this method is known to never panic on the
result types it is implemented for. Therefore, it can be used
instead of `unwrap_err` as a maintainability safeguard that will fail
to compile if the ok type of the `Result` is later changed
to a type that can actually occur.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-25)Examples

```
fn only_bad_news() -> Result<!, String> {
    Err("Oops, it failed".into())
}

let error: String = only_bad_news().into_err();
println!("{error}");
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1435-1439)

#### pub fn [and](https://doc.rust-lang.org/std/result/enum.Result.html#method.and)<U>(self, res: [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E>

Returns `res` if the result is [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), otherwise returns the [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value of `self`.

Arguments passed to `and` are eagerly evaluated; if you are passing the
result of a function call, it is recommended to use [`and_then`](https://doc.rust-lang.org/std/result/enum.Result.html#method.and_then "method std::result::Result::and_then"), which is
lazily evaluated.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-26)Examples

```
let x: Result<u32, &str> = Ok(2);
let y: Result<&str, &str> = Err("late error");
assert_eq!(x.and(y), Err("late error"));

let x: Result<u32, &str> = Err("early error");
let y: Result<&str, &str> = Ok("foo");
assert_eq!(x.and(y), Err("early error"));

let x: Result<u32, &str> = Err("not a 2");
let y: Result<&str, &str> = Err("late error");
assert_eq!(x.and(y), Err("not a 2"));

let x: Result<u32, &str> = Ok(2);
let y: Result<&str, &str> = Ok("different result type");
assert_eq!(x.and(y), Ok("different result type"));
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1481-1483)

#### pub fn [and\_then](https://doc.rust-lang.org/std/result/enum.Result.html#method.and_then)<U, F>(self, op: F) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E>,

Calls `op` if the result is [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), otherwise returns the [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value of `self`.

This function can be used for control flow based on `Result` values.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-27)Examples

```
fn sq_then_to_string(x: u32) -> Result<String, &'static str> {
    x.checked_mul(x).map(|sq| sq.to_string()).ok_or("overflowed")
}

assert_eq!(Ok(2).and_then(sq_then_to_string), Ok(4.to_string()));
assert_eq!(Ok(1_000_000).and_then(sq_then_to_string), Err("overflowed"));
assert_eq!(Err("not a number").and_then(sq_then_to_string), Err("not a number"));
```

Often used to chain fallible operations that may return [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err").

```
use std::{io::ErrorKind, path::Path};

// Note: on Windows "/" maps to "C:\"
let root_modified_time = Path::new("/").metadata().and_then(|md| md.modified());
assert!(root_modified_time.is_ok());

let should_fail = Path::new("/bad/path").metadata().and_then(|md| md.modified());
assert!(should_fail.is_err());
assert_eq!(should_fail.unwrap_err().kind(), ErrorKind::NotFound);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1521-1525)

#### pub fn [or](https://doc.rust-lang.org/std/result/enum.Result.html#method.or)<F>(self, res: [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>

Returns `res` if the result is [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), otherwise returns the [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value of `self`.

Arguments passed to `or` are eagerly evaluated; if you are passing the
result of a function call, it is recommended to use [`or_else`](https://doc.rust-lang.org/std/result/enum.Result.html#method.or_else "method std::result::Result::or_else"), which is
lazily evaluated.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-28)Examples

```
let x: Result<u32, &str> = Ok(2);
let y: Result<u32, &str> = Err("late error");
assert_eq!(x.or(y), Ok(2));

let x: Result<u32, &str> = Err("early error");
let y: Result<u32, &str> = Ok(2);
assert_eq!(x.or(y), Ok(2));

let x: Result<u32, &str> = Err("not a 2");
let y: Result<u32, &str> = Err("late error");
assert_eq!(x.or(y), Err("late error"));

let x: Result<u32, &str> = Ok(2);
let y: Result<u32, &str> = Ok(100);
assert_eq!(x.or(y), Ok(2));
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1552-1554)

#### pub fn [or\_else](https://doc.rust-lang.org/std/result/enum.Result.html#method.or_else)<F, O>(self, op: O) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F> where O: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(E) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>,

Calls `op` if the result is [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), otherwise returns the [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value of `self`.

This function can be used for control flow based on result values.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-29)Examples

```
fn sq(x: u32) -> Result<u32, u32> { Ok(x * x) }
fn err(x: u32) -> Result<u32, u32> { Err(x) }

assert_eq!(Ok(2).or_else(sq).or_else(sq), Ok(2));
assert_eq!(Ok(2).or_else(err).or_else(sq), Ok(2));
assert_eq!(Err(3).or_else(sq).or_else(err), Ok(9));
assert_eq!(Err(3).or_else(err).or_else(err), Err(3));
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1583-1586)

#### pub fn [unwrap\_or](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or)(self, default: T) -> T

Returns the contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value or a provided default.

Arguments passed to `unwrap_or` are eagerly evaluated; if you are passing
the result of a function call, it is recommended to use [`unwrap_or_else`](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or_else "method std::result::Result::unwrap_or_else"),
which is lazily evaluated.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-30)Examples

```
let default = 2;
let x: Result<u32, &str> = Ok(9);
assert_eq!(x.unwrap_or(default), 9);

let x: Result<u32, &str> = Err("error");
assert_eq!(x.unwrap_or(default), default);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/144211 "Tracking issue for const_result_trait_fn")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1609-1611)

#### pub fn [unwrap\_or\_else](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_or_else)<F>(self, op: F) -> T where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(E) -> T,

Returns the contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value or computes it from a closure.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-31)Examples

```
fn count(x: &str) -> usize { x.len() }

assert_eq!(Ok(2).unwrap_or_else(count), 2);
assert_eq!(Err("foo").unwrap_or_else(count), 3);
```

1.58.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1642)

#### pub unsafe fn [unwrap\_unchecked](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_unchecked)(self) -> T

Returns the contained [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") value, consuming the `self` value,
without checking that the value is not an [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#safety)Safety

Calling this method on an [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-32)Examples

```
let x: Result<u32, &str> = Ok(2);
assert_eq!(unsafe { x.unwrap_unchecked() }, 2);
```

```
let x: Result<u32, &str> = Err("emergency failure");
unsafe { x.unwrap_unchecked() }; // Undefined behavior!
```

1.58.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1673)

#### pub unsafe fn [unwrap\_err\_unchecked](https://doc.rust-lang.org/std/result/enum.Result.html#method.unwrap_err_unchecked)(self) -> E

Returns the contained [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") value, consuming the `self` value,
without checking that the value is not an [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok").

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#safety-1)Safety

Calling this method on an [`Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-33)Examples

```
let x: Result<u32, &str> = Ok(2);
unsafe { x.unwrap_err_unchecked() }; // Undefined behavior!
```

```
let x: Result<u32, &str> = Err("emergency failure");
assert_eq!(unsafe { x.unwrap_err_unchecked() }, "emergency failure");
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1682)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Result%3C%26T,+E%3E)

### impl<T, E> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[&T](https://doc.rust-lang.org/std/primitive.reference.html), E>

1.59.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1699-1701)

#### pub const fn [copied](https://doc.rust-lang.org/std/result/enum.Result.html#method.copied)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

Maps a `Result<&T, E>` to a `Result<T, E>` by copying the contents of the
`Ok` part.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-34)Examples

```
let val = 12;
let x: Result<&i32, i32> = Ok(&val);
assert_eq!(x, Ok(&12));
let copied = x.copied();
assert_eq!(copied, Ok(12));
```

1.59.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1725-1727)

#### pub fn [cloned](https://doc.rust-lang.org/std/result/enum.Result.html#method.cloned)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Maps a `Result<&T, E>` to a `Result<T, E>` by cloning the contents of the
`Ok` part.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-35)Examples

```
let val = 12;
let x: Result<&i32, i32> = Ok(&val);
assert_eq!(x, Ok(&12));
let cloned = x.cloned();
assert_eq!(cloned, Ok(12));
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1733)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Result%3C%26mut+T,+E%3E)

### impl<T, E> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html), E>

1.59.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1750-1752)

#### pub const fn [copied](https://doc.rust-lang.org/std/result/enum.Result.html#method.copied-1)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

Maps a `Result<&mut T, E>` to a `Result<T, E>` by copying the contents of the
`Ok` part.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-36)Examples

```
let mut val = 12;
let x: Result<&mut i32, i32> = Ok(&mut val);
assert_eq!(x, Ok(&mut 12));
let copied = x.copied();
assert_eq!(copied, Ok(12));
```

1.59.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1776-1778)

#### pub fn [cloned](https://doc.rust-lang.org/std/result/enum.Result.html#method.cloned-1)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Maps a `Result<&mut T, E>` to a `Result<T, E>` by cloning the contents of the
`Ok` part.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-37)Examples

```
let mut val = 12;
let x: Result<&mut i32, i32> = Ok(&mut val);
assert_eq!(x, Ok(&mut 12));
let cloned = x.cloned();
assert_eq!(cloned, Ok(12));
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1784)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Result%3COption%3CT%3E,+E%3E)

### impl<T, E> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>, E>

1.33.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1804)

#### pub const fn [transpose](https://doc.rust-lang.org/std/result/enum.Result.html#method.transpose)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>>

Transposes a `Result` of an `Option` into an `Option` of a `Result`.

`Ok(None)` will be mapped to `None`.
`Ok(Some(_))` and `Err(_)` will be mapped to `Some(Ok(_))` and `Some(Err(_))`.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-38)Examples

```
#[derive(Debug, Eq, PartialEq)]
struct SomeErr;

let x: Result<Option<i32>, SomeErr> = Ok(Some(5));
let y: Option<Result<i32, SomeErr>> = Some(Ok(5));
assert_eq!(x.transpose(), y);
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1813)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Result%3CResult%3CT,+E%3E,+E%3E)

### impl<T, E> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>, E>

1.89.0 (const: 1.89.0) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1840)

#### pub const fn [flatten](https://doc.rust-lang.org/std/result/enum.Result.html#method.flatten)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

Converts from `Result<Result<T, E>, E>` to `Result<T, E>`

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-39)Examples

```
let x: Result<Result<&'static str, u32>, u32> = Ok(Ok("hello"));
assert_eq!(Ok("hello"), x.flatten());

let x: Result<Result<&'static str, u32>, u32> = Ok(Err(6));
assert_eq!(Err(6), x.flatten());

let x: Result<Result<&'static str, u32>, u32> = Err(6);
assert_eq!(Err(6), x.flatten());
```

Flattening only removes one level of nesting at a time:

```
let x: Result<Result<Result<&'static str, u32>, u32>, u32> = Ok(Ok(Ok("hello")));
assert_eq!(Ok(Ok("hello")), x.flatten());
assert_eq!(Ok("hello"), x.flatten().flatten());
```

## Trait Implementations[§](https://doc.rust-lang.org/std/result/enum.Result.html#trait-implementations)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1875-1878)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Clone-for-Result%3CT,+E%3E)

### impl<T, E> [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"), E: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1881)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.clone)

#### fn [clone](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)(&self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

Returns a duplicate of the value. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1889)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.clone_from)

#### fn [clone\_from](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)(&mut self, source: &[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>)

Performs copy-assignment from `source`. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#545)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Debug-for-Result%3CT,+E%3E)

### impl<T, E> [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"), E: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"),

[Source](https://doc.rust-lang.org/src/core/result.rs.html#545)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#2099)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-FromIterator%3CResult%3CA,+E%3E%3E-for-Result%3CV,+E%3E)

### impl<A, E, V> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<A, E>> for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<V, E> where V: [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<A>,

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2143)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.from_iter)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<V, E> where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<A, E>>,

Takes each element in the `Iterator`: if it is an `Err`, no further
elements are taken, and the `Err` is returned. Should no `Err` occur, a
container with the values of each `Result` is returned.

Here is an example which increments every integer in a vector,
checking for overflow:

```
let v = vec![1, 2];
let res: Result<Vec<u32>, &'static str> = v.iter().map(|x: &u32|
    x.checked_add(1).ok_or("Overflow!")
).collect();
assert_eq!(res, Ok(vec![2, 3]));
```

Here is another example that tries to subtract one from another list
of integers, this time checking for underflow:

```
let v = vec![1, 2, 0];
let res: Result<Vec<u32>, &'static str> = v.iter().map(|x: &u32|
    x.checked_sub(1).ok_or("Underflow!")
).collect();
assert_eq!(res, Err("Underflow!"));
```

Here is a variation on the previous example, showing that no
further elements are taken from `iter` after the first `Err`.

```
let v = vec![3, 2, 1, 10];
let mut shared = 0;
let res: Result<Vec<u32>, &'static str> = v.iter().map(|x: &u32| {
    shared += x;
    x.checked_sub(2).ok_or("Underflow!")
}).collect();
assert_eq!(res, Err("Underflow!"));
assert_eq!(shared, 6);
```

Since the third element caused an underflow, no further elements were taken,
so the final value of `shared` is 6 (= `3 + 2 + 1`), not 16.

[Source](https://doc.rust-lang.org/src/core/task/poll.rs.html#285-286)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-FromResidual%3CResult%3CInfallible,+E%3E%3E-for-Poll%3COption%3CResult%3CT,+F%3E%3E%3E)

### impl<T, E, F> [FromResidual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html "trait std::ops::FromResidual")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>> for [Poll](https://doc.rust-lang.org/std/task/enum.Poll.html "enum std::task::Poll")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>>> where F: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<E>,

[Source](https://doc.rust-lang.org/src/core/task/poll.rs.html#289)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.from_residual-3)

#### fn [from\_residual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)(x: [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>) -> [Poll](https://doc.rust-lang.org/std/task/enum.Poll.html "enum std::task::Poll")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>>>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from a compatible `Residual` type. [Read more](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)

[Source](https://doc.rust-lang.org/src/core/task/poll.rs.html#254)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-FromResidual%3CResult%3CInfallible,+E%3E%3E-for-Poll%3CResult%3CT,+F%3E%3E)

### impl<T, E, F> [FromResidual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html "trait std::ops::FromResidual")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>> for [Poll](https://doc.rust-lang.org/std/task/enum.Poll.html "enum std::task::Poll")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>> where F: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<E>,

[Source](https://doc.rust-lang.org/src/core/task/poll.rs.html#256)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.from_residual-2)

#### fn [from\_residual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)(x: [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>) -> [Poll](https://doc.rust-lang.org/std/task/enum.Poll.html "enum std::task::Poll")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from a compatible `Residual` type. [Read more](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2170-2171)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-FromResidual%3CResult%3CInfallible,+E%3E%3E-for-Result%3CT,+F%3E)

### impl<T, E, F> [FromResidual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html "trait std::ops::FromResidual")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>> for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F> where F: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<E>,

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2175)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.from_residual)

#### fn [from\_residual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)(residual: [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from a compatible `Residual` type. [Read more](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2184)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-FromResidual%3CYeet%3CE%3E%3E-for-Result%3CT,+F%3E)

### impl<T, E, F> [FromResidual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html "trait std::ops::FromResidual")<[Yeet](https://doc.rust-lang.org/std/ops/struct.Yeet.html "struct std::ops::Yeet")<E>> for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F> where F: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<E>,

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2186)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.from_residual-1)

#### fn [from\_residual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)(\_: [Yeet](https://doc.rust-lang.org/std/ops/struct.Yeet.html "struct std::ops::Yeet")<E>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, F>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from a compatible `Residual` type. [Read more](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#545)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Hash-for-Result%3CT,+E%3E)

### impl<T, E> [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash"), E: [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash"),

[Source](https://doc.rust-lang.org/src/core/result.rs.html#545)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.hash)

#### fn [hash](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)<\_\_H>(&self, state: [&mut \_\_H](https://doc.rust-lang.org/std/primitive.reference.html)) where \_\_H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"),

Feeds this value into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)

1.3.0 · [Source](https://doc.rust-lang.org/src/core/hash/mod.rs.html#235-237)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.hash_slice)

#### fn [hash\_slice](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)<H>(data: &[Self], state: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"), Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Feeds a slice of this type into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)

1.4.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1933)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-IntoIterator-for-%26Result%3CT,+E%3E)

### impl<'a, T, E> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for &'a [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1934)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Item-1)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = [&'a T](https://doc.rust-lang.org/std/primitive.reference.html)

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1935)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.IntoIter-1)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [Iter](https://doc.rust-lang.org/std/result/struct.Iter.html "struct std::result::Iter")<'a, T>

Which kind of iterator are we turning this into?

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1937)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.into_iter-1)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> [Iter](https://doc.rust-lang.org/std/result/struct.Iter.html "struct std::result::Iter")<'a, T> [ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html)

Creates an iterator from a value. [Read more](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)

1.4.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1943)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-IntoIterator-for-%26mut+Result%3CT,+E%3E)

### impl<'a, T, E> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for &'a mut [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1944)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Item-2)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = [&'a mut T](https://doc.rust-lang.org/std/primitive.reference.html)

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1945)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.IntoIter-2)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [IterMut](https://doc.rust-lang.org/std/result/struct.IterMut.html "struct std::result::IterMut")<'a, T>

Which kind of iterator are we turning this into?

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1947)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.into_iter-2)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> [IterMut](https://doc.rust-lang.org/std/result/struct.IterMut.html "struct std::result::IterMut")<'a, T> [ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html)

Creates an iterator from a value. [Read more](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#1907)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-IntoIterator-for-Result%3CT,+E%3E)

### impl<T, E> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1927)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.into_iter)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> [IntoIter](https://doc.rust-lang.org/std/result/struct.IntoIter.html "struct std::result::IntoIter")<T> [ⓘ](https://doc.rust-lang.org/std/result/enum.Result.html)

Returns a consuming iterator over the possibly contained value.

The iterator yields one value if the result is [`Result::Ok`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok"), otherwise none.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-40)Examples

```
let x: Result<u32, &str> = Ok(5);
let v: Vec<u32> = x.into_iter().collect();
assert_eq!(v, [5]);

let x: Result<u32, &str> = Err("nothing!");
let v: Vec<u32> = x.into_iter().collect();
assert_eq!(v, []);
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1908)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Item)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = T

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1909)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.IntoIter)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [IntoIter](https://doc.rust-lang.org/std/result/struct.IntoIter.html "struct std::result::IntoIter")<T>

Which kind of iterator are we turning this into?

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/118304 "Tracking issue for derive_const")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Ord-for-Result%3CT,+E%3E)

### impl<T, E> [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"), E: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

[Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.cmp)

#### fn [cmp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)(&self, other: &[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")

This method returns an [`Ordering`](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering") between `self` and `other`. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1023-1025)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.max)

#### fn [max](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the maximum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1062-1064)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.min)

#### fn [min](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the minimum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)

1.50.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1088-1090)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.clamp)

#### fn [clamp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)(self, min: Self, max: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Restrict a value to a certain interval. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/118304 "Tracking issue for derive_const")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-PartialEq-for-Result%3CT,+E%3E)

### impl<T, E> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"), E: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

[Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.eq)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.ne)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/118304 "Tracking issue for derive_const")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-PartialOrd-for-Result%3CT,+E%3E)

### impl<T, E> [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd"), E: [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd"),

[Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.partial_cmp)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.lt)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.le)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.gt)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.ge)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.16.0 · [Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#240-242)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Product%3CResult%3CU,+E%3E%3E-for-Result%3CT,+E%3E)

### impl<T, U, E> [Product](https://doc.rust-lang.org/std/iter/trait.Product.html "trait std::iter::Product")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E>> for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Product](https://doc.rust-lang.org/std/iter/trait.Product.html "trait std::iter::Product")<U>,

[Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#261-263)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.product)

#### fn [product](https://doc.rust-lang.org/std/iter/trait.Product.html#tymethod.product)<I>(iter: I) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where I: [Iterator](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator")<Item = [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E>>,

Takes each element in the [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator"): if it is an [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), no further
elements are taken, and the [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") is returned. Should no [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err")
occur, the product of all elements is returned.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-42)Examples

This multiplies each number in a vector of strings,
if a string could not be parsed the operation returns `Err`:

```
let nums = vec!["5", "10", "1", "2"];
let total: Result<usize, _> = nums.iter().map(|w| w.parse::<usize>()).product();
assert_eq!(total, Ok(100));
let nums = vec!["5", "10", "one", "2"];
let total: Result<usize, _> = nums.iter().map(|w| w.parse::<usize>()).product();
assert!(total.is_err());
```

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2193)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Residual%3CT%3E-for-Result%3CInfallible,+E%3E)

### impl<T, E> [Residual](https://doc.rust-lang.org/std/ops/trait.Residual.html "trait std::ops::Residual")<T> for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2194)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.TryType)

#### type [TryType](https://doc.rust-lang.org/std/ops/trait.Residual.html#associatedtype.TryType) = [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

🔬This is a nightly-only experimental API. (`try_trait_v2_residual` [#91285](https://github.com/rust-lang/rust/issues/91285))

The “return” type of this meta-function.

1.16.0 · [Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#209-211)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Sum%3CResult%3CU,+E%3E%3E-for-Result%3CT,+E%3E)

### impl<T, U, E> [Sum](https://doc.rust-lang.org/std/iter/trait.Sum.html "trait std::iter::Sum")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E>> for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Sum](https://doc.rust-lang.org/std/iter/trait.Sum.html "trait std::iter::Sum")<U>,

[Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#231-233)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.sum)

#### fn [sum](https://doc.rust-lang.org/std/iter/trait.Sum.html#tymethod.sum)<I>(iter: I) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where I: [Iterator](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator")<Item = [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, E>>,

Takes each element in the [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator"): if it is an [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err"), no further
elements are taken, and the [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err") is returned. Should no [`Err`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err")
occur, the sum of all elements is returned.

##### [§](https://doc.rust-lang.org/std/result/enum.Result.html#examples-41)Examples

This sums up every integer in a vector, rejecting the sum if a negative
element is encountered:

```
let f = |&x: &i32| if x < 0 { Err("Negative element found") } else { Ok(x) };
let v = vec![1, 2];
let res: Result<i32, _> = v.iter().map(f).sum();
assert_eq!(res, Ok(3));
let v = vec![1, -2];
let res: Result<i32, _> = v.iter().map(f).sum();
assert_eq!(res, Err("Negative element found"));
```

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2576-2586)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Termination-for-Result%3CT,+E%3E)

### impl<T: [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination"), E: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug")> [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

[Source](https://doc.rust-lang.org/src/std/process.rs.html#2577-2585)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.report)

#### fn [report](https://doc.rust-lang.org/std/process/trait.Termination.html#tymethod.report)(self) -> [ExitCode](https://doc.rust-lang.org/std/process/struct.ExitCode.html "struct std::process::ExitCode")

Is called to get the representation of the value as status code.
This status code is returned to the operating system.

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2150)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Try-for-Result%3CT,+E%3E)

### impl<T, E> [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2151)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Output)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Output) = T

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

The type of the value produced by `?` when *not* short-circuiting.

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2152)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Residual)

#### type [Residual](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Residual) = [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible"), E>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

The type of the value passed to [`FromResidual::from_residual`](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual "associated function std::ops::FromResidual::from_residual")
as part of `?` when short-circuiting. [Read more](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Residual)

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2155)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.from_output)

#### fn [from\_output](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.from_output)(output: <[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> as [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try")>::[Output](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Output "type std::ops::Try::Output")) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from its `Output` type. [Read more](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.from_output)

[Source](https://doc.rust-lang.org/src/core/result.rs.html#2160)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.branch)

#### fn [branch](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.branch)( self, ) -> [ControlFlow](https://doc.rust-lang.org/std/ops/enum.ControlFlow.html "enum std::ops::ControlFlow")<<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> as [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try")>::[Residual](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Residual "type std::ops::Try::Residual"), <[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> as [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try")>::[Output](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Output "type std::ops::Try::Output")>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Used in `?` to decide whether the operator should produce a value
(because this returned [`ControlFlow::Continue`](https://doc.rust-lang.org/std/ops/enum.ControlFlow.html#variant.Continue "variant std::ops::ControlFlow::Continue"))
or propagate a value back to the caller
(because this returned [`ControlFlow::Break`](https://doc.rust-lang.org/std/ops/enum.ControlFlow.html#variant.Break "variant std::ops::ControlFlow::Break")). [Read more](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.branch)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#545)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Copy-for-Result%3CT,+E%3E)

### impl<T, E> [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"), E: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/118304 "Tracking issue for derive_const")) · [Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Eq-for-Result%3CT,+E%3E)

### impl<T, E> [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq"), E: [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq"),

1.0.0 · [Source](https://doc.rust-lang.org/src/core/result.rs.html#546)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-StructuralPartialEq-for-Result%3CT,+E%3E)

### impl<T, E> [StructuralPartialEq](https://doc.rust-lang.org/std/marker/trait.StructuralPartialEq.html "trait std::marker::StructuralPartialEq") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

[Source](https://doc.rust-lang.org/src/core/result.rs.html#1899-1902)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-UseCloned-for-Result%3CT,+E%3E)

### impl<T, E> [UseCloned](https://doc.rust-lang.org/std/clone/trait.UseCloned.html "trait std::clone::UseCloned") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [UseCloned](https://doc.rust-lang.org/std/clone/trait.UseCloned.html "trait std::clone::UseCloned"), E: [UseCloned](https://doc.rust-lang.org/std/clone/trait.UseCloned.html "trait std::clone::UseCloned"),

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/result/enum.Result.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Freeze-for-Result%3CT,+E%3E)

### impl<T, E> [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze"), E: [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze"),

[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-RefUnwindSafe-for-Result%3CT,+E%3E)

### impl<T, E> [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe"), E: [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe"),

[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Send-for-Result%3CT,+E%3E)

### impl<T, E> [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send"), E: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send"),

[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Sync-for-Result%3CT,+E%3E)

### impl<T, E> [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync"), E: [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync"),

[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Unpin-for-Result%3CT,+E%3E)

### impl<T, E> [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin"), E: [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin"),

[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-UnwindSafe-for-Result%3CT,+E%3E)

### impl<T, E> [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where T: [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe"), E: [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe"),

## Blanket Implementations[§](https://doc.rust-lang.org/std/result/enum.Result.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#515)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-CloneToUninit-for-T)

### impl<T> [CloneToUninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html "trait std::clone::CloneToUninit") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#517)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.clone_to_uninit)

#### unsafe fn [clone\_to\_uninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)(&self, dest: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html))

🔬This is a nightly-only experimental API. (`clone_to_uninit` [#126799](https://github.com/rust-lang/rust/issues/126799))

Performs copy-assignment from `self` to `dest`. [Read more](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#785)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-From%3CT%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#788)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: T) -> T

Returns the argument unchanged.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#767-769)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-Into%3CU%3E-for-T)

### impl<T, U> [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<U> for T where U: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#777)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.into)

#### fn [into](https://doc.rust-lang.org/std/convert/trait.Into.html#tymethod.into)(self) -> U

Calls `U::from(self)`.

That is, this conversion is whatever the implementation of
`From<T> for U` chooses to do.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#85-87)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-ToOwned-for-T)

### impl<T> [ToOwned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html "trait std::borrow::ToOwned") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#89)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Owned)

#### type [Owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#associatedtype.Owned) = T

The resulting type after obtaining ownership.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#90)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.to_owned)

#### fn [to\_owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)(&self) -> T

Creates owned data from borrowed data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#94)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.clone_into)

#### fn [clone\_into](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)(&self, target: [&mut T](https://doc.rust-lang.org/std/primitive.reference.html))

Uses borrowed data to replace owned data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#827-829)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-TryFrom%3CU%3E-for-T)

### impl<T, U> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U> for T where U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#831)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#834)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: U) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, <T as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#811-813)[§](https://doc.rust-lang.org/std/result/enum.Result.html#impl-TryInto%3CU%3E-for-T)

### impl<T, U> [TryInto](https://doc.rust-lang.org/std/convert/trait.TryInto.html "trait std::convert::TryInto")<U> for T where U: [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#815)[§](https://doc.rust-lang.org/std/result/enum.Result.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryInto.html#associatedtype.Error) = <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#818)[§](https://doc.rust-lang.org/std/result/enum.Result.html#method.try_into)

#### fn [try\_into](https://doc.rust-lang.org/std/convert/trait.TryInto.html#tymethod.try_into)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.