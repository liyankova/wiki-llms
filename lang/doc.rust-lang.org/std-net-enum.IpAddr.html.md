---
url: https://doc.rust-lang.org/std/net/enum.IpAddr.html
title: IpAddr in std::net - Rust
source_domain: doc.rust-lang.org
---

# IpAddr in std::net - Rust

## [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html)

[std](https://doc.rust-lang.org/std/index.html)::[net](https://doc.rust-lang.org/std/net/index.html)

# Enum IpAddr

1.0.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#30)

```
pub enum IpAddr {
    V4(Ipv4Addr),
    V6(Ipv6Addr),
}
```

Expand description

An IP address, either IPv4 or IPv6.

This enum can contain either an [`Ipv4Addr`](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr") or an [`Ipv6Addr`](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr"), see their
respective documentation for more details.

## [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples)Examples

```
use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

let localhost_v4 = IpAddr::V4(Ipv4Addr::new(127, 0, 0, 1));
let localhost_v6 = IpAddr::V6(Ipv6Addr::new(0, 0, 0, 0, 0, 0, 0, 1));

assert_eq!("127.0.0.1".parse(), Ok(localhost_v4));
assert_eq!("::1".parse(), Ok(localhost_v6));

assert_eq!(localhost_v4.is_ipv6(), false);
assert_eq!(localhost_v4.is_ipv4(), true);
```

## Variants[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#variants)

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#variant.V4)1.7.0

### V4([Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr"))

An IPv4 address.

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#variant.V6)1.7.0

### V6([Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr"))

An IPv6 address.

## Implementations[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#implementations)

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#235)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-IpAddr)

### impl [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

1.12.0 (const: 1.50.0) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#253)

#### pub const fn [is\_unspecified](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_unspecified)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") for the special ‘unspecified’ address.

See the documentation for [`Ipv4Addr::is_unspecified()`](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html#method.is_unspecified "method std::net::Ipv4Addr::is_unspecified") and
[`Ipv6Addr::is_unspecified()`](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html#method.is_unspecified "method std::net::Ipv6Addr::is_unspecified") for more details.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-1)Examples

```
use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(0, 0, 0, 0)).is_unspecified(), true);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0, 0, 0, 0, 0, 0, 0, 0)).is_unspecified(), true);
```

1.12.0 (const: 1.50.0) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#277)

#### pub const fn [is\_loopback](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_loopback)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") if this is a loopback address.

See the documentation for [`Ipv4Addr::is_loopback()`](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html#method.is_loopback "method std::net::Ipv4Addr::is_loopback") and
[`Ipv6Addr::is_loopback()`](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html#method.is_loopback "method std::net::Ipv6Addr::is_loopback") for more details.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-2)Examples

```
use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(127, 0, 0, 1)).is_loopback(), true);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0, 0, 0, 0, 0, 0, 0, 0x1)).is_loopback(), true);
```

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#302)

#### pub const fn [is\_global](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_global)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`ip` [#27709](https://github.com/rust-lang/rust/issues/27709))

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") if the address appears to be globally routable.

See the documentation for [`Ipv4Addr::is_global()`](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html#method.is_global "method std::net::Ipv4Addr::is_global") and
[`Ipv6Addr::is_global()`](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html#method.is_global "method std::net::Ipv6Addr::is_global") for more details.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-3)Examples

```
#![feature(ip)]

use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(80, 9, 12, 3)).is_global(), true);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0, 0, 0x1c9, 0, 0, 0xafc8, 0, 0x1)).is_global(), true);
```

1.12.0 (const: 1.50.0) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#326)

#### pub const fn [is\_multicast](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_multicast)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") if this is a multicast address.

See the documentation for [`Ipv4Addr::is_multicast()`](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html#method.is_multicast "method std::net::Ipv4Addr::is_multicast") and
[`Ipv6Addr::is_multicast()`](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html#method.is_multicast "method std::net::Ipv6Addr::is_multicast") for more details.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-4)Examples

```
use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(224, 254, 0, 0)).is_multicast(), true);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0xff00, 0, 0, 0, 0, 0, 0, 0)).is_multicast(), true);
```

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#354)

#### pub const fn [is\_documentation](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_documentation)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`ip` [#27709](https://github.com/rust-lang/rust/issues/27709))

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") if this address is in a range designated for documentation.

See the documentation for [`Ipv4Addr::is_documentation()`](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html#method.is_documentation "method std::net::Ipv4Addr::is_documentation") and
[`Ipv6Addr::is_documentation()`](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html#method.is_documentation "method std::net::Ipv6Addr::is_documentation") for more details.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-5)Examples

```
#![feature(ip)]

use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(203, 0, 113, 6)).is_documentation(), true);
assert_eq!(
    IpAddr::V6(Ipv6Addr::new(0x2001, 0xdb8, 0, 0, 0, 0, 0, 0)).is_documentation(),
    true
);
```

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#379)

#### pub const fn [is\_benchmarking](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_benchmarking)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

🔬This is a nightly-only experimental API. (`ip` [#27709](https://github.com/rust-lang/rust/issues/27709))

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") if this address is in a range designated for benchmarking.

See the documentation for [`Ipv4Addr::is_benchmarking()`](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html#method.is_benchmarking "method std::net::Ipv4Addr::is_benchmarking") and
[`Ipv6Addr::is_benchmarking()`](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html#method.is_benchmarking "method std::net::Ipv6Addr::is_benchmarking") for more details.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-6)Examples

```
#![feature(ip)]

use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(198, 19, 255, 255)).is_benchmarking(), true);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0x2001, 0x2, 0, 0, 0, 0, 0, 0)).is_benchmarking(), true);
```

1.16.0 (const: 1.50.0) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#403)

#### pub const fn [is\_ipv4](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_ipv4)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") if this address is an [`IPv4` address](https://doc.rust-lang.org/std/net/enum.IpAddr.html#variant.V4 "variant std::net::IpAddr::V4"), and [`false`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool")
otherwise.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-7)Examples

```
use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(203, 0, 113, 6)).is_ipv4(), true);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0x2001, 0xdb8, 0, 0, 0, 0, 0, 0)).is_ipv4(), false);
```

1.16.0 (const: 1.50.0) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#424)

#### pub const fn [is\_ipv6](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.is_ipv6)(&self) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Returns [`true`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool") if this address is an [`IPv6` address](https://doc.rust-lang.org/std/net/enum.IpAddr.html#variant.V6 "variant std::net::IpAddr::V6"), and [`false`](https://doc.rust-lang.org/std/primitive.bool.html "primitive bool")
otherwise.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-8)Examples

```
use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

assert_eq!(IpAddr::V4(Ipv4Addr::new(203, 0, 113, 6)).is_ipv6(), false);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0x2001, 0xdb8, 0, 0, 0, 0, 0, 0)).is_ipv6(), true);
```

1.75.0 (const: 1.75.0) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#449)

#### pub const fn [to\_canonical](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.to_canonical)(&self) -> [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

Converts this address to an `IpAddr::V4` if it is an IPv4-mapped IPv6
address, otherwise returns `self` as-is.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-9)Examples

```
use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

let localhost_v4 = Ipv4Addr::new(127, 0, 0, 1);

assert_eq!(IpAddr::V4(localhost_v4).to_canonical(), localhost_v4);
assert_eq!(IpAddr::V6(localhost_v4.to_ipv6_mapped()).to_canonical(), localhost_v4);
assert_eq!(IpAddr::V4(Ipv4Addr::new(127, 0, 0, 1)).to_canonical().is_loopback(), true);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0, 0, 0, 0, 0, 0xffff, 0x7f00, 0x1)).is_loopback(), false);
assert_eq!(IpAddr::V6(Ipv6Addr::new(0, 0, 0, 0, 0, 0xffff, 0x7f00, 0x1)).to_canonical().is_loopback(), true);
```

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#471)

#### pub const fn [as\_octets](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.as_octets)(&self) -> &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)] [ⓘ](https://doc.rust-lang.org/std/net/enum.IpAddr.html)

🔬This is a nightly-only experimental API. (`ip_as_octets` [#137259](https://github.com/rust-lang/rust/issues/137259))

Returns the eight-bit integers this address consists of as a slice.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-10)Examples

```
#![feature(ip_as_octets)]

use std::net::{Ipv4Addr, Ipv6Addr, IpAddr};

assert_eq!(IpAddr::V4(Ipv4Addr::LOCALHOST).as_octets(), &[127, 0, 0, 1]);
assert_eq!(IpAddr::V6(Ipv6Addr::LOCALHOST).as_octets(),
           &[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1])
```

[Source](https://doc.rust-lang.org/src/core/net/parser.rs.html#295)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-IpAddr-1)

### impl [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/parser.rs.html#310)

#### pub fn [parse\_ascii](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.parse_ascii)(b: &[[u8](https://doc.rust-lang.org/std/primitive.u8.html)]) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr"), [AddrParseError](https://doc.rust-lang.org/std/net/struct.AddrParseError.html "struct std::net::AddrParseError")>

🔬This is a nightly-only experimental API. (`addr_parse_ascii` [#101035](https://github.com/rust-lang/rust/issues/101035))

Parse an IP address from a slice of bytes.

```
#![feature(addr_parse_ascii)]

use std::net::{IpAddr, Ipv4Addr, Ipv6Addr};

let localhost_v4 = IpAddr::V4(Ipv4Addr::new(127, 0, 0, 1));
let localhost_v6 = IpAddr::V6(Ipv6Addr::new(0, 0, 0, 0, 0, 0, 0, 1));

assert_eq!(IpAddr::parse_ascii(b"127.0.0.1"), Ok(localhost_v4));
assert_eq!(IpAddr::parse_ascii(b"::1"), Ok(localhost_v6));
```

## Trait Implementations[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#trait-implementations)

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Clone-for-IpAddr)

### impl [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.clone)

#### fn [clone](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)(&self) -> [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

Returns a duplicate of the value. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#tymethod.clone)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/clone.rs.html#245-247)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.clone_from)

#### fn [clone\_from](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)(&mut self, source: &Self)

Performs copy-assignment from `source`. [Read more](https://doc.rust-lang.org/std/clone/trait.Clone.html#method.clone_from)

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1083)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Debug-for-IpAddr)

### impl [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1084)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.fmt)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)(&self, fmt: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Debug.html#tymethod.fmt)

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1073)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Display-for-IpAddr)

### impl [Display](https://doc.rust-lang.org/std/fmt/trait.Display.html "trait std::fmt::Display") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1074)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.fmt-1)

#### fn [fmt](https://doc.rust-lang.org/std/fmt/trait.Display.html#tymethod.fmt)(&self, fmt: &mut [Formatter](https://doc.rust-lang.org/std/fmt/struct.Formatter.html "struct std::fmt::Formatter")<'\_>) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[()](https://doc.rust-lang.org/std/primitive.unit.html), [Error](https://doc.rust-lang.org/std/fmt/struct.Error.html "struct std::fmt::Error")>

Formats the value using the given formatter. [Read more](https://doc.rust-lang.org/std/fmt/trait.Display.html#tymethod.fmt)

1.17.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2323)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-From%3C%5Bu16;+8%5D%3E-for-IpAddr)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[[u16](https://doc.rust-lang.org/std/primitive.u16.html); [8](https://doc.rust-lang.org/std/primitive.array.html)]> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2344)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.from-4)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(segments: [[u16](https://doc.rust-lang.org/std/primitive.u16.html); [8](https://doc.rust-lang.org/std/primitive.array.html)]) -> [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

Creates an `IpAddr::V6` from an eight element 16-bit array.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-15)Examples

```
use std::net::{IpAddr, Ipv6Addr};

let addr = IpAddr::from([
    0x20du16, 0x20cu16, 0x20bu16, 0x20au16,
    0x209u16, 0x208u16, 0x207u16, 0x206u16,
]);
assert_eq!(
    IpAddr::V6(Ipv6Addr::new(
        0x20d, 0x20c, 0x20b, 0x20a,
        0x209, 0x208, 0x207, 0x206,
    )),
    addr
);
```

1.17.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2295)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-From%3C%5Bu8;+16%5D%3E-for-IpAddr)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[[u8](https://doc.rust-lang.org/std/primitive.u8.html); [16](https://doc.rust-lang.org/std/primitive.array.html)]> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2316)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.from-3)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(octets: [[u8](https://doc.rust-lang.org/std/primitive.u8.html); [16](https://doc.rust-lang.org/std/primitive.array.html)]) -> [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

Creates an `IpAddr::V6` from a sixteen element byte array.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-14)Examples

```
use std::net::{IpAddr, Ipv6Addr};

let addr = IpAddr::from([
    0x19u8, 0x18u8, 0x17u8, 0x16u8, 0x15u8, 0x14u8, 0x13u8, 0x12u8,
    0x11u8, 0x10u8, 0x0fu8, 0x0eu8, 0x0du8, 0x0cu8, 0x0bu8, 0x0au8,
]);
assert_eq!(
    IpAddr::V6(Ipv6Addr::new(
        0x1918, 0x1716, 0x1514, 0x1312,
        0x1110, 0x0f0e, 0x0d0c, 0x0b0a,
    )),
    addr
);
```

1.17.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1264)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-From%3C%5Bu8;+4%5D%3E-for-IpAddr)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[[u8](https://doc.rust-lang.org/std/primitive.u8.html); [4](https://doc.rust-lang.org/std/primitive.array.html)]> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1276)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.from-2)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(octets: [[u8](https://doc.rust-lang.org/std/primitive.u8.html); [4](https://doc.rust-lang.org/std/primitive.array.html)]) -> [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

Creates an `IpAddr::V4` from a four element byte array.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-13)Examples

```
use std::net::{IpAddr, Ipv4Addr};

let addr = IpAddr::from([13u8, 12u8, 11u8, 10u8]);
assert_eq!(IpAddr::V4(Ipv4Addr::new(13, 12, 11, 10)), addr);
```

1.16.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1091)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-From%3CIpv4Addr%3E-for-IpAddr)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1107)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.from)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(ipv4: [Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")) -> [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

Copies this address to a new `IpAddr::V4`.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-11)Examples

```
use std::net::{IpAddr, Ipv4Addr};

let addr = Ipv4Addr::new(127, 0, 0, 1);

assert_eq!(
    IpAddr::V4(addr),
    IpAddr::from(addr)
)
```

1.16.0 (const: [unstable](https://github.com/rust-lang/rust/issues/143773 "Tracking issue for const_convert")) · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1114)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-From%3CIpv6Addr%3E-for-IpAddr)

### impl [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<[Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1130)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.from-1)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(ipv6: [Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")) -> [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

Copies this address to a new `IpAddr::V6`.

##### [§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#examples-12)Examples

```
use std::net::{IpAddr, Ipv6Addr};

let addr = Ipv6Addr::new(0, 0, 0, 0, 0, 0xffff, 0xc00a, 0x2ff);

assert_eq!(
    IpAddr::V6(addr),
    IpAddr::from(addr)
);
```

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/parser.rs.html#316)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-FromStr-for-IpAddr)

### impl [FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html "trait std::str::FromStr") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/parser.rs.html#317)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#associatedtype.Err)

#### type [Err](https://doc.rust-lang.org/std/str/trait.FromStr.html#associatedtype.Err) = [AddrParseError](https://doc.rust-lang.org/std/net/struct.AddrParseError.html "struct std::net::AddrParseError")

The associated error which can be returned from parsing.

[Source](https://doc.rust-lang.org/src/core/net/parser.rs.html#318)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.from_str)

#### fn [from\_str](https://doc.rust-lang.org/std/str/trait.FromStr.html#tymethod.from_str)(s: &[str](https://doc.rust-lang.org/std/primitive.str.html)) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr"), [AddrParseError](https://doc.rust-lang.org/std/net/struct.AddrParseError.html "struct std::net::AddrParseError")>

Parses a string `s` to return a value of this type. [Read more](https://doc.rust-lang.org/std/str/trait.FromStr.html#tymethod.from_str)

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Hash-for-IpAddr)

### impl [Hash](https://doc.rust-lang.org/std/hash/trait.Hash.html "trait std::hash::Hash") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.hash)

#### fn [hash](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)<\_\_H>(&self, state: [&mut \_\_H](https://doc.rust-lang.org/std/primitive.reference.html)) where \_\_H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"),

Feeds this value into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#tymethod.hash)

1.3.0 · [Source](https://doc.rust-lang.org/src/core/hash/mod.rs.html#235-237)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.hash_slice)

#### fn [hash\_slice](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)<H>(data: &[Self], state: [&mut H](https://doc.rust-lang.org/std/primitive.reference.html)) where H: [Hasher](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"), Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Feeds a slice of this type into the given [`Hasher`](https://doc.rust-lang.org/std/hash/trait.Hasher.html "trait std::hash::Hasher"). [Read more](https://doc.rust-lang.org/std/hash/trait.Hash.html#method.hash_slice)

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Ord-for-IpAddr)

### impl [Ord](https://doc.rust-lang.org/std/cmp/trait.Ord.html "trait std::cmp::Ord") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.cmp)

#### fn [cmp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)(&self, other: &[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")) -> [Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")

This method returns an [`Ordering`](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering") between `self` and `other`. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#tymethod.cmp)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1023-1025)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.max)

#### fn [max](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the maximum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.max)

1.21.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1062-1064)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.min)

#### fn [min](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)(self, other: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Compares and returns the minimum of two values. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.min)

1.50.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1088-1090)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.clamp)

#### fn [clamp](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)(self, min: Self, max: Self) -> Self where Self: [Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

Restrict a value to a certain interval. [Read more](https://doc.rust-lang.org/std/cmp/trait.Ord.html#method.clamp)

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1175)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialEq%3CIpAddr%3E-for-Ipv4Addr)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")> for [Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1177)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.eq-2)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ne-2)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2158)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialEq%3CIpAddr%3E-for-Ipv6Addr)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")> for [Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2160)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.eq-3)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ne-3)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1164)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialEq%3CIpv4Addr%3E-for-IpAddr)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1166)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.eq-1)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ne-1)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2169)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialEq%3CIpv6Addr%3E-for-IpAddr)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq")<[Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2171)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.eq-4)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ne-4)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialEq-for-IpAddr)

