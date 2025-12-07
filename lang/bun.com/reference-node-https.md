---
url: https://bun.com/reference/node/https
title: Node.js https module | API Reference | Bun
source_domain: bun.com
---

# Node.js https module | API Reference | Bun

Node.js module

# [https](https://bun.com/reference/node/https)

The `'node:https'` module extends `http` to support secure TLS/SSL connections. It provides `https.createServer` and `https.request` methods for serving and consuming encrypted HTTPS traffic.

Works in Bun

APIs are implemented, but the Agent is not always used yet, which might affect connection pooling and other Agent features.

* ### class [Agent](https://bun.com/reference/node/https/Agent)

  An `Agent` object for HTTPS similar to `http.Agent`. See request for more information.

  + readonly [freeSockets](https://bun.com/reference/node/https/Agent/freeSockets): ReadOnlyDict<[Socket](https://bun.com/reference/node/net/Socket)[]>

    An object which contains arrays of sockets currently awaiting use by the agent when `keepAlive` is enabled. Do not modify.

    Sockets in the `freeSockets` list will be automatically destroyed and removed from the array on `'timeout'`.
  + [maxFreeSockets](https://bun.com/reference/node/https/Agent/maxFreeSockets): number

    By default set to 256. For agents with `keepAlive` enabled, this sets the maximum number of sockets that will be left open in the free state.
  + [maxSockets](https://bun.com/reference/node/https/Agent/maxSockets): number

    By default set to `Infinity`. Determines how many concurrent sockets the agent can have open per origin. Origin is the returned value of `agent.getName()`.
  + [maxTotalSockets](https://bun.com/reference/node/https/Agent/maxTotalSockets): number

    By default set to `Infinity`. Determines how many concurrent sockets the agent can have open. Unlike `maxSockets`, this parameter applies across all origins.
  + [options](https://bun.com/reference/node/https/Agent/options): [AgentOptions](https://bun.com/reference/node/https/AgentOptions)
  + readonly [requests](https://bun.com/reference/node/https/Agent/requests): ReadOnlyDict<[IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)[]>

    An object which contains queues of requests that have not yet been assigned to sockets. Do not modify.
  + readonly [sockets](https://bun.com/reference/node/https/Agent/sockets): ReadOnlyDict<[Socket](https://bun.com/reference/node/net/Socket)[]>

    An object which contains arrays of sockets currently in use by the agent. Do not modify.
  + static [captureRejections](https://bun.com/reference/node/https/Agent/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/https/Agent/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/https/Agent/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/https/Agent/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/https/Agent/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/https/Agent/addListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [createConnection](https://bun.com/reference/node/https/Agent/createConnection)(

    options: [RequestOptions](https://bun.com/reference/node/https/RequestOptions),

    callback?: (err: null | [Error](https://bun.com/reference/globals/Error), stream: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): undefined | null | [Duplex](https://bun.com/reference/node/stream/default/Duplex);

    Produces a socket/stream to be used for HTTP requests.

    By default, this function is the same as `net.createConnection()`. However, custom agents may override this method in case greater flexibility is desired.

    A socket/stream can be supplied in one of two ways: by returning the socket/stream from this function, or by passing the socket/stream to `callback`.

    This method is guaranteed to return an instance of the `net.Socket` class, a subclass of `stream.Duplex`, unless the user specifies a socket type other than `net.Socket`.

    `callback` has a signature of `(err, stream)`.

    @param options

    Options containing connection details. Check `createConnection` for the format of the options

    @param callback

    Callback function that receives the created socket
  + [destroy](https://bun.com/reference/node/https/Agent/destroy)(): void;

    Destroy any sockets that are currently in use by the agent.

    It is usually not necessary to do this. However, if using an agent with `keepAlive` enabled, then it is best to explicitly shut down the agent when it is no longer needed. Otherwise, sockets might stay open for quite a long time before the server terminates them.
  + [emit](https://bun.com/reference/node/https/Agent/emit)<K>(

    eventName: string | symbol,

    ...args: AnyRest

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
  + [eventNames](https://bun.com/reference/node/https/Agent/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/https/Agent/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getName](https://bun.com/reference/node/https/Agent/getName)(

    options?: [RequestOptions](https://bun.com/reference/node/https/RequestOptions)

    ): string;

    Get a unique name for a set of request options, to determine whether a connection can be reused. For an HTTP agent, this returns`host:port:localAddress` or `host:port:localAddress:family`. For an HTTPS agent, the name includes the CA, cert, ciphers, and other HTTPS/TLS-specific options that determine socket reusability.

    @param options

    A set of options providing information for name generation
  + [keepSocketAlive](https://bun.com/reference/node/https/Agent/keepSocketAlive)(

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    ): void;

    Called when `socket` is detached from a request and could be persisted by the`Agent`. Default behavior is to:

    ```
    socket.setKeepAlive(true, this.keepAliveMsecs);
    socket.unref();
    return true;
    ```

    This method can be overridden by a particular `Agent` subclass. If this method returns a falsy value, the socket will be destroyed instead of persisting it for use with the next request.

    The `socket` argument can be an instance of `net.Socket`, a subclass of `stream.Duplex`.
  + [listenerCount](https://bun.com/reference/node/https/Agent/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/https/Agent/listeners)<K>(

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
  + [off](https://bun.com/reference/node/https/Agent/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/https/Agent/on)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

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

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [once](https://bun.com/reference/node/https/Agent/once)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

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

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [prependListener](https://bun.com/reference/node/https/Agent/prependListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [prependOnceListener](https://bun.com/reference/node/https/Agent/prependOnceListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param eventName

    The name of the event.

    @param listener

    The callback function
  + [rawListeners](https://bun.com/reference/node/https/Agent/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/https/Agent/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/https/Agent/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

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
  + [reuseSocket](https://bun.com/reference/node/https/Agent/reuseSocket)(

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex),

    request: [ClientRequest](https://bun.com/reference/node/http/ClientRequest)

    ): void;

    Called when `socket` is attached to `request` after being persisted because of the keep-alive options. Default behavior is to:

    ```
    socket.ref();
    ```

    This method can be overridden by a particular `Agent` subclass.

    The `socket` argument can be an instance of `net.Socket`, a subclass of `stream.Duplex`.
  + [setMaxListeners](https://bun.com/reference/node/https/Agent/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/https/Agent/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/https/Agent/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/https/Agent/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/https/Agent/on)(

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

    static [on](https://bun.com/reference/node/https/Agent/on)(

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
  + static [once](https://bun.com/reference/node/https/Agent/once)(

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

    static [once](https://bun.com/reference/node/https/Agent/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/https/Agent/setMaxListeners)(

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
* ### class [Server](https://bun.com/reference/node/https/Server)<Request extends typeof [http.IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [http.IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [http.ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [http.ServerResponse](https://bun.com/reference/node/http/ServerResponse)>

  See `http.Server` for more information.

  + [connections](https://bun.com/reference/node/https/Server/connections): number
  + [headersTimeout](https://bun.com/reference/node/https/Server/headersTimeout): number

    Limit the amount of time the parser will wait to receive the complete HTTP headers.

    If the timeout expires, the server responds with status 408 without forwarding the request to the request listener and then closes the connection.

    It must be set to a non-zero value (e.g. 120 seconds) to protect against potential Denial-of-Service attacks in case the server is deployed without a reverse proxy in front.
  + [keepAliveTimeout](https://bun.com/reference/node/https/Server/keepAliveTimeout): number

    The number of milliseconds of inactivity a server needs to wait for additional incoming data, after it has finished writing the last response, before a socket will be destroyed.

    This timeout value is combined with the `server.keepAliveTimeoutBuffer` option to determine the actual socket timeout, calculated as: socketTimeout = keepAliveTimeout + keepAliveTimeoutBuffer If the server receives new data before the keep-alive timeout has fired, it will reset the regular inactivity timeout, i.e., `server.timeout`.

    A value of `0` will disable the keep-alive timeout behavior on incoming connections. A value of `0` makes the HTTP server behave similarly to Node.js versions prior to 8.0.0, which did not have a keep-alive timeout.

    The socket timeout logic is set up on connection, so changing this value only affects new connections to the server, not any existing connections.
  + [keepAliveTimeoutBuffer](https://bun.com/reference/node/https/Server/keepAliveTimeoutBuffer): number

    An additional buffer time added to the `server.keepAliveTimeout` to extend the internal socket timeout.

    This buffer helps reduce connection reset (`ECONNRESET`) errors by increasing the socket timeout slightly beyond the advertised keep-alive timeout.

    This option applies only to new incoming connections.
  + readonly [listening](https://bun.com/reference/node/https/Server/listening): boolean

    Indicates whether or not the server is listening for connections.
  + [maxConnections](https://bun.com/reference/node/https/Server/maxConnections): number

    Set this property to reject connections when the server's connection count gets high.

    It is not recommended to use this option once a socket has been sent to a child with `child_process.fork()`.
  + [maxHeadersCount](https://bun.com/reference/node/https/Server/maxHeadersCount): null | number

    Limits maximum incoming headers count. If set to 0, no limit will be applied.
  + [maxRequestsPerSocket](https://bun.com/reference/node/https/Server/maxRequestsPerSocket): null | number

    The maximum number of requests socket can handle before closing keep alive connection.

    A value of `0` will disable the limit.

    When the limit is reached it will set the `Connection` header value to `close`, but will not actually close the connection, subsequent requests sent after the limit is reached will get `503 Service Unavailable` as a response.
  + [requestTimeout](https://bun.com/reference/node/https/Server/requestTimeout): number

    Sets the timeout value in milliseconds for receiving the entire request from the client.

    If the timeout expires, the server responds with status 408 without forwarding the request to the request listener and then closes the connection.

    It must be set to a non-zero value (e.g. 120 seconds) to protect against potential Denial-of-Service attacks in case the server is deployed without a reverse proxy in front.
  + [timeout](https://bun.com/reference/node/https/Server/timeout): number

    The number of milliseconds of inactivity before a socket is presumed to have timed out.

    A value of `0` will disable the timeout behavior on incoming connections.

    The socket timeout logic is set up on connection, so changing this value only affects new connections to the server, not any existing connections.
  + static [captureRejections](https://bun.com/reference/node/https/Server/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/https/Server/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/https/Server/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/https/Server/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/https/Server/[asyncDispose])(): Promise<void>;

    Calls () and returns a promise that fulfills when the server has closed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/https/Server/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addContext](https://bun.com/reference/node/https/Server/addContext)(

    hostname: string,

    context: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions) | [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    ): void;

    The `server.addContext()` method adds a secure context that will be used if the client request's SNI name matches the supplied `hostname` (or wildcard).

    When there are multiple matching contexts, the most recently added one is used.

    @param hostname

    A SNI host name or wildcard (e.g. `'*'`)

    @param context

    An object containing any of the possible properties from the createSecureContext `options` arguments (e.g. `key`, `cert`, `ca`, etc), or a TLS context object created with createSecureContext itself.
  + [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'connection',

    listener: (socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [addListener](https://bun.com/reference/node/https/Server/addListener)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [address](https://bun.com/reference/node/https/Server/address)(): null | string | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

    Returns the bound `address`, the address `family` name, and `port` of the server as reported by the operating system if listening on an IP socket (useful to find which port was assigned when getting an OS-assigned address):`{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`.

    For a server listening on a pipe or Unix domain socket, the name is returned as a string.

    ```
    const server = net.createServer((socket) => {
      socket.end('goodbye\n');
    }).on('error', (err) => {
      // Handle errors here.
      throw err;
    });

    // Grab an arbitrary unused port.
    server.listen(() => {
      console.log('opened server on', server.address());
    });
    ```

    `server.address()` returns `null` before the `'listening'` event has been emitted or after calling `server.close()`.
  + [close](https://bun.com/reference/node/https/Server/close)(

    callback?: (err?: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Stops the server from accepting new connections and keeps existing connections. This function is asynchronous, the server is finally closed when all connections are ended and the server emits a `'close'` event. The optional `callback` will be called once the `'close'` event occurs. Unlike that event, it will be called with an `Error` as its only argument if the server was not open when it was closed.

    @param callback

    Called when the server is closed.
  + [closeAllConnections](https://bun.com/reference/node/https/Server/closeAllConnections)(): void;

    Closes all connections connected to this server.
  + [closeIdleConnections](https://bun.com/reference/node/https/Server/closeIdleConnections)(): void;

    Closes all connections connected to this server which are not sending a request or waiting for a response.
  + [emit](https://bun.com/reference/node/https/Server/emit)(

    event: string,

    ...args: any[]

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

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'keylog',

    line: NonSharedBuffer,

    tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'newSession',

    sessionId: NonSharedBuffer,

    sessionData: NonSharedBuffer,

    callback: () => void

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'OCSPRequest',

    certificate: NonSharedBuffer,

    issuer: NonSharedBuffer,

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'resumeSession',

    sessionId: NonSharedBuffer,

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'secureConnection',

    tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'tlsClientError',

    err: [Error](https://bun.com/reference/globals/Error),

    tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'connection',

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'listening'

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'checkContinue',

    req: InstanceType<Request>,

    res: InstanceType<Response>

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'checkExpectation',

    req: InstanceType<Request>,

    res: InstanceType<Response>

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'clientError',

    err: [Error](https://bun.com/reference/globals/Error),

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'connect',

    req: InstanceType<Request>,

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex),

    head: NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'request',

    req: InstanceType<Request>,

    res: InstanceType<Response>

    ): boolean;

    [emit](https://bun.com/reference/node/https/Server/emit)(

    event: 'upgrade',

    req: InstanceType<Request>,

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex),

    head: NonSharedBuffer

    ): boolean;
  + [eventNames](https://bun.com/reference/node/https/Server/eventNames)(): string | symbol[];

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
  + [getConnections](https://bun.com/reference/node/https/Server/getConnections)(

    cb: (error: null | [Error](https://bun.com/reference/globals/Error), count: number) => void

    ): this;

    Asynchronously get the number of concurrent connections on the server. Works when sockets were sent to forks.

    Callback should take two arguments `err` and `count`.
  + [getMaxListeners](https://bun.com/reference/node/https/Server/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getTicketKeys](https://bun.com/reference/node/https/Server/getTicketKeys)(): NonSharedBuffer;

    Returns the session ticket keys.

    See `Session Resumption` for more information.

    @returns

    A 48-byte buffer containing the session ticket keys.
  + [listen](https://bun.com/reference/node/https/Server/listen)(

    port?: number,

    hostname?: string,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    port?: number,

    hostname?: string,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    port?: number,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    port?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    path: string,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    path: string,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    options: [ListenOptions](https://bun.com/reference/node/net/ListenOptions),

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    handle: any,

    backlog?: number,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```

    [listen](https://bun.com/reference/node/https/Server/listen)(

    handle: any,

    listeningListener?: () => void

    ): this;

    Start a server listening for connections. A `net.Server` can be a TCP or an `IPC` server depending on what it listens to.

    Possible signatures:

    - `server.listen(handle[, backlog][, callback])`
    - `server.listen(options[, callback])`
    - `server.listen(path[, backlog][, callback])` for `IPC` servers
    - `server.listen([port[, host[, backlog]]][, callback])` for TCP servers

    This function is asynchronous. When the server starts listening, the `'listening'` event will be emitted. The last parameter `callback`will be added as a listener for the `'listening'` event.

    All `listen()` methods can take a `backlog` parameter to specify the maximum length of the queue of pending connections. The actual length will be determined by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this parameter is 511 (not 512).

    All Socket are set to `SO_REUSEADDR` (see [`socket(7)`](https://man7.org/linux/man-pages/man7/socket.7.html) for details).

    The `server.listen()` method can be called again if and only if there was an error during the first `server.listen()` call or `server.close()` has been called. Otherwise, an `ERR_SERVER_ALREADY_LISTEN` error will be thrown.

    One of the most common errors raised when listening is `EADDRINUSE`. This happens when another server is already listening on the requested`port`/`path`/`handle`. One way to handle this would be to retry after a certain amount of time:

    ```
    server.on('error', (e) => {
      if (e.code === 'EADDRINUSE') {
        console.error('Address in use, retrying...');
        setTimeout(() => {
          server.close();
          server.listen(PORT, HOST);
        }, 1000);
      }
    });
    ```
  + [listenerCount](https://bun.com/reference/node/https/Server/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/https/Server/listeners)<K>(

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
  + [off](https://bun.com/reference/node/https/Server/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/https/Server/on)(

    event: string,

    listener: (...args: any[]) => void

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

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'connection',

    listener: (socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'listening',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [on](https://bun.com/reference/node/https/Server/on)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [once](https://bun.com/reference/node/https/Server/once)(

    event: string,

    listener: (...args: any[]) => void

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

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'connection',

    listener: (socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'listening',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [once](https://bun.com/reference/node/https/Server/once)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: string,

    listener: (...args: any[]) => void

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

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'connection',

    listener: (socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependListener](https://bun.com/reference/node/https/Server/prependListener)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: string,

    listener: (...args: any[]) => void

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

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'connection',

    listener: (socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependOnceListener](https://bun.com/reference/node/https/Server/prependOnceListener)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/https/Server/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/https/Server/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed server will *not* let the program exit if it's the only server left (the default behavior). If the server is `ref`ed calling `ref()` again will have no effect.
  + [removeAllListeners](https://bun.com/reference/node/https/Server/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/https/Server/removeListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

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
  + [setMaxListeners](https://bun.com/reference/node/https/Server/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setSecureContext](https://bun.com/reference/node/https/Server/setSecureContext)(

    options: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions)

    ): void;

    The `server.setSecureContext()` method replaces the secure context of an existing server. Existing connections to the server are not interrupted.

    @param options

    An object containing any of the possible properties from the createSecureContext `options` arguments (e.g. `key`, `cert`, `ca`, etc).
  + [setTicketKeys](https://bun.com/reference/node/https/Server/setTicketKeys)(

    keys: [Buffer](https://bun.com/reference/node/buffer/Buffer)

    ): void;

    Sets the session ticket keys.

    Changes to the ticket keys are effective only for future server connections. Existing or currently pending server connections will use the previous keys.

    See `Session Resumption` for more information.

    @param keys

    A 48-byte buffer containing the session ticket keys.
  + [setTimeout](https://bun.com/reference/node/https/Server/setTimeout)(

    msecs?: number,

    callback?: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    Sets the timeout value for sockets, and emits a `'timeout'` event on the Server object, passing the socket as an argument, if a timeout occurs.

    If there is a `'timeout'` event listener on the Server object, then it will be called with the timed-out socket as an argument.

    By default, the Server does not timeout sockets. However, if a callback is assigned to the Server's `'timeout'` event, timeouts must be handled explicitly.

    [setTimeout](https://bun.com/reference/node/https/Server/setTimeout)(

    callback: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    Sets the timeout value for sockets, and emits a `'timeout'` event on the Server object, passing the socket as an argument, if a timeout occurs.

    If there is a `'timeout'` event listener on the Server object, then it will be called with the timed-out socket as an argument.

    By default, the Server does not timeout sockets. However, if a callback is assigned to the Server's `'timeout'` event, timeouts must be handled explicitly.
  + [unref](https://bun.com/reference/node/https/Server/unref)(): this;

    Calling `unref()` on a server will allow the program to exit if this is the only active server in the event system. If the server is already `unref`ed calling`unref()` again will have no effect.
  + static [addAbortListener](https://bun.com/reference/node/https/Server/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/https/Server/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/https/Server/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/https/Server/on)(

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

    static [on](https://bun.com/reference/node/https/Server/on)(

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
  + static [once](https://bun.com/reference/node/https/Server/once)(

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

    static [once](https://bun.com/reference/node/https/Server/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/https/Server/setMaxListeners)(

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
* const [globalAgent](https://bun.com/reference/node/https/globalAgent): [Agent](https://bun.com/reference/node/https/Agent)
* function [createServer](https://bun.com/reference/node/https/createServer)<Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse)>(

  requestListener?: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

  ): [Server](https://bun.com/reference/node/https/Server)<Request, Response>;

  ```
  // curl -k https://localhost:8000/
  import https from 'node:https';
  import fs from 'node:fs';

  const options = {
    key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
    cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
  };

  https.createServer(options, (req, res) => {
    res.writeHead(200);
    res.end('hello world\n');
  }).listen(8000);
  ```

  Or

  ```
  import https from 'node:https';
  import fs from 'node:fs';

  const options = {
    pfx: fs.readFileSync('test/fixtures/test_cert.pfx'),
    passphrase: 'sample',
  };

  https.createServer(options, (req, res) => {
    res.writeHead(200);
    res.end('hello world\n');
  }).listen(8000);
  ```

  @param requestListener

  A listener to be added to the `'request'` event.

  function [createServer](https://bun.com/reference/node/https/createServer)<Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse)>(

  options: [ServerOptions](https://bun.com/reference/node/https/ServerOptions)<Request, Response>,

  requestListener?: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

  ): [Server](https://bun.com/reference/node/https/Server)<Request, Response>;

  ```
  // curl -k https://localhost:8000/
  import https from 'node:https';
  import fs from 'node:fs';

  const options = {
    key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
    cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
  };

  https.createServer(options, (req, res) => {
    res.writeHead(200);
    res.end('hello world\n');
  }).listen(8000);
  ```

  Or

  ```
  import https from 'node:https';
  import fs from 'node:fs';

  const options = {
    pfx: fs.readFileSync('test/fixtures/test_cert.pfx'),
    passphrase: 'sample',
  };

  https.createServer(options, (req, res) => {
    res.writeHead(200);
    res.end('hello world\n');
  }).listen(8000);
  ```

  @param options

  Accepts `options` from `createServer`, `createSecureContext` and `createServer`.

  @param requestListener

  A listener to be added to the `'request'` event.
* function [get](https://bun.com/reference/node/https/get)(

  options: string | [URL](https://bun.com/reference/node/url/URL) | [RequestOptions](https://bun.com/reference/node/https/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  Like `http.get()` but for HTTPS.

  `options` can be an object, a string, or a `URL` object. If `options` is a string, it is automatically parsed with `new URL()`. If it is a `URL` object, it will be automatically converted to an ordinary `options` object.

  ```
  import https from 'node:https';

  https.get('https://encrypted.google.com/', (res) => {
    console.log('statusCode:', res.statusCode);
    console.log('headers:', res.headers);

    res.on('data', (d) => {
      process.stdout.write(d);
    });

  }).on('error', (e) => {
    console.error(e);
  });
  ```

  @param options

  Accepts the same `options` as request, with the `method` always set to `GET`.

  function [get](https://bun.com/reference/node/https/get)(

  url: string | [URL](https://bun.com/reference/node/url/URL),

  options: [RequestOptions](https://bun.com/reference/node/https/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  Like `http.get()` but for HTTPS.

  `options` can be an object, a string, or a `URL` object. If `options` is a string, it is automatically parsed with `new URL()`. If it is a `URL` object, it will be automatically converted to an ordinary `options` object.

  ```
  import https from 'node:https';

  https.get('https://encrypted.google.com/', (res) => {
    console.log('statusCode:', res.statusCode);
    console.log('headers:', res.headers);

    res.on('data', (d) => {
      process.stdout.write(d);
    });

  }).on('error', (e) => {
    console.error(e);
  });
  ```

  @param options

  Accepts the same `options` as request, with the `method` always set to `GET`.
* function [request](https://bun.com/reference/node/https/request)(

  options: string | [URL](https://bun.com/reference/node/url/URL) | [RequestOptions](https://bun.com/reference/node/https/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  Makes a request to a secure web server.

  The following additional `options` from `tls.connect()` are also accepted: `ca`, `cert`, `ciphers`, `clientCertEngine`, `crl`, `dhparam`, `ecdhCurve`, `honorCipherOrder`, `key`, `passphrase`, `pfx`, `rejectUnauthorized`, `secureOptions`, `secureProtocol`, `servername`, `sessionIdContext`, `highWaterMark`.

  `options` can be an object, a string, or a `URL` object. If `options` is a string, it is automatically parsed with `new URL()`. If it is a `URL` object, it will be automatically converted to an ordinary `options` object.

  `https.request()` returns an instance of the `http.ClientRequest` class. The `ClientRequest` instance is a writable stream. If one needs to upload a file with a POST request, then write to the `ClientRequest` object.

  ```
  import https from 'node:https';

  const options = {
    hostname: 'encrypted.google.com',
    port: 443,
    path: '/',
    method: 'GET',
  };

  const req = https.request(options, (res) => {
    console.log('statusCode:', res.statusCode);
    console.log('headers:', res.headers);

    res.on('data', (d) => {
      process.stdout.write(d);
    });
  });

  req.on('error', (e) => {
    console.error(e);
  });
  req.end();
  ```

  Example using options from `tls.connect()`:

  ```
  const options = {
    hostname: 'encrypted.google.com',
    port: 443,
    path: '/',
    method: 'GET',
    key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
    cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
  };
  options.agent = new https.Agent(options);

  const req = https.request(options, (res) => {
    // ...
  });
  ```

  Alternatively, opt out of connection pooling by not using an `Agent`.

  ```
  const options = {
    hostname: 'encrypted.google.com',
    port: 443,
    path: '/',
    method: 'GET',
    key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
    cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
    agent: false,
  };

  const req = https.request(options, (res) => {
    // ...
  });
  ```

  Example using a `URL` as `options`:

  ```
  const options = new URL('https://abc:xyz@example.com');

  const req = https.request(options, (res) => {
    // ...
  });
  ```

  Example pinning on certificate fingerprint, or the public key (similar to`pin-sha256`):

  ```
  import tls from 'node:tls';
  import https from 'node:https';
  import crypto from 'node:crypto';

  function sha256(s) {
    return crypto.createHash('sha256').update(s).digest('base64');
  }
  const options = {
    hostname: 'github.com',
    port: 443,
    path: '/',
    method: 'GET',
    checkServerIdentity: function(host, cert) {
      // Make sure the certificate is issued to the host we are connected to
      const err = tls.checkServerIdentity(host, cert);
      if (err) {
        return err;
      }

      // Pin the public key, similar to HPKP pin-sha256 pinning
      const pubkey256 = 'pL1+qb9HTMRZJmuC/bB/ZI9d302BYrrqiVuRyW+DGrU=';
      if (sha256(cert.pubkey) !== pubkey256) {
        const msg = 'Certificate verification error: ' +
          `The public key of '${cert.subject.CN}' ` +
          'does not match our pinned fingerprint';
        return new Error(msg);
      }

      // Pin the exact certificate, rather than the pub key
      const cert256 = '25:FE:39:32:D9:63:8C:8A:FC:A1:9A:29:87:' +
        'D8:3E:4C:1D:98:DB:71:E4:1A:48:03:98:EA:22:6A:BD:8B:93:16';
      if (cert.fingerprint256 !== cert256) {
        const msg = 'Certificate verification error: ' +
          `The certificate of '${cert.subject.CN}' ` +
          'does not match our pinned fingerprint';
        return new Error(msg);
      }

      // This loop is informational only.
      // Print the certificate and public key fingerprints of all certs in the
      // chain. Its common to pin the public key of the issuer on the public
      // internet, while pinning the public key of the service in sensitive
      // environments.
      do {
        console.log('Subject Common Name:', cert.subject.CN);
        console.log('  Certificate SHA256 fingerprint:', cert.fingerprint256);

        hash = crypto.createHash('sha256');
        console.log('  Public key ping-sha256:', sha256(cert.pubkey));

        lastprint256 = cert.fingerprint256;
        cert = cert.issuerCertificate;
      } while (cert.fingerprint256 !== lastprint256);

    },
  };

  options.agent = new https.Agent(options);
  const req = https.request(options, (res) => {
    console.log('All OK. Server matched our pinned cert or public key');
    console.log('statusCode:', res.statusCode);
    // Print the HPKP values
    console.log('headers:', res.headers['public-key-pins']);

    res.on('data', (d) => {});
  });

  req.on('error', (e) => {
    console.error(e.message);
  });
  req.end();
  ```

  Outputs for example:

  ```
  Subject Common Name: github.com
    Certificate SHA256 fingerprint: 25:FE:39:32:D9:63:8C:8A:FC:A1:9A:29:87:D8:3E:4C:1D:98:DB:71:E4:1A:48:03:98:EA:22:6A:BD:8B:93:16
    Public key ping-sha256: pL1+qb9HTMRZJmuC/bB/ZI9d302BYrrqiVuRyW+DGrU=
  Subject Common Name: DigiCert SHA2 Extended Validation Server CA
    Certificate SHA256 fingerprint: 40:3E:06:2A:26:53:05:91:13:28:5B:AF:80:A0:D4:AE:42:2C:84:8C:9F:78:FA:D0:1F:C9:4B:C5:B8:7F:EF:1A
    Public key ping-sha256: RRM1dGqnDFsCJXBTHky16vi1obOlCgFFn/yOhI/y+ho=
  Subject Common Name: DigiCert High Assurance EV Root CA
    Certificate SHA256 fingerprint: 74:31:E5:F4:C3:C1:CE:46:90:77:4F:0B:61:E0:54:40:88:3B:A9:A0:1E:D0:0B:A6:AB:D7:80:6E:D3:B1:18:CF
    Public key ping-sha256: WoiWRyIOVNa9ihaBciRSC7XHjliYS9VwUGOIud4PB18=
  All OK. Server matched our pinned cert or public key
  statusCode: 200
  headers: max-age=0; pin-sha256="WoiWRyIOVNa9ihaBciRSC7XHjliYS9VwUGOIud4PB18="; pin-sha256="RRM1dGqnDFsCJXBTHky16vi1obOlCgFFn/yOhI/y+ho=";
  pin-sha256="k2v657xBsOVe1PQRwOsHsw3bsGT2VzIqz5K+59sNQws="; pin-sha256="K87oWBWM9UZfyddvDfoxL+8lpNyoUB2ptGtn0fv6G2Q="; pin-sha256="IQBnNBEiFuhj+8x6X8XLgh01V9Ic5/V3IRQLNFFc7v4=";
  pin-sha256="iie1VXtL7HzAMF+/PVPR9xzT80kQxdZeJ+zduCB3uj0="; pin-sha256="LvRiGEjRqfzurezaWuj8Wie2gyHMrW5Q06LspMnox7A="; includeSubDomains
  ```

  @param options

  Accepts all `options` from `request`, with some differences in default values:

  function [request](https://bun.com/reference/node/https/request)(

  url: string | [URL](https://bun.com/reference/node/url/URL),

  options: [RequestOptions](https://bun.com/reference/node/https/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  Makes a request to a secure web server.

  The following additional `options` from `tls.connect()` are also accepted: `ca`, `cert`, `ciphers`, `clientCertEngine`, `crl`, `dhparam`, `ecdhCurve`, `honorCipherOrder`, `key`, `passphrase`, `pfx`, `rejectUnauthorized`, `secureOptions`, `secureProtocol`, `servername`, `sessionIdContext`, `highWaterMark`.

  `options` can be an object, a string, or a `URL` object. If `options` is a string, it is automatically parsed with `new URL()`. If it is a `URL` object, it will be automatically converted to an ordinary `options` object.

  `https.request()` returns an instance of the `http.ClientRequest` class. The `ClientRequest` instance is a writable stream. If one needs to upload a file with a POST request, then write to the `ClientRequest` object.

  ```
  import https from 'node:https';

  const options = {
    hostname: 'encrypted.google.com',
    port: 443,
    path: '/',
    method: 'GET',
  };

  const req = https.request(options, (res) => {
    console.log('statusCode:', res.statusCode);
    console.log('headers:', res.headers);

    res.on('data', (d) => {
      process.stdout.write(d);
    });
  });

  req.on('error', (e) => {
    console.error(e);
  });
  req.end();
  ```

  Example using options from `tls.connect()`:

  ```
  const options = {
    hostname: 'encrypted.google.com',
    port: 443,
    path: '/',
    method: 'GET',
    key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
    cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
  };
  options.agent = new https.Agent(options);

  const req = https.request(options, (res) => {
    // ...
  });
  ```

  Alternatively, opt out of connection pooling by not using an `Agent`.

  ```
  const options = {
    hostname: 'encrypted.google.com',
    port: 443,
    path: '/',
    method: 'GET',
    key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
    cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem'),
    agent: false,
  };

  const req = https.request(options, (res) => {
    // ...
  });
  ```

  Example using a `URL` as `options`:

  ```
  const options = new URL('https://abc:xyz@example.com');

  const req = https.request(options, (res) => {
    // ...
  });
  ```

  Example pinning on certificate fingerprint, or the public key (similar to`pin-sha256`):

  ```
  import tls from 'node:tls';
  import https from 'node:https';
  import crypto from 'node:crypto';

  function sha256(s) {
    return crypto.createHash('sha256').update(s).digest('base64');
  }
  const options = {
    hostname: 'github.com',
    port: 443,
    path: '/',
    method: 'GET',
    checkServerIdentity: function(host, cert) {
      // Make sure the certificate is issued to the host we are connected to
      const err = tls.checkServerIdentity(host, cert);
      if (err) {
        return err;
      }

      // Pin the public key, similar to HPKP pin-sha256 pinning
      const pubkey256 = 'pL1+qb9HTMRZJmuC/bB/ZI9d302BYrrqiVuRyW+DGrU=';
      if (sha256(cert.pubkey) !== pubkey256) {
        const msg = 'Certificate verification error: ' +
          `The public key of '${cert.subject.CN}' ` +
          'does not match our pinned fingerprint';
        return new Error(msg);
      }

      // Pin the exact certificate, rather than the pub key
      const cert256 = '25:FE:39:32:D9:63:8C:8A:FC:A1:9A:29:87:' +
        'D8:3E:4C:1D:98:DB:71:E4:1A:48:03:98:EA:22:6A:BD:8B:93:16';
      if (cert.fingerprint256 !== cert256) {
        const msg = 'Certificate verification error: ' +
          `The certificate of '${cert.subject.CN}' ` +
          'does not match our pinned fingerprint';
        return new Error(msg);
      }

      // This loop is informational only.
      // Print the certificate and public key fingerprints of all certs in the
      // chain. Its common to pin the public key of the issuer on the public
      // internet, while pinning the public key of the service in sensitive
      // environments.
      do {
        console.log('Subject Common Name:', cert.subject.CN);
        console.log('  Certificate SHA256 fingerprint:', cert.fingerprint256);

        hash = crypto.createHash('sha256');
        console.log('  Public key ping-sha256:', sha256(cert.pubkey));

        lastprint256 = cert.fingerprint256;
        cert = cert.issuerCertificate;
      } while (cert.fingerprint256 !== lastprint256);

    },
  };

  options.agent = new https.Agent(options);
  const req = https.request(options, (res) => {
    console.log('All OK. Server matched our pinned cert or public key');
    console.log('statusCode:', res.statusCode);
    // Print the HPKP values
    console.log('headers:', res.headers['public-key-pins']);

    res.on('data', (d) => {});
  });

  req.on('error', (e) => {
    console.error(e.message);
  });
  req.end();
  ```

  Outputs for example:

  ```
  Subject Common Name: github.com
    Certificate SHA256 fingerprint: 25:FE:39:32:D9:63:8C:8A:FC:A1:9A:29:87:D8:3E:4C:1D:98:DB:71:E4:1A:48:03:98:EA:22:6A:BD:8B:93:16
    Public key ping-sha256: pL1+qb9HTMRZJmuC/bB/ZI9d302BYrrqiVuRyW+DGrU=
  Subject Common Name: DigiCert SHA2 Extended Validation Server CA
    Certificate SHA256 fingerprint: 40:3E:06:2A:26:53:05:91:13:28:5B:AF:80:A0:D4:AE:42:2C:84:8C:9F:78:FA:D0:1F:C9:4B:C5:B8:7F:EF:1A
    Public key ping-sha256: RRM1dGqnDFsCJXBTHky16vi1obOlCgFFn/yOhI/y+ho=
  Subject Common Name: DigiCert High Assurance EV Root CA
    Certificate SHA256 fingerprint: 74:31:E5:F4:C3:C1:CE:46:90:77:4F:0B:61:E0:54:40:88:3B:A9:A0:1E:D0:0B:A6:AB:D7:80:6E:D3:B1:18:CF
    Public key ping-sha256: WoiWRyIOVNa9ihaBciRSC7XHjliYS9VwUGOIud4PB18=
  All OK. Server matched our pinned cert or public key
  statusCode: 200
  headers: max-age=0; pin-sha256="WoiWRyIOVNa9ihaBciRSC7XHjliYS9VwUGOIud4PB18="; pin-sha256="RRM1dGqnDFsCJXBTHky16vi1obOlCgFFn/yOhI/y+ho=";
  pin-sha256="k2v657xBsOVe1PQRwOsHsw3bsGT2VzIqz5K+59sNQws="; pin-sha256="K87oWBWM9UZfyddvDfoxL+8lpNyoUB2ptGtn0fv6G2Q="; pin-sha256="IQBnNBEiFuhj+8x6X8XLgh01V9Ic5/V3IRQLNFFc7v4=";
  pin-sha256="iie1VXtL7HzAMF+/PVPR9xzT80kQxdZeJ+zduCB3uj0="; pin-sha256="LvRiGEjRqfzurezaWuj8Wie2gyHMrW5Q06LspMnox7A="; includeSubDomains
  ```

  @param options

  Accepts all `options` from `request`, with some differences in default values:

## Type definitions

* ### interface [AgentOptions](https://bun.com/reference/node/https/AgentOptions)

  + [agentKeepAliveTimeoutBuffer](https://bun.com/reference/node/https/AgentOptions/agentKeepAliveTimeoutBuffer)?: number

    Milliseconds to subtract from the server-provided `keep-alive: timeout=...` hint when determining socket expiration time. This buffer helps ensure the agent closes the socket slightly before the server does, reducing the chance of sending a request on a socket that’s about to be closed by the server.
  + [allowPartialTrustChain](https://bun.com/reference/node/https/AgentOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/https/AgentOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [autoSelectFamily](https://bun.com/reference/node/https/AgentOptions/autoSelectFamily)?: boolean
  + [autoSelectFamilyAttemptTimeout](https://bun.com/reference/node/https/AgentOptions/autoSelectFamilyAttemptTimeout)?: number
  + [blockList](https://bun.com/reference/node/https/AgentOptions/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)
  + [ca](https://bun.com/reference/node/https/AgentOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/https/AgentOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [checkServerIdentity](https://bun.com/reference/node/https/AgentOptions/checkServerIdentity)?: (hostname: string, cert: [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate)) => undefined | [Error](https://bun.com/reference/globals/Error)
  + [ciphers](https://bun.com/reference/node/https/AgentOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/https/AgentOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [defaultPort](https://bun.com/reference/node/https/AgentOptions/defaultPort)?: number

    Default port to use when the port is not specified in requests.
  + [dhparam](https://bun.com/reference/node/https/AgentOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/https/AgentOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/https/AgentOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [family](https://bun.com/reference/node/https/AgentOptions/family)?: number
  + [hints](https://bun.com/reference/node/https/AgentOptions/hints)?: number
  + [honorCipherOrder](https://bun.com/reference/node/https/AgentOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [host](https://bun.com/reference/node/https/AgentOptions/host)?: string
  + [keepAlive](https://bun.com/reference/node/https/AgentOptions/keepAlive)?: boolean

    Keep sockets around in a pool to be used by other requests in the future. Default = false
  + [keepAliveInitialDelay](https://bun.com/reference/node/https/AgentOptions/keepAliveInitialDelay)?: number
  + [keepAliveMsecs](https://bun.com/reference/node/https/AgentOptions/keepAliveMsecs)?: number

    When using HTTP KeepAlive, how often to send TCP KeepAlive packets over sockets being kept alive. Default = 1000. Only relevant if keepAlive is set to true.
  + [key](https://bun.com/reference/node/https/AgentOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [localAddress](https://bun.com/reference/node/https/AgentOptions/localAddress)?: string
  + [localPort](https://bun.com/reference/node/https/AgentOptions/localPort)?: number
  + [lookup](https://bun.com/reference/node/https/AgentOptions/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxCachedSessions](https://bun.com/reference/node/https/AgentOptions/maxCachedSessions)?: number
  + [maxFreeSockets](https://bun.com/reference/node/https/AgentOptions/maxFreeSockets)?: number

    Maximum number of sockets to leave open in a free state. Only relevant if keepAlive is set to true. Default = 256.
  + [maxSockets](https://bun.com/reference/node/https/AgentOptions/maxSockets)?: number

    Maximum number of sockets to allow per host. Default for Node 0.10 is 5, default for Node 0.12 is Infinity
  + [maxTotalSockets](https://bun.com/reference/node/https/AgentOptions/maxTotalSockets)?: number

    Maximum number of sockets allowed for all hosts in total. Each request will use a new socket until the maximum is reached. Default: Infinity.
  + [maxVersion](https://bun.com/reference/node/https/AgentOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minDHSize](https://bun.com/reference/node/https/AgentOptions/minDHSize)?: number
  + [minVersion](https://bun.com/reference/node/https/AgentOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [noDelay](https://bun.com/reference/node/https/AgentOptions/noDelay)?: boolean
  + [passphrase](https://bun.com/reference/node/https/AgentOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [path](https://bun.com/reference/node/https/AgentOptions/path)?: string
  + [pfx](https://bun.com/reference/node/https/AgentOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [port](https://bun.com/reference/node/https/AgentOptions/port)?: number
  + [proxyEnv](https://bun.com/reference/node/https/AgentOptions/proxyEnv)?: [ProxyEnv](https://bun.com/reference/node/http/ProxyEnv)

    Environment variables for proxy configuration. See [Built-in Proxy Support](https://nodejs.org/docs/latest-v24.x/api/http.html#built-in-proxy-support) for details.
  + [pskCallback](https://bun.com/reference/node/https/AgentOptions/pskCallback)?: (hint: null | string) => null | [PSKCallbackNegotation](https://bun.com/reference/node/tls/PSKCallbackNegotation)

    When negotiating TLS-PSK (pre-shared keys), this function is called with optional identity `hint` provided by the server or `null` in case of TLS 1.3 where `hint` was removed. It will be necessary to provide a custom `tls.checkServerIdentity()` for the connection as the default one will try to check hostname/IP of the server against the certificate but that's not applicable for PSK because there won't be a certificate present. More information can be found in the RFC 4279.
  + [rejectUnauthorized](https://bun.com/reference/node/https/AgentOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [requestCert](https://bun.com/reference/node/https/AgentOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [scheduling](https://bun.com/reference/node/https/AgentOptions/scheduling)?: 'fifo' | 'lifo'

    Scheduling strategy to apply when picking the next free socket to use.
  + [secureContext](https://bun.com/reference/node/https/AgentOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/https/AgentOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [servername](https://bun.com/reference/node/https/AgentOptions/servername)?: string
  + [session](https://bun.com/reference/node/https/AgentOptions/session)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>
  + [sessionIdContext](https://bun.com/reference/node/https/AgentOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/https/AgentOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [sigalgs](https://bun.com/reference/node/https/AgentOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/https/AgentOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [socket](https://bun.com/reference/node/https/AgentOptions/socket)?: [Duplex](https://bun.com/reference/node/stream/default/Duplex)
  + [ticketKeys](https://bun.com/reference/node/https/AgentOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data. See Session Resumption for more information.
  + [timeout](https://bun.com/reference/node/https/AgentOptions/timeout)?: number

    Socket timeout in milliseconds. This will set the timeout after the socket is connected.
* ### interface [RequestOptions](https://bun.com/reference/node/https/RequestOptions)

  + [\_defaultAgent](https://bun.com/reference/node/https/RequestOptions/_defaultAgent)?: [Agent](https://bun.com/reference/node/http/Agent)
  + [agent](https://bun.com/reference/node/https/RequestOptions/agent)?: boolean | [Agent](https://bun.com/reference/node/http/Agent)
  + [allowPartialTrustChain](https://bun.com/reference/node/https/RequestOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/https/RequestOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [auth](https://bun.com/reference/node/https/RequestOptions/auth)?: null | string
  + [ca](https://bun.com/reference/node/https/RequestOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/https/RequestOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [checkServerIdentity](https://bun.com/reference/node/https/RequestOptions/checkServerIdentity)?: (hostname: string, cert: [DetailedPeerCertificate](https://bun.com/reference/node/tls/DetailedPeerCertificate)) => undefined | [Error](https://bun.com/reference/globals/Error)
  + [ciphers](https://bun.com/reference/node/https/RequestOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [createConnection](https://bun.com/reference/node/https/RequestOptions/createConnection)?: (options: [ClientRequestArgs](https://bun.com/reference/node/http/ClientRequestArgs), oncreate: (err: null | [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void) => undefined | null | [Duplex](https://bun.com/reference/node/stream/default/Duplex)
  + [crl](https://bun.com/reference/node/https/RequestOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [defaultPort](https://bun.com/reference/node/https/RequestOptions/defaultPort)?: string | number
  + [dhparam](https://bun.com/reference/node/https/RequestOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/https/RequestOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [family](https://bun.com/reference/node/https/RequestOptions/family)?: number
  + [headers](https://bun.com/reference/node/https/RequestOptions/headers)?: readonly string[] | [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)
  + [hints](https://bun.com/reference/node/https/RequestOptions/hints)?: number

    One or more [supported `getaddrinfo`](https://nodejs.org/docs/latest-v24.x/api/dns.html#supported-getaddrinfo-flags) flags. Multiple flags may be passed by bitwise `OR`ing their values.
  + [honorCipherOrder](https://bun.com/reference/node/https/RequestOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [host](https://bun.com/reference/node/https/RequestOptions/host)?: null | string
  + [hostname](https://bun.com/reference/node/https/RequestOptions/hostname)?: null | string
  + [insecureHTTPParser](https://bun.com/reference/node/https/RequestOptions/insecureHTTPParser)?: boolean
  + [joinDuplicateHeaders](https://bun.com/reference/node/https/RequestOptions/joinDuplicateHeaders)?: boolean
  + [key](https://bun.com/reference/node/https/RequestOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [localAddress](https://bun.com/reference/node/https/RequestOptions/localAddress)?: string
  + [localPort](https://bun.com/reference/node/https/RequestOptions/localPort)?: number
  + [lookup](https://bun.com/reference/node/https/RequestOptions/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxHeaderSize](https://bun.com/reference/node/https/RequestOptions/maxHeaderSize)?: number
  + [maxVersion](https://bun.com/reference/node/https/RequestOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [method](https://bun.com/reference/node/https/RequestOptions/method)?: string
  + [minVersion](https://bun.com/reference/node/https/RequestOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [passphrase](https://bun.com/reference/node/https/RequestOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [path](https://bun.com/reference/node/https/RequestOptions/path)?: null | string
  + [pfx](https://bun.com/reference/node/https/RequestOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [port](https://bun.com/reference/node/https/RequestOptions/port)?: null | string | number
  + [rejectUnauthorized](https://bun.com/reference/node/https/RequestOptions/rejectUnauthorized)?: boolean
  + [secureOptions](https://bun.com/reference/node/https/RequestOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [servername](https://bun.com/reference/node/https/RequestOptions/servername)?: string
  + [sessionIdContext](https://bun.com/reference/node/https/RequestOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/https/RequestOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [setDefaultHeaders](https://bun.com/reference/node/https/RequestOptions/setDefaultHeaders)?: boolean
  + [setHost](https://bun.com/reference/node/https/RequestOptions/setHost)?: boolean
  + [sigalgs](https://bun.com/reference/node/https/RequestOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [signal](https://bun.com/reference/node/https/RequestOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [socketPath](https://bun.com/reference/node/https/RequestOptions/socketPath)?: string
  + [ticketKeys](https://bun.com/reference/node/https/RequestOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data. See Session Resumption for more information.
  + [timeout](https://bun.com/reference/node/https/RequestOptions/timeout)?: number
  + [uniqueHeaders](https://bun.com/reference/node/https/RequestOptions/uniqueHeaders)?: string | string[][]
* ### interface [ServerOptions](https://bun.com/reference/node/https/ServerOptions)<Request extends typeof [http.IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [http.IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [http.ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [http.ServerResponse](https://bun.com/reference/node/http/ServerResponse)>

  + [allowHalfOpen](https://bun.com/reference/node/https/ServerOptions/allowHalfOpen)?: boolean

    Indicates whether half-opened TCP connections are allowed.
  + [allowPartialTrustChain](https://bun.com/reference/node/https/ServerOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/https/ServerOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [blockList](https://bun.com/reference/node/https/ServerOptions/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)

    `blockList` can be used for disabling inbound access to specific IP addresses, IP ranges, or IP subnets. This does not work if the server is behind a reverse proxy, NAT, etc. because the address checked against the block list is the address of the proxy, or the one specified by the NAT.
  + [ca](https://bun.com/reference/node/https/ServerOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/https/ServerOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [ciphers](https://bun.com/reference/node/https/ServerOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [connectionsCheckingInterval](https://bun.com/reference/node/https/ServerOptions/connectionsCheckingInterval)?: number

    Sets the interval value in milliseconds to check for request and headers timeout in incomplete requests.
  + [crl](https://bun.com/reference/node/https/ServerOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/https/ServerOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/https/ServerOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/https/ServerOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [handshakeTimeout](https://bun.com/reference/node/https/ServerOptions/handshakeTimeout)?: number

    Abort the connection if the SSL/TLS handshake does not finish in the specified number of milliseconds. A 'tlsClientError' is emitted on the tls.Server object whenever a handshake times out. Default: 120000 (120 seconds).
  + [headersTimeout](https://bun.com/reference/node/https/ServerOptions/headersTimeout)?: number

    Sets the timeout value in milliseconds for receiving the complete HTTP headers from the client. See Server.headersTimeout for more information.
  + [highWaterMark](https://bun.com/reference/node/https/ServerOptions/highWaterMark)?: number

    Optionally overrides all `socket`s' `readableHighWaterMark` and `writableHighWaterMark`. This affects `highWaterMark` property of both `IncomingMessage` and `ServerResponse`. Default:
  + [honorCipherOrder](https://bun.com/reference/node/https/ServerOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [IncomingMessage](https://bun.com/reference/node/https/ServerOptions/IncomingMessage)?: Request

    Specifies the `IncomingMessage` class to be used. Useful for extending the original `IncomingMessage`.
  + [insecureHTTPParser](https://bun.com/reference/node/https/ServerOptions/insecureHTTPParser)?: boolean

    Use an insecure HTTP parser that accepts invalid HTTP headers when `true`. Using the insecure parser should be avoided. See --insecure-http-parser for more information.
  + [joinDuplicateHeaders](https://bun.com/reference/node/https/ServerOptions/joinDuplicateHeaders)?: boolean

    It joins the field line values of multiple headers in a request with `,`  instead of discarding the duplicates.
  + [keepAlive](https://bun.com/reference/node/https/ServerOptions/keepAlive)?: boolean

    If set to `true`, it enables keep-alive functionality on the socket immediately after a new incoming connection is received, similarly on what is done in `socket.setKeepAlive([enable][, initialDelay])`.
  + [keepAliveInitialDelay](https://bun.com/reference/node/https/ServerOptions/keepAliveInitialDelay)?: number

    If set to a positive number, it sets the initial delay before the first keepalive probe is sent on an idle socket.
  + [keepAliveTimeout](https://bun.com/reference/node/https/ServerOptions/keepAliveTimeout)?: number

    The number of milliseconds of inactivity a server needs to wait for additional incoming data, after it has finished writing the last response, before a socket will be destroyed.
  + [keepAliveTimeoutBuffer](https://bun.com/reference/node/https/ServerOptions/keepAliveTimeoutBuffer)?: number

    An additional buffer time added to the `server.keepAliveTimeout` to extend the internal socket timeout.
  + [key](https://bun.com/reference/node/https/ServerOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [maxHeaderSize](https://bun.com/reference/node/https/ServerOptions/maxHeaderSize)?: number

    Optionally overrides the value of `--max-http-header-size` for requests received by this server, i.e. the maximum length of request headers in bytes.
  + [maxVersion](https://bun.com/reference/node/https/ServerOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minVersion](https://bun.com/reference/node/https/ServerOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [noDelay](https://bun.com/reference/node/https/ServerOptions/noDelay)?: boolean

    If set to `true`, it disables the use of Nagle's algorithm immediately after a new incoming connection is received.
  + [passphrase](https://bun.com/reference/node/https/ServerOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [pauseOnConnect](https://bun.com/reference/node/https/ServerOptions/pauseOnConnect)?: boolean

    Indicates whether the socket should be paused on incoming connections.
  + [pfx](https://bun.com/reference/node/https/ServerOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [pskCallback](https://bun.com/reference/node/https/ServerOptions/pskCallback)?: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket), identity: string) => null | ArrayBufferView<ArrayBufferLike>
  + [pskIdentityHint](https://bun.com/reference/node/https/ServerOptions/pskIdentityHint)?: string

    hint to send to a client to help with selecting the identity during TLS-PSK negotiation. Will be ignored in TLS 1.3. Upon failing to set pskIdentityHint `tlsClientError` will be emitted with `ERR_TLS_PSK_SET_IDENTIY_HINT_FAILED` code.
  + [rejectNonStandardBodyWrites](https://bun.com/reference/node/https/ServerOptions/rejectNonStandardBodyWrites)?: boolean

    If set to `true`, an error is thrown when writing to an HTTP response which does not have a body.
  + [rejectUnauthorized](https://bun.com/reference/node/https/ServerOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [requestCert](https://bun.com/reference/node/https/ServerOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [requestTimeout](https://bun.com/reference/node/https/ServerOptions/requestTimeout)?: number

    Sets the timeout value in milliseconds for receiving the entire request from the client.
  + [requireHostHeader](https://bun.com/reference/node/https/ServerOptions/requireHostHeader)?: boolean

    If set to `true`, it forces the server to respond with a 400 (Bad Request) status code to any HTTP/1.1 request message that lacks a Host header (as mandated by the specification).
  + [secureContext](https://bun.com/reference/node/https/ServerOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/https/ServerOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [ServerResponse](https://bun.com/reference/node/https/ServerOptions/ServerResponse)?: Response

    Specifies the `ServerResponse` class to be used. Useful for extending the original `ServerResponse`.
  + [sessionIdContext](https://bun.com/reference/node/https/ServerOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/https/ServerOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [shouldUpgradeCallback](https://bun.com/reference/node/https/ServerOptions/shouldUpgradeCallback)?: (request: InstanceType<Request>) => boolean

    A callback which receives an incoming request and returns a boolean, to control which upgrade attempts should be accepted. Accepted upgrades will fire an `'upgrade'` event (or their sockets will be destroyed, if no listener is registered) while rejected upgrades will fire a `'request'` event like any non-upgrade request.
  + [sigalgs](https://bun.com/reference/node/https/ServerOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/https/ServerOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [ticketKeys](https://bun.com/reference/node/https/ServerOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data.
  + [uniqueHeaders](https://bun.com/reference/node/https/ServerOptions/uniqueHeaders)?: string | string[][]

    A list of response headers that should be sent only once. If the header's value is an array, the items will be joined using `;` .