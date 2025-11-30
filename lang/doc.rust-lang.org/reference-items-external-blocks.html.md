---
url: https://doc.rust-lang.org/reference/items/external-blocks.html
title: External blocks - The Rust Reference
source_domain: doc.rust-lang.org
---

# External blocks - The Rust Reference

[[items.extern]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern "items.extern")

# [External blocks](https://doc.rust-lang.org/reference/items/external-blocks.html#external-blocks)

[[items.extern.syntax]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.syntax "items.extern.syntax")

**Syntax**
  
[ExternBlock](https://doc.rust-lang.org/reference/items/external-blocks.html#railroad-ExternBlock) →   
    unsafe?​[1](https://doc.rust-lang.org/reference/items/external-blocks.html#footnote-unsafe-2024) extern [Abi](https://doc.rust-lang.org/reference/items/functions.html#grammar-Abi)? {   
        [InnerAttribute](https://doc.rust-lang.org/reference/attributes.html#grammar-InnerAttribute)\*   
        [ExternalItem](https://doc.rust-lang.org/reference/items/external-blocks.html#grammar-ExternalItem)\*   
    }

[ExternalItem](https://doc.rust-lang.org/reference/items/external-blocks.html#railroad-ExternalItem) →   
    [OuterAttribute](https://doc.rust-lang.org/reference/attributes.html#grammar-OuterAttribute)\* (   
        [MacroInvocationSemi](https://doc.rust-lang.org/reference/macros.html#grammar-MacroInvocationSemi)   
      | [Visibility](https://doc.rust-lang.org/reference/visibility-and-privacy.html#grammar-Visibility)? [StaticItem](https://doc.rust-lang.org/reference/items/static-items.html#grammar-StaticItem)   
      | [Visibility](https://doc.rust-lang.org/reference/visibility-and-privacy.html#grammar-Visibility)? [Function](https://doc.rust-lang.org/reference/items/functions.html#grammar-Function)   
    )

[[items.extern.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.intro "items.extern.intro")

External blocks provide *declarations* of items that are not *defined* in the
current crate and are the basis of Rust’s foreign function interface. These are
akin to unchecked imports.

[[items.extern.allowed-kinds]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.allowed-kinds "items.extern.allowed-kinds")

Two kinds of item *declarations* are allowed in external blocks: [functions](https://doc.rust-lang.org/reference/items/functions.html) and
[statics](https://doc.rust-lang.org/reference/items/static-items.html).

[[items.extern.safety]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.safety "items.extern.safety")

Calling unsafe functions or accessing unsafe statics that are declared in external blocks is only allowed in an [`unsafe` context](https://doc.rust-lang.org/reference/unsafe-keyword.html).

[[items.extern.namespace]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.namespace "items.extern.namespace")

The external block defines its functions and statics in the [value namespace](https://doc.rust-lang.org/reference/names/namespaces.html) of the module or block where it is located.

[[items.extern.unsafe-required]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.unsafe-required "items.extern.unsafe-required")

The `unsafe` keyword is semantically required to appear before the `extern` keyword on external blocks.

[[items.extern.edition2024]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.edition2024 "items.extern.edition2024")

> 2024 Edition differences
>
> Prior to the 2024 edition, the `unsafe` keyword is optional. The `safe` and `unsafe` item qualifiers are only allowed if the external block itself is marked as `unsafe`.

[[items.extern.fn]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.fn "items.extern.fn")

## [Functions](https://doc.rust-lang.org/reference/items/external-blocks.html#functions)

[[items.extern.fn.body]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.fn.body "items.extern.fn.body")

Functions within external blocks are declared in the same way as other Rust
functions, with the exception that they must not have a body and are instead
terminated by a semicolon.

[[items.extern.fn.param-patterns]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.fn.param-patterns "items.extern.fn.param-patterns")

Patterns are not allowed in parameters, only [IDENTIFIER](https://doc.rust-lang.org/reference/identifiers.html#grammar-IDENTIFIER) or `_` may be used.

[[items.extern.fn.qualifiers]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.fn.qualifiers "items.extern.fn.qualifiers")

The `safe` and `unsafe` function qualifiers are
allowed, but other function qualifiers (e.g. `const`, `async`, `extern`) are
not.

[[items.extern.fn.foreign-abi]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.fn.foreign-abi "items.extern.fn.foreign-abi")

Functions within external blocks may be called by Rust code, just like
functions defined in Rust. The Rust compiler automatically translates between
the Rust ABI and the foreign ABI.

[[items.extern.fn.safety]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.fn.safety "items.extern.fn.safety")

A function declared in an extern block is implicitly `unsafe` unless the `safe`
function qualifier is present.

[[items.extern.fn.fn-ptr]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.fn.fn-ptr "items.extern.fn.fn-ptr")

When coerced to a function pointer, a function declared in an extern block has
type `extern "abi" for<'l1, ..., 'lm> fn(A1, ..., An) -> R`, where `'l1`,
… `'lm` are its lifetime parameters, `A1`, …, `An` are the declared types of
its parameters, `R` is the declared return type.

[[items.extern.static]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.static "items.extern.static")

## [Statics](https://doc.rust-lang.org/reference/items/external-blocks.html#statics)

[[items.extern.static.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.static.intro "items.extern.static.intro")

Statics within external blocks are declared in the same way as [statics](https://doc.rust-lang.org/reference/items/static-items.html) outside of external blocks,
except that they do not have an expression initializing their value.

[[items.extern.static.safety]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.static.safety "items.extern.static.safety")

Unless a static item declared in an extern block is qualified as `safe`, it is `unsafe` to access that item, whether or
not it’s mutable, because there is nothing guaranteeing that the bit pattern at the static’s
memory is valid for the type it is declared with, since some arbitrary (e.g. C) code is in charge
of initializing the static.

[[items.extern.static.mut]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.static.mut "items.extern.static.mut")

Extern statics can be either immutable or mutable just like [statics](https://doc.rust-lang.org/reference/items/static-items.html) outside of external blocks.

[[items.extern.static.read-only]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.static.read-only "items.extern.static.read-only")

An immutable static *must* be initialized before any Rust code is executed. It is not enough for
the static to be initialized before Rust code reads from it.
Once Rust code runs, mutating an immutable static (from inside or outside Rust) is UB,
except if the mutation happens to bytes inside of an `UnsafeCell`.

[[items.extern.abi]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi "items.extern.abi")

## [ABI](https://doc.rust-lang.org/reference/items/external-blocks.html#abi)

[[items.extern.abi.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.intro "items.extern.abi.intro")

By default external blocks assume that the library they are calling uses the
standard C ABI on the specific platform. Other ABIs may be specified using an
`abi` string, as shown here:

```
```
#![allow(unused)]
fn main() {
// Interface to the Windows API
unsafe extern "system" { }
}
```
```

[[items.extern.abi.standard]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.standard "items.extern.abi.standard")

The following ABI strings are supported on all platforms:

[[items.extern.abi.rust]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.rust "items.extern.abi.rust")

* `unsafe extern "Rust"` – The default ABI when you write a normal `fn foo()` in any
  Rust code.

[[items.extern.abi.c]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.c "items.extern.abi.c")

* `unsafe extern "C"` – This is the same as `extern fn foo()`; whatever the default
  your C compiler supports.

[[items.extern.abi.system]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.system "items.extern.abi.system")

* `unsafe extern "system"` – Usually the same as `extern "C"`, except on Win32, in
  which case it’s `"stdcall"`, or what you should use to link to the Windows
  API itself

[[items.extern.abi.unwind]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.unwind "items.extern.abi.unwind")

* `extern "C-unwind"` and `extern "system-unwind"` – identical to `"C"` and `"system"`, respectively, but with [different behavior](https://doc.rust-lang.org/reference/items/functions.html#unwinding) when the callee unwinds (by panicking or throwing a C++ style exception).

[[items.extern.abi.platform]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.platform "items.extern.abi.platform")

There are also some platform-specific ABI strings:

[[items.extern.abi.cdecl]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.cdecl "items.extern.abi.cdecl")

* `unsafe extern "cdecl"` – The default for x86\_32 C code.

[[items.extern.abi.stdcall]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.stdcall "items.extern.abi.stdcall")

* `unsafe extern "stdcall"` – The default for the Win32 API on x86\_32.

[[items.extern.abi.win64]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.win64 "items.extern.abi.win64")

* `unsafe extern "win64"` – The default for C code on x86\_64 Windows.

[[items.extern.abi.sysv64]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.sysv64 "items.extern.abi.sysv64")

* `unsafe extern "sysv64"` – The default for C code on non-Windows x86\_64.

[[items.extern.abi.aapcs]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.aapcs "items.extern.abi.aapcs")

* `unsafe extern "aapcs"` – The default for ARM.

[[items.extern.abi.fastcall]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.fastcall "items.extern.abi.fastcall")

* `unsafe extern "fastcall"` – The `fastcall` ABI – corresponds to MSVC’s
  `__fastcall` and GCC and clang’s `__attribute__((fastcall))`

[[items.extern.abi.thiscall]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.thiscall "items.extern.abi.thiscall")

* `unsafe extern "thiscall"` – The default for C++ member functions on x86\_32 MSVC – corresponds to MSVC’s
  `__thiscall` and GCC and clang’s `__attribute__((thiscall))`

[[items.extern.abi.efiapi]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.efiapi "items.extern.abi.efiapi")

* `unsafe extern "efiapi"` – The ABI used for [UEFI](https://uefi.org/specifications) functions.

[[items.extern.abi.platform-unwind-variants]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.abi.platform-unwind-variants "items.extern.abi.platform-unwind-variants")

Like `"C"` and `"system"`, most platform-specific ABI strings also have a [corresponding `-unwind` variant](https://doc.rust-lang.org/reference/items/functions.html#unwinding); specifically, these are:

* `"aapcs-unwind"`
* `"cdecl-unwind"`
* `"fastcall-unwind"`
* `"stdcall-unwind"`
* `"sysv64-unwind"`
* `"thiscall-unwind"`
* `"win64-unwind"`

[[items.extern.variadic]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.variadic "items.extern.variadic")

## [Variadic functions](https://doc.rust-lang.org/reference/items/external-blocks.html#variadic-functions)

Functions within external blocks may be variadic by specifying `...` as the
last argument. The variadic parameter may optionally be specified with an
identifier.

```
```
#![allow(unused)]
fn main() {
unsafe extern "C" {
    unsafe fn foo(...);
    unsafe fn bar(x: i32, ...);
    unsafe fn with_name(format: *const u8, args: ...);
    // SAFETY: This function guarantees it will not access
    // variadic arguments.
    safe fn ignores_variadic_arguments(x: i32, ...);
}
}
```
```

> Warning
>
> The `safe` qualifier should not be used on a function in an `extern` block unless that function guarantees that it will not access the variadic arguments at all. Passing an unexpected number of arguments or arguments of unexpected type to a variadic function may lead to [undefined behavior](https://doc.rust-lang.org/reference/behavior-considered-undefined.html#r-undefined).

[[items.extern.attributes]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes "items.extern.attributes")

## [Attributes on extern blocks](https://doc.rust-lang.org/reference/items/external-blocks.html#attributes-on-extern-blocks)

[[items.extern.attributes.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.intro "items.extern.attributes.intro")

The following [attributes](https://doc.rust-lang.org/reference/attributes.html) control the behavior of external blocks.

[[items.extern.attributes.link]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link "items.extern.attributes.link")

### [The `link` attribute](https://doc.rust-lang.org/reference/items/external-blocks.html#the-link-attribute)

[[items.extern.attributes.link.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.intro "items.extern.attributes.link.intro")

The *`link` attribute* specifies the name of a native library that the
compiler should link with for the items within an `extern` block.

[[items.extern.attributes.link.syntax]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.syntax "items.extern.attributes.link.syntax")

It uses the [MetaListNameValueStr](https://doc.rust-lang.org/reference/attributes.html#grammar-MetaListNameValueStr) syntax to specify its inputs. The `name` key is the
name of the native library to link. The `kind` key is an optional value which
specifies the kind of library with the following possible values:

[[items.extern.attributes.link.dylib]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.dylib "items.extern.attributes.link.dylib")

* `dylib` — Indicates a dynamic library. This is the default if `kind` is not
  specified.

[[items.extern.attributes.link.static]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.static "items.extern.attributes.link.static")

* `static` — Indicates a static library.

[[items.extern.attributes.link.framework]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.framework "items.extern.attributes.link.framework")

* `framework` — Indicates a macOS framework. This is only valid for macOS
  targets.

[[items.extern.attributes.link.raw-dylib]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.raw-dylib "items.extern.attributes.link.raw-dylib")

* `raw-dylib` — Indicates a dynamic library where the compiler will generate
  an import library to link against (see [`dylib` versus `raw-dylib`](https://doc.rust-lang.org/reference/items/external-blocks.html#dylib-versus-raw-dylib) below
  for details). This is only valid for Windows targets.

[[items.extern.attributes.link.name-requirement]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.name-requirement "items.extern.attributes.link.name-requirement")

The `name` key must be included if `kind` is specified.

[[items.extern.attributes.link.modifiers]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers "items.extern.attributes.link.modifiers")

The optional `modifiers` argument is a way to specify linking modifiers for the
library to link.

[[items.extern.attributes.link.modifiers.syntax]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.syntax "items.extern.attributes.link.modifiers.syntax")

Modifiers are specified as a comma-delimited string with each modifier prefixed
with either a `+` or `-` to indicate that the modifier is enabled or disabled,
respectively.

[[items.extern.attributes.link.modifiers.multiple]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.multiple "items.extern.attributes.link.modifiers.multiple")

Specifying multiple `modifiers` arguments in a single `link` attribute,
or multiple identical modifiers in the same `modifiers` argument is not currently supported.   
Example: `#[link(name = "mylib", kind = "static", modifiers = "+whole-archive")]`.

[[items.extern.attributes.link.wasm\_import\_module]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.wasm_import_module "items.extern.attributes.link.wasm_import_module")

The `wasm_import_module` key may be used to specify the [WebAssembly module](https://webassembly.github.io/spec/core/syntax/modules.html)
name for the items within an `extern` block when importing symbols from the
host environment. The default module name is `env` if `wasm_import_module` is
not specified.

```
#[link(name = "crypto")]
unsafe extern {
    // …
}

#[link(name = "CoreFoundation", kind = "framework")]
unsafe extern {
    // …
}

#[link(wasm_import_module = "foo")]
unsafe extern {
    // …
}
```

[[items.extern.attributes.link.empty-block]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.empty-block "items.extern.attributes.link.empty-block")

It is valid to add the `link` attribute on an empty extern block. You can use
this to satisfy the linking requirements of extern blocks elsewhere in your
code (including upstream crates) instead of adding the attribute to each extern
block.

[[items.extern.attributes.link.modifiers.bundle]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.bundle "items.extern.attributes.link.modifiers.bundle")

#### [Linking modifiers: `bundle`](https://doc.rust-lang.org/reference/items/external-blocks.html#linking-modifiers-bundle)

[[items.extern.attributes.link.modifiers.bundle.allowed-kinds]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.bundle.allowed-kinds "items.extern.attributes.link.modifiers.bundle.allowed-kinds")

This modifier is only compatible with the `static` linking kind.
Using any other kind will result in a compiler error.

[[items.extern.attributes.link.modifiers.bundle.behavior]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.bundle.behavior "items.extern.attributes.link.modifiers.bundle.behavior")

When building a rlib or staticlib `+bundle` means that the native static library
will be packed into the rlib or staticlib archive, and then retrieved from there
during linking of the final binary.

[[items.extern.attributes.link.modifiers.bundle.behavior-negative]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.bundle.behavior-negative "items.extern.attributes.link.modifiers.bundle.behavior-negative")

When building a rlib `-bundle` means that the native static library is registered as a dependency
of that rlib “by name”, and object files from it are included only during linking of the final
binary, the file search by that name is also performed during final linking.   
When building a staticlib `-bundle` means that the native static library is simply not included
into the archive and some higher level build system will need to add it later during linking of
the final binary.

[[items.extern.attributes.link.modifiers.bundle.no-effect]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.bundle.no-effect "items.extern.attributes.link.modifiers.bundle.no-effect")

This modifier has no effect when building other targets like executables or dynamic libraries.

[[items.extern.attributes.link.modifiers.bundle.default]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.bundle.default "items.extern.attributes.link.modifiers.bundle.default")

The default for this modifier is `+bundle`.

More implementation details about this modifier can be found in
[`bundle` documentation for rustc](https://doc.rust-lang.org/rustc/command-line-arguments.html#linking-modifiers-bundle).

[[items.extern.attributes.link.modifiers.whole-archive]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.whole-archive "items.extern.attributes.link.modifiers.whole-archive")

#### [Linking modifiers: `whole-archive`](https://doc.rust-lang.org/reference/items/external-blocks.html#linking-modifiers-whole-archive)

[[items.extern.attributes.link.modifiers.whole-archive.allowed-kinds]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.whole-archive.allowed-kinds "items.extern.attributes.link.modifiers.whole-archive.allowed-kinds")

This modifier is only compatible with the `static` linking kind.
Using any other kind will result in a compiler error.

[[items.extern.attributes.link.modifiers.whole-archive.behavior]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.whole-archive.behavior "items.extern.attributes.link.modifiers.whole-archive.behavior")

`+whole-archive` means that the static library is linked as a whole archive
without throwing any object files away.

[[items.extern.attributes.link.modifiers.whole-archive.default]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.whole-archive.default "items.extern.attributes.link.modifiers.whole-archive.default")

The default for this modifier is `-whole-archive`.

More implementation details about this modifier can be found in
[`whole-archive` documentation for rustc](https://doc.rust-lang.org/rustc/command-line-arguments.html#linking-modifiers-whole-archive).

[[items.extern.attributes.link.modifiers.verbatim]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.verbatim "items.extern.attributes.link.modifiers.verbatim")

### [Linking modifiers: `verbatim`](https://doc.rust-lang.org/reference/items/external-blocks.html#linking-modifiers-verbatim)

[[items.extern.attributes.link.modifiers.verbatim.allowed-kinds]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.verbatim.allowed-kinds "items.extern.attributes.link.modifiers.verbatim.allowed-kinds")

This modifier is compatible with all linking kinds.

[[items.extern.attributes.link.modifiers.verbatim.behavior]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.verbatim.behavior "items.extern.attributes.link.modifiers.verbatim.behavior")

`+verbatim` means that rustc itself won’t add any target-specified library prefixes or suffixes
(like `lib` or `.a`) to the library name, and will try its best to ask for the same thing from the
linker.

[[items.extern.attributes.link.modifiers.verbatim.behavior-negative]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.verbatim.behavior-negative "items.extern.attributes.link.modifiers.verbatim.behavior-negative")

`-verbatim` means that rustc will either add a target-specific prefix and suffix to the library
name before passing it to linker, or won’t prevent linker from implicitly adding it.

[[items.extern.attributes.link.modifiers.verbatim.default]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.modifiers.verbatim.default "items.extern.attributes.link.modifiers.verbatim.default")

The default for this modifier is `-verbatim`.

More implementation details about this modifier can be found in
[`verbatim` documentation for rustc](https://doc.rust-lang.org/rustc/command-line-arguments.html#linking-modifiers-verbatim).

[[items.extern.attributes.link.kind-raw-dylib]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.kind-raw-dylib "items.extern.attributes.link.kind-raw-dylib")

#### [`dylib` versus `raw-dylib`](https://doc.rust-lang.org/reference/items/external-blocks.html#dylib-versus-raw-dylib)

[[items.extern.attributes.link.kind-raw-dylib.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.kind-raw-dylib.intro "items.extern.attributes.link.kind-raw-dylib.intro")

On Windows, linking against a dynamic library requires that an import library
is provided to the linker: this is a special static library that declares all
of the symbols exported by the dynamic library in such a way that the linker
knows that they have to be dynamically loaded at runtime.

[[items.extern.attributes.link.kind-raw-dylib.import]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.kind-raw-dylib.import "items.extern.attributes.link.kind-raw-dylib.import")

Specifying `kind = "dylib"` instructs the Rust compiler to link an import
library based on the `name` key. The linker will then use its normal library
resolution logic to find that import library. Alternatively, specifying
`kind = "raw-dylib"` instructs the compiler to generate an import library
during compilation and provide that to the linker instead.

[[items.extern.attributes.link.kind-raw-dylib.platform-specific]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.kind-raw-dylib.platform-specific "items.extern.attributes.link.kind-raw-dylib.platform-specific")

`raw-dylib` is only supported on Windows. Using it when targeting other
platforms will result in a compiler error.

[[items.extern.attributes.link.import\_name\_type]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.import_name_type "items.extern.attributes.link.import_name_type")

#### [The `import_name_type` key](https://doc.rust-lang.org/reference/items/external-blocks.html#the-import_name_type-key)

[[items.extern.attributes.link.import\_name\_type.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.import_name_type.intro "items.extern.attributes.link.import_name_type.intro")

On x86 Windows, names of functions are “decorated” (i.e., have a specific prefix
and/or suffix added) to indicate their calling convention. For example, a
`stdcall` calling convention function with the name `fn1` that has no arguments
would be decorated as `_fn1@0`. However, the [PE Format](https://learn.microsoft.com/windows/win32/debug/pe-format#import-name-type) does also permit names
to have no prefix or be undecorated. Additionally, the MSVC and GNU toolchains
use different decorations for the same calling conventions which means, by
default, some Win32 functions cannot be called using the `raw-dylib` link kind
via the GNU toolchain.

[[items.extern.attributes.link.import\_name\_type.values]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.import_name_type.values "items.extern.attributes.link.import_name_type.values")

To allow for these differences, when using the `raw-dylib` link kind you may
also specify the `import_name_type` key with one of the following values to
change how functions are named in the generated import library:

* `decorated`: The function name will be fully-decorated using the MSVC
  toolchain format.
* `noprefix`: The function name will be decorated using the MSVC toolchain
  format, but skipping the leading `?`, `@`, or optionally `_`.
* `undecorated`: The function name will not be decorated.

[[items.extern.attributes.link.import\_name\_type.default]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.import_name_type.default "items.extern.attributes.link.import_name_type.default")

If the `import_name_type` key is not specified, then the function name will be
fully-decorated using the target toolchain’s format.

[[items.extern.attributes.link.import\_name\_type.variables]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.import_name_type.variables "items.extern.attributes.link.import_name_type.variables")

Variables are never decorated and so the `import_name_type` key has no effect on
how they are named in the generated import library.

[[items.extern.attributes.link.import\_name\_type.platform-specific]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link.import_name_type.platform-specific "items.extern.attributes.link.import_name_type.platform-specific")

The `import_name_type` key is only supported on x86 Windows. Using it when
targeting other platforms will result in a compiler error.

[[items.extern.attributes.link\_name]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_name "items.extern.attributes.link_name")

### [The `link_name` attribute](https://doc.rust-lang.org/reference/items/external-blocks.html#the-link_name-attribute)

[[items.extern.attributes.link\_name.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_name.intro "items.extern.attributes.link_name.intro")

The *`link_name` [attribute](https://doc.rust-lang.org/reference/attributes.html)* may be applied to declarations inside an `extern` block to specify the symbol to import for the given function or static.

> Example
>
> ```
> ```
> #![allow(unused)]
> fn main() {
> unsafe extern "C" {
>     #[link_name = "actual_symbol_name"]
>     safe fn name_in_rust();
> }
> }
> ```
> ```

[[items.extern.attributes.link\_name.syntax]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_name.syntax "items.extern.attributes.link_name.syntax")

The `link_name` attribute uses the [MetaNameValueStr](https://doc.rust-lang.org/reference/attributes.html#grammar-MetaNameValueStr) syntax.

[[items.extern.attributes.link\_name.allowed-positions]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_name.allowed-positions "items.extern.attributes.link_name.allowed-positions")

The `link_name` attribute may only be applied to a function or static item in an `extern` block.

> Note
>
> `rustc` ignores use in other positions but lints against it. This may become an error in the future.

[[items.extern.attributes.link\_name.duplicates]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_name.duplicates "items.extern.attributes.link_name.duplicates")

Only the last use of `link_name` on an item has effect.

> Note
>
> `rustc` lints against any use preceding the last. This may become an error in the future.

[[items.extern.attributes.link\_name.link\_ordinal]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_name.link_ordinal "items.extern.attributes.link_name.link_ordinal")

The `link_name` attribute may not be used with the [`link_ordinal`](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_ordinal) attribute.

[[items.extern.attributes.link\_ordinal]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_ordinal "items.extern.attributes.link_ordinal")

### [The `link_ordinal` attribute](https://doc.rust-lang.org/reference/items/external-blocks.html#the-link_ordinal-attribute)

[[items.extern.attributes.link\_ordinal.intro]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_ordinal.intro "items.extern.attributes.link_ordinal.intro")

The *`link_ordinal` attribute* can be applied on declarations inside an `extern`
block to indicate the numeric ordinal to use when generating the import library
to link against. An ordinal is a unique number per symbol exported by a dynamic
library on Windows and can be used when the library is being loaded to find
that symbol rather than having to look it up by name.

> Warning
>
> `link_ordinal` should only be used in cases where the ordinal of the symbol is known to be stable: if the ordinal of a symbol is not explicitly set when its containing binary is built then one will be automatically assigned to it, and that assigned ordinal may change between builds of the binary.

```
```
#![allow(unused)]
fn main() {
#[cfg(all(windows, target_arch = "x86"))]
#[link(name = "exporter", kind = "raw-dylib")]
unsafe extern "stdcall" {
    #[link_ordinal(15)]
    safe fn imported_function_stdcall(i: i32);
}
}
```
```

[[items.extern.attributes.link\_ordinal.allowed-kinds]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_ordinal.allowed-kinds "items.extern.attributes.link_ordinal.allowed-kinds")

This attribute is only used with the `raw-dylib` linking kind.
Using any other kind will result in a compiler error.

[[items.extern.attributes.link\_ordinal.exclusive]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.link_ordinal.exclusive "items.extern.attributes.link_ordinal.exclusive")

Using this attribute with the `link_name` attribute will result in a
compiler error.

[[items.extern.attributes.fn-parameters]](https://doc.rust-lang.org/reference/items/external-blocks.html#r-items.extern.attributes.fn-parameters "items.extern.attributes.fn-parameters")

### [Attributes on function parameters](https://doc.rust-lang.org/reference/items/external-blocks.html#attributes-on-function-parameters)

Attributes on extern function parameters follow the same rules and
restrictions as [regular function parameters](https://doc.rust-lang.org/reference/items/functions.html#attributes-on-function-parameters).

---

1. Starting with the 2024 Edition, the `unsafe` keyword is required semantically. [↩](https://doc.rust-lang.org/reference/items/external-blocks.html#fr-unsafe-2024-1)