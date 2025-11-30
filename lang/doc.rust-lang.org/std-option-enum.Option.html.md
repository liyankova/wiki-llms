---
url: https://doc.rust-lang.org/std/option/enum.Option.html
title: Option in std::option - Rust
source_domain: doc.rust-lang.org
---

# Option in std::option - Rust

## [Option](https://doc.rust-lang.org/std/option/enum.Option.html)

[std](https://doc.rust-lang.org/std/index.html)::[option](https://doc.rust-lang.org/std/option/index.html)

# Enum Option

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#594)

```
pub enum Option<T> {
    None,
    Some(T),
}
```

Expand description

The `Option` type. See [the module level documentation](https://doc.rust-lang.org/std/option/index.html "mod std::option") for more.

## Variants[§](https://doc.rust-lang.org/std/option/enum.Option.html#variants)

[§](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None)1.0.0

### None

No value.

[§](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some)1.0.0

### Some(T)

Some value of type `T`.

## Implementations[§](https://doc.rust-lang.org/std/option/enum.Option.html#implementations)

[Source](https://doc.rust-lang.org/src/core/option.rs.html#609)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Option%3CT%3E)

### impl<T> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

1.0.0 (const: 1.48.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#629)

#### pub const fn [is\_some](https://doc.rust-lang.org/std/option/enum.Option.html#method.is_some)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the option is a [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples)Examples

```
let x: Option<u32> = Some(2);
assert_eq!(x.is_some(), true);

let x: Option<u32> = None;
assert_eq!(x.is_some(), false);
```

1.70.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#655)

#### pub fn [is\_some\_and](https://doc.rust-lang.org/std/option/enum.Option.html#method.is_some_and)(self, f: impl [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the option is a [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") and the value inside of it matches a predicate.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-1)Examples

```
let x: Option<u32> = Some(2);
assert_eq!(x.is_some_and(|x| x > 1), true);

let x: Option<u32> = Some(0);
assert_eq!(x.is_some_and(|x| x > 1), false);

let x: Option<u32> = None;
assert_eq!(x.is_some_and(|x| x > 1), false);

let x: Option<String> = Some("ownership".to_string());
assert_eq!(x.as_ref().is_some_and(|x| x.len() > 1), true);
println!("still alive {:?}", x);
```

1.0.0 (const: 1.48.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#678)

#### pub const fn [is\_none](https://doc.rust-lang.org/std/option/enum.Option.html#method.is_none)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the option is a [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-2)Examples

```
let x: Option<u32> = Some(2);
assert_eq!(x.is_none(), false);

let x: Option<u32> = None;
assert_eq!(x.is_none(), true);
```

1.82.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#704)

#### pub fn [is\_none\_or](https://doc.rust-lang.org/std/option/enum.Option.html#method.is_none_or)(self, f: impl [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns `true` if the option is a [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") or the value inside of it matches a predicate.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-3)Examples

```
let x: Option<u32> = Some(2);
assert_eq!(x.is_none_or(|x| x > 1), true);

let x: Option<u32> = Some(0);
assert_eq!(x.is_none_or(|x| x > 1), false);

let x: Option<u32> = None;
assert_eq!(x.is_none_or(|x| x > 1), true);

let x: Option<String> = Some("ownership".to_string());
assert_eq!(x.as_ref().is_none_or(|x| x.len() > 1), true);
println!("still alive {:?}", x);
```

1.0.0 (const: 1.48.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#738)

#### pub const fn [as\_ref](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_ref)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&T](https://doc.rust-lang.org/std/primitive.reference.html)>

Converts from `&Option<T>` to `Option<&T>`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-4)Examples

Calculates the length of an `Option<String>` as an `Option<usize>`
without moving the [`String`](https://doc.rust-lang.org/std/string/struct.String.html "String"). The [`map`](https://doc.rust-lang.org/std/option/enum.Option.html#method.map "method std::option::Option::map") method takes the `self` argument by value,
consuming the original, so this technique uses `as_ref` to first take an `Option` to a
reference to the value inside the original.

```
let text: Option<String> = Some("Hello, world!".to_string());
// First, cast `Option<String>` to `Option<&String>` with `as_ref`,
// then consume *that* with `map`, leaving `text` on the stack.
let text_length: Option<usize> = text.as_ref().map(|s| s.len());
println!("still can print text: {text:?}");
```

1.0.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#760)

#### pub const fn [as\_mut](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_mut)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

Converts from `&mut Option<T>` to `Option<&mut T>`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-5)Examples

```
let mut x = Some(2);
match x.as_mut() {
    Some(v) => *v = 42,
    None => {},
}
assert_eq!(x, Some(42));
```

1.33.0 (const: 1.84.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#774)

#### pub const fn [as\_pin\_ref](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_pin_ref)(self: [Pin](https://doc.rust-lang.org/std/pin/struct.Pin.html "struct std::pin::Pin")<&[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Pin](https://doc.rust-lang.org/std/pin/struct.Pin.html "struct std::pin::Pin")<[&T](https://doc.rust-lang.org/std/primitive.reference.html)>>

Converts from `Pin<&Option<T>>` to `Option<Pin<&T>>`.

1.33.0 (const: 1.84.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#791)

#### pub const fn [as\_pin\_mut](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_pin_mut)(self: [Pin](https://doc.rust-lang.org/std/pin/struct.Pin.html "struct std::pin::Pin")<&mut [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Pin](https://doc.rust-lang.org/std/pin/struct.Pin.html "struct std::pin::Pin")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html)>>

Converts from `Pin<&mut Option<T>>` to `Option<Pin<&mut T>>`.

1.75.0 (const: 1.84.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#838)

#### pub const fn [as\_slice](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_slice)(&self) -> &[[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Returns a slice of the contained value, if any. If this is `None`, an
empty slice is returned. This can be useful to have a single type of
iterator over an `Option` or slice.

Note: Should you have an `Option<&T>` and wish to get a slice of `T`,
you can unpack it via `opt.map_or(&[], std::slice::from_ref)`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-6)Examples

```
assert_eq!(
    [Some(1234).as_slice(), None.as_slice()],
    [&[1234][..], &[][..]],
);
```

The inverse of this function is (discounting
borrowing) [`[_]::first`](https://doc.rust-lang.org/std/primitive.slice.html#method.first "method slice::first"):

```
for i in [Some(1234_u16), None] {
    assert_eq!(i.as_ref(), i.as_slice().first());
}
```

1.75.0 (const: 1.84.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#893)

#### pub const fn [as\_mut\_slice](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_mut_slice)(&mut self) -> &mut [[T]](https://doc.rust-lang.org/std/primitive.slice.html)

Returns a mutable slice of the contained value, if any. If this is
`None`, an empty slice is returned. This can be useful to have a
single type of iterator over an `Option` or slice.

Note: Should you have an `Option<&mut T>` instead of a
`&mut Option<T>`, which this method takes, you can obtain a mutable
slice via `opt.map_or(&mut [], std::slice::from_mut)`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-7)Examples

```
assert_eq!(
    [Some(1234).as_mut_slice(), None.as_mut_slice()],
    [&mut [1234][..], &mut [][..]],
);
```

The result is a mutable slice of zero or one items that points into
our original `Option`:

```
let mut x = Some(1234);
x.as_mut_slice()[0] += 1;
assert_eq!(x, Some(1235));
```

The inverse of this method (discounting borrowing)
is [`[_]::first_mut`](https://doc.rust-lang.org/std/primitive.slice.html#method.first_mut "method slice::first_mut"):

```
assert_eq!(Some(123).as_mut_slice().first_mut(), Some(&mut 123))
```

1.0.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#962)

#### pub const fn [expect](https://doc.rust-lang.org/std/option/enum.Option.html#method.expect)(self, msg: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> T

Returns the contained [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") value, consuming the `self` value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#panics)Panics

Panics if the value is a [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") with a custom panic message provided by
`msg`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-8)Examples

```
let x = Some("value");
assert_eq!(x.expect("fruits are healthy"), "value");
```

[ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html "This example panics")

```
let x: Option<&str> = None;
x.expect("fruits are healthy"); // panics with `fruits are healthy`
```

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#recommended-message-style)Recommended Message Style

We recommend that `expect` messages are used to describe the reason you
*expect* the `Option` should be `Some`.

[ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html "This example panics")

```
let item = slice.get(0)
    .expect("slice should not be empty");
```

**Hint**: If you’re having trouble remembering how to phrase expect
error messages remember to focus on the word “should” as in “env
variable should be set by blah” or “the given binary should be available
and executable by the current user”.

For more detail on expect message styles and the reasoning behind our
recommendation please refer to the section on [“Common Message
Styles”](https://doc.rust-lang.org/std/error/index.html#common-message-styles) in the [`std::error`](https://doc.rust-lang.org/std/error/index.html) module docs.

1.0.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1007)

#### pub const fn [unwrap](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap)(self) -> T

Returns the contained [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") value, consuming the `self` value.

Because this function may panic, its use is generally discouraged.
Panics are meant for unrecoverable errors, and
[may abort the entire program](https://doc.rust-lang.org/book/ch09-01-unrecoverable-errors-with-panic.html).

Instead, prefer to use pattern matching and handle the [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None")
case explicitly, or call [`unwrap_or`](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_or "method std::option::Option::unwrap_or"), [`unwrap_or_else`](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_or_else "method std::option::Option::unwrap_or_else"), or
[`unwrap_or_default`](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_or_default "method std::option::Option::unwrap_or_default"). In functions returning `Option`, you can use
[the `?` (try) operator](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html#where-the--operator-can-be-used).

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#panics-1)Panics

Panics if the self value equals [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-9)Examples

```
let x = Some("air");
assert_eq!(x.unwrap(), "air");
```

[ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html "This example panics")

```
let x: Option<&str> = None;
assert_eq!(x.unwrap(), "air"); // fails
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1032-1034)

#### pub fn [unwrap\_or](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_or)(self, default: T) -> T

Returns the contained [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") value or a provided default.

Arguments passed to `unwrap_or` are eagerly evaluated; if you are passing
the result of a function call, it is recommended to use [`unwrap_or_else`](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_or_else "method std::option::Option::unwrap_or_else"),
which is lazily evaluated.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-10)Examples

```
assert_eq!(Some("car").unwrap_or("bike"), "car");
assert_eq!(None.unwrap_or("bike"), "bike");
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1055-1057)

#### pub fn [unwrap\_or\_else](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_or_else)<F>(self, f: F) -> T where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> T,

Returns the contained [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") value or computes it from a closure.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-11)Examples

```
let k = 10;
assert_eq!(Some(4).unwrap_or_else(|| 2 * k), 4);
assert_eq!(None.unwrap_or_else(|| 2 * k), 20);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1087-1089)

#### pub fn [unwrap\_or\_default](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_or_default)(self) -> T where T: [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default"),

Returns the contained [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") value or a default.

Consumes the `self` argument then, if [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some"), returns the contained
value, otherwise if [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), returns the [default value](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default "associated function std::default::Default::default") for that
type.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-12)Examples

```
let x: Option<u32> = None;
let y: Option<u32> = Some(12);

assert_eq!(x.unwrap_or_default(), 0);
assert_eq!(y.unwrap_or_default(), 12);
```

1.58.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1122)

#### pub const unsafe fn [unwrap\_unchecked](https://doc.rust-lang.org/std/option/enum.Option.html#method.unwrap_unchecked)(self) -> T

Returns the contained [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") value, consuming the `self` value,
without checking that the value is not [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#safety)Safety

Calling this method on [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") is *[undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html)*.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-13)Examples

```
let x = Some("air");
assert_eq!(unsafe { x.unwrap_unchecked() }, "air");
```

```
let x: Option<&str> = None;
assert_eq!(unsafe { x.unwrap_unchecked() }, "air"); // Undefined behavior!
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1154-1156)

#### pub fn [map](https://doc.rust-lang.org/std/option/enum.Option.html#method.map)<U, F>(self, f: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U,

Maps an `Option<T>` to `Option<U>` by applying a function to a contained value (if `Some`) or returns `None` (if `None`).

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-14)Examples

Calculates the length of an `Option<String>` as an
`Option<usize>`, consuming the original:

```
let maybe_some_string = Some(String::from("Hello, World!"));
// `Option::map` takes self *by value*, consuming `maybe_some_string`
let maybe_some_len = maybe_some_string.map(|s| s.len());
assert_eq!(maybe_some_len, Some(13));

let x: Option<&str> = None;
assert_eq!(x.map(|s| s.len()), None);
```

1.76.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1185-1187)

#### pub fn [inspect](https://doc.rust-lang.org/std/option/enum.Option.html#method.inspect)<F>(self, f: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")([&T](https://doc.rust-lang.org/std/primitive.reference.html)),

Calls a function with a reference to the contained value if [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some").

Returns the original option.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-15)Examples

```
let list = vec![1, 2, 3];

// prints "got: 2"
let x = list
    .get(1)
    .inspect(|x| println!("got: {x}"))
    .expect("list should be long enough");

// prints nothing
list.get(5).inspect(|x| println!("got: {x}"));
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1218-1221)

#### pub fn [map\_or](https://doc.rust-lang.org/std/option/enum.Option.html#method.map_or)<U, F>(self, default: U, f: F) -> U where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U,

Returns the provided default result (if none),
or applies a function to the contained value (if any).

Arguments passed to `map_or` are eagerly evaluated; if you are passing
the result of a function call, it is recommended to use [`map_or_else`](https://doc.rust-lang.org/std/option/enum.Option.html#method.map_or_else "method std::option::Option::map_or_else"),
which is lazily evaluated.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-16)Examples

```
let x = Some("foo");
assert_eq!(x.map_or(42, |v| v.len()), 3);

let x: Option<&str> = None;
assert_eq!(x.map_or(42, |v| v.len()), 42);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1265-1268)

#### pub fn [map\_or\_else](https://doc.rust-lang.org/std/option/enum.Option.html#method.map_or_else)<U, D, F>(self, default: D, f: F) -> U where D: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> U, F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U,

Computes a default function result (if none), or
applies a different function to the contained value (if any).

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#basic-examples)Basic examples

```
let k = 21;

let x = Some("foo");
assert_eq!(x.map_or_else(|| 2 * k, |v| v.len()), 3);

let x: Option<&str> = None;
assert_eq!(x.map_or_else(|| 2 * k, |v| v.len()), 42);
```

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#handling-a-result-based-fallback)Handling a Result-based fallback

A somewhat common occurrence when dealing with optional values
in combination with [`Result<T, E>`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result") is the case where one wants to invoke
a fallible fallback if the option is not present. This example
parses a command line argument (if present), or the contents of a file to
an integer. However, unlike accessing the command line argument, reading
the file is fallible, so it must be wrapped with `Ok`.

```
let v: u64 = std::env::args()
   .nth(1)
   .map_or_else(|| std::fs::read_to_string("/etc/someconfig.conf"), Ok)?
   .parse()?;
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#1296-1299)

#### pub const fn [map\_or\_default](https://doc.rust-lang.org/std/option/enum.Option.html#method.map_or_default)<U, F>(self, f: F) -> U where U: [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default"), F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> U,

🔬This is a nightly-only experimental API. (`result_option_map_or_default` [#138099](https://github.com/rust-lang/rust/issues/138099))

Maps an `Option<T>` to a `U` by applying function `f` to the contained
value if the option is [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some"), otherwise if [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), returns the
[default value](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default "associated function std::default::Default::default") for the type `U`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-17)Examples

```
#![feature(result_option_map_or_default)]

let x: Option<&str> = Some("hi");
let y: Option<&str> = None;

assert_eq!(x.map_or_default(|x| x.len()), 2);
assert_eq!(y.map_or_default(|y| y.len()), 0);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1331)

#### pub fn [ok\_or](https://doc.rust-lang.org/std/option/enum.Option.html#method.ok_or)<E>(self, err: E) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>

Transforms the `Option<T>` into a [`Result<T, E>`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result"), mapping [`Some(v)`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") to
[`Ok(v)`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") and [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") to [`Err(err)`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err").

Arguments passed to `ok_or` are eagerly evaluated; if you are passing the
result of a function call, it is recommended to use [`ok_or_else`](https://doc.rust-lang.org/std/option/enum.Option.html#method.ok_or_else "method std::option::Option::ok_or_else"), which is
lazily evaluated.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-18)Examples

```
let x = Some("foo");
assert_eq!(x.ok_or(0), Ok("foo"));

let x: Option<&str> = None;
assert_eq!(x.ok_or(0), Err(0));
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1357-1359)

#### pub fn [ok\_or\_else](https://doc.rust-lang.org/std/option/enum.Option.html#method.ok_or_else)<E, F>(self, err: F) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> E,

Transforms the `Option<T>` into a [`Result<T, E>`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result"), mapping [`Some(v)`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") to
[`Ok(v)`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Ok "variant std::result::Result::Ok") and [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") to [`Err(err())`](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err "variant std::result::Result::Err").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-19)Examples

```
let x = Some("foo");
assert_eq!(x.ok_or_else(|| 0), Ok("foo"));

let x: Option<&str> = None;
assert_eq!(x.ok_or_else(|| 0), Err(0));
```

1.40.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1384-1386)

#### pub fn [as\_deref](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_deref)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&<T as [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")>::[Target](https://doc.rust-lang.org/std/ops/trait.Deref.html#associatedtype.Target "type std::ops::Deref::Target")> where T: [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref"),

Converts from `Option<T>` (or `&Option<T>`) to `Option<&T::Target>`.

Leaves the original Option in-place, creating a new one with a reference
to the original one, additionally coercing the contents via [`Deref`](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-20)Examples

```
let x: Option<String> = Some("hey".to_owned());
assert_eq!(x.as_deref(), Some("hey"));

let x: Option<String> = None;
assert_eq!(x.as_deref(), None);
```

1.40.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1408-1410)

#### pub fn [as\_deref\_mut](https://doc.rust-lang.org/std/option/enum.Option.html#method.as_deref_mut)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<&mut <T as [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html "trait std::ops::Deref")>::[Target](https://doc.rust-lang.org/std/ops/trait.Deref.html#associatedtype.Target "type std::ops::Deref::Target")> where T: [DerefMut](https://doc.rust-lang.org/std/ops/trait.DerefMut.html "trait std::ops::DerefMut"),

Converts from `Option<T>` (or `&mut Option<T>`) to `Option<&mut T::Target>`.

Leaves the original `Option` in-place, creating a new one containing a mutable reference to
the inner type’s [`Deref::Target`](https://doc.rust-lang.org/std/ops/trait.Deref.html#associatedtype.Target "associated type std::ops::Deref::Target") type.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-21)Examples

```
let mut x: Option<String> = Some("hey".to_owned());
assert_eq!(x.as_deref_mut().map(|x| {
    x.make_ascii_uppercase();
    x
}), Some("HEY".to_owned().as_mut_str()));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1432)

#### pub fn [iter](https://doc.rust-lang.org/std/option/enum.Option.html#method.iter)(&self) -> [Iter](https://doc.rust-lang.org/std/option/struct.Iter.html "struct std::option::Iter")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html)

Returns an iterator over the possibly contained value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-22)Examples

```
let x = Some(4);
assert_eq!(x.iter().next(), Some(&4));

let x: Option<u32> = None;
assert_eq!(x.iter().next(), None);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1453)

#### pub fn [iter\_mut](https://doc.rust-lang.org/std/option/enum.Option.html#method.iter_mut)(&mut self) -> [IterMut](https://doc.rust-lang.org/std/option/struct.IterMut.html "struct std::option::IterMut")<'\_, T> [ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html)

Returns a mutable iterator over the possibly contained value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-23)Examples

```
let mut x = Some(4);
match x.iter_mut().next() {
    Some(v) => *v = 42,
    None => {},
}
assert_eq!(x, Some(42));

let mut x: Option<u32> = None;
assert_eq!(x.iter_mut().next(), None);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1491-1494)

#### pub fn [and](https://doc.rust-lang.org/std/option/enum.Option.html#method.and)<U>(self, optb: [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the option is [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), otherwise returns `optb`.

Arguments passed to `and` are eagerly evaluated; if you are passing the
result of a function call, it is recommended to use [`and_then`](https://doc.rust-lang.org/std/option/enum.Option.html#method.and_then "method std::option::Option::and_then"), which is
lazily evaluated.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-24)Examples

```
let x = Some(2);
let y: Option<&str> = None;
assert_eq!(x.and(y), None);

let x: Option<u32> = None;
let y = Some("foo");
assert_eq!(x.and(y), None);

let x = Some(2);
let y = Some("foo");
assert_eq!(x.and(y), Some("foo"));

let x: Option<u32> = None;
let y: Option<&str> = None;
assert_eq!(x.and(y), None);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1535-1537)

#### pub fn [and\_then](https://doc.rust-lang.org/std/option/enum.Option.html#method.and_then)<U, F>(self, f: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>,

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the option is [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), otherwise calls `f` with the
wrapped value and returns the result.

Some languages call this operation flatmap.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-25)Examples

```
fn sq_then_to_string(x: u32) -> Option<String> {
    x.checked_mul(x).map(|sq| sq.to_string())
}

assert_eq!(Some(2).and_then(sq_then_to_string), Some(4.to_string()));
assert_eq!(Some(1_000_000).and_then(sq_then_to_string), None); // overflowed!
assert_eq!(None.and_then(sq_then_to_string), None);
```

Often used to chain fallible operations that may return [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None").

```
let arr_2d = [["A0", "A1"], ["B0", "B1"]];

let item_0_1 = arr_2d.get(0).and_then(|row| row.get(1));
assert_eq!(item_0_1, Some(&"A1"));

let item_2_0 = arr_2d.get(2).and_then(|row| row.get(0));
assert_eq!(item_2_0, None);
```

1.27.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1572-1575)

#### pub fn [filter](https://doc.rust-lang.org/std/option/enum.Option.html#method.filter)<P>(self, predicate: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where P: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")([&T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if the option is [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), otherwise calls `predicate`
with the wrapped value and returns:

* [`Some(t)`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") if `predicate` returns `true` (where `t` is the wrapped
  value), and
* [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") if `predicate` returns `false`.

This function works similar to [`Iterator::filter()`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.filter "method std::iter::Iterator::filter"). You can imagine
the `Option<T>` being an iterator over one or zero elements. `filter()`
lets you decide which elements to keep.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-26)Examples

```
fn is_even(n: &i32) -> bool {
    n % 2 == 0
}

assert_eq!(None.filter(is_even), None);
assert_eq!(Some(3).filter(is_even), None);
assert_eq!(Some(4).filter(is_even), Some(4));
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1615-1617)

#### pub fn [or](https://doc.rust-lang.org/std/option/enum.Option.html#method.or)(self, optb: [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Returns the option if it contains a value, otherwise returns `optb`.

Arguments passed to `or` are eagerly evaluated; if you are passing the
result of a function call, it is recommended to use [`or_else`](https://doc.rust-lang.org/std/option/enum.Option.html#method.or_else "method std::option::Option::or_else"), which is
lazily evaluated.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-27)Examples

```
let x = Some(2);
let y = None;
assert_eq!(x.or(y), Some(2));

let x = None;
let y = Some(100);
assert_eq!(x.or(y), Some(100));

let x = Some(2);
let y = Some(100);
assert_eq!(x.or(y), Some(2));

let x: Option<u32> = None;
let y = None;
assert_eq!(x.or(y), None);
```

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1641-1646)

#### pub fn [or\_else](https://doc.rust-lang.org/std/option/enum.Option.html#method.or_else)<F>(self, f: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>,

Returns the option if it contains a value, otherwise calls `f` and
returns the result.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-28)Examples

```
fn nobody() -> Option<&'static str> { None }
fn vikings() -> Option<&'static str> { Some("vikings") }

assert_eq!(Some("barbarians").or_else(vikings), Some("barbarians"));
assert_eq!(None.or_else(vikings), Some("vikings"));
assert_eq!(None.or_else(nobody), None);
```

1.37.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1678-1680)

#### pub fn [xor](https://doc.rust-lang.org/std/option/enum.Option.html#method.xor)(self, optb: [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Returns [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") if exactly one of `self`, `optb` is [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some"), otherwise returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-29)Examples

```
let x = Some(2);
let y: Option<u32> = None;
assert_eq!(x.xor(y), Some(2));

let x: Option<u32> = None;
let y = Some(2);
assert_eq!(x.xor(y), Some(2));

let x = Some(2);
let y = Some(2);
assert_eq!(x.xor(y), None);

let x: Option<u32> = None;
let y: Option<u32> = None;
assert_eq!(x.xor(y), None);
```

1.53.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1716-1718)

#### pub fn [insert](https://doc.rust-lang.org/std/option/enum.Option.html#method.insert)(&mut self, value: T) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Inserts `value` into the option, then returns a mutable reference to it.

If the option already contains a value, the old value is dropped.

See also [`Option::get_or_insert`](https://doc.rust-lang.org/std/option/enum.Option.html#method.get_or_insert "method std::option::Option::get_or_insert"), which doesn’t update the value if
the option already contains [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#example)Example

```
let mut opt = None;
let val = opt.insert(1);
assert_eq!(*val, 1);
assert_eq!(opt.unwrap(), 1);
let val = opt.insert(2);
assert_eq!(*val, 2);
*val = 3;
assert_eq!(opt.unwrap(), 3);
```

1.20.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1748)

#### pub fn [get\_or\_insert](https://doc.rust-lang.org/std/option/enum.Option.html#method.get_or_insert)(&mut self, value: T) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Inserts `value` into the option if it is [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), then
returns a mutable reference to the contained value.

See also [`Option::insert`](https://doc.rust-lang.org/std/option/enum.Option.html#method.insert "method std::option::Option::insert"), which updates the value even if
the option already contains [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-30)Examples

```
let mut x = None;

{
    let y: &mut u32 = x.get_or_insert(5);
    assert_eq!(y, &5);

    *y = 7;
}

assert_eq!(x, Some(7));
```

1.83.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1772-1774)

#### pub fn [get\_or\_insert\_default](https://doc.rust-lang.org/std/option/enum.Option.html#method.get_or_insert_default)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html) where T: [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default"),

Inserts the default value into the option if it is [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), then
returns a mutable reference to the contained value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-31)Examples

```
let mut x = None;

{
    let y: &mut u32 = x.get_or_insert_default();
    assert_eq!(y, &0);

    *y = 7;
}

assert_eq!(x, Some(7));
```

1.20.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1799-1802)

#### pub fn [get\_or\_insert\_with](https://doc.rust-lang.org/std/option/enum.Option.html#method.get_or_insert_with)<F>(&mut self, f: F) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html) where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")() -> T,

Inserts a value computed from `f` into the option if it is [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"),
then returns a mutable reference to the contained value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-32)Examples

```
let mut x = None;

{
    let y: &mut u32 = x.get_or_insert_with(|| 5);
    assert_eq!(y, &5);

    *y = 7;
}

assert_eq!(x, Some(7));
```

1.0.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1835)

#### pub const fn [take](https://doc.rust-lang.org/std/option/enum.Option.html#method.take)(&mut self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Takes the value out of the option, leaving a [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") in its place.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-33)Examples

```
let mut x = Some(2);
let y = x.take();
assert_eq!(x, None);
assert_eq!(y, Some(2));

let mut x: Option<u32> = None;
let y = x.take();
assert_eq!(x, None);
assert_eq!(y, None);
```

1.80.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1867-1869)

