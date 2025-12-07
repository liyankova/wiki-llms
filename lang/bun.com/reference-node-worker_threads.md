---
url: https://bun.com/reference/node/worker_threads
title: Node.js worker_threads module | API Reference | Bun
source_domain: bun.com
---

# Node.js worker_threads module | API Reference | Bun

Node.js module

# [worker\_threads](https://bun.com/reference/node/worker_threads)

The `'node:worker_threads'` module enables multithreaded execution in Node.js by spawning Worker threads that run JavaScript in isolated V8 instances.

Features include message passing, transferable objects, SharedArrayBuffer support, and performance measurement, allowing compute-intensive tasks to be offloaded from the main event loop.

Works in Bun

Core worker creation and communication works. Several worker options (stdio, resourceLimits, etc.) and some advanced methods related to transferable objects and heap snapshots are not supported.

* ### class [BroadcastChannel](https://bun.com/reference/node/worker_threads/BroadcastChannel)

  Instances of `BroadcastChannel` allow asynchronous one-to-many communication with all other `BroadcastChannel` instances bound to the same channel name.

  ```
  'use strict';

  import {
    isMainThread,
    BroadcastChannel,
    Worker,
  } from 'node:worker_threads';

  const bc = new BroadcastChannel('hello');

  if (isMainThread) {
    let c = 0;
    bc.onmessage = (event) => {
      console.log(event.data);
      if (++c === 10) bc.close();
    };
    for (let n = 0; n < 10; n++)
      new Worker(__filename);
  } else {
    bc.postMessage('hello from every worker');
    bc.close();
  }
  ```

  + readonly [name](https://bun.com/reference/node/worker_threads/BroadcastChannel/name): string
  + [onmessage](https://bun.com/reference/node/worker_threads/BroadcastChannel/onmessage): (message: MessageEvent) => void

    Invoked with a single `MessageEvent` argument when a message is received.
  + [onmessageerror](https://bun.com/reference/node/worker_threads/BroadcastChannel/onmessageerror): (message: MessageEvent) => void

    Invoked with a received message cannot be deserialized.
  + [addEventListener](https://bun.com/reference/node/worker_threads/BroadcastChannel/addEventListener)(

    type: string,

    callback: null | EventListenerOrEventListenerObject,

    options?: boolean | [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

    ): void;

    Appends an event listener for events whose type attribute value is type. The callback argument sets the callback that will be invoked when the event is dispatched.

    The options argument sets listener-specific options. For compatibility this can be a boolean, in which case the method behaves exactly as if the value was specified as options's capture.

    When set to true, options's capture prevents callback from being invoked when the event's eventPhase attribute value is BUBBLING\_PHASE. When false (or not present), callback will not be invoked when event's eventPhase attribute value is CAPTURING\_PHASE. Either way, callback will be invoked if event's eventPhase attribute value is AT\_TARGET.

    When set to true, options's passive indicates that the callback will not cancel the event by invoking preventDefault(). This is used to enable performance optimizations described in § 2.8 Observing event listeners.

    When set to true, options's once indicates that the callback will only be invoked once after which the event listener will be removed.

    If an AbortSignal is passed for options's signal, then the event listener will be removed when signal is aborted.

    The event listener is appended to target's event listener list and is not appended if it has the same type, callback, and capture.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener)

    [addEventListener](https://bun.com/reference/node/worker_threads/BroadcastChannel/addEventListener)(

    type: string,

    listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

    options?: boolean | [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

    ): void;

    Adds a new handler for the `type` event. Any given `listener` is added only once per `type` and per `capture` option value.

    If the `once` option is true, the `listener` is removed after the next time a `type` event is dispatched.

    The `capture` option is not used by Node.js in any functional way other than tracking registered event listeners per the `EventTarget` specification. Specifically, the `capture` option is used as part of the key when registering a `listener`. Any individual `listener` may be added once with `capture = false`, and once with `capture = true`.
  + [close](https://bun.com/reference/node/worker_threads/BroadcastChannel/close)(): void;

    Closes the `BroadcastChannel` connection.
  + [dispatchEvent](https://bun.com/reference/node/worker_threads/BroadcastChannel/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [postMessage](https://bun.com/reference/node/worker_threads/BroadcastChannel/postMessage)(

    message: unknown

    ): void;

    @param message

    Any cloneable JavaScript value.
  + [ref](https://bun.com/reference/node/worker_threads/BroadcastChannel/ref)(): this;
  + [removeEventListener](https://bun.com/reference/node/worker_threads/BroadcastChannel/removeEventListener)(

    type: string,

    callback: null | EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/node/worker_threads/BroadcastChannel/removeEventListener)(

    type: string,

    listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

    options?: boolean | [EventListenerOptions](https://bun.com/reference/bun/EventListenerOptions)

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.
  + [unref](https://bun.com/reference/node/worker_threads/BroadcastChannel/unref)(): this;
* ### class [MessageChannel](https://bun.com/reference/node/worker_threads/MessageChannel)

  Instances of the `worker.MessageChannel` class represent an asynchronous, two-way communications channel. The `MessageChannel` has no methods of its own. `new MessageChannel()` yields an object with `port1` and `port2` properties, which refer to linked `MessagePort` instances.

  ```
  import { MessageChannel } from 'node:worker_threads';

  const { port1, port2 } = new MessageChannel();
  port1.on('message', (message) => console.log('received', message));
  port2.postMessage({ foo: 'bar' });
  // Prints: received { foo: 'bar' } from the `port1.on('message')` listener
  ```

  + readonly [port1](https://bun.com/reference/node/worker_threads/MessageChannel/port1): [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort)
  + readonly [port2](https://bun.com/reference/node/worker_threads/MessageChannel/port2): [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort)
* ### class [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort)

  Instances of the `worker.MessagePort` class represent one end of an asynchronous, two-way communications channel. It can be used to transfer structured data, memory regions and other `MessagePort`s between different `Worker`s.

  This implementation matches [browser `MessagePort`](https://developer.mozilla.org/en-US/docs/Web/API/MessagePort) s.

  + [addEventListener](https://bun.com/reference/node/worker_threads/MessagePort/addEventListener)(

    type: string,

    callback: null | EventListenerOrEventListenerObject,

    options?: boolean | [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

    ): void;

    Appends an event listener for events whose type attribute value is type. The callback argument sets the callback that will be invoked when the event is dispatched.

    The options argument sets listener-specific options. For compatibility this can be a boolean, in which case the method behaves exactly as if the value was specified as options's capture.

    When set to true, options's capture prevents callback from being invoked when the event's eventPhase attribute value is BUBBLING\_PHASE. When false (or not present), callback will not be invoked when event's eventPhase attribute value is CAPTURING\_PHASE. Either way, callback will be invoked if event's eventPhase attribute value is AT\_TARGET.

    When set to true, options's passive indicates that the callback will not cancel the event by invoking preventDefault(). This is used to enable performance optimizations described in § 2.8 Observing event listeners.

    When set to true, options's once indicates that the callback will only be invoked once after which the event listener will be removed.

    If an AbortSignal is passed for options's signal, then the event listener will be removed when signal is aborted.

    The event listener is appended to target's event listener list and is not appended if it has the same type, callback, and capture.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/addEventListener)

    [addEventListener](https://bun.com/reference/node/worker_threads/MessagePort/addEventListener)(

    type: string,

    listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

    options?: boolean | [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

    ): void;

    Adds a new handler for the `type` event. Any given `listener` is added only once per `type` and per `capture` option value.

    If the `once` option is true, the `listener` is removed after the next time a `type` event is dispatched.

    The `capture` option is not used by Node.js in any functional way other than tracking registered event listeners per the `EventTarget` specification. Specifically, the `capture` option is used as part of the key when registering a `listener`. Any individual `listener` may be added once with `capture = false`, and once with `capture = true`.
  + [addListener](https://bun.com/reference/node/worker_threads/MessagePort/addListener)(

    event: 'close',

    listener: (ev: [Event](https://bun.com/reference/globals/Event)) => void

    ): this;

    Node.js-specific extension to the `EventTarget` class that emulates the equivalent `EventEmitter` API. The only difference between `addListener()` and `addEventListener()` is that `addListener()` will return a reference to the `EventTarget`.

    [addListener](https://bun.com/reference/node/worker_threads/MessagePort/addListener)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [addListener](https://bun.com/reference/node/worker_threads/MessagePort/addListener)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [addListener](https://bun.com/reference/node/worker_threads/MessagePort/addListener)(

    event: string,

    listener: (arg: any) => void

    ): this;
  + [close](https://bun.com/reference/node/worker_threads/MessagePort/close)(): void;

    Disables further sending of messages on either side of the connection. This method can be called when no further communication will happen over this `MessagePort`.

    The `'close' event` is emitted on both `MessagePort` instances that are part of the channel.
  + [dispatchEvent](https://bun.com/reference/node/worker_threads/MessagePort/dispatchEvent)(

    event: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
  + [emit](https://bun.com/reference/node/worker_threads/MessagePort/emit)(

    event: 'close',

    ev: [Event](https://bun.com/reference/globals/Event)

    ): boolean;

    Node.js-specific extension to the `EventTarget` class that dispatches the `arg` to the list of handlers for `type`.

    @returns

    `true` if event listeners registered for the `type` exist, otherwise `false`.

    [emit](https://bun.com/reference/node/worker_threads/MessagePort/emit)(

    event: 'message',

    value: any

    ): boolean;

    [emit](https://bun.com/reference/node/worker_threads/MessagePort/emit)(

    event: 'messageerror',

    error: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/worker_threads/MessagePort/emit)(

    event: string,

    arg: any

    ): boolean;
  + [eventNames](https://bun.com/reference/node/worker_threads/MessagePort/eventNames)(): string[];

    Node.js-specific extension to the `EventTarget` class that returns an array of event `type` names for which event listeners are registered.
  + [getMaxListeners](https://bun.com/reference/node/worker_threads/MessagePort/getMaxListeners)(): number;

    Node.js-specific extension to the `EventTarget` class that returns the number of max event listeners.
  + [hasRef](https://bun.com/reference/node/worker_threads/MessagePort/hasRef)(): boolean;

    If true, the `MessagePort` object will keep the Node.js event loop active.
  + [listenerCount](https://bun.com/reference/node/worker_threads/MessagePort/listenerCount)(

    type: string

    ): number;

    Node.js-specific extension to the `EventTarget` class that returns the number of event listeners registered for the `type`.
  + [off](https://bun.com/reference/node/worker_threads/MessagePort/off)(

    event: 'close',

    listener: (ev: [Event](https://bun.com/reference/globals/Event)) => void,

    options?: EventListenerOptions

    ): this;

    Node.js-specific alias for `eventTarget.removeEventListener()`.

    [off](https://bun.com/reference/node/worker_threads/MessagePort/off)(

    event: 'message',

    listener: (value: any) => void,

    options?: EventListenerOptions

    ): this;

    [off](https://bun.com/reference/node/worker_threads/MessagePort/off)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void,

    options?: EventListenerOptions

    ): this;

    [off](https://bun.com/reference/node/worker_threads/MessagePort/off)(

    event: string,

    listener: (arg: any) => void,

    options?: EventListenerOptions

    ): this;
  + [on](https://bun.com/reference/node/worker_threads/MessagePort/on)(

    event: 'close',

    listener: (ev: [Event](https://bun.com/reference/globals/Event)) => void

    ): this;

    Node.js-specific alias for `eventTarget.addEventListener()`.

    [on](https://bun.com/reference/node/worker_threads/MessagePort/on)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [on](https://bun.com/reference/node/worker_threads/MessagePort/on)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/worker_threads/MessagePort/on)(

    event: string,

    listener: (arg: any) => void

    ): this;
  + [once](https://bun.com/reference/node/worker_threads/MessagePort/once)(

    event: 'close',

    listener: (ev: [Event](https://bun.com/reference/globals/Event)) => void

    ): this;

    Node.js-specific extension to the `EventTarget` class that adds a `once` listener for the given event `type`. This is equivalent to calling `on` with the `once` option set to `true`.

    [once](https://bun.com/reference/node/worker_threads/MessagePort/once)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [once](https://bun.com/reference/node/worker_threads/MessagePort/once)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/worker_threads/MessagePort/once)(

    event: string,

    listener: (arg: any) => void

    ): this;
  + [postMessage](https://bun.com/reference/node/worker_threads/MessagePort/postMessage)(

    value: any,

    transferList?: readonly [Transferable](https://bun.com/reference/node/worker_threads/Transferable)[]

    ): void;

    Sends a JavaScript value to the receiving side of this channel. `value` is transferred in a way which is compatible with the [HTML structured clone algorithm](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm).

    In particular, the significant differences to `JSON` are:

    - `value` may contain circular references.
    - `value` may contain instances of builtin JS types such as `RegExp`s, `BigInt`s, `Map`s, `Set`s, etc.
    - `value` may contain typed arrays, both using `ArrayBuffer`s and `SharedArrayBuffer`s.
    - `value` may contain [`WebAssembly.Module`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly/Module) instances.
    - `value` may not contain native (C++-backed) objects other than:

    ```
    import { MessageChannel } from 'node:worker_threads';
    const { port1, port2 } = new MessageChannel();

    port1.on('message', (message) => console.log(message));

    const circularData = {};
    circularData.foo = circularData;
    // Prints: { foo: [Circular] }
    port2.postMessage(circularData);
    ```

    `transferList` may be a list of [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer), `MessagePort`, and `FileHandle` objects. After transferring, they are not usable on the sending side of the channel anymore (even if they are not contained in `value`). Unlike with `child processes`, transferring handles such as network sockets is currently not supported.

    If `value` contains [`SharedArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) instances, those are accessible from either thread. They cannot be listed in `transferList`.

    `value` may still contain `ArrayBuffer` instances that are not in `transferList`; in that case, the underlying memory is copied rather than moved.

    ```
    import { MessageChannel } from 'node:worker_threads';
    const { port1, port2 } = new MessageChannel();

    port1.on('message', (message) => console.log(message));

    const uint8Array = new Uint8Array([ 1, 2, 3, 4 ]);
    // This posts a copy of `uint8Array`:
    port2.postMessage(uint8Array);
    // This does not copy data, but renders `uint8Array` unusable:
    port2.postMessage(uint8Array, [ uint8Array.buffer ]);

    // The memory for the `sharedUint8Array` is accessible from both the
    // original and the copy received by `.on('message')`:
    const sharedUint8Array = new Uint8Array(new SharedArrayBuffer(4));
    port2.postMessage(sharedUint8Array);

    // This transfers a freshly created message port to the receiver.
    // This can be used, for example, to create communication channels between
    // multiple `Worker` threads that are children of the same parent thread.
    const otherChannel = new MessageChannel();
    port2.postMessage({ port: otherChannel.port1 }, [ otherChannel.port1 ]);
    ```

    The message object is cloned immediately, and can be modified after posting without having side effects.

    For more information on the serialization and deserialization mechanisms behind this API, see the `serialization API of the node:v8 module`.
  + [ref](https://bun.com/reference/node/worker_threads/MessagePort/ref)(): void;

    Opposite of `unref()`. Calling `ref()` on a previously `unref()`ed port does *not* let the program exit if it's the only active handle left (the default behavior). If the port is `ref()`ed, calling `ref()` again has no effect.

    If listeners are attached or removed using `.on('message')`, the port is `ref()`ed and `unref()`ed automatically depending on whether listeners for the event exist.
  + [removeAllListeners](https://bun.com/reference/node/worker_threads/MessagePort/removeAllListeners)(

    type?: string

    ): this;

    Node.js-specific extension to the `EventTarget` class. If `type` is specified, removes all registered listeners for `type`, otherwise removes all registered listeners.
  + [removeEventListener](https://bun.com/reference/node/worker_threads/MessagePort/removeEventListener)(

    type: string,

    callback: null | EventListenerOrEventListenerObject,

    options?: boolean | EventListenerOptions

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

    [removeEventListener](https://bun.com/reference/node/worker_threads/MessagePort/removeEventListener)(

    type: string,

    listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

    options?: boolean | [EventListenerOptions](https://bun.com/reference/bun/EventListenerOptions)

    ): void;

    Removes the event listener in target's event listener list with the same type, callback, and options.
  + [removeListener](https://bun.com/reference/node/worker_threads/MessagePort/removeListener)(

    event: 'close',

    listener: (ev: [Event](https://bun.com/reference/globals/Event)) => void,

    options?: EventListenerOptions

    ): this;

    Node.js-specific extension to the `EventTarget` class that removes the `listener` for the given `type`. The only difference between `removeListener()` and `removeEventListener()` is that `removeListener()` will return a reference to the `EventTarget`.

    [removeListener](https://bun.com/reference/node/worker_threads/MessagePort/removeListener)(

    event: 'message',

    listener: (value: any) => void,

    options?: EventListenerOptions

    ): this;

    [removeListener](https://bun.com/reference/node/worker_threads/MessagePort/removeListener)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void,

    options?: EventListenerOptions

    ): this;

    [removeListener](https://bun.com/reference/node/worker_threads/MessagePort/removeListener)(

    event: string,

    listener: (arg: any) => void,

    options?: EventListenerOptions

    ): this;
  + [setMaxListeners](https://bun.com/reference/node/worker_threads/MessagePort/setMaxListeners)(

    n: number

    ): void;

    Node.js-specific extension to the `EventTarget` class that sets the number of max event listeners as `n`.
  + [start](https://bun.com/reference/node/worker_threads/MessagePort/start)(): void;

    Starts receiving messages on this `MessagePort`. When using this port as an event emitter, this is called automatically once `'message'` listeners are attached.

    This method exists for parity with the Web `MessagePort` API. In Node.js, it is only useful for ignoring messages when no event listener is present. Node.js also diverges in its handling of `.onmessage`. Setting it automatically calls `.start()`, but unsetting it lets messages queue up until a new handler is set or the port is discarded.
  + [unref](https://bun.com/reference/node/worker_threads/MessagePort/unref)(): void;

    Calling `unref()` on a port allows the thread to exit if this is the only active handle in the event system. If the port is already `unref()`ed calling `unref()` again has no effect.

    If listeners are attached or removed using `.on('message')`, the port is `ref()`ed and `unref()`ed automatically depending on whether listeners for the event exist.
* ### class [Worker](https://bun.com/reference/node/worker_threads/Worker)

  The `Worker` class represents an independent JavaScript execution thread. Most Node.js APIs are available inside of it.

  Notable differences inside a Worker environment are:

  + The `process.stdin`, `process.stdout`, and `process.stderr` streams may be redirected by the parent thread.
  + The `import { isMainThread } from 'node:worker_threads'` variable is set to `false`.
  + The `import { parentPort } from 'node:worker_threads'` message port is available.
  + `process.exit()` does not stop the whole program, just the single thread, and `process.abort()` is not available.
  + `process.chdir()` and `process` methods that set group or user ids are not available.
  + `process.env` is a copy of the parent thread's environment variables, unless otherwise specified. Changes to one copy are not visible in other threads, and are not visible to native add-ons (unless `worker.SHARE_ENV` is passed as the `env` option to the `Worker` constructor). On Windows, unlike the main thread, a copy of the environment variables operates in a case-sensitive manner.
  + `process.title` cannot be modified.
  + Signals are not delivered through `process.on('...')`.
  + Execution may stop at any point as a result of `worker.terminate()` being invoked.
  + IPC channels from parent processes are not accessible.
  + The `trace_events` module is not supported.
  + Native add-ons can only be loaded from multiple threads if they fulfill `certain conditions`.

  Creating `Worker` instances inside of other `Worker`s is possible.

  Like [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API) and the `node:cluster module`, two-way communication can be achieved through inter-thread message passing. Internally, a `Worker` has a built-in pair of `MessagePort` s that are already associated with each other when the `Worker` is created. While the `MessagePort` object on the parent side is not directly exposed, its functionalities are exposed through `worker.postMessage()` and the `worker.on('message')` event on the `Worker` object for the parent thread.

  To create custom messaging channels (which is encouraged over using the default global channel because it facilitates separation of concerns), users can create a `MessageChannel` object on either thread and pass one of the`MessagePort`s on that `MessageChannel` to the other thread through a pre-existing channel, such as the global one.

  See `port.postMessage()` for more information on how messages are passed, and what kind of JavaScript values can be successfully transported through the thread barrier.

  ```
  import assert from 'node:assert';
  import {
    Worker, MessageChannel, MessagePort, isMainThread, parentPort,
  } from 'node:worker_threads';
  if (isMainThread) {
    const worker = new Worker(__filename);
    const subChannel = new MessageChannel();
    worker.postMessage({ hereIsYourPort: subChannel.port1 }, [subChannel.port1]);
    subChannel.port2.on('message', (value) => {
      console.log('received:', value);
    });
  } else {
    parentPort.once('message', (value) => {
      assert(value.hereIsYourPort instanceof MessagePort);
      value.hereIsYourPort.postMessage('the worker is sending this');
      value.hereIsYourPort.close();
    });
  }
  ```

  + readonly [performance](https://bun.com/reference/node/worker_threads/Worker/performance): [WorkerPerformance](https://bun.com/reference/node/worker_threads/WorkerPerformance)

    An object that can be used to query performance information from a worker instance. Similar to `perf_hooks.performance`.
  + readonly [resourceLimits](https://bun.com/reference/node/worker_threads/Worker/resourceLimits)?: [ResourceLimits](https://bun.com/reference/node/worker_threads/ResourceLimits)

    Provides the set of JS engine resource constraints for this Worker thread. If the `resourceLimits` option was passed to the `Worker` constructor, this matches its values.

    If the worker has stopped, the return value is an empty object.
  + readonly [stderr](https://bun.com/reference/node/worker_threads/Worker/stderr): [Readable](https://bun.com/reference/node/stream/default/Readable)

    This is a readable stream which contains data written to `process.stderr` inside the worker thread. If `stderr: true` was not passed to the `Worker` constructor, then data is piped to the parent thread's `process.stderr` stream.
  + readonly [stdin](https://bun.com/reference/node/worker_threads/Worker/stdin): null | [Writable](https://bun.com/reference/node/stream/default/Writable)

    If `stdin: true` was passed to the `Worker` constructor, this is a writable stream. The data written to this stream will be made available in the worker thread as `process.stdin`.
  + readonly [stdout](https://bun.com/reference/node/worker_threads/Worker/stdout): [Readable](https://bun.com/reference/node/stream/default/Readable)

    This is a readable stream which contains data written to `process.stdout` inside the worker thread. If `stdout: true` was not passed to the `Worker` constructor, then data is piped to the parent thread's `process.stdout` stream.
  + readonly [threadId](https://bun.com/reference/node/worker_threads/Worker/threadId): number

    An integer identifier for the referenced thread. Inside the worker thread, it is available as `import { threadId } from 'node:worker_threads'`. This value is unique for each `Worker` instance inside a single process.
  + readonly [threadName](https://bun.com/reference/node/worker_threads/Worker/threadName): null | string

    A string identifier for the referenced thread or null if the thread is not running. Inside the worker thread, it is available as `require('node:worker_threads').threadName`.
  + static [captureRejections](https://bun.com/reference/node/worker_threads/Worker/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/worker_threads/Worker/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/worker_threads/Worker/defaultMaxListeners): number

    By default, a maximum of `10` listeners can be registered for any single event. This limit can be changed for individual `EventEmitter` instances using the `emitter.setMaxListeners(n)` method. To change the default for *all*`EventEmitter` instances, the `events.defaultMaxListeners` property can be used. If this value is not a positive number, a `RangeError` is thrown.

    Take caution when setting the `events.defaultMaxListeners` because the change affects *all* `EventEmitter` instances, including those created before the change is made. However, calling `emitter.setMaxListeners(n)` still has precedence over `events.defaultMaxListeners`.

    This is not a hard limit. The `EventEmitter` instance will allow more listeners to be added but will output a trace warning to stderr indicating that a "possible EventEmitter memory leak" has been detected. For any single `EventEmitter`, the `emitter.getMaxListeners()` and `emitter.setMaxListeners()` methods can be used to temporarily avoid this warning:

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.setMaxListeners(emitter.getMaxListeners() + 1);
    emitter.once('event', () => {
      // do stuff
      emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
    });
    ```

    The `--trace-warnings` command-line flag can be used to display the stack trace for such warnings.

    The emitted warning can be inspected with `process.on('warning')` and will have the additional `emitter`, `type`, and `count` properties, referring to the event emitter instance, the event's name and the number of attached listeners, respectively. Its `name` property is set to `'MaxListenersExceededWarning'`.
  + readonly static [errorMonitor](https://bun.com/reference/node/worker_threads/Worker/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/worker_threads/Worker/[asyncDispose])(): Promise<void>;

    Calls `worker.terminate()` when the dispose scope is exited.

    ```
    async function example() {
      await using worker = new Worker('for (;;) {}', { eval: true });
      // Worker is automatically terminate when the scope is exited.
    }
    ```
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/worker_threads/Worker/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/worker_threads/Worker/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/worker_threads/Worker/addListener)(

    event: 'exit',

    listener: (exitCode: number) => void

    ): this;

    [addListener](https://bun.com/reference/node/worker_threads/Worker/addListener)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [addListener](https://bun.com/reference/node/worker_threads/Worker/addListener)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [addListener](https://bun.com/reference/node/worker_threads/Worker/addListener)(

    event: 'online',

    listener: () => void

    ): this;

    [addListener](https://bun.com/reference/node/worker_threads/Worker/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [cpuUsage](https://bun.com/reference/node/worker_threads/Worker/cpuUsage)(

    prev?: CpuUsage

    ): Promise<CpuUsage>;

    This method returns a `Promise` that will resolve to an object identical to `process.threadCpuUsage()`, or reject with an `ERR_WORKER_NOT_RUNNING` error if the worker is no longer running. This methods allows the statistics to be observed from outside the actual thread.
  + [emit](https://bun.com/reference/node/worker_threads/Worker/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/worker_threads/Worker/emit)(

    event: 'exit',

    exitCode: number

    ): boolean;

    [emit](https://bun.com/reference/node/worker_threads/Worker/emit)(

    event: 'message',

    value: any

    ): boolean;

    [emit](https://bun.com/reference/node/worker_threads/Worker/emit)(

    event: 'messageerror',

    error: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/worker_threads/Worker/emit)(

    event: 'online'

    ): boolean;

    [emit](https://bun.com/reference/node/worker_threads/Worker/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/worker_threads/Worker/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [getHeapSnapshot](https://bun.com/reference/node/worker_threads/Worker/getHeapSnapshot)(): Promise<[Readable](https://bun.com/reference/node/stream/default/Readable)>;

    Returns a readable stream for a V8 snapshot of the current state of the Worker. See `v8.getHeapSnapshot()` for more details.

    If the Worker thread is no longer running, which may occur before the `'exit' event` is emitted, the returned `Promise` is rejected immediately with an `ERR_WORKER_NOT_RUNNING` error.

    @returns

    A promise for a Readable Stream containing a V8 heap snapshot
  + [getHeapStatistics](https://bun.com/reference/node/worker_threads/Worker/getHeapStatistics)(): Promise<[HeapInfo](https://bun.com/reference/node/v8/HeapInfo)>;

    This method returns a `Promise` that will resolve to an object identical to `v8.getHeapStatistics()`, or reject with an `ERR_WORKER_NOT_RUNNING` error if the worker is no longer running. This methods allows the statistics to be observed from outside the actual thread.
  + [getMaxListeners](https://bun.com/reference/node/worker_threads/Worker/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/worker_threads/Worker/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/worker_threads/Worker/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/worker_threads/Worker/off)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Alias for `emitter.removeListener()`.

    [off](https://bun.com/reference/node/worker_threads/Worker/off)(

    event: 'exit',

    listener: (exitCode: number) => void

    ): this;

    [off](https://bun.com/reference/node/worker_threads/Worker/off)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [off](https://bun.com/reference/node/worker_threads/Worker/off)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [off](https://bun.com/reference/node/worker_threads/Worker/off)(

    event: 'online',

    listener: () => void

    ): this;

    [off](https://bun.com/reference/node/worker_threads/Worker/off)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    event: 'exit',

    listener: (exitCode: number) => void

    ): this;

    [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    event: 'online',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    event: 'exit',

    listener: (exitCode: number) => void

    ): this;

    [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    event: 'online',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [postMessage](https://bun.com/reference/node/worker_threads/Worker/postMessage)(

    value: any,

    transferList?: readonly [Transferable](https://bun.com/reference/node/worker_threads/Transferable)[]

    ): void;

    Send a message to the worker that is received via `require('node:worker_threads').parentPort.on('message')`. See `port.postMessage()` for more details.
  + [prependListener](https://bun.com/reference/node/worker_threads/Worker/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/worker_threads/Worker/prependListener)(

    event: 'exit',

    listener: (exitCode: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/worker_threads/Worker/prependListener)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/worker_threads/Worker/prependListener)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/worker_threads/Worker/prependListener)(

    event: 'online',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/worker_threads/Worker/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/worker_threads/Worker/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/worker_threads/Worker/prependOnceListener)(

    event: 'exit',

    listener: (exitCode: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/worker_threads/Worker/prependOnceListener)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/worker_threads/Worker/prependOnceListener)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/worker_threads/Worker/prependOnceListener)(

    event: 'online',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/worker_threads/Worker/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/worker_threads/Worker/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [ref](https://bun.com/reference/node/worker_threads/Worker/ref)(): void;

    Opposite of `unref()`, calling `ref()` on a previously `unref()`ed worker does *not* let the program exit if it's the only active handle left (the default behavior). If the worker is `ref()`ed, calling `ref()` again has no effect.
  + [removeAllListeners](https://bun.com/reference/node/worker_threads/Worker/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/worker_threads/Worker/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/worker_threads/Worker/removeListener)(

    event: 'exit',

    listener: (exitCode: number) => void

    ): this;

    [removeListener](https://bun.com/reference/node/worker_threads/Worker/removeListener)(

    event: 'message',

    listener: (value: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/worker_threads/Worker/removeListener)(

    event: 'messageerror',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/worker_threads/Worker/removeListener)(

    event: 'online',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/worker_threads/Worker/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [setMaxListeners](https://bun.com/reference/node/worker_threads/Worker/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [startCpuProfile](https://bun.com/reference/node/worker_threads/Worker/startCpuProfile)(): Promise<[CPUProfileHandle](https://bun.com/reference/node/v8/CPUProfileHandle)>;

    Starting a CPU profile then return a Promise that fulfills with an error or an `CPUProfileHandle` object. This API supports `await using` syntax.

    ```
    const { Worker } = require('node:worker_threads');

    const worker = new Worker(`
      const { parentPort } = require('worker_threads');
      parentPort.on('message', () => {});
      `, { eval: true });

    worker.on('online', async () => {
      const handle = await worker.startCpuProfile();
      const profile = await handle.stop();
      console.log(profile);
      worker.terminate();
    });
    ```

    `await using` example.

    ```
    const { Worker } = require('node:worker_threads');

    const w = new Worker(`
      const { parentPort } = require('node:worker_threads');
      parentPort.on('message', () => {});
      `, { eval: true });

    w.on('online', async () => {
      // Stop profile automatically when return and profile will be discarded
      await using handle = await w.startCpuProfile();
    });
    ```
  + [startHeapProfile](https://bun.com/reference/node/worker_threads/Worker/startHeapProfile)(): Promise<[HeapProfileHandle](https://bun.com/reference/node/v8/HeapProfileHandle)>;

    Starting a Heap profile then return a Promise that fulfills with an error or an `HeapProfileHandle` object. This API supports `await using` syntax.

    ```
    const { Worker } = require('node:worker_threads');

    const worker = new Worker(`
      const { parentPort } = require('worker_threads');
      parentPort.on('message', () => {});
      `, { eval: true });

    worker.on('online', async () => {
      const handle = await worker.startHeapProfile();
      const profile = await handle.stop();
      console.log(profile);
      worker.terminate();
    });
    ```

    `await using` example.

    ```
    const { Worker } = require('node:worker_threads');

    const w = new Worker(`
      const { parentPort } = require('node:worker_threads');
      parentPort.on('message', () => {});
      `, { eval: true });

    w.on('online', async () => {
      // Stop profile automatically when return and profile will be discarded
      await using handle = await w.startHeapProfile();
    });
    ```
  + [terminate](https://bun.com/reference/node/worker_threads/Worker/terminate)(): Promise<number>;

    Stop all JavaScript execution in the worker thread as soon as possible. Returns a Promise for the exit code that is fulfilled when the `'exit' event` is emitted.
  + [unref](https://bun.com/reference/node/worker_threads/Worker/unref)(): void;

    Calling `unref()` on a worker allows the thread to exit if this is the only active handle in the event system. If the worker is already `unref()`ed calling `unref()` again has no effect.
  + static [addAbortListener](https://bun.com/reference/node/worker_threads/Worker/addAbortListener)(

    signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal),

    resource: (event: [Event](https://bun.com/reference/globals/Event)) => void

    ): Disposable;

    Listens once to the `abort` event on the provided `signal`.

    Listening to the `abort` event on abort signals is unsafe and may lead to resource leaks since another third party with the signal can call `e.stopImmediatePropagation()`. Unfortunately Node.js cannot change this since it would violate the web standard. Additionally, the original API makes it easy to forget to remove listeners.

    This API allows safely using `AbortSignal`s in Node.js APIs by solving these two issues by listening to the event such that `stopImmediatePropagation` does not prevent the listener from running.

    Returns a disposable so that it may be unsubscribed from more easily.

    ```
    import { addAbortListener } from 'node:events';

    function example(signal) {
      let disposable;
      try {
        signal.addEventListener('abort', (e) => e.stopImmediatePropagation());
        disposable = addAbortListener(signal, (e) => {
          // Do something when signal is aborted.
        });
      } finally {
        disposable?.[Symbol.dispose]();
      }
    }
    ```

    @returns

    Disposable that removes the `abort` listener.
  + static [getEventListeners](https://bun.com/reference/node/worker_threads/Worker/getEventListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget),

    name: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    For `EventEmitter`s this behaves exactly the same as calling `.listeners` on the emitter.

    For `EventTarget`s this is the only way to get the event listeners for the event target. This is useful for debugging and diagnostic purposes.

    ```
    import { getEventListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      const listener = () => console.log('Events are fun');
      ee.on('foo', listener);
      console.log(getEventListeners(ee, 'foo')); // [ [Function: listener] ]
    }
    {
      const et = new EventTarget();
      const listener = () => console.log('Events are fun');
      et.addEventListener('foo', listener);
      console.log(getEventListeners(et, 'foo')); // [ [Function: listener] ]
    }
    ```
  + static [getMaxListeners](https://bun.com/reference/node/worker_threads/Worker/getMaxListeners)(

    emitter: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)

    ): number;

    Returns the currently set max amount of listeners.

    For `EventEmitter`s this behaves exactly the same as calling `.getMaxListeners` on the emitter.

    For `EventTarget`s this is the only way to get the max event listeners for the event target. If the number of event handlers on a single EventTarget exceeds the max set, the EventTarget will print a warning.

    ```
    import { getMaxListeners, setMaxListeners, EventEmitter } from 'node:events';

    {
      const ee = new EventEmitter();
      console.log(getMaxListeners(ee)); // 10
      setMaxListeners(11, ee);
      console.log(getMaxListeners(ee)); // 11
    }
    {
      const et = new EventTarget();
      console.log(getMaxListeners(et)); // 10
      setMaxListeners(11, et);
      console.log(getMaxListeners(et)); // 11
    }
    ```
  + static [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`

    static [on](https://bun.com/reference/node/worker_threads/Worker/on)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterIteratorOptions

    ): AsyncIterator<any[]>;

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
    });

    for await (const event of on(ee, 'foo')) {
      // The execution of this inner block is synchronous and it
      // processes one event at a time (even with await). Do not use
      // if concurrent execution is required.
      console.log(event); // prints ['bar'] [42]
    }
    // Unreachable here
    ```

    Returns an `AsyncIterator` that iterates `eventName` events. It will throw if the `EventEmitter` emits `'error'`. It removes all listeners when exiting the loop. The `value` returned by each iteration is an array composed of the emitted event arguments.

    An `AbortSignal` can be used to cancel waiting on events:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ac = new AbortController();

    (async () => {
      const ee = new EventEmitter();

      // Emit later on
      process.nextTick(() => {
        ee.emit('foo', 'bar');
        ee.emit('foo', 42);
      });

      for await (const event of on(ee, 'foo', { signal: ac.signal })) {
        // The execution of this inner block is synchronous and it
        // processes one event at a time (even with await). Do not use
        // if concurrent execution is required.
        console.log(event); // prints ['bar'] [42]
      }
      // Unreachable here
    })();

    process.nextTick(() => ac.abort());
    ```

    Use the `close` option to specify an array of event names that will end the iteration:

    ```
    import { on, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    // Emit later on
    process.nextTick(() => {
      ee.emit('foo', 'bar');
      ee.emit('foo', 42);
      ee.emit('close');
    });

    for await (const event of on(ee, 'foo', { close: ['close'] })) {
      console.log(event); // prints ['bar'] [42]
    }
    // the loop will exit after 'close' is emitted
    console.log('done'); // prints 'done'
    ```

    @returns

    An `AsyncIterator` that iterates `eventName` events emitted by the `emitter`
  + static [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    emitter: EventEmitter,

    eventName: string | symbol,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```

    static [once](https://bun.com/reference/node/worker_threads/Worker/once)(

    emitter: [EventTarget](https://bun.com/reference/globals/EventTarget),

    eventName: string,

    options?: StaticEventEmitterOptions

    ): Promise<any[]>;

    Creates a `Promise` that is fulfilled when the `EventEmitter` emits the given event or that is rejected if the `EventEmitter` emits `'error'` while waiting. The `Promise` will resolve with an array of all the arguments emitted to the given event.

    This method is intentionally generic and works with the web platform [EventTarget](https://dom.spec.whatwg.org/#interface-eventtarget) interface, which has no special`'error'` event semantics and does not listen to the `'error'` event.

    ```
    import { once, EventEmitter } from 'node:events';
    import process from 'node:process';

    const ee = new EventEmitter();

    process.nextTick(() => {
      ee.emit('myevent', 42);
    });

    const [value] = await once(ee, 'myevent');
    console.log(value);

    const err = new Error('kaboom');
    process.nextTick(() => {
      ee.emit('error', err);
    });

    try {
      await once(ee, 'myevent');
    } catch (err) {
      console.error('error happened', err);
    }
    ```

    The special handling of the `'error'` event is only used when `events.once()` is used to wait for another event. If `events.once()` is used to wait for the '`error'` event itself, then it is treated as any other kind of event without special handling:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();

    once(ee, 'error')
      .then(([err]) => console.log('ok', err.message))
      .catch((err) => console.error('error', err.message));

    ee.emit('error', new Error('boom'));

    // Prints: ok boom
    ```

    An `AbortSignal` can be used to cancel waiting for the event:

    ```
    import { EventEmitter, once } from 'node:events';

    const ee = new EventEmitter();
    const ac = new AbortController();

    async function foo(emitter, event, signal) {
      try {
        await once(emitter, event, { signal });
        console.log('event emitted!');
      } catch (error) {
        if (error.name === 'AbortError') {
          console.error('Waiting for the event was canceled!');
        } else {
          console.error('There was an error', error.message);
        }
      }
    }

    foo(ee, 'foo', ac.signal);
    ac.abort(); // Abort waiting for the event
    ee.emit('foo'); // Prints: Waiting for the event was canceled!
    ```
  + static [setMaxListeners](https://bun.com/reference/node/worker_threads/Worker/setMaxListeners)(

    n?: number,

    ...eventTargets: EventEmitter<DefaultEventMap> | [EventTarget](https://bun.com/reference/globals/EventTarget)[]

    ): void;

    ```
    import { setMaxListeners, EventEmitter } from 'node:events';

    const target = new EventTarget();
    const emitter = new EventEmitter();

    setMaxListeners(5, target, emitter);
    ```

    @param n

    A non-negative number. The maximum number of listeners per `EventTarget` event.

    @param eventTargets

    Zero or more {EventTarget} or {EventEmitter} instances. If none are specified, `n` is set as the default max for all newly created {EventTarget} and {EventEmitter} objects.
* const [isInternalThread](https://bun.com/reference/node/worker_threads/isInternalThread): boolean
* const [isMainThread](https://bun.com/reference/node/worker_threads/isMainThread): boolean
* const [locks](https://bun.com/reference/node/worker_threads/locks): [LockManager](https://bun.com/reference/node/worker_threads/LockManager)
* const [parentPort](https://bun.com/reference/node/worker_threads/parentPort): null | [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort)
* const [resourceLimits](https://bun.com/reference/node/worker_threads/resourceLimits): [ResourceLimits](https://bun.com/reference/node/worker_threads/ResourceLimits)
* const [SHARE\_ENV](https://bun.com/reference/node/worker_threads/SHARE_ENV): unique symbol
* const [threadId](https://bun.com/reference/node/worker_threads/threadId): number
* const [threadName](https://bun.com/reference/node/worker_threads/threadName): string | null
* const [workerData](https://bun.com/reference/node/worker_threads/workerData): any
* function [getEnvironmentData](https://bun.com/reference/node/worker_threads/getEnvironmentData)(

  key: [Serializable](https://bun.com/reference/node/worker_threads/Serializable)

  ): [Serializable](https://bun.com/reference/node/worker_threads/Serializable);

  Within a worker thread, `worker.getEnvironmentData()` returns a clone of data passed to the spawning thread's `worker.setEnvironmentData()`. Every new `Worker` receives its own copy of the environment data automatically.

  ```
  import {
    Worker,
    isMainThread,
    setEnvironmentData,
    getEnvironmentData,
  } from 'node:worker_threads';

  if (isMainThread) {
    setEnvironmentData('Hello', 'World!');
    const worker = new Worker(__filename);
  } else {
    console.log(getEnvironmentData('Hello'));  // Prints 'World!'.
  }
  ```

  @param key

  Any arbitrary, cloneable JavaScript value that can be used as a {Map} key.
* function [isMarkedAsUntransferable](https://bun.com/reference/node/worker_threads/isMarkedAsUntransferable)(

  object: object

  ): boolean;

  Check if an object is marked as not transferable with markAsUntransferable.
* function [markAsUncloneable](https://bun.com/reference/node/worker_threads/markAsUncloneable)(

  object: object

  ): void;

  Mark an object as not cloneable. If `object` is used as `message` in a `port.postMessage()` call, an error is thrown. This is a no-op if `object` is a primitive value.

  This has no effect on `ArrayBuffer`, or any `Buffer` like objects.

  This operation cannot be undone.

  ```
  const { markAsUncloneable } = require('node:worker_threads');

  const anyObject = { foo: 'bar' };
  markAsUncloneable(anyObject);
  const { port1 } = new MessageChannel();
  try {
    // This will throw an error, because anyObject is not cloneable.
    port1.postMessage(anyObject)
  } catch (error) {
    // error.name === 'DataCloneError'
  }
  ```

  There is no equivalent to this API in browsers.
* function [markAsUntransferable](https://bun.com/reference/node/worker_threads/markAsUntransferable)(

  object: object

  ): void;

  Mark an object as not transferable. If `object` occurs in the transfer list of a `port.postMessage()` call, it is ignored.

  In particular, this makes sense for objects that can be cloned, rather than transferred, and which are used by other objects on the sending side. For example, Node.js marks the `ArrayBuffer`s it uses for its `Buffer pool` with this.

  This operation cannot be undone.

  ```
  import { MessageChannel, markAsUntransferable } from 'node:worker_threads';

  const pooledBuffer = new ArrayBuffer(8);
  const typedArray1 = new Uint8Array(pooledBuffer);
  const typedArray2 = new Float64Array(pooledBuffer);

  markAsUntransferable(pooledBuffer);

  const { port1 } = new MessageChannel();
  port1.postMessage(typedArray1, [ typedArray1.buffer ]);

  // The following line prints the contents of typedArray1 -- it still owns
  // its memory and has been cloned, not transferred. Without
  // `markAsUntransferable()`, this would print an empty Uint8Array.
  // typedArray2 is intact as well.
  console.log(typedArray1);
  console.log(typedArray2);
  ```

  There is no equivalent to this API in browsers.
* function [moveMessagePortToContext](https://bun.com/reference/node/worker_threads/moveMessagePortToContext)(

  port: [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort),

  contextifiedSandbox: [Context](https://bun.com/reference/node/vm/Context)

  ): [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort);

  Transfer a `MessagePort` to a different `vm` Context. The original `port` object is rendered unusable, and the returned `MessagePort` instance takes its place.

  The returned `MessagePort` is an object in the target context and inherits from its global `Object` class. Objects passed to the [`port.onmessage()`](https://developer.mozilla.org/en-US/docs/Web/API/MessagePort/onmessage) listener are also created in the target context and inherit from its global `Object` class.

  However, the created `MessagePort` no longer inherits from [`EventTarget`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget), and only [`port.onmessage()`](https://developer.mozilla.org/en-US/docs/Web/API/MessagePort/onmessage) can be used to receive events using it.

  @param port

  The message port to transfer.

  @param contextifiedSandbox

  A `contextified` object as returned by the `vm.createContext()` method.
* function [postMessageToThread](https://bun.com/reference/node/worker_threads/postMessageToThread)(

  threadId: number,

  value: any,

  timeout?: number

  ): Promise<void>;

  Sends a value to another worker, identified by its thread ID.

  @param threadId

  The target thread ID. If the thread ID is invalid, a `ERR_WORKER_MESSAGING_FAILED` error will be thrown. If the target thread ID is the current thread ID, a `ERR_WORKER_MESSAGING_SAME_THREAD` error will be thrown.

  @param value

  The value to send.

  @param timeout

  Time to wait for the message to be delivered in milliseconds. By default it's `undefined`, which means wait forever. If the operation times out, a `ERR_WORKER_MESSAGING_TIMEOUT` error is thrown.

  function [postMessageToThread](https://bun.com/reference/node/worker_threads/postMessageToThread)(

  threadId: number,

  value: any,

  transferList: readonly [Transferable](https://bun.com/reference/node/worker_threads/Transferable)[],

  timeout?: number

  ): Promise<void>;

  Sends a value to another worker, identified by its thread ID.

  @param threadId

  The target thread ID. If the thread ID is invalid, a `ERR_WORKER_MESSAGING_FAILED` error will be thrown. If the target thread ID is the current thread ID, a `ERR_WORKER_MESSAGING_SAME_THREAD` error will be thrown.

  @param value

  The value to send.

  @param transferList

  If one or more `MessagePort`-like objects are passed in value, a `transferList` is required for those items or `ERR_MISSING_MESSAGE_PORT_IN_TRANSFER_LIST` is thrown. See `port.postMessage()` for more information.

  @param timeout

  Time to wait for the message to be delivered in milliseconds. By default it's `undefined`, which means wait forever. If the operation times out, a `ERR_WORKER_MESSAGING_TIMEOUT` error is thrown.
* function [receiveMessageOnPort](https://bun.com/reference/node/worker_threads/receiveMessageOnPort)(

  port: [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort)

  ): undefined | { message: any };

  Receive a single message from a given `MessagePort`. If no message is available,`undefined` is returned, otherwise an object with a single `message` property that contains the message payload, corresponding to the oldest message in the `MessagePort`'s queue.

  ```
  import { MessageChannel, receiveMessageOnPort } from 'node:worker_threads';
  const { port1, port2 } = new MessageChannel();
  port1.postMessage({ hello: 'world' });

  console.log(receiveMessageOnPort(port2));
  // Prints: { message: { hello: 'world' } }
  console.log(receiveMessageOnPort(port2));
  // Prints: undefined
  ```

  When this function is used, no `'message'` event is emitted and the `onmessage` listener is not invoked.
* function [setEnvironmentData](https://bun.com/reference/node/worker_threads/setEnvironmentData)(

  key: [Serializable](https://bun.com/reference/node/worker_threads/Serializable),

  value?: [Serializable](https://bun.com/reference/node/worker_threads/Serializable)

  ): void;

  The `worker.setEnvironmentData()` API sets the content of `worker.getEnvironmentData()` in the current thread and all new `Worker` instances spawned from the current context.

  @param key

  Any arbitrary, cloneable JavaScript value that can be used as a {Map} key.

  @param value

  Any arbitrary, cloneable JavaScript value that will be cloned and passed automatically to all new `Worker` instances. If `value` is passed as `undefined`, any previously set value for the `key` will be deleted.

## Type definitions

* ### interface [Lock](https://bun.com/reference/node/worker_threads/Lock)

  + readonly [mode](https://bun.com/reference/node/worker_threads/Lock/mode): [LockMode](https://bun.com/reference/node/worker_threads/LockMode)
  + readonly [name](https://bun.com/reference/node/worker_threads/Lock/name): string
* ### interface [LockGrantedCallback](https://bun.com/reference/node/worker_threads/LockGrantedCallback)<T>
* ### interface [LockInfo](https://bun.com/reference/node/worker_threads/LockInfo)

  + [clientId](https://bun.com/reference/node/worker_threads/LockInfo/clientId): string
  + [mode](https://bun.com/reference/node/worker_threads/LockInfo/mode): [LockMode](https://bun.com/reference/node/worker_threads/LockMode)
  + [name](https://bun.com/reference/node/worker_threads/LockInfo/name): string
* ### interface [LockManager](https://bun.com/reference/node/worker_threads/LockManager)

  + [query](https://bun.com/reference/node/worker_threads/LockManager/query)(): Promise<[LockManagerSnapshot](https://bun.com/reference/node/worker_threads/LockManagerSnapshot)>;
  + [request](https://bun.com/reference/node/worker_threads/LockManager/request)<T>(

    name: string,

    callback: [LockGrantedCallback](https://bun.com/reference/node/worker_threads/LockGrantedCallback)<T>

    ): Promise<Awaited<T>>;

    [request](https://bun.com/reference/node/worker_threads/LockManager/request)<T>(

    name: string,

    options: [LockOptions](https://bun.com/reference/node/worker_threads/LockOptions),

    callback: [LockGrantedCallback](https://bun.com/reference/node/worker_threads/LockGrantedCallback)<T>

    ): Promise<Awaited<T>>;
* ### interface [LockManagerSnapshot](https://bun.com/reference/node/worker_threads/LockManagerSnapshot)

  + [held](https://bun.com/reference/node/worker_threads/LockManagerSnapshot/held): [LockInfo](https://bun.com/reference/node/worker_threads/LockInfo)[]
  + [pending](https://bun.com/reference/node/worker_threads/LockManagerSnapshot/pending): [LockInfo](https://bun.com/reference/node/worker_threads/LockInfo)[]
* ### interface [LockOptions](https://bun.com/reference/node/worker_threads/LockOptions)

  + [ifAvailable](https://bun.com/reference/node/worker_threads/LockOptions/ifAvailable)?: boolean
  + [mode](https://bun.com/reference/node/worker_threads/LockOptions/mode)?: [LockMode](https://bun.com/reference/node/worker_threads/LockMode)
  + [signal](https://bun.com/reference/node/worker_threads/LockOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [steal](https://bun.com/reference/node/worker_threads/LockOptions/steal)?: boolean
* ### interface [ResourceLimits](https://bun.com/reference/node/worker_threads/ResourceLimits)

  + [codeRangeSizeMb](https://bun.com/reference/node/worker_threads/ResourceLimits/codeRangeSizeMb)?: number

    The size of a pre-allocated memory range used for generated code.
  + [maxOldGenerationSizeMb](https://bun.com/reference/node/worker_threads/ResourceLimits/maxOldGenerationSizeMb)?: number

    The maximum size of the main heap in MB.
  + [maxYoungGenerationSizeMb](https://bun.com/reference/node/worker_threads/ResourceLimits/maxYoungGenerationSizeMb)?: number

    The maximum size of a heap space for recently created objects.
  + [stackSizeMb](https://bun.com/reference/node/worker_threads/ResourceLimits/stackSizeMb)?: number

    The default maximum stack size for the thread. Small values may lead to unusable Worker instances.
* ### interface [WorkerOptions](https://bun.com/reference/node/worker_threads/WorkerOptions)

  + [argv](https://bun.com/reference/node/worker_threads/WorkerOptions/argv)?: any[]

    List of arguments which would be stringified and appended to `process.argv` in the worker. This is mostly similar to the `workerData` but the values will be available on the global `process.argv` as if they were passed as CLI options to the script.
  + [env](https://bun.com/reference/node/worker_threads/WorkerOptions/env)?: Dict<string> | typeof [SHARE\_ENV](https://bun.com/reference/node/worker_threads/SHARE_ENV)
  + [eval](https://bun.com/reference/node/worker_threads/WorkerOptions/eval)?: boolean
  + [execArgv](https://bun.com/reference/node/worker_threads/WorkerOptions/execArgv)?: string[]
  + [name](https://bun.com/reference/node/worker_threads/WorkerOptions/name)?: string

    An optional `name` to be appended to the worker title for debugging/identification purposes, making the final title as `[worker ${id}] ${name}`.
  + [resourceLimits](https://bun.com/reference/node/worker_threads/WorkerOptions/resourceLimits)?: [ResourceLimits](https://bun.com/reference/node/worker_threads/ResourceLimits)
  + [stderr](https://bun.com/reference/node/worker_threads/WorkerOptions/stderr)?: boolean
  + [stdin](https://bun.com/reference/node/worker_threads/WorkerOptions/stdin)?: boolean
  + [stdout](https://bun.com/reference/node/worker_threads/WorkerOptions/stdout)?: boolean
  + [trackUnmanagedFds](https://bun.com/reference/node/worker_threads/WorkerOptions/trackUnmanagedFds)?: boolean
  + [transferList](https://bun.com/reference/node/worker_threads/WorkerOptions/transferList)?: [Transferable](https://bun.com/reference/node/worker_threads/Transferable)[]

    Additional data to send in the first worker message.
  + [workerData](https://bun.com/reference/node/worker_threads/WorkerOptions/workerData)?: any
* ### interface [WorkerPerformance](https://bun.com/reference/node/worker_threads/WorkerPerformance)

  + [eventLoopUtilization](https://bun.com/reference/node/worker_threads/WorkerPerformance/eventLoopUtilization): [EventLoopUtilityFunction](https://bun.com/reference/node/perf_hooks/EventLoopUtilityFunction)
* type [LockMode](https://bun.com/reference/node/worker_threads/LockMode) = 'exclusive' | 'shared'
* type [Serializable](https://bun.com/reference/node/worker_threads/Serializable) = string | object | number | boolean | bigint
* type [Transferable](https://bun.com/reference/node/worker_threads/Transferable) = [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | [MessagePort](https://bun.com/reference/node/worker_threads/MessagePort) | [AbortSignal](https://bun.com/reference/globals/AbortSignal) | [FileHandle](https://bun.com/reference/node/fs/promises/FileHandle) | [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream) | [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) | [TransformStream](https://bun.com/reference/node/stream/web/TransformStream)