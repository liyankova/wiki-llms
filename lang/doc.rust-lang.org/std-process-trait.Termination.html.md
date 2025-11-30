---
url: https://doc.rust-lang.org/std/process/trait.Termination.html
title: Termination in std::process - Rust
source_domain: doc.rust-lang.org
---

# Termination in std::process - Rust

## [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html)

[std](https://doc.rust-lang.org/std/index.html)::[process](https://doc.rust-lang.org/std/process/index.html)

# Trait Termination

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2538-2543)

```
pub trait Termination {
    // Required method
    fn report(self) -> ExitCode;
}
```

Expand description

A trait for implementing arbitrary return types in the `main` function.

The C-main function only supports returning integers.
So, every type implementing the `Termination` trait has to be converted
to an integer.

The default implementations are returning `libc::EXIT_SUCCESS` to indicate
a successful execution. In case of a failure, `libc::EXIT_FAILURE` is returned.

Because different runtimes have different specifications on the return value
of the `main` function, this trait is likely to be available only on
standard library’s runtime for convenience. Other runtimes are not required
to provide similar functionality.

## Required Methods[§](https://doc.rust-lang.org/std/process/trait.Termination.html#required-methods)

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2542)

#### fn [report](https://doc.rust-lang.org/std/process/trait.Termination.html#tymethod.report)(self) -> [ExitCode](https://doc.rust-lang.org/std/process/struct.ExitCode.html "struct std::process::ExitCode")

Is called to get the representation of the value as status code.
This status code is returned to the operating system.

## Implementors[§](https://doc.rust-lang.org/std/process/trait.Termination.html#implementors)

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2561-2565)[§](https://doc.rust-lang.org/std/process/trait.Termination.html#impl-Termination-for-Infallible)

### impl [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination") for [Infallible](https://doc.rust-lang.org/std/convert/enum.Infallible.html "enum std::convert::Infallible")

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2554-2558)[§](https://doc.rust-lang.org/std/process/trait.Termination.html#impl-Termination-for-!)

### impl [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination") for [!](https://doc.rust-lang.org/std/primitive.never.html)

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2546-2551)[§](https://doc.rust-lang.org/std/process/trait.Termination.html#impl-Termination-for-())

### impl [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination") for [()](https://doc.rust-lang.org/std/primitive.unit.html)

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2568-2573)[§](https://doc.rust-lang.org/std/process/trait.Termination.html#impl-Termination-for-ExitCode)

### impl [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination") for [ExitCode](https://doc.rust-lang.org/std/process/struct.ExitCode.html "struct std::process::ExitCode")

1.61.0 · [Source](https://doc.rust-lang.org/src/std/process.rs.html#2576-2586)[§](https://doc.rust-lang.org/std/process/trait.Termination.html#impl-Termination-for-Result%3CT,+E%3E)

### impl<T: [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination"), E: [Debug](https://doc.rust-lang.org/std/fmt/trait.Debug.html "trait std::fmt::Debug")> [Termination](https://doc.rust-lang.org/std/process/trait.Termination.html "trait std::process::Termination") for [Result](https://doc.rust-lang.org/std/result/enum.Result.html "enum std::result::Result")<T, E>