#### pub fn [take\_if](https://doc.rust-lang.org/std/option/enum.Option.html#method.take_if)<P>(&mut self, predicate: P) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where P: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")([&mut T](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html),

Takes the value out of the option, but only if the predicate evaluates to
`true` on a mutable reference to the value.

In other words, replaces `self` with `None` if the predicate returns `true`.
This method operates similar to [`Option::take`](https://doc.rust-lang.org/std/option/enum.Option.html#method.take "method std::option::Option::take") but conditional.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-34)Examples

```
let mut x = Some(42);

let prev = x.take_if(|v| if *v == 42 {
    *v += 1;
    false
} else {
    false
});
assert_eq!(x, Some(43));
assert_eq!(prev, None);

let prev = x.take_if(|v| *v == 43);
assert_eq!(x, None);
assert_eq!(prev, Some(43));
```

1.31.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1894)

#### pub const fn [replace](https://doc.rust-lang.org/std/option/enum.Option.html#method.replace)(&mut self, value: T) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Replaces the actual value in the option by the value given in parameter,
returning the old value if present,
leaving a [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some") in its place without deinitializing either one.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-35)Examples

```
let mut x = Some(2);
let old = x.replace(5);
assert_eq!(x, Some(5));
assert_eq!(old, Some(2));

let mut x = None;
let old = x.replace(3);
assert_eq!(x, Some(3));
assert_eq!(old, None);
```

1.46.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143956 "Tracking issue for const_option_ops")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#1915-1918)

