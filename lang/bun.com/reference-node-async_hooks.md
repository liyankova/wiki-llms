---
url: https://bun.com/reference/node/async_hooks
title: Node.js async_hooks module | API Reference | Bun
source_domain: bun.com
---

# Node.js async_hooks module | API Reference | Bun

Node.js module

# [async\_hooks](https://bun.com/reference/node/async_hooks)

The `'node:async_hooks'` module provides hooks to track the lifecycle of asynchronous resources in Node.js—init, before, after, and destroy—for tasks like promises, timers, callbacks, and I/O operations.

It's useful for keeping state across async callbacks, measuring performance, or building custom logging and tracing tools in your application.

Works in Bun

AsyncLocalStorage and AsyncResource are implemented. However, v8 promise hooks required for broader compatibility are not called.

* ### namespace [asyncWrapProviders](https://bun.com/reference/node/async_hooks/asyncWrapProviders)

  + const [CHECKPRIMEREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/CHECKPRIMEREQUEST): number
  + const [CIPHERREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/CIPHERREQUEST): number
  + const [DERIVEBITSREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/DERIVEBITSREQUEST): number
  + const [DIRHANDLE](https://bun.com/reference/node/async_hooks/asyncWrapProviders/DIRHANDLE): number
  + const [DNSCHANNEL](https://bun.com/reference/node/async_hooks/asyncWrapProviders/DNSCHANNEL): number
  + const [ELDHISTOGRAM](https://bun.com/reference/node/async_hooks/asyncWrapProviders/ELDHISTOGRAM): number
  + const [FILEHANDLE](https://bun.com/reference/node/async_hooks/asyncWrapProviders/FILEHANDLE): number
  + const [FILEHANDLECLOSEREQ](https://bun.com/reference/node/async_hooks/asyncWrapProviders/FILEHANDLECLOSEREQ): number
  + const [FIXEDSIZEBLOBCOPY](https://bun.com/reference/node/async_hooks/asyncWrapProviders/FIXEDSIZEBLOBCOPY): number
  + const [FSEVENTWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/FSEVENTWRAP): number
  + const [FSREQCALLBACK](https://bun.com/reference/node/async_hooks/asyncWrapProviders/FSREQCALLBACK): number
  + const [FSREQPROMISE](https://bun.com/reference/node/async_hooks/asyncWrapProviders/FSREQPROMISE): number
  + const [GETADDRINFOREQWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/GETADDRINFOREQWRAP): number
  + const [GETNAMEINFOREQWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/GETNAMEINFOREQWRAP): number
  + const [HASHREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HASHREQUEST): number
  + const [HEAPSNAPSHOT](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HEAPSNAPSHOT): number
  + const [HTTP2PING](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HTTP2PING): number
  + const [HTTP2SESSION](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HTTP2SESSION): number
  + const [HTTP2SETTINGS](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HTTP2SETTINGS): number
  + const [HTTP2STREAM](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HTTP2STREAM): number
  + const [HTTPCLIENTREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HTTPCLIENTREQUEST): number
  + const [HTTPINCOMINGMESSAGE](https://bun.com/reference/node/async_hooks/asyncWrapProviders/HTTPINCOMINGMESSAGE): number
  + const [JSSTREAM](https://bun.com/reference/node/async_hooks/asyncWrapProviders/JSSTREAM): number
  + const [JSUDPWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/JSUDPWRAP): number
  + const [KEYEXPORTREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/KEYEXPORTREQUEST): number
  + const [KEYGENREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/KEYGENREQUEST): number
  + const [KEYPAIRGENREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/KEYPAIRGENREQUEST): number
  + const [MESSAGEPORT](https://bun.com/reference/node/async_hooks/asyncWrapProviders/MESSAGEPORT): number
  + const [NONE](https://bun.com/reference/node/async_hooks/asyncWrapProviders/NONE): number
  + const [PBKDF2REQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/PBKDF2REQUEST): number
  + const [PIPECONNECTWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/PIPECONNECTWRAP): number
  + const [PIPESERVERWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/PIPESERVERWRAP): number
  + const [PIPEWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/PIPEWRAP): number
  + const [PROCESSWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/PROCESSWRAP): number
  + const [PROMISE](https://bun.com/reference/node/async_hooks/asyncWrapProviders/PROMISE): number
  + const [QUERYWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/QUERYWRAP): number
  + const [RANDOMBYTESREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/RANDOMBYTESREQUEST): number
  + const [RANDOMPRIMEREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/RANDOMPRIMEREQUEST): number
  + const [SCRYPTREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/SCRYPTREQUEST): number
  + const [SHUTDOWNWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/SHUTDOWNWRAP): number
  + const [SIGINTWATCHDOG](https://bun.com/reference/node/async_hooks/asyncWrapProviders/SIGINTWATCHDOG): number
  + const [SIGNALWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/SIGNALWRAP): number
  + const [SIGNREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/SIGNREQUEST): number
  + const [STATWATCHER](https://bun.com/reference/node/async_hooks/asyncWrapProviders/STATWATCHER): number
  + const [STREAMPIPE](https://bun.com/reference/node/async_hooks/asyncWrapProviders/STREAMPIPE): number
  + const [TCPCONNECTWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/TCPCONNECTWRAP): number
  + const [TCPSERVERWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/TCPSERVERWRAP): number
  + const [TCPWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/TCPWRAP): number
  + const [TLSWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/TLSWRAP): number
  + const [TTYWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/TTYWRAP): number
  + const [UDPSENDWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/UDPSENDWRAP): number
  + const [UDPWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/UDPWRAP): number
  + const [VERIFYREQUEST](https://bun.com/reference/node/async_hooks/asyncWrapProviders/VERIFYREQUEST): number
  + const [WORKER](https://bun.com/reference/node/async_hooks/asyncWrapProviders/WORKER): number
  + const [WORKERHEAPSNAPSHOT](https://bun.com/reference/node/async_hooks/asyncWrapProviders/WORKERHEAPSNAPSHOT): number
  + const [WRITEWRAP](https://bun.com/reference/node/async_hooks/asyncWrapProviders/WRITEWRAP): number
  + const [ZLIB](https://bun.com/reference/node/async_hooks/asyncWrapProviders/ZLIB): number
* ### class [AsyncLocalStorage](https://bun.com/reference/node/async_hooks/AsyncLocalStorage)<T>

  This class creates stores that stay coherent through asynchronous operations.

  While you can create your own implementation on top of the `node:async_hooks` module, `AsyncLocalStorage` should be preferred as it is a performant and memory safe implementation that involves significant optimizations that are non-obvious to implement.

  The following example uses `AsyncLocalStorage` to build a simple logger that assigns IDs to incoming HTTP requests and includes them in messages logged within each request.

  ```
  import http from 'node:http';
  import { AsyncLocalStorage } from 'node:async_hooks';

  const asyncLocalStorage = new AsyncLocalStorage();

  function logWithId(msg) {
    const id = asyncLocalStorage.getStore();
    console.log(`${id !== undefined ? id : '-'}:`, msg);
  }

  let idSeq = 0;
  http.createServer((req, res) => {
    asyncLocalStorage.run(idSeq++, () => {
      logWithId('start');
      // Imagine any chain of async operations here
      setImmediate(() => {
        logWithId('finish');
        res.end();
      });
    });
  }).listen(8080);

  http.get('http://localhost:8080');
  http.get('http://localhost:8080');
  // Prints:
  //   0: start
  //   0: finish
  //   1: start
  //   1: finish
  ```

  Each instance of `AsyncLocalStorage` maintains an independent storage context. Multiple instances can safely exist simultaneously without risk of interfering with each other's data.

  + readonly [name](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/name): string

    The name of the `AsyncLocalStorage` instance if provided.
  + [disable](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/disable)(): void;

    Disables the instance of `AsyncLocalStorage`. All subsequent calls to `asyncLocalStorage.getStore()` will return `undefined` until `asyncLocalStorage.run()` or `asyncLocalStorage.enterWith()` is called again.

    When calling `asyncLocalStorage.disable()`, all current contexts linked to the instance will be exited.

    Calling `asyncLocalStorage.disable()` is required before the `asyncLocalStorage` can be garbage collected. This does not apply to stores provided by the `asyncLocalStorage`, as those objects are garbage collected along with the corresponding async resources.

    Use this method when the `asyncLocalStorage` is not in use anymore in the current process.
  + [enterWith](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/enterWith)(

    store: T

    ): void;

    Transitions into the context for the remainder of the current synchronous execution and then persists the store through any following asynchronous calls.

    Example:

    ```
    const store = { id: 1 };
    // Replaces previous store with the given store object
    asyncLocalStorage.enterWith(store);
    asyncLocalStorage.getStore(); // Returns the store object
    someAsyncOperation(() => {
      asyncLocalStorage.getStore(); // Returns the same object
    });
    ```

    This transition will continue for the *entire* synchronous execution. This means that if, for example, the context is entered within an event handler subsequent event handlers will also run within that context unless specifically bound to another context with an `AsyncResource`. That is why `run()` should be preferred over `enterWith()` unless there are strong reasons to use the latter method.

    ```
    const store = { id: 1 };

    emitter.on('my-event', () => {
      asyncLocalStorage.enterWith(store);
    });
    emitter.on('my-event', () => {
      asyncLocalStorage.getStore(); // Returns the same object
    });

    asyncLocalStorage.getStore(); // Returns undefined
    emitter.emit('my-event');
    asyncLocalStorage.getStore(); // Returns the same object
    ```
  + [exit](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/exit)<R, TArgs extends any[]>(

    callback: (...args: TArgs) => R,

    ...args: TArgs

    ): R;

    Runs a function synchronously outside of a context and returns its return value. The store is not accessible within the callback function or the asynchronous operations created within the callback. Any `getStore()` call done within the callback function will always return `undefined`.

    The optional `args` are passed to the callback function.

    If the callback function throws an error, the error is thrown by `exit()` too. The stacktrace is not impacted by this call and the context is re-entered.

    Example:

    ```
    // Within a call to run
    try {
      asyncLocalStorage.getStore(); // Returns the store object or value
      asyncLocalStorage.exit(() => {
        asyncLocalStorage.getStore(); // Returns undefined
        throw new Error();
      });
    } catch (e) {
      asyncLocalStorage.getStore(); // Returns the same object or value
      // The error will be caught here
    }
    ```
  + [getStore](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/getStore)(): undefined | T;

    Returns the current store. If called outside of an asynchronous context initialized by calling `asyncLocalStorage.run()` or `asyncLocalStorage.enterWith()`, it returns `undefined`.
  + [run](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/run)<R>(

    store: T,

    callback: () => R

    ): R;

    Runs a function synchronously within a context and returns its return value. The store is not accessible outside of the callback function. The store is accessible to any asynchronous operations created within the callback.

    The optional `args` are passed to the callback function.

    If the callback function throws an error, the error is thrown by `run()` too. The stacktrace is not impacted by this call and the context is exited.

    Example:

    ```
    const store = { id: 2 };
    try {
      asyncLocalStorage.run(store, () => {
        asyncLocalStorage.getStore(); // Returns the store object
        setTimeout(() => {
          asyncLocalStorage.getStore(); // Returns the store object
        }, 200);
        throw new Error();
      });
    } catch (e) {
      asyncLocalStorage.getStore(); // Returns undefined
      // The error will be caught here
    }
    ```

    [run](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/run)<R, TArgs extends any[]>(

    store: T,

    callback: (...args: TArgs) => R,

    ...args: TArgs

    ): R;

    Runs a function synchronously within a context and returns its return value. The store is not accessible outside of the callback function. The store is accessible to any asynchronous operations created within the callback.

    The optional `args` are passed to the callback function.

    If the callback function throws an error, the error is thrown by `run()` too. The stacktrace is not impacted by this call and the context is exited.

    Example:

    ```
    const store = { id: 2 };
    try {
      asyncLocalStorage.run(store, () => {
        asyncLocalStorage.getStore(); // Returns the store object
        setTimeout(() => {
          asyncLocalStorage.getStore(); // Returns the store object
        }, 200);
        throw new Error();
      });
    } catch (e) {
      asyncLocalStorage.getStore(); // Returns undefined
      // The error will be caught here
    }
    ```
  + static [bind](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/bind)<Func extends (...args: any[]) => any>(

    fn: Func

    ): Func;

    Binds the given function to the current execution context.

    @param fn

    The function to bind to the current execution context.

    @returns

    A new function that calls `fn` within the captured execution context.
  + static [snapshot](https://bun.com/reference/node/async_hooks/AsyncLocalStorage/snapshot)(): (fn: (...args: TArgs) => R, ...args: TArgs) => R;

    Captures the current execution context and returns a function that accepts a function as an argument. Whenever the returned function is called, it calls the function passed to it within the captured context.

    ```
    const asyncLocalStorage = new AsyncLocalStorage();
    const runInAsyncScope = asyncLocalStorage.run(123, () => AsyncLocalStorage.snapshot());
    const result = asyncLocalStorage.run(321, () => runInAsyncScope(() => asyncLocalStorage.getStore()));
    console.log(result);  // returns 123
    ```

    AsyncLocalStorage.snapshot() can replace the use of AsyncResource for simple async context tracking purposes, for example:

    ```
    class Foo {
      #runInAsyncScope = AsyncLocalStorage.snapshot();

      get() { return this.#runInAsyncScope(() => asyncLocalStorage.getStore()); }
    }

    const foo = asyncLocalStorage.run(123, () => new Foo());
    console.log(asyncLocalStorage.run(321, () => foo.get())); // returns 123
    ```

    @returns

    A new function with the signature `(fn: (...args) : R, ...args) : R`.
* ### class [AsyncResource](https://bun.com/reference/node/async_hooks/AsyncResource)

  The class `AsyncResource` is designed to be extended by the embedder's async resources. Using this, users can easily trigger the lifetime events of their own resources.

  The `init` hook will trigger when an `AsyncResource` is instantiated.

  The following is an overview of the `AsyncResource` API.

  ```
  import { AsyncResource, executionAsyncId } from 'node:async_hooks';

  // AsyncResource() is meant to be extended. Instantiating a
  // new AsyncResource() also triggers init. If triggerAsyncId is omitted then
  // async_hook.executionAsyncId() is used.
  const asyncResource = new AsyncResource(
    type, { triggerAsyncId: executionAsyncId(), requireManualDestroy: false },
  );

  // Run a function in the execution context of the resource. This will
  // * establish the context of the resource
  // * trigger the AsyncHooks before callbacks
  // * call the provided function `fn` with the supplied arguments
  // * trigger the AsyncHooks after callbacks
  // * restore the original execution context
  asyncResource.runInAsyncScope(fn, thisArg, ...args);

  // Call AsyncHooks destroy callbacks.
  asyncResource.emitDestroy();

  // Return the unique ID assigned to the AsyncResource instance.
  asyncResource.asyncId();

  // Return the trigger ID for the AsyncResource instance.
  asyncResource.triggerAsyncId();
  ```

  + [asyncId](https://bun.com/reference/node/async_hooks/AsyncResource/asyncId)(): number;

    @returns

    The unique `asyncId` assigned to the resource.
  + [bind](https://bun.com/reference/node/async_hooks/AsyncResource/bind)<Func extends (...args: any[]) => any>(

    fn: Func

    ): Func;

    Binds the given function to execute to this `AsyncResource`'s scope.

    @param fn

    The function to bind to the current `AsyncResource`.
  + [emitDestroy](https://bun.com/reference/node/async_hooks/AsyncResource/emitDestroy)(): this;

    Call all `destroy` hooks. This should only ever be called once. An error will be thrown if it is called more than once. This **must** be manually called. If the resource is left to be collected by the GC then the `destroy` hooks will never be called.

    @returns

    A reference to `asyncResource`.
  + [runInAsyncScope](https://bun.com/reference/node/async_hooks/AsyncResource/runInAsyncScope)<This, Result>(

    fn: (this: This, ...args: any[]) => Result,

    thisArg?: This,

    ...args: any[]

    ): Result;

    Call the provided function with the provided arguments in the execution context of the async resource. This will establish the context, trigger the AsyncHooks before callbacks, call the function, trigger the AsyncHooks after callbacks, and then restore the original execution context.

    @param fn

    The function to call in the execution context of this async resource.

    @param thisArg

    The receiver to be used for the function call.

    @param args

    Optional arguments to pass to the function.
  + [triggerAsyncId](https://bun.com/reference/node/async_hooks/AsyncResource/triggerAsyncId)(): number;

    @returns

    The same `triggerAsyncId` that is passed to the `AsyncResource` constructor.
  + static [bind](https://bun.com/reference/node/async_hooks/AsyncResource/bind)<Func extends (this: ThisArg, ...args: any[]) => any, ThisArg>(

    fn: Func,

    type?: string,

    thisArg?: ThisArg

    ): Func;

    Binds the given function to the current execution context.

    @param fn

    The function to bind to the current execution context.

    @param type

    An optional name to associate with the underlying `AsyncResource`.
* function [createHook](https://bun.com/reference/node/async_hooks/createHook)(

  callbacks: [HookCallbacks](https://bun.com/reference/node/async_hooks/HookCallbacks)

  ): [AsyncHook](https://bun.com/reference/node/async_hooks/AsyncHook);

  Registers functions to be called for different lifetime events of each async operation.

  The callbacks `init()`/`before()`/`after()`/`destroy()` are called for the respective asynchronous event during a resource's lifetime.

  All callbacks are optional. For example, if only resource cleanup needs to be tracked, then only the `destroy` callback needs to be passed. The specifics of all functions that can be passed to `callbacks` is in the `Hook Callbacks` section.

  ```
  import { createHook } from 'node:async_hooks';

  const asyncHook = createHook({
    init(asyncId, type, triggerAsyncId, resource) { },
    destroy(asyncId) { },
  });
  ```

  The callbacks will be inherited via the prototype chain:

  ```
  class MyAsyncCallbacks {
    init(asyncId, type, triggerAsyncId, resource) { }
    destroy(asyncId) {}
  }

  class MyAddedCallbacks extends MyAsyncCallbacks {
    before(asyncId) { }
    after(asyncId) { }
  }

  const asyncHook = async_hooks.createHook(new MyAddedCallbacks());
  ```

  Because promises are asynchronous resources whose lifecycle is tracked via the async hooks mechanism, the `init()`, `before()`, `after()`, and`destroy()` callbacks *must not* be async functions that return promises.

  @param callbacks

  The `Hook Callbacks` to register

  @returns

  Instance used for disabling and enabling hooks
* function [executionAsyncId](https://bun.com/reference/node/async_hooks/executionAsyncId)(): number;

  ```
  import { executionAsyncId } from 'node:async_hooks';
  import fs from 'node:fs';

  console.log(executionAsyncId());  // 1 - bootstrap
  const path = '.';
  fs.open(path, 'r', (err, fd) => {
    console.log(executionAsyncId());  // 6 - open()
  });
  ```

  The ID returned from `executionAsyncId()` is related to execution timing, not causality (which is covered by `triggerAsyncId()`):

  ```
  const server = net.createServer((conn) => {
    // Returns the ID of the server, not of the new connection, because the
    // callback runs in the execution scope of the server's MakeCallback().
    async_hooks.executionAsyncId();

  }).listen(port, () => {
    // Returns the ID of a TickObject (process.nextTick()) because all
    // callbacks passed to .listen() are wrapped in a nextTick().
    async_hooks.executionAsyncId();
  });
  ```

  Promise contexts may not get precise `executionAsyncIds` by default. See the section on [promise execution tracking](https://nodejs.org/docs/latest-v24.x/api/async_hooks.html#promise-execution-tracking).

  @returns

  The `asyncId` of the current execution context. Useful to track when something calls.
* function [executionAsyncResource](https://bun.com/reference/node/async_hooks/executionAsyncResource)(): object;

  Resource objects returned by `executionAsyncResource()` are most often internal Node.js handle objects with undocumented APIs. Using any functions or properties on the object is likely to crash your application and should be avoided.

  Using `executionAsyncResource()` in the top-level execution context will return an empty object as there is no handle or request object to use, but having an object representing the top-level can be helpful.

  ```
  import { open } from 'node:fs';
  import { executionAsyncId, executionAsyncResource } from 'node:async_hooks';

  console.log(executionAsyncId(), executionAsyncResource());  // 1 {}
  open(new URL(import.meta.url), 'r', (err, fd) => {
    console.log(executionAsyncId(), executionAsyncResource());  // 7 FSReqWrap
  });
  ```

  This can be used to implement continuation local storage without the use of a tracking `Map` to store the metadata:

  ```
  import { createServer } from 'node:http';
  import {
    executionAsyncId,
    executionAsyncResource,
    createHook,
  } from 'node:async_hooks';
  const sym = Symbol('state'); // Private symbol to avoid pollution

  createHook({
    init(asyncId, type, triggerAsyncId, resource) {
      const cr = executionAsyncResource();
      if (cr) {
        resource[sym] = cr[sym];
      }
    },
  }).enable();

  const server = createServer((req, res) => {
    executionAsyncResource()[sym] = { state: req.url };
    setTimeout(function() {
      res.end(JSON.stringify(executionAsyncResource()[sym]));
    }, 100);
  }).listen(3000);
  ```

  @returns

  The resource representing the current execution. Useful to store data within the resource.
* function [triggerAsyncId](https://bun.com/reference/node/async_hooks/triggerAsyncId)(): number;

  ```
  const server = net.createServer((conn) => {
    // The resource that caused (or triggered) this callback to be called
    // was that of the new connection. Thus the return value of triggerAsyncId()
    // is the asyncId of "conn".
    async_hooks.triggerAsyncId();

  }).listen(port, () => {
    // Even though all callbacks passed to .listen() are wrapped in a nextTick()
    // the callback itself exists because the call to the server's .listen()
    // was made. So the return value would be the ID of the server.
    async_hooks.triggerAsyncId();
  });
  ```

  Promise contexts may not get valid `triggerAsyncId`s by default. See the section on [promise execution tracking](https://nodejs.org/docs/latest-v24.x/api/async_hooks.html#promise-execution-tracking).

  @returns

  The ID of the resource responsible for calling the callback that is currently being executed.

## Type definitions

* ### interface [AsyncHook](https://bun.com/reference/node/async_hooks/AsyncHook)

  + [disable](https://bun.com/reference/node/async_hooks/AsyncHook/disable)(): this;

    Disable the callbacks for a given AsyncHook instance from the global pool of AsyncHook callbacks to be executed. Once a hook has been disabled it will not be called again until enabled.
  + [enable](https://bun.com/reference/node/async_hooks/AsyncHook/enable)(): this;

    Enable the callbacks for a given AsyncHook instance. If no callbacks are provided enabling is a noop.
* ### interface [AsyncLocalStorageOptions](https://bun.com/reference/node/async_hooks/AsyncLocalStorageOptions)

  + [defaultValue](https://bun.com/reference/node/async_hooks/AsyncLocalStorageOptions/defaultValue)?: any

    The default value to be used when no store is provided.
  + [name](https://bun.com/reference/node/async_hooks/AsyncLocalStorageOptions/name)?: string

    A name for the `AsyncLocalStorage` value.
* ### interface [AsyncResourceOptions](https://bun.com/reference/node/async_hooks/AsyncResourceOptions)

  + [requireManualDestroy](https://bun.com/reference/node/async_hooks/AsyncResourceOptions/requireManualDestroy)?: boolean

    Disables automatic `emitDestroy` when the object is garbage collected. This usually does not need to be set (even if `emitDestroy` is called manually), unless the resource's `asyncId` is retrieved and the sensitive API's `emitDestroy` is called with it.
  + [triggerAsyncId](https://bun.com/reference/node/async_hooks/AsyncResourceOptions/triggerAsyncId)?: number

    The ID of the execution context that created this async event.
* ### interface [HookCallbacks](https://bun.com/reference/node/async_hooks/HookCallbacks)

  + [after](https://bun.com/reference/node/async_hooks/HookCallbacks/after)(

    asyncId: number

    ): void;

    Called immediately after the callback specified in `before` is completed.

    If an uncaught exception occurs during execution of the callback, then `after` will run after the `'uncaughtException'` event is emitted or a `domain`'s handler runs.

    @param asyncId

    the unique identifier assigned to the resource which has executed the callback.
  + [before](https://bun.com/reference/node/async_hooks/HookCallbacks/before)(

    asyncId: number

    ): void;

    When an asynchronous operation is initiated or completes a callback is called to notify the user. The before callback is called just before said callback is executed.

    @param asyncId

    the unique identifier assigned to the resource about to execute the callback.
  + [destroy](https://bun.com/reference/node/async_hooks/HookCallbacks/destroy)(

    asyncId: number

    ): void;

    Called after the resource corresponding to asyncId is destroyed

    @param asyncId

    a unique ID for the async resource
  + [init](https://bun.com/reference/node/async_hooks/HookCallbacks/init)(

    asyncId: number,

    type: string,

    triggerAsyncId: number,

    resource: object

    ): void;

    Called when a class is constructed that has the possibility to emit an asynchronous event.

    @param asyncId

    A unique ID for the async resource

    @param type

    The type of the async resource

    @param triggerAsyncId

    The unique ID of the async resource in whose execution context this async resource was created

    @param resource

    Reference to the resource representing the async operation, needs to be released during destroy
  + [promiseResolve](https://bun.com/reference/node/async_hooks/HookCallbacks/promiseResolve)(

    asyncId: number

    ): void;

    Called when a promise has resolve() called. This may not be in the same execution id as the promise itself.

    @param asyncId

    the unique id for the promise that was resolve()d.