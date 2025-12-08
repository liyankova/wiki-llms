---
url: https://nix.dev/manual/nix/2.32/language/import-from-derivation
title: Import From Derivation - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Import From Derivation - Nix 2.32.2 Reference Manual

# [Import From Derivation](https://nix.dev/manual/nix/2.32/language/import-from-derivation#import-from-derivation)

The value of a Nix expression can depend on the contents of a [store object](https://nix.dev/manual/nix/2.32/store/store-object).

Passing an expression `expr` that evaluates to a [store path](https://nix.dev/manual/nix/2.32/store/store-path) to any built-in function which reads from the filesystem constitutes Import From Derivation (IFD):

* [`import`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-import) `expr`
* [`builtins.readFile`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-readFile) `expr`
* [`builtins.readFileType`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-readFileType) `expr`
* [`builtins.readDir`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-readDir) `expr`
* [`builtins.pathExists`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-pathExists) `expr`
* [`builtins.filterSource`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-filterSource) `f expr`
* [`builtins.path`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-path) `{ path = expr; }`
* [`builtins.hashFile`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-hashFile) `t expr`
* `builtins.scopedImport x drv`

When the store path needs to be accessed, evaluation will be paused, the corresponding store object [realised](https://nix.dev/manual/nix/2.32/glossary#gloss-realise), and then evaluation resumed.

This has performance implications:
Evaluation can only finish when all required store objects are realised.
Since the Nix language evaluator is sequential, it only finds store paths to read from one at a time.
While realisation is always parallel, in this case it cannot be done for all required store paths at once, and is therefore much slower than otherwise.

Realising store objects during evaluation can be disabled by setting [`allow-import-from-derivation`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-allow-import-from-derivation) to `false`.
Without IFD it is ensured that evaluation is complete and Nix can produce a build plan before starting any realisation.

## [Example](https://nix.dev/manual/nix/2.32/language/import-from-derivation#example)

In the following Nix expression, the inner derivation `drv` produces a file with contents `hello`.

```
# IFD.nix
let
  drv = derivation {
    name = "hello";
    builder = "/bin/sh";
    args = [ "-c" "echo -n hello > $out" ];
    system = builtins.currentSystem;
  };
in "${builtins.readFile drv} world"
```

```
nix-instantiate IFD.nix --eval --read-write-mode
```

```
building '/nix/store/348q1cal6sdgfxs8zqi9v8llrsn4kqkq-hello.drv'...
"hello world"
```

The contents of the derivation's output have to be [realised](https://nix.dev/manual/nix/2.32/glossary#gloss-realise) before they can be read with [`readFile`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-readFile).
Only then evaluation can continue to produce the final result.

## [Illustration](https://nix.dev/manual/nix/2.32/language/import-from-derivation#illustration)

As a first approximation, the following data flow graph shows how evaluation and building are interleaved, if the value of a Nix expression depends on realising a [store object](https://nix.dev/manual/nix/2.32/store/store-object).
Boxes are data structures, arrow labels are transformations.

```
+----------------------+             +------------------------+
| Nix evaluator        |             | Nix store              |
|  .----------------.  |             |                        |
|  | Nix expression |  |             |                        |
|  '----------------'  |             |                        |
|          |           |             |                        |
|       evaluate       |             |                        |
|          |           |             |                        |
|          V           |             |                        |
|    .------------.    |             |                        |
|    | derivation |    |             |  .------------------.  |
|    | expression |----|-instantiate-|->| store derivation |  |
|    '------------'    |             |  '------------------'  |
|                      |             |           |            |
|                      |             |        realise         |
|                      |             |           |            |
|                      |             |           V            |
|  .----------------.  |             |    .--------------.    |
|  | Nix expression |<-|----read-----|----| store object |    |
|  '----------------'  |             |    '--------------'    |
|          |           |             |                        |
|       evaluate       |             |                        |
|          |           |             |                        |
|          V           |             |                        |
|    .------------.    |             |                        |
|    |   value    |    |             |                        |
|    '------------'    |             |                        |
+----------------------+             +------------------------+
```

In more detail, the following sequence diagram shows how the expression is evaluated step by step, and where evaluation is blocked to wait for the build output to appear.

```
.-------.     .-------------.                        .---------.
|Nix CLI|     |Nix evaluator|                        |Nix store|
'-------'     '-------------'                        '---------'
    |                |                                    |
    |evaluate IFD.nix|                                    |
    |--------------->|                                    |
    |                |                                    |
    |  evaluate `"${readFile drv} world"`                 |
    |                |                                    |
    |    evaluate `readFile drv`                          |
    |                |                                    |
    |   evaluate `drv` as string                          |
    |                |                                    |
    |                |instantiate /nix/store/...-hello.drv|
    |                |----------------------------------->|
    |                :                                    |
    |                :  realise /nix/store/...-hello.drv  |
    |                :----------------------------------->|
    |                :                                    |
    |                                                     |--------.
    |                :                                    |        |
    |      (evaluation blocked)                           |  echo hello > $out
    |                :                                    |        |
    |                                                     |<-------'
    |                :        /nix/store/...-hello        |
    |                |<-----------------------------------|
    |                |                                    |
    |  resume `readFile /nix/store/...-hello`             |
    |                |                                    |
    |                |   readFile /nix/store/...-hello    |
    |                |----------------------------------->|
    |                |                                    |
    |                |               hello                |
    |                |<-----------------------------------|
    |                |                                    |
    |      resume `"${"hello"} world"`                    |
    |                |                                    |
    |        resume `"hello world"`                       |
    |                |                                    |
    | "hello world"  |                                    |
    |<---------------|                                    |
.-------.     .-------------.                        .---------.
|Nix CLI|     |Nix evaluator|                        |Nix store|
'-------'     '-------------'                        '---------'
```