#### pub fn [zip](https://doc.rust-lang.org/std/option/enum.Option.html#method.zip)<U>(self, other: [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[(T, U)](https://doc.rust-lang.org/std/primitive.tuple.html)>

Zips `self` with another `Option`.

If `self` is `Some(s)` and `other` is `Some(o)`, this method returns `Some((s, o))`.
Otherwise, `None` is returned.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-36)Examples

```
let x = Some(1);
let y = Some("hi");
let z = None::<u8>;

assert_eq!(x.zip(y), Some((1, "hi")));
assert_eq!(x.zip(z), None);
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#1956-1960)

#### pub const fn [zip\_with](https://doc.rust-lang.org/std/option/enum.Option.html#method.zip_with)<U, F, R>(self, other: [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>, f: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<R> where F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T, U) -> R,

🔬This is a nightly-only experimental API. (`option_zip` [#70086](https://github.com/rust-lang/rust/issues/70086))

Zips `self` and another `Option` with function `f`.

If `self` is `Some(s)` and `other` is `Some(o)`, this method returns `Some(f(s, o))`.
Otherwise, `None` is returned.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-37)Examples

```
#![feature(option_zip)]

#[derive(Debug, PartialEq)]
struct Point {
    x: f64,
    y: f64,
}

impl Point {
    fn new(x: f64, y: f64) -> Self {
        Self { x, y }
    }
}