### impl [PartialEq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html "trait std::cmp::PartialEq") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.eq)

#### fn [eq](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#tymethod.eq)(&self, other: &[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `self` and `other` values to be equal, and is used by `==`.

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#264)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ne)

#### fn [ne](https://doc.rust-lang.org/std/cmp/trait.PartialEq.html#method.ne)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests for `!=`. The default implementation is almost always sufficient,
and should not be overridden without very good reason.

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1205)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialOrd%3CIpAddr%3E-for-Ipv4Addr)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd")<[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")> for [Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1207)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.partial_cmp-2)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.lt-2)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.le-2)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.gt-2)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ge-2)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2199)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialOrd%3CIpAddr%3E-for-Ipv6Addr)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd")<[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")> for [Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2201)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.partial_cmp-4)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.lt-4)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.le-4)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.gt-4)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ge-4)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1194)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialOrd%3CIpv4Addr%3E-for-IpAddr)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd")<[Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#1196)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.partial_cmp-1)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[Ipv4Addr](https://doc.rust-lang.org/std/net/struct.Ipv4Addr.html "struct std::net::Ipv4Addr")) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.lt-1)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.le-1)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.gt-1)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ge-1)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.16.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2188)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialOrd%3CIpv6Addr%3E-for-IpAddr)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd")<[Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")> for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#2190)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.partial_cmp-3)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[Ipv6Addr](https://doc.rust-lang.org/std/net/struct.Ipv6Addr.html "struct std::net::Ipv6Addr")) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.lt-3)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.le-3)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.gt-3)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ge-3)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-PartialOrd-for-IpAddr)

### impl [PartialOrd](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html "trait std::cmp::PartialOrd") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.partial_cmp)

#### fn [partial\_cmp](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)(&self, other: &[IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")) -> [Option](https://doc.rust-lang.org/std/option/enum.Option.html "enum std::option::Option")<[Ordering](https://doc.rust-lang.org/std/cmp/enum.Ordering.html "enum std::cmp::Ordering")>

This method returns an ordering between `self` and `other` values if one exists. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#tymethod.partial_cmp)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1399)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.lt)

#### fn [lt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than (for `self` and `other`) and is used by the `<` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.lt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1417)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.le)

#### fn [le](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests less than or equal to (for `self` and `other`) and is used by the
`<=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.le)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1435)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.gt)

#### fn [gt](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than (for `self` and `other`) and is used by the `>`
operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.gt)

1.0.0 · [Source](https://doc.rust-lang.org/src/core/cmp.rs.html#1453)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.ge)

#### fn [ge](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)(&self, other: [&Rhs](https://doc.rust-lang.org/std/primitive.reference.html)) -> [bool](https://doc.rust-lang.org/std/primitive.bool.html)

Tests greater than or equal to (for `self` and `other`) and is used by
the `>=` operator. [Read more](https://doc.rust-lang.org/std/cmp/trait.PartialOrd.html#method.ge)

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Copy-for-IpAddr)

### impl [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html "trait std::marker::Copy") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Eq-for-IpAddr)

### impl [Eq](https://doc.rust-lang.org/std/cmp/trait.Eq.html "trait std::cmp::Eq") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

1.7.0 · [Source](https://doc.rust-lang.org/src/core/net/ip_addr.rs.html#29)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-StructuralPartialEq-for-IpAddr)

### impl [StructuralPartialEq](https://doc.rust-lang.org/std/marker/trait.StructuralPartialEq.html "trait std::marker::StructuralPartialEq") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

## Auto Trait Implementations[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#synthetic-implementations)

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Freeze-for-IpAddr)

### impl [Freeze](https://doc.rust-lang.org/std/marker/trait.Freeze.html "trait std::marker::Freeze") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-RefUnwindSafe-for-IpAddr)

### impl [RefUnwindSafe](https://doc.rust-lang.org/std/panic/trait.RefUnwindSafe.html "trait std::panic::RefUnwindSafe") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Send-for-IpAddr)

### impl [Send](https://doc.rust-lang.org/std/marker/trait.Send.html "trait std::marker::Send") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Sync-for-IpAddr)

### impl [Sync](https://doc.rust-lang.org/std/marker/trait.Sync.html "trait std::marker::Sync") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Unpin-for-IpAddr)

### impl [Unpin](https://doc.rust-lang.org/std/marker/trait.Unpin.html "trait std::marker::Unpin") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-UnwindSafe-for-IpAddr)

### impl [UnwindSafe](https://doc.rust-lang.org/std/panic/trait.UnwindSafe.html "trait std::panic::UnwindSafe") for [IpAddr](https://doc.rust-lang.org/std/net/enum.IpAddr.html "enum std::net::IpAddr")

## Blanket Implementations[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#blanket-implementations)

[Source](https://doc.rust-lang.org/src/core/any.rs.html#138)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Any-for-T)

### impl<T> [Any](https://doc.rust-lang.org/std/any/trait.Any.html "trait std::any::Any") for T where T: 'static + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/any.rs.html#139)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.type_id)

#### fn [type\_id](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)(&self) -> [TypeId](https://doc.rust-lang.org/std/any/struct.TypeId.html "struct std::any::TypeId")

Gets the `TypeId` of `self`. [Read more](https://doc.rust-lang.org/std/any/trait.Any.html#tymethod.type_id)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#212)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Borrow%3CT%3E-for-T)

### impl<T> [Borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html "trait std::borrow::Borrow")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#214)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.borrow)

#### fn [borrow](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)(&self) -> [&T](https://doc.rust-lang.org/std/primitive.reference.html)

Immutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.Borrow.html#tymethod.borrow)

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#221)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-BorrowMut%3CT%3E-for-T)

### impl<T> [BorrowMut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html "trait std::borrow::BorrowMut")<T> for T where T: ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/core/borrow.rs.html#222)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.borrow_mut)

#### fn [borrow\_mut](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)(&mut self) -> [&mut T](https://doc.rust-lang.org/std/primitive.reference.html)

Mutably borrows from an owned value. [Read more](https://doc.rust-lang.org/std/borrow/trait.BorrowMut.html#tymethod.borrow_mut)

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#515)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-CloneToUninit-for-T)

### impl<T> [CloneToUninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html "trait std::clone::CloneToUninit") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/core/clone.rs.html#517)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.clone_to_uninit)

#### unsafe fn [clone\_to\_uninit](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)(&self, dest: [\*mut](https://doc.rust-lang.org/std/primitive.pointer.html) [u8](https://doc.rust-lang.org/std/primitive.u8.html))

🔬This is a nightly-only experimental API. (`clone_to_uninit` [#126799](https://github.com/rust-lang/rust/issues/126799))

Performs copy-assignment from `self` to `dest`. [Read more](https://doc.rust-lang.org/std/clone/trait.CloneToUninit.html#tymethod.clone_to_uninit)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#785)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-From%3CT%3E-for-T)

### impl<T> [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T> for T

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#788)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.from-5)

#### fn [from](https://doc.rust-lang.org/std/convert/trait.From.html#tymethod.from)(t: T) -> T

Returns the argument unchanged.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#767-769)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-Into%3CU%3E-for-T)

### impl<T, U> [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<U> for T where U: [From](https://doc.rust-lang.org/std/convert/trait.From.html "trait std::convert::From")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#777)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.into)

#### fn [into](https://doc.rust-lang.org/std/convert/trait.Into.html#tymethod.into)(self) -> U

Calls `U::from(self)`.

That is, this conversion is whatever the implementation of
`From<T> for U` chooses to do.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#85-87)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-ToOwned-for-T)

### impl<T> [ToOwned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html "trait std::borrow::ToOwned") for T where T: [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html "trait std::clone::Clone"),

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#89)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#associatedtype.Owned)

#### type [Owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#associatedtype.Owned) = T

The resulting type after obtaining ownership.

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#90)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.to_owned)

#### fn [to\_owned](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)(&self) -> T

Creates owned data from borrowed data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#tymethod.to_owned)

[Source](https://doc.rust-lang.org/src/alloc/borrow.rs.html#94)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.clone_into)

#### fn [clone\_into](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)(&self, target: [&mut T](https://doc.rust-lang.org/std/primitive.reference.html))

Uses borrowed data to replace owned data, usually by cloning. [Read more](https://doc.rust-lang.org/std/borrow/trait.ToOwned.html#method.clone_into)

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2796)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-ToString-for-T)

### impl<T> [ToString](https://doc.rust-lang.org/std/string/trait.ToString.html "trait std::string::ToString") for T where T: [Display](https://doc.rust-lang.org/std/fmt/trait.Display.html "trait std::fmt::Display") + ?[Sized](https://doc.rust-lang.org/std/marker/trait.Sized.html "trait std::marker::Sized"),

[Source](https://doc.rust-lang.org/src/alloc/string.rs.html#2798)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.to_string)

#### fn [to\_string](https://doc.rust-lang.org/std/string/trait.ToString.html#tymethod.to_string)(&self) -> [String](https://doc.rust-lang.org/std/string/struct.String.html "struct std::string::String")

Converts the given value to a `String`. [Read more](https://doc.rust-lang.org/std/string/trait.ToString.html#tymethod.to_string)

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#827-829)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-TryFrom%3CU%3E-for-T)

### impl<T, U> [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U> for T where U: [Into](https://doc.rust-lang.org/std/convert/trait.Into.html "trait std::convert::Into")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#831)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#associatedtype.Error-1)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error) = [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#834)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.try_from)

#### fn [try\_from](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#tymethod.try_from)(value: U) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, <T as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<U>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#811-813)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#impl-TryInto%3CU%3E-for-T)

### impl<T, U> [TryInto](https://doc.rust-lang.org/std/convert/trait.TryInto.html "trait std::convert::TryInto")<U> for T where U: [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>,

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#815)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#associatedtype.Error)

#### type [Error](https://doc.rust-lang.org/std/convert/trait.TryInto.html#associatedtype.Error) = <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")

The type returned in the event of a conversion error.

[Source](https://doc.rust-lang.org/src/core/convert/mod.rs.html#818)[§](https://doc.rust-lang.org/std/net/enum.IpAddr.html#method.try_into)

#### fn [try\_into](https://doc.rust-lang.org/std/convert/trait.TryInto.html#tymethod.try_into)(self) -> [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<U, <U as [TryFrom](https://doc.rust-lang.org/std/convert/trait.TryFrom.html "trait std::convert::TryFrom")<T>>::[Error](https://doc.rust-lang.org/std/convert/trait.TryFrom.html#associatedtype.Error "type std::convert::TryFrom::Error")>

Performs the conversion.