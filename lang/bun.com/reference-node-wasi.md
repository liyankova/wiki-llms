---
url: https://bun.com/reference/node/wasi
title: Node.js wasi module | API Reference | Bun
source_domain: bun.com
---

# Node.js wasi module | API Reference | Bun

Node.js module

# [wasi](https://bun.com/reference/node/wasi)

The `'node:wasi'` module provides an implementation of the WebAssembly System Interface (WASI), allowing WASI-compliant WebAssembly modules to run in Node.js with access to file systems, clocks, and other host functions.

It includes `WASI` class for instantiating and executing WASI modules with configurable filesystem and environment.

Works in Bun

Partially implemented. Specific missing features are not detailed.

* ### class [WASI](https://bun.com/reference/node/wasi/WASI)

  The `WASI` class provides the WASI system call API and additional convenience methods for working with WASI-based applications. Each `WASI` instance represents a distinct environment.

  + readonly [wasiImport](https://bun.com/reference/node/wasi/WASI/wasiImport): Dict<any>

    `wasiImport` is an object that implements the WASI system call API. This object should be passed as the `wasi_snapshot_preview1` import during the instantiation of a [`WebAssembly.Instance`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Instance).
  + [finalizeBindings](https://bun.com/reference/node/wasi/WASI/finalizeBindings)(

    instance: object,

    options?: [FinalizeBindingsOptions](https://bun.com/reference/node/wasi/FinalizeBindingsOptions)

    ): void;

    Set up WASI host bindings to `instance` without calling `initialize()` or `start()`. This method is useful when the WASI module is instantiated in child threads for sharing the memory across threads.

    `finalizeBindings()` requires that either `instance` exports a [`WebAssembly.Memory`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Memory) named `memory` or user specify a [`WebAssembly.Memory`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Memory) object in `options.memory`. If the `memory` is invalid an exception is thrown.

    `start()` and `initialize()` will call `finalizeBindings()` internally. If `finalizeBindings()` is called more than once, an exception is thrown.
  + [getImportObject](https://bun.com/reference/node/wasi/WASI/getImportObject)(): object;

    Return an import object that can be passed to `WebAssembly.instantiate()` if no other WASM imports are needed beyond those provided by WASI.

    If version `unstable` was passed into the constructor it will return:

    ```
    { wasi_unstable: wasi.wasiImport }
    ```

    If version `preview1` was passed into the constructor or no version was specified it will return:

    ```
    { wasi_snapshot_preview1: wasi.wasiImport }
    ```
  + [initialize](https://bun.com/reference/node/wasi/WASI/initialize)(

    instance: object

    ): void;

    Attempt to initialize `instance` as a WASI reactor by invoking its `_initialize()` export, if it is present. If `instance` contains a `_start()` export, then an exception is thrown.

    `initialize()` requires that `instance` exports a [`WebAssembly.Memory`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Memory) named `memory`. If `instance` does not have a `memory` export an exception is thrown.

    If `initialize()` is called more than once, an exception is thrown.
  + [start](https://bun.com/reference/node/wasi/WASI/start)(

    instance: object

    ): number;

    Attempt to begin execution of `instance` as a WASI command by invoking its `_start()` export. If `instance` does not contain a `_start()` export, or if `instance` contains an `_initialize()` export, then an exception is thrown.

    `start()` requires that `instance` exports a [`WebAssembly.Memory`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Memory) named `memory`. If `instance` does not have a `memory` export an exception is thrown.

    If `start()` is called more than once, an exception is thrown.

## Type definitions

* ### interface [FinalizeBindingsOptions](https://bun.com/reference/node/wasi/FinalizeBindingsOptions)

  + [memory](https://bun.com/reference/node/wasi/FinalizeBindingsOptions/memory)?: object
* ### interface [WASIOptions](https://bun.com/reference/node/wasi/WASIOptions)

  + [args](https://bun.com/reference/node/wasi/WASIOptions/args)?: readonly string[]

    An array of strings that the WebAssembly application will see as command line arguments. The first argument is the virtual path to the WASI command itself.
  + [env](https://bun.com/reference/node/wasi/WASIOptions/env)?: object

    An object similar to `process.env` that the WebAssembly application will see as its environment.
  + [preopens](https://bun.com/reference/node/wasi/WASIOptions/preopens)?: Dict<string>

    This object represents the WebAssembly application's sandbox directory structure. The string keys of `preopens` are treated as directories within the sandbox. The corresponding values in `preopens` are the real paths to those directories on the host machine.
  + [returnOnExit](https://bun.com/reference/node/wasi/WASIOptions/returnOnExit)?: boolean

    By default, when WASI applications call `__wasi_proc_exit()` `wasi.start()` will return with the exit code specified rather than terminatng the process. Setting this option to `false` will cause the Node.js process to exit with the specified exit code instead.
  + [stderr](https://bun.com/reference/node/wasi/WASIOptions/stderr)?: number

    The file descriptor used as standard error in the WebAssembly application.
  + [stdin](https://bun.com/reference/node/wasi/WASIOptions/stdin)?: number

    The file descriptor used as standard input in the WebAssembly application.
  + [stdout](https://bun.com/reference/node/wasi/WASIOptions/stdout)?: number

    The file descriptor used as standard output in the WebAssembly application.
  + [version](https://bun.com/reference/node/wasi/WASIOptions/version): 'unstable' | 'preview1'

    The version of WASI requested. Currently the only supported versions are `'unstable'` and `'preview1'`. This option is mandatory.