let x = Some(17.5);
let y = Some(42.7);

assert_eq!(x.zip_with(y, Point::new), Some(Point { x: 17.5, y: 42.7 }));
assert_eq!(x.zip_with(None, Point::new), None);
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#1990-1994)

#### pub fn [reduce](https://doc.rust-lang.org/std/option/enum.Option.html#method.reduce)<U, R, F>(self, other: [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>, f: F) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<R> where T: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<R>, U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<R>, F: [FnOnce](https://doc.rust-lang.org/std/ops/trait.FnOnce.html "trait std::ops::FnOnce")(T, U) -> R,

🔬This is a nightly-only experimental API. (`option_reduce` [#144273](https://github.com/rust-lang/rust/issues/144273))

Reduces two options into one, using the provided function if both are `Some`.

If `self` is `Some(s)` and `other` is `Some(o)`, this method returns `Some(f(s, o))`.
Otherwise, if only one of `self` and `other` is `Some`, that one is returned.
If both `self` and `other` are `None`, `None` is returned.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-38)Examples

```
#![feature(option_reduce)]

let s12 = Some(12);
let s17 = Some(17);
let n = None;
let f = |a, b| a + b;

assert_eq!(s12.reduce(s17, f), Some(29));
assert_eq!(s12.reduce(n, f), Some(12));
assert_eq!(n.reduce(s17, f), Some(17));
assert_eq!(n.reduce(n, f), None);
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2005)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Option%3C(T,+U)%3E)

### impl<T, U> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[(T, U)](https://doc.rust-lang.org/std/primitive.tuple.html)>

1.66.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2022)

#### pub fn [unzip](https://doc.rust-lang.org/std/option/enum.Option.html#method.unzip)(self) -> ([Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>, [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>)

Unzips an option containing a tuple of two options.

If `self` is `Some((a, b))` this method returns `(Some(a), Some(b))`.
Otherwise, `(None, None)` is returned.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-39)Examples

```
let x = Some((1, "hi"));
let y = None::<(u8, u32)>;

assert_eq!(x.unzip(), (Some(1), Some("hi")));
assert_eq!(y.unzip(), (None, None));
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2030)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Option%3C%26T%3E)

