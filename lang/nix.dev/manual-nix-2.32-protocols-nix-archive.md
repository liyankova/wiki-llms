---
url: https://nix.dev/manual/nix/2.32/protocols/nix-archive
title: Nix Archive (NAR) Format - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Nix Archive (NAR) Format - Nix 2.32.2 Reference Manual

# [Nix Archive (NAR) format](https://nix.dev/manual/nix/2.32/protocols/nix-archive#nix-archive-nar-format)

This is the complete specification of the [Nix Archive](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#nix-archive) format.
The Nix Archive format closely follows the abstract specification of a [file system object](https://nix.dev/manual/nix/2.32/store/file-system-object) tree,
because it is designed to serialize exactly that data structure.

The format of this specification is close to [Extended Backus–Naur form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form), with the exception of the `str(..)` function / parameterized rule, which length-prefixes and pads strings.
This makes the resulting binary format easier to parse.

Regular users do *not* need to know this information.
But for those interested in exactly how Nix works, e.g. if they are reimplementing it, this information can be useful.

```
nar = str("nix-archive-1"), nar-obj;

nar-obj = str("("), nar-obj-inner, str(")");

nar-obj-inner
  = str("type"), str("regular") regular
  | str("type"), str("symlink") symlink
  | str("type"), str("directory") directory
  ;

regular = [ str("executable") ], str("contents"), str(contents);

symlink = str("target"), str(target);

(* side condition: directory entries must be ordered by their names *)
directory = { directory-entry };

directory-entry = str("entry"), str("("), str("name"), str(name), str("node"), nar-obj, str(")");
```

The `str` function / parameterized rule is defined as follows:

* `str(s)` = `int(|s|), pad(s);`
* `int(n)` = the 64-bit little endian representation of the number `n`
* `pad(s)` = the byte sequence `s`, padded with 0s to a multiple of 8 byte