### impl<T> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&T](https://doc.rust-lang.org/std/primitive.reference.html)>

1.35.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2046-2048)

#### pub const fn [copied](https://doc.rust-lang.org/std/option/enum.Option.html#method.copied)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

Maps an `Option<&T>` to an `Option<T>` by copying the contents of the
option.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-40)Examples

```
let x = 12;
let opt_x = Some(&x);
assert_eq!(opt_x, Some(&12));
let copied = opt_x.copied();
assert_eq!(copied, Some(12));
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2072-2074)

#### pub fn [cloned](https://doc.rust-lang.org/std/option/enum.Option.html#method.cloned)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Maps an `Option<&T>` to an `Option<T>` by cloning the contents of the
option.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-41)Examples

```
let x = 12;
let opt_x = Some(&x);
assert_eq!(opt_x, Some(&12));
let cloned = opt_x.cloned();
assert_eq!(cloned, Some(12));
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2083)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Option%3C%26mut+T%3E)

### impl<T> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

1.35.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2099-2101)

#### pub const fn [copied](https://doc.rust-lang.org/std/option/enum.Option.html#method.copied-1)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

Maps an `Option<&mut T>` to an `Option<T>` by copying the contents of the
option.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-42)Examples

```
let mut x = 12;
let opt_x = Some(&mut x);
assert_eq!(opt_x, Some(&mut 12));
let copied = opt_x.copied();
assert_eq!(copied, Some(12));
```

1.26.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2123-2125)

#### pub fn [cloned](https://doc.rust-lang.org/std/option/enum.Option.html#method.cloned-1)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

Maps an `Option<&mut T>` to an `Option<T>` by cloning the contents of the
option.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-43)Examples

```
let mut x = 12;
let opt_x = Some(&mut x);
assert_eq!(opt_x, Some(&mut 12));
let cloned = opt_x.cloned();
assert_eq!(cloned, Some(12));
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2134)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Option%3CResult%3CT,+E%3E%3E)

### impl<T, E> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>>

1.33.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2155)

#### pub const fn [transpose](https://doc.rust-lang.org/std/option/enum.Option.html#method.transpose)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>, E>

Transposes an `Option` of a [`Result`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result") into a [`Result`](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result") of an `Option`.

`Some(Ok(_))` is mapped to `Ok(Some(_))`,
`Some(Err(_))` is mapped to `Err(_)`,
and [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") will be mapped to `Ok(None)`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-44)Examples

```
#[derive(Debug, Eq, PartialEq)]
struct SomeErr;

let x: Option<Result<i32, SomeErr>> = Some(Ok(5));
let y: Result<Option<i32>, SomeErr> = Ok(Some(5));
assert_eq!(x.transpose(), y);
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2691)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Option%3COption%3CT%3E%3E)

### impl<T> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>>

1.40.0 (const: 1.83.0) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2720)

#### pub const fn [flatten](https://doc.rust-lang.org/std/option/enum.Option.html#method.flatten)(self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Converts from `Option<Option<T>>` to `Option<T>`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-45)Examples

Basic usage:

```
let x: Option<Option<u32>> = Some(Some(6));
assert_eq!(Some(6), x.flatten());

let x: Option<Option<u32>> = Some(None);
assert_eq!(None, x.flatten());

let x: Option<Option<u32>> = None;
assert_eq!(None, x.flatten());
```

Flattening only removes one level of nesting at a time:

```
let x: Option<Option<Option<u32>>> = Some(Some(Some(6)));
assert_eq!(Some(Some(6)), x.flatten());
assert_eq!(Some(6), x.flatten().flatten());
```

## Trait Implementations[§](https://doc.rust-lang.org/std/option/enum.Option.html#trait-implementations)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/142757 "Tracking issue for const_clone")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2187-2191)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Clone-for-Option%3CT%3E)

### impl<T> [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2194)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.clone)

#### fn [clone](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)(&self) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Returns a duplicate of the value. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2202)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.clone_from)

#### fn [clone\_from](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)(&mut self, source: &[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>)

Performs copy-assignment from `source`. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#588)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Debug-for-Option%3CT%3E)

### impl<T> [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug"),

[Source](https://doc.rust-lang.org/src/core/option.rs.html#588)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, f: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143894 "Tracking issue for const_default")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2215)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Default-for-Option%3CT%3E)

### impl<T> [Default](https://doc.rust-lang.org/std/default/trait.Default.html "trait std::default::Default") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2225)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.default)

#### fn [default](https://doc.rust-lang.org/std/default/trait.Default.html#tymethod.default)() -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Returns [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-46)Examples

```
let opt: Option<u32> = Option::default();
assert!(opt.is_none());
```

1.30.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2293)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-From%3C%26Option%3CT%3E%3E-for-Option%3C%26T%3E)

### impl<'a, T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&'a [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a T](https://doc.rust-lang.org/std/primitive.reference.html)>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2314)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from-1)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(o: &'a [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a T](https://doc.rust-lang.org/std/primitive.reference.html)>

Converts from `&Option<T>` to `Option<&T>`.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-48)Examples

Converts an `Option<String>` into an `Option<usize>`, preserving
the original. The [`map`](https://doc.rust-lang.org/std/option/enum.Option.html#method.map "method std::option::Option::map") method takes the `self` argument by value, consuming the original,
so this technique uses `from` to first take an [`Option`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option") to a reference
to the value inside the original.

```
let s: Option<String> = Some(String::from("Hello, Rustaceans!"));
let o: Option<usize> = Option::from(&s).map(|ss: &String| ss.len());

println!("Can still print s: {s:?}");

assert_eq!(o, Some(18));
```

1.30.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2321)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-From%3C%26mut+Option%3CT%3E%3E-for-Option%3C%26mut+T%3E)

### impl<'a, T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<&'a mut [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2337)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from-2)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(o: &'a mut [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[&'a mut T](https://doc.rust-lang.org/std/primitive.reference.html)>

Converts from `&mut Option<T>` to `Option<&mut T>`

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-49)Examples

```
let mut s = Some(String::from("Hello"));
let o: Option<&mut String> = Option::from(&mut s);

match o {
    Some(t) => *t = String::from("Hello, Rustaceans!"),
    None => (),
}

assert_eq!(s, Some(String::from("Hello, Rustaceans!")));
```

1.12.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2276)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-From%3CT%3E-for-Option%3CT%3E)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2286)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(val: T) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

Moves `val` into a new [`Some`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.Some "variant std::option::Option::Some").

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-47)Examples

```
let o: Option<u8> = Option::from(67);

assert_eq!(Some(67), o);
```

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2572)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-FromIterator%3COption%3CA%3E%3E-for-Option%3CV%3E)

### impl<A, V> [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<A>> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<V> where V: [FromIterator](https://doc.rust-lang.org/std/iter/trait.FromIterator.html "trait std::iter::FromIterator")<A>,

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2634)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from_iter)

#### fn [from\_iter](https://doc.rust-lang.org/std/iter/trait.FromIterator.html#tymethod.from_iter)<I>(iter: I) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<V> where I: [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator")<Item = [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<A>>,

Takes each element in the [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator"): if it is [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"),
no further elements are taken, and the [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") is
returned. Should no [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") occur, a container of type
`V` containing the values of each [`Option`](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option") is returned.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-53)Examples

Here is an example which increments every integer in a vector.
We use the checked variant of `add` that returns `None` when the
calculation would result in an overflow.

```
let items = vec![0_u16, 1, 2];

let res: Option<Vec<u16>> = items
    .iter()
    .map(|x| x.checked_add(1))
    .collect();

assert_eq!(res, Some(vec![1, 2, 3]));
```

As you can see, this will return the expected, valid items.

Here is another example that tries to subtract one from another list
of integers, this time checking for underflow:

```
let items = vec![2_u16, 1, 0];

let res: Option<Vec<u16>> = items
    .iter()
    .map(|x| x.checked_sub(1))
    .collect();

assert_eq!(res, None);
```

Since the last element is zero, it would underflow. Thus, the resulting
value is `None`.

Here is a variation on the previous example, showing that no
further elements are taken from `iter` after the first `None`.

```
let items = vec![3_u16, 2, 1, 10];

let mut shared = 0;

let res: Option<Vec<u16>> = items
    .iter()
    .map(|x| { shared += x; x.checked_sub(2) })
    .collect();

assert_eq!(res, None);
assert_eq!(shared, 6);
```

Since the third element caused an underflow, no further elements were taken,
so the final value of `shared` is 6 (= `3 + 2 + 1`), not 16.

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2666)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-FromResidual%3COption%3CInfallible%3E%3E-for-Option%3CT%3E)

### impl<T> [FromResidual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html "trait std::ops::FromResidual")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")>> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2668)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from_residual)

#### fn [from\_residual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)(residual: [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from a compatible `Residual` type. [Read more](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2678)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-FromResidual%3CYeet%3C()%3E%3E-for-Option%3CT%3E)

### impl<T> [FromResidual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html "trait std::ops::FromResidual")<[Yeet](https://doc.rust-lang.org/std/ops/struct.Yeet.html "struct std::ops::Yeet")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2680)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from_residual-1)

#### fn [from\_residual](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)(\_: [Yeet](https://doc.rust-lang.org/std/ops/struct.Yeet.html "struct std::ops::Yeet")<[()](https://doc.rust-lang.org/std/primitive.unit.html)>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from a compatible `Residual` type. [Read more](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#588)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Hash-for-Option%3CT%3E)

### impl<T> [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash"),

[Source](https://doc.rust-lang.org/src/core/option.rs.html#588)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.hash)

#### fn [hash](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)<\_\_H>(&self, state: [&mut \_\_H](https://doc.rust-lang.org/std/primitive.reference.html)) where \_\_H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"),

Feeds this value into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)

1.3.0 · [Source](https://doc.rust-lang.org/src/core/hash/mod.rs.html#235-237)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.hash_slice)

#### fn [hash\_slice](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)<H>(data: &[Self], state: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"), Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Feeds a slice of this type into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)

1.4.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2255)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-IntoIterator-for-%26Option%3CT%3E)

### impl<'a, T> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for &'a [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2256)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Item-1)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = [&'a T](https://doc.rust-lang.org/std/primitive.reference.html)

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2257)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.IntoIter-1)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [Iter](https://doc.rust-lang.org/std/option/struct.Iter.html "struct std::option::Iter")<'a, T>

Which kind of iterator are we turning this into?

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2259)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.into_iter-1)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> [Iter](https://doc.rust-lang.org/std/option/struct.Iter.html "struct std::option::Iter")<'a, T> [ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html)

Creates an iterator from a value. [Read more](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)

1.4.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2265)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-IntoIterator-for-%26mut+Option%3CT%3E)

### impl<'a, T> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for &'a mut [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2266)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Item-2)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = [&'a mut T](https://doc.rust-lang.org/std/primitive.reference.html)

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2267)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.IntoIter-2)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [IterMut](https://doc.rust-lang.org/std/option/struct.IterMut.html "struct std::option::IterMut")<'a, T>

Which kind of iterator are we turning this into?

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2269)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.into_iter-2)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> [IterMut](https://doc.rust-lang.org/std/option/struct.IterMut.html "struct std::option::IterMut")<'a, T> [ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html)

Creates an iterator from a value. [Read more](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2231)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-IntoIterator-for-Option%3CT%3E)

### impl<T> [IntoIterator](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html "trait std::iter::IntoIterator") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2249)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.into_iter)

#### fn [into\_iter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#tymethod.into_iter)(self) -> [IntoIter](https://doc.rust-lang.org/std/option/struct.IntoIter.html "struct std::option::IntoIter")<T> [ⓘ](https://doc.rust-lang.org/std/option/enum.Option.html)

Returns a consuming iterator over the possibly contained value.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-50)Examples

```
let x = Some("string");
let v: Vec<&str> = x.into_iter().collect();
assert_eq!(v, ["string"]);

let x = None;
let v: Vec<&str> = x.into_iter().collect();
assert!(v.is_empty());
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2232)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Item)

#### type [Item](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.Item) = T

The type of the elements being iterated over.

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2233)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.IntoIter)

#### type [IntoIter](https://doc.rust-lang.org/std/iter/trait.IntoIterator.html#associatedtype.IntoIter) = [IntoIter](https://doc.rust-lang.org/std/option/struct.IntoIter.html "struct std::option::IntoIter")<T>

Which kind of iterator are we turning this into?

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143800 "Tracking issue for const_cmp")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2382)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Ord-for-Option%3CT%3E)

### impl<T> [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord"),

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2384)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.cmp)

#### fn [cmp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)(&self, other: &[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")

This method returns an [`Ordering`](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering") between `self` and `other`. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1023-1025)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.max)

#### fn [max](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the maximum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1062-1064)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.min)

#### fn [min](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the minimum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)

1.50.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1088-1090)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.clamp)

#### fn [clamp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)(self, min: Self, max: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Restrict a value to a certain interval. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143800 "Tracking issue for const_cmp")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2349)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-PartialEq-for-Option%3CT%3E)

### impl<T> [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq"),

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2351)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.eq)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.ne)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143800 "Tracking issue for const_cmp")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2368)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-PartialOrd-for-Option%3CT%3E)

### impl<T> [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd"),

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2370)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.partial_cmp)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.lt)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.le)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.gt)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.ge)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.37.0 · [Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#300-302)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Product%3COption%3CU%3E%3E-for-Option%3CT%3E)

### impl<T, U> [Product](https://doc.rust-lang.org/std/iter/trait.Product.html "trait std::iter::Product")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Product](https://doc.rust-lang.org/std/iter/trait.Product.html "trait std::iter::Product")<U>,

[Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#321-323)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.product)

#### fn [product](https://doc.rust-lang.org/std/iter/trait.Product.html#tymethod.product)<I>(iter: I) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where I: [Iterator](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator")<Item = [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>>,

Takes each element in the [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator"): if it is a [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), no further
elements are taken, and the [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") is returned. Should no [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None")
occur, the product of all elements is returned.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-52)Examples

This multiplies each number in a vector of strings,
if a string could not be parsed the operation returns `None`:

```
let nums = vec!["5", "10", "1", "2"];
let total: Option<usize> = nums.iter().map(|w| w.parse::<usize>().ok()).product();
assert_eq!(total, Some(100));
let nums = vec!["5", "10", "one", "2"];
let total: Option<usize> = nums.iter().map(|w| w.parse::<usize>().ok()).product();
assert_eq!(total, None);
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2687)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Residual%3CT%3E-for-Option%3CInfallible%3E)

### impl<T> [Residual](https://doc.rust-lang.org/std/ops/trait.Residual.html "trait std::ops::Residual")<T> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2688)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.TryType)

#### type [TryType](https://doc.rust-lang.org/std/ops/trait.Residual.html#associatedtype.TryType) = [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

🔬This is a nightly-only experimental API. (`try_trait_v2_residual` [#91285](https://github.com/rust-lang/rust/issues/91285))

The “return” type of this meta-function.

1.37.0 · [Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#270-272)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Sum%3COption%3CU%3E%3E-for-Option%3CT%3E)

### impl<T, U> [Sum](https://doc.rust-lang.org/std/iter/trait.Sum.html "trait std::iter::Sum")<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>> for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Sum](https://doc.rust-lang.org/std/iter/trait.Sum.html "trait std::iter::Sum")<U>,

[Source](https://doc.rust-lang.org/src/core/iter/traits/accum.rs.html#291-293)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.sum)

#### fn [sum](https://doc.rust-lang.org/std/iter/trait.Sum.html#tymethod.sum)<I>(iter: I) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where I: [Iterator](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator")<Item = [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<U>>,

Takes each element in the [`Iterator`](https://doc.rust-lang.org/std/iter/trait.Iterator.html "trait std::iter::Iterator"): if it is a [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None"), no further
elements are taken, and the [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None") is returned. Should no [`None`](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None "variant std::option::Option::None")
occur, the sum of all elements is returned.

##### [§](https://doc.rust-lang.org/std/option/enum.Option.html#examples-51)Examples

This sums up the position of the character ‘a’ in a vector of strings,
if a word did not have the character ‘a’ the operation returns `None`:

```
let words = vec!["have", "a", "great", "day"];
let total: Option<usize> = words.iter().map(|w| w.find('a')).sum();
assert_eq!(total, Some(5));
let words = vec!["have", "a", "good", "day"];
let total: Option<usize> = words.iter().map(|w| w.find('a')).sum();
assert_eq!(total, None);
```

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2644)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Try-for-Option%3CT%3E)

### impl<T> [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2645)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Output)

#### type [Output](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Output) = T

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

The type of the value produced by `?` when *not* short-circuiting.

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2646)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Residual)

#### type [Residual](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Residual) = [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

The type of the value passed to [`FromResidual::from_residual`](https://doc.rust-lang.org/std/ops/trait.FromResidual.html#tymethod.from_residual "associated function std::ops::FromResidual::from_residual")
as part of `?` when short-circuiting. [Read more](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Residual)

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2649)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from_output)

#### fn [from\_output](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.from_output)(output: <[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> as [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try")>::[Output](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Output "type std::ops::Try::Output")) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Constructs the type from its `Output` type. [Read more](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.from_output)

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2654)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.branch)

#### fn [branch](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.branch)( self, ) -> [ControlFlow](https://doc.rust-lang.org/std/ops/enum.ControlFlow.html "enum std::ops::ControlFlow")<<[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> as [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try")>::[Residual](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Residual "type std::ops::Try::Residual"), <[Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> as [Try](https://doc.rust-lang.org/std/ops/trait.Try.html "trait std::ops::Try")>::[Output](https://doc.rust-lang.org/std/ops/trait.Try.html#associatedtype.Output "type std::ops::Try::Output")>

🔬This is a nightly-only experimental API. (`try_trait_v2` [#84277](https://github.com/rust-lang/rust/issues/84277))

Used in `?` to decide whether the operator should produce a value
(because this returned [`ControlFlow::Continue`](https://doc.rust-lang.org/std/ops/enum.ControlFlow.html#variant.Continue "variant std::ops::ControlFlow::Continue"))
or propagate a value back to the caller
(because this returned [`ControlFlow::Break`](https://doc.rust-lang.org/std/ops/enum.ControlFlow.html#variant.Break "variant std::ops::ControlFlow::Break")). [Read more](https://doc.rust-lang.org/std/ops/trait.Try.html#tymethod.branch)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#588)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Copy-for-Option%3CT%3E)

### impl<T> [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy"),

1.0.0 (const: [unstable](https://github.com/rust-lang/rust/issues/118304 "Tracking issue for derive_const")) · [Source](https://doc.rust-lang.org/src/core/option.rs.html#589)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Eq-for-Option%3CT%3E)

### impl<T> [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq"),

1.0.0 · [Source](https://doc.rust-lang.org/src/core/option.rs.html#2346)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-StructuralPartialEq-for-Option%3CT%3E)

### impl<T> [StructuralPartialEq](https://doc.rust-lang.org/std/marker/trait.StructuralPartialEq.html "trait std::marker::StructuralPartialEq") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T>

[Source](https://doc.rust-lang.org/src/core/option.rs.html#2211)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-UseCloned-for-Option%3CT%3E)

### impl<T> [UseCloned](https://doc.rust-lang.org/std/clone/trait.UseCloned.html "trait std::clone::UseCloned") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [UseCloned](https://doc.rust-lang.org/std/clone/trait.UseCloned.html "trait std::clone::UseCloned"),

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/option/enum.Option.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Freeze-for-Option%3CT%3E)

### impl<T> [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze"),

[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-RefUnwindSafe-for-Option%3CT%3E)

### impl<T> [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe"),

[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Send-for-Option%3CT%3E)

### impl<T> [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send"),

[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Sync-for-Option%3CT%3E)

### impl<T> [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync"),

[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Unpin-for-Option%3CT%3E)

### impl<T> [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin"),

[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-UnwindSafe-for-Option%3CT%3E)

### impl<T> [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<T> where T: [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe"),

## Blanket Implementations[§](https://doc.rust-lang.org/std/option/enum.Option.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#515)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-CloneToUninit-for-T)

### impl<T> [CloneToUninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html "trait std::clone::CloneToUninit") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#517)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.clone_to_uninit)

#### unsafe fn [clone\_to\_uninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)(&self, dest: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html))

🔬This is a nightly-only experimental API. (`clone_to_uninit` [#126799](https://github.com/rust-lang/rust/issues/126799))

Performs copy-assignment from `self` to `dest`. [Read more](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#802)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-From%3C!%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[!](https://doc.rust-lang.org/std/primitive.never.html)> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#803)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from-4)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: [!](https://doc.rust-lang.org/std/primitive.never.html)) -> T

Converts to this type from the input type.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#785)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-From%3CT%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#788)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.from-3)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: T) -> T

Returns the argument unchanged.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#767-769)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-Into%3CU%3E-for-T)

### impl<T, U> [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<U> for T where U: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#777)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.into)

#### fn [into](https://doc.rust-lang.org/std/convert/trait.Into.html#tymethod.into)(self) -> U

Calls `U::from(self)`.

That is, this conversion is whatever the implementation of
`From<T> for U` chooses to do.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#85-87)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-ToOwned-for-T)

### impl<T> [ToOwned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html "trait std::borrow::ToOwned") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#89)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Owned)

#### type [Owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#associatedtype.Owned) = T

The resulting type after obtaining ownership.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#90)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.to_owned)

#### fn [to\_owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)(&self) -> T

Creates owned data from borrowed data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#94)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.clone_into)

#### fn [clone\_into](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)(&self, target: [&mut T](https://doc.rust-lang.org/std/primitive.reference.html))

Uses borrowed data to replace owned data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#827-829)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-TryFrom%3CU%3E-for-T)

### impl<T, U> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U> for T where U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#831)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#834)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: U) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, <T as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#811-813)[§](https://doc.rust-lang.org/std/option/enum.Option.html#impl-TryInto%3CU%3E-for-T)

### impl<T, U> [TryInto](https://doc.rust-lang.org/std/convert/trait.TryInto.html "trait std::convert::TryInto")<U> for T where U: [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#815)[§](https://doc.rust-lang.org/std/option/enum.Option.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryInto.html#associatedtype.Error) = <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#818)[§](https://doc.rust-lang.org/std/option/enum.Option.html#method.try_into)

#### fn [try\_into](https://doc.rust-lang.org/std/convert/trait.TryInto.html#tymethod.try_into)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.