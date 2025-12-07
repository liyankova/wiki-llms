---
url: https://bun.com/reference/node/http
title: Node.js http module | API Reference | Bun
source_domain: bun.com
---

# Node.js http module | API Reference | Bun

Node.js module

# [http](https://bun.com/reference/node/http)

The `'node:http'` module provides classes and methods to create HTTP servers and clients. It includes the `IncomingMessage` and `ServerResponse` classes for handling request/response lifecycles on the server side, and the `ClientRequest` and `IncomingMessage` classes for client-side HTTP interactions.

Works in Bun

Fully implemented. Note: Outgoing client request body is currently buffered instead of streamed.

* ### class [Agent](https://bun.com/reference/node/http/Agent)

  An `Agent` is responsible for managing connection persistence and reuse for HTTP clients. It maintains a queue of pending requests for a given host and port, reusing a single socket connection for each until the queue is empty, at which time the socket is either destroyed or put into a pool where it is kept to be used again for requests to the same host and port. Whether it is destroyed or pooled depends on the `keepAlive` `option`.

  Pooled connections have TCP Keep-Alive enabled for them, but servers may still close idle connections, in which case they will be removed from the pool and a new connection will be made when a new HTTP request is made for that host and port. Servers may also refuse to allow multiple requests over the same connection, in which case the connection will have to be remade for every request and cannot be pooled. The `Agent` will still make the requests to that server, but each one will occur over a new connection.

  When a connection is closed by the client or the server, it is removed from the pool. Any unused sockets in the pool will be unrefed so as not to keep the Node.js process running when there are no outstanding requests. (see `socket.unref()`).

  It is good practice, to `destroy()` an `Agent` instance when it is no longer in use, because unused sockets consume OS resources.

  Sockets are removed from an agent when the socket emits either a `'close'` event or an `'agentRemove'` event. When intending to keep one HTTP request open for a long time without keeping it in the agent, something like the following may be done:

  ```
  http.get(options, (res) => {
    // Do stuff
  }).on('socket', (socket) => {
    socket.emit('agentRemove');
  });
  ```

  An agent may also be used for an individual request. By providing `{agent: false}` as an option to the `http.get()` or `http.request()` functions, a one-time use `Agent` with default options will be used for the client connection.

  `agent:false`:

  ```
  http.get({
    hostname: 'localhost',
    port: 80,
    path: '/',
    agent: false,  // Create a new agent just for this one request
  }, (res) => {
    // Do stuff with response
  });
  ```

  `options` in [`socket.connect()`](https://nodejs.org/docs/latest-v24.x/api/net.html#socketconnectoptions-connectlistener) are also supported.

  To configure any of them, a custom Agent instance must be created.

  ```
  import http from 'node:http';
  const keepAliveAgent = new http.Agent({ keepAlive: true });
  options.agent = keepAliveAgent;
  http.request(options, onResponseCallback)
  ```

  + readonly [freeSockets](https://bun.com/reference/node/http/Agent/freeSockets): ReadOnlyDict<[Socket](https://bun.com/reference/node/net/Socket)[]>

    An object which contains arrays of sockets currently awaiting use by the agent when `keepAlive` is enabled. Do not modify.

    Sockets in the `freeSockets` list will be automatically destroyed and removed from the array on `'timeout'`.
  + [maxFreeSockets](https://bun.com/reference/node/http/Agent/maxFreeSockets): number

    By default set to 256. For agents with `keepAlive` enabled, this sets the maximum number of sockets that will be left open in the free state.
  + [maxSockets](https://bun.com/reference/node/http/Agent/maxSockets): number

    By default set to `Infinity`. Determines how many concurrent sockets the agent can have open per origin. Origin is the returned value of `agent.getName()`.
  + [maxTotalSockets](https://bun.com/reference/node/http/Agent/maxTotalSockets): number

    By default set to `Infinity`. Determines how many concurrent sockets the agent can have open. Unlike `maxSockets`, this parameter applies across all origins.
  + readonly [requests](https://bun.com/reference/node/http/Agent/requests): ReadOnlyDict<[IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)[]>

    An object which contains queues of requests that have not yet been assigned to sockets. Do not modify.
  + readonly [sockets](https://bun.com/reference/node/http/Agent/sockets): ReadOnlyDict<[Socket](https://bun.com/reference/node/net/Socket)[]>

    An object which contains arrays of sockets currently in use by the agent. Do not modify.
  + static [captureRejections](https://bun.com/reference/node/http/Agent/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http/Agent/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http/Agent/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/http/Agent/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http/Agent/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http/Agent/addListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [createConnection](https://bun.com/reference/node/http/Agent/createConnection)(

    options: [ClientRequestArgs](https://bun.com/reference/node/http/ClientRequestArgs),

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
  + [destroy](https://bun.com/reference/node/http/Agent/destroy)(): void;

    Destroy any sockets that are currently in use by the agent.

    It is usually not necessary to do this. However, if using an agent with `keepAlive` enabled, then it is best to explicitly shut down the agent when it is no longer needed. Otherwise, sockets might stay open for quite a long time before the server terminates them.
  + [emit](https://bun.com/reference/node/http/Agent/emit)<K>(

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
  + [eventNames](https://bun.com/reference/node/http/Agent/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/http/Agent/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getName](https://bun.com/reference/node/http/Agent/getName)(

    options?: [ClientRequestArgs](https://bun.com/reference/node/http/ClientRequestArgs)

    ): string;

    Get a unique name for a set of request options, to determine whether a connection can be reused. For an HTTP agent, this returns`host:port:localAddress` or `host:port:localAddress:family`. For an HTTPS agent, the name includes the CA, cert, ciphers, and other HTTPS/TLS-specific options that determine socket reusability.

    @param options

    A set of options providing information for name generation
  + [keepSocketAlive](https://bun.com/reference/node/http/Agent/keepSocketAlive)(

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
  + [listenerCount](https://bun.com/reference/node/http/Agent/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http/Agent/listeners)<K>(

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
  + [off](https://bun.com/reference/node/http/Agent/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http/Agent/on)<K>(

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
  + [once](https://bun.com/reference/node/http/Agent/once)<K>(

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
  + [prependListener](https://bun.com/reference/node/http/Agent/prependListener)<K>(

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
  + [prependOnceListener](https://bun.com/reference/node/http/Agent/prependOnceListener)<K>(

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
  + [rawListeners](https://bun.com/reference/node/http/Agent/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/http/Agent/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http/Agent/removeListener)<K>(

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
  + [reuseSocket](https://bun.com/reference/node/http/Agent/reuseSocket)(

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex),

    request: [ClientRequest](https://bun.com/reference/node/http/ClientRequest)

    ): void;

    Called when `socket` is attached to `request` after being persisted because of the keep-alive options. Default behavior is to:

    ```
    socket.ref();
    ```

    This method can be overridden by a particular `Agent` subclass.

    The `socket` argument can be an instance of `net.Socket`, a subclass of `stream.Duplex`.
  + [setMaxListeners](https://bun.com/reference/node/http/Agent/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/http/Agent/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/http/Agent/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/http/Agent/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/http/Agent/on)(

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

    static [on](https://bun.com/reference/node/http/Agent/on)(

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
  + static [once](https://bun.com/reference/node/http/Agent/once)(

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

    static [once](https://bun.com/reference/node/http/Agent/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/http/Agent/setMaxListeners)(

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
* ### class [ClientRequest](https://bun.com/reference/node/http/ClientRequest)

  This object is created internally and returned from request. It represents an *in-progress* request whose header has already been queued. The header is still mutable using the `setHeader(name, value)`, `getHeader(name)`, `removeHeader(name)` API. The actual header will be sent along with the first data chunk or when calling `request.end()`.

  To get the response, add a listener for `'response'` to the request object. `'response'` will be emitted from the request object when the response headers have been received. The `'response'` event is executed with one argument which is an instance of IncomingMessage.

  During the `'response'` event, one can add listeners to the response object; particularly to listen for the `'data'` event.

  If no `'response'` handler is added, then the response will be entirely discarded. However, if a `'response'` event handler is added, then the data from the response object **must** be consumed, either by calling `response.read()` whenever there is a `'readable'` event, or by adding a `'data'` handler, or by calling the `.resume()` method. Until the data is consumed, the `'end'` event will not fire. Also, until the data is read it will consume memory that can eventually lead to a 'process out of memory' error.

  For backward compatibility, `res` will only emit `'error'` if there is an `'error'` listener registered.

  Set `Content-Length` header to limit the response body size. If `response.strictContentLength` is set to `true`, mismatching the `Content-Length` header value will result in an `Error` being thrown, identified by ``` code:``'ERR_HTTP_CONTENT_LENGTH_MISMATCH' ```.

  `Content-Length` value should be in bytes, not characters. Use `Buffer.byteLength()` to determine the length of the body in bytes.

  + [chunkedEncoding](https://bun.com/reference/node/http/ClientRequest/chunkedEncoding): boolean
  + readonly [closed](https://bun.com/reference/node/http/ClientRequest/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/http/ClientRequest/destroyed): boolean

    Is `true` after `writable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/http/ClientRequest/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [headersSent](https://bun.com/reference/node/http/ClientRequest/headersSent): boolean

    Read-only. `true` if the headers were sent, otherwise `false`.
  + [host](https://bun.com/reference/node/http/ClientRequest/host): string

    The request host.
  + [maxHeadersCount](https://bun.com/reference/node/http/ClientRequest/maxHeadersCount): number

    Limits maximum response headers count. If set to 0, no limit will be applied.
  + [method](https://bun.com/reference/node/http/ClientRequest/method): string

    The request method.
  + [path](https://bun.com/reference/node/http/ClientRequest/path): string

    The request path.
  + readonly [req](https://bun.com/reference/node/http/ClientRequest/req): [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)
  + [reusedSocket](https://bun.com/reference/node/http/ClientRequest/reusedSocket): boolean

    When sending request through a keep-alive enabled agent, the underlying socket might be reused. But if server closes connection at unfortunate time, client may run into a 'ECONNRESET' error.

    ```
    import http from 'node:http';

    // Server has a 5 seconds keep-alive timeout by default
    http
      .createServer((req, res) => {
        res.write('hello\n');
        res.end();
      })
      .listen(3000);

    setInterval(() => {
      // Adapting a keep-alive agent
      http.get('http://localhost:3000', { agent }, (res) => {
        res.on('data', (data) => {
          // Do nothing
        });
      });
    }, 5000); // Sending request on 5s interval so it's easy to hit idle timeout
    ```

    By marking a request whether it reused socket or not, we can do automatic error retry base on it.

    ```
    import http from 'node:http';
    const agent = new http.Agent({ keepAlive: true });

    function retriableRequest() {
      const req = http
        .get('http://localhost:3000', { agent }, (res) => {
          // ...
        })
        .on('error', (err) => {
          // Check if retry is needed
          if (req.reusedSocket &#x26;&#x26; err.code === 'ECONNRESET') {
            retriableRequest();
          }
        });
    }

    retriableRequest();
    ```
  + [sendDate](https://bun.com/reference/node/http/ClientRequest/sendDate): boolean
  + [shouldKeepAlive](https://bun.com/reference/node/http/ClientRequest/shouldKeepAlive): boolean
  + readonly [socket](https://bun.com/reference/node/http/ClientRequest/socket): null | [Socket](https://bun.com/reference/node/net/Socket)

    Reference to the underlying socket. Usually, users will not want to access this property.

    After calling `outgoingMessage.end()`, this property will be nulled.
  + [useChunkedEncodingByDefault](https://bun.com/reference/node/http/ClientRequest/useChunkedEncodingByDefault): boolean
  + readonly [writable](https://bun.com/reference/node/http/ClientRequest/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/http/ClientRequest/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/http/ClientRequest/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/http/ClientRequest/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/http/ClientRequest/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/http/ClientRequest/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/http/ClientRequest/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/http/ClientRequest/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/http/ClientRequest/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + static [captureRejections](https://bun.com/reference/node/http/ClientRequest/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http/ClientRequest/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http/ClientRequest/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/http/ClientRequest/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/http/ClientRequest/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http/ClientRequest/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/http/ClientRequest/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_write](https://bun.com/reference/node/http/ClientRequest/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/http/ClientRequest/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http/ClientRequest/[asyncDispose])(): Promise<void>;

    Calls `writable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http/ClientRequest/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;

  + [addTrailers](https://bun.com/reference/node/http/ClientRequest/addTrailers)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders) | readonly [string, string][]

    ): void;

    Adds HTTP trailers (headers but at the end of the message) to the message.

    Trailers will **only** be emitted if the message is chunked encoded. If not, the trailers will be silently discarded.

    HTTP requires the `Trailer` header to be sent to emit trailers, with a list of header field names in its value, e.g.

    ```
    message.writeHead(200, { 'Content-Type': 'text/plain',
                             'Trailer': 'Content-MD5' });
    message.write(fileData);
    message.addTrailers({ 'Content-MD5': '7895bf4b8828b55ceaf47747b4bca667' });
    message.end();
    ```

    Attempting to set a header field name or value that contains invalid characters will result in a `TypeError` being thrown.
  + [appendHeader](https://bun.com/reference/node/http/ClientRequest/appendHeader)(

    name: string,

    value: string | readonly string[]

    ): this;

    Append a single header value to the header object.

    If the value is an array, this is equivalent to calling this method multiple times.

    If there were no previous values for the header, this is equivalent to calling `outgoingMessage.setHeader(name, value)`.

    Depending of the value of `options.uniqueHeaders` when the client request or the server were created, this will end up in the header being sent multiple times or a single time with values joined using `;` .

    @param name

    Header name

    @param value

    Header value
  + [compose](https://bun.com/reference/node/http/ClientRequest/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/http/ClientRequest/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/http/ClientRequest/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the writable stream has ended and subsequent calls to `write()` or `end()` will result in an `ERR_STREAM_DESTROYED` error. This is a destructive and immediate way to destroy a stream. Previous calls to `write()` may not have drained, and may trigger an `ERR_STREAM_DESTROYED` error. Use `end()` instead of destroy if data should flush before close, or wait for the `'drain'` event before destroying the stream.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `writable._destroy()`.

    @param error

    Optional, an error to emit with `'error'` event.
  + [emit](https://bun.com/reference/node/http/ClientRequest/emit)(

    event: 'close'

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

    [emit](https://bun.com/reference/node/http/ClientRequest/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/http/ClientRequest/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http/ClientRequest/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/http/ClientRequest/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http/ClientRequest/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http/ClientRequest/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/http/ClientRequest/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/http/ClientRequest/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/http/ClientRequest/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/http/ClientRequest/eventNames)(): string | symbol[];

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
  + [flushHeaders](https://bun.com/reference/node/http/ClientRequest/flushHeaders)(): void;

    Flushes the message headers.

    For efficiency reason, Node.js normally buffers the message headers until `outgoingMessage.end()` is called or the first chunk of message data is written. It then tries to pack the headers and data into a single TCP packet.

    It is usually desired (it saves a TCP round-trip), but not when the first data is not sent until possibly much later. `outgoingMessage.flushHeaders()` bypasses the optimization and kickstarts the message.
  + [getHeader](https://bun.com/reference/node/http/ClientRequest/getHeader)(

    name: string

    ): undefined | string | number | string[];

    Gets the value of the HTTP header with the given name. If that header is not set, the returned value will be `undefined`.

    @param name

    Name of header
  + [getHeaderNames](https://bun.com/reference/node/http/ClientRequest/getHeaderNames)(): string[];

    Returns an array containing the unique names of the current outgoing headers. All names are lowercase.
  + [getHeaders](https://bun.com/reference/node/http/ClientRequest/getHeaders)(): [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders);

    Returns a shallow copy of the current outgoing headers. Since a shallow copy is used, array values may be mutated without additional calls to various header-related HTTP module methods. The keys of the returned object are the header names and the values are the respective header values. All header names are lowercase.

    The object returned by the `outgoingMessage.getHeaders()` method does not prototypically inherit from the JavaScript `Object`. This means that typical `Object` methods such as `obj.toString()`, `obj.hasOwnProperty()`, and others are not defined and will not work.

    ```
    outgoingMessage.setHeader('Foo', 'bar');
    outgoingMessage.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

    const headers = outgoingMessage.getHeaders();
    // headers === { foo: 'bar', 'set-cookie': ['foo=bar', 'bar=baz'] }
    ```
  + [getMaxListeners](https://bun.com/reference/node/http/ClientRequest/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getRawHeaderNames](https://bun.com/reference/node/http/ClientRequest/getRawHeaderNames)(): string[];

    Returns an array containing the unique names of the current outgoing raw headers. Header names are returned with their exact casing being set.

    ```
    request.setHeader('Foo', 'bar');
    request.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

    const headerNames = request.getRawHeaderNames();
    // headerNames === ['Foo', 'Set-Cookie']
    ```
  + [hasHeader](https://bun.com/reference/node/http/ClientRequest/hasHeader)(

    name: string

    ): boolean;

    Returns `true` if the header identified by `name` is currently set in the outgoing headers. The header name is case-insensitive.

    ```
    const hasContentType = outgoingMessage.hasHeader('content-type');
    ```
  + [listenerCount](https://bun.com/reference/node/http/ClientRequest/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http/ClientRequest/listeners)<K>(

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
  + [off](https://bun.com/reference/node/http/ClientRequest/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.

  + [onSocket](https://bun.com/reference/node/http/ClientRequest/onSocket)(

    socket: [Socket](https://bun.com/reference/node/net/Socket)

    ): void;
  + [pipe](https://bun.com/reference/node/http/ClientRequest/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;

  + [rawListeners](https://bun.com/reference/node/http/ClientRequest/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/http/ClientRequest/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeHeader](https://bun.com/reference/node/http/ClientRequest/removeHeader)(

    name: string

    ): void;

    Removes a header that is queued for implicit sending.

    ```
    outgoingMessage.removeHeader('Content-Encoding');
    ```

    @param name

    Header name
  + [removeListener](https://bun.com/reference/node/http/ClientRequest/removeListener)(

    event: 'close',

    listener: () => void

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

    [removeListener](https://bun.com/reference/node/http/ClientRequest/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ClientRequest/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ClientRequest/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ClientRequest/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ClientRequest/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ClientRequest/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [setDefaultEncoding](https://bun.com/reference/node/http/ClientRequest/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setHeader](https://bun.com/reference/node/http/ClientRequest/setHeader)(

    name: string,

    value: string | number | readonly string[]

    ): this;

    Sets a single header value. If the header already exists in the to-be-sent headers, its value will be replaced. Use an array of strings to send multiple headers with the same name.

    @param name

    Header name

    @param value

    Header value
  + [setHeaders](https://bun.com/reference/node/http/ClientRequest/setHeaders)(

    headers: [Headers](https://bun.com/reference/globals/Headers) | Map<string, string | number | readonly string[]>

    ): this;

    Sets multiple header values for implicit headers. headers must be an instance of `Headers` or `Map`, if a header already exists in the to-be-sent headers, its value will be replaced.

    ```
    const headers = new Headers({ foo: 'bar' });
    outgoingMessage.setHeaders(headers);
    ```

    or

    ```
    const headers = new Map([['foo', 'bar']]);
    outgoingMessage.setHeaders(headers);
    ```

    When headers have been set with `outgoingMessage.setHeaders()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    ```
    // Returns content-type = text/plain
    const server = http.createServer((req, res) => {
      const headers = new Headers({ 'Content-Type': 'text/html' });
      res.setHeaders(headers);
      res.writeHead(200, { 'Content-Type': 'text/plain' });
      res.end('ok');
    });
    ```
  + [setMaxListeners](https://bun.com/reference/node/http/ClientRequest/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setNoDelay](https://bun.com/reference/node/http/ClientRequest/setNoDelay)(

    noDelay?: boolean

    ): void;

    Once a socket is assigned to this request and is connected `socket.setNoDelay()` will be called.
  + [setSocketKeepAlive](https://bun.com/reference/node/http/ClientRequest/setSocketKeepAlive)(

    enable?: boolean,

    initialDelay?: number

    ): void;

    Once a socket is assigned to this request and is connected `socket.setKeepAlive()` will be called.
  + [setTimeout](https://bun.com/reference/node/http/ClientRequest/setTimeout)(

    timeout: number,

    callback?: () => void

    ): this;

    Once a socket is assigned to this request and is connected `socket.setTimeout()` will be called.

    @param timeout

    Milliseconds before a request times out.

    @param callback

    Optional function to be called when a timeout occurs. Same as binding to the `'timeout'` event.
  + [uncork](https://bun.com/reference/node/http/ClientRequest/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [write](https://bun.com/reference/node/http/ClientRequest/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/http/ClientRequest/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
  + static [addAbortListener](https://bun.com/reference/node/http/ClientRequest/addAbortListener)(

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
  + static [fromWeb](https://bun.com/reference/node/http/ClientRequest/fromWeb)(

    writableStream: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream),

    options?: Pick<[WritableOptions](https://bun.com/reference/node/stream/default/WritableOptions)<[Writable](https://bun.com/reference/node/stream/default/Writable)>, 'signal' | 'decodeStrings' | 'highWaterMark' | 'objectMode'>

    ): [Writable](https://bun.com/reference/node/stream/default/Writable);

    A utility method for creating a `Writable` from a web `WritableStream`.
  + static [getEventListeners](https://bun.com/reference/node/http/ClientRequest/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/http/ClientRequest/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/http/ClientRequest/on)(

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

    static [on](https://bun.com/reference/node/http/ClientRequest/on)(

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
  + static [once](https://bun.com/reference/node/http/ClientRequest/once)(

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

    static [once](https://bun.com/reference/node/http/ClientRequest/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/http/ClientRequest/setMaxListeners)(

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
  + static [toWeb](https://bun.com/reference/node/http/ClientRequest/toWeb)(

    streamWritable: [Writable](https://bun.com/reference/node/stream/default/Writable)

    ): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream);

    A utility method for creating a web `WritableStream` from a `Writable`.
* ### class [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)

  An `IncomingMessage` object is created by Server or ClientRequest and passed as the first argument to the `'request'` and `'response'` event respectively. It may be used to access response status, headers, and data.

  Different from its `socket` value which is a subclass of `stream.Duplex`, the `IncomingMessage` itself extends `stream.Readable` and is created separately to parse and emit the incoming HTTP headers and payload, as the underlying socket may be reused multiple times in case of keep-alive.

  + readonly [closed](https://bun.com/reference/node/http/IncomingMessage/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [complete](https://bun.com/reference/node/http/IncomingMessage/complete): boolean

    The `message.complete` property will be `true` if a complete HTTP message has been received and successfully parsed.

    This property is particularly useful as a means of determining if a client or server fully transmitted a message before a connection was terminated:

    ```
    const req = http.request({
      host: '127.0.0.1',
      port: 8080,
      method: 'POST',
    }, (res) => {
      res.resume();
      res.on('end', () => {
        if (!res.complete)
          console.error(
            'The connection was terminated while the message was still being sent');
      });
    });
    ```
  + [destroyed](https://bun.com/reference/node/http/IncomingMessage/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/http/IncomingMessage/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [headers](https://bun.com/reference/node/http/IncomingMessage/headers): [IncomingHttpHeaders](https://bun.com/reference/node/http/IncomingHttpHeaders)

    The request/response headers object.

    Key-value pairs of header names and values. Header names are lower-cased.

    ```
    // Prints something like:
    //
    // { 'user-agent': 'curl/7.22.0',
    //   host: '127.0.0.1:8000',
    //   accept: '*' }
    console.log(request.headers);
    ```

    Duplicates in raw headers are handled in the following ways, depending on the header name:

    - Duplicates of `age`, `authorization`, `content-length`, `content-type`, `etag`, `expires`, `from`, `host`, `if-modified-since`, `if-unmodified-since`, `last-modified`, `location`, `max-forwards`, `proxy-authorization`, `referer`, `retry-after`, `server`, or `user-agent` are discarded. To allow duplicate values of the headers listed above to be joined, use the option `joinDuplicateHeaders` in request and createServer. See RFC 9110 Section 5.3 for more information.
    - `set-cookie` is always an array. Duplicates are added to the array.
    - For duplicate `cookie` headers, the values are joined together with `;` .
    - For all other headers, the values are joined together with `,` .
  + [headersDistinct](https://bun.com/reference/node/http/IncomingMessage/headersDistinct): Dict<string[]>

    Similar to `message.headers`, but there is no join logic and the values are always arrays of strings, even for headers received just once.

    ```
    // Prints something like:
    //
    // { 'user-agent': ['curl/7.22.0'],
    //   host: ['127.0.0.1:8000'],
    //   accept: ['*'] }
    console.log(request.headersDistinct);
    ```
  + [httpVersion](https://bun.com/reference/node/http/IncomingMessage/httpVersion): string

    In case of server request, the HTTP version sent by the client. In the case of client response, the HTTP version of the connected-to server. Probably either `'1.1'` or `'1.0'`.

    Also `message.httpVersionMajor` is the first integer and `message.httpVersionMinor` is the second.
  + [httpVersionMajor](https://bun.com/reference/node/http/IncomingMessage/httpVersionMajor): number
  + [httpVersionMinor](https://bun.com/reference/node/http/IncomingMessage/httpVersionMinor): number
  + [method](https://bun.com/reference/node/http/IncomingMessage/method)?: string

    **Only valid for request obtained from Server.**

    The request method as a string. Read only. Examples: `'GET'`, `'DELETE'`.
  + [rawHeaders](https://bun.com/reference/node/http/IncomingMessage/rawHeaders): string[]

    The raw request/response headers list exactly as they were received.

    The keys and values are in the same list. It is *not* a list of tuples. So, the even-numbered offsets are key values, and the odd-numbered offsets are the associated values.

    Header names are not lowercased, and duplicates are not merged.

    ```
    // Prints something like:
    //
    // [ 'user-agent',
    //   'this is invalid because there can be only one',
    //   'User-Agent',
    //   'curl/7.22.0',
    //   'Host',
    //   '127.0.0.1:8000',
    //   'ACCEPT',
    //   '*' ]
    console.log(request.rawHeaders);
    ```
  + [rawTrailers](https://bun.com/reference/node/http/IncomingMessage/rawTrailers): string[]

    The raw request/response trailer keys and values exactly as they were received. Only populated at the `'end'` event.
  + [readable](https://bun.com/reference/node/http/IncomingMessage/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/http/IncomingMessage/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/http/IncomingMessage/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/http/IncomingMessage/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/http/IncomingMessage/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/http/IncomingMessage/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/http/IncomingMessage/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/http/IncomingMessage/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/http/IncomingMessage/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [socket](https://bun.com/reference/node/http/IncomingMessage/socket): [Socket](https://bun.com/reference/node/net/Socket)

    The `net.Socket` object associated with the connection.

    With HTTPS support, use `request.socket.getPeerCertificate()` to obtain the client's authentication details.

    This property is guaranteed to be an instance of the `net.Socket` class, a subclass of `stream.Duplex`, unless the user specified a socket type other than `net.Socket` or internally nulled.
  + [statusCode](https://bun.com/reference/node/http/IncomingMessage/statusCode)?: number

    **Only valid for response obtained from ClientRequest.**

    The 3-digit HTTP response status code. E.G. `404`.
  + [statusMessage](https://bun.com/reference/node/http/IncomingMessage/statusMessage)?: string

    **Only valid for response obtained from ClientRequest.**

    The HTTP response status message (reason phrase). E.G. `OK` or `Internal Server Error`.
  + [trailers](https://bun.com/reference/node/http/IncomingMessage/trailers): Dict<string>

    The request/response trailers object. Only populated at the `'end'` event.
  + [trailersDistinct](https://bun.com/reference/node/http/IncomingMessage/trailersDistinct): Dict<string[]>

    Similar to `message.trailers`, but there is no join logic and the values are always arrays of strings, even for headers received just once. Only populated at the `'end'` event.
  + [url](https://bun.com/reference/node/http/IncomingMessage/url)?: string

    **Only valid for request obtained from Server.**

    Request URL string. This contains only the URL that is present in the actual HTTP request. Take the following request:

    ```
    GET /status?name=ryan HTTP/1.1
    Accept: text/plain
    ```

    To parse the URL into its parts:

    ```
    new URL(`http://${process.env.HOST ?? 'localhost'}${request.url}`);
    ```

    When `request.url` is `'/status?name=ryan'` and `process.env.HOST` is undefined:

    ```
    $ node
    > new URL(`http://${process.env.HOST ?? 'localhost'}${request.url}`);
    URL {
      href: 'http://localhost/status?name=ryan',
      origin: 'http://localhost',
      protocol: 'http:',
      username: '',
      password: '',
      host: 'localhost',
      hostname: 'localhost',
      port: '',
      pathname: '/status',
      search: '?name=ryan',
      searchParams: URLSearchParams { 'name' => 'ryan' },
      hash: ''
    }
    ```

    Ensure that you set `process.env.HOST` to the server's host name, or consider replacing this part entirely. If using `req.headers.host`, ensure proper validation is used, as clients may specify a custom `Host` header.
  + static [captureRejections](https://bun.com/reference/node/http/IncomingMessage/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http/IncomingMessage/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http/IncomingMessage/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/http/IncomingMessage/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/http/IncomingMessage/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http/IncomingMessage/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/http/IncomingMessage/_read)(

    size: number

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http/IncomingMessage/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/http/IncomingMessage/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http/IncomingMessage/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume

    [addListener](https://bun.com/reference/node/http/IncomingMessage/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. end
    4. error
    5. pause
    6. readable
    7. resume
  + [asIndexedPairs](https://bun.com/reference/node/http/IncomingMessage/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [compose](https://bun.com/reference/node/http/IncomingMessage/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [destroy](https://bun.com/reference/node/http/IncomingMessage/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Calls `destroy()` on the socket that received the `IncomingMessage`. If `error` is provided, an `'error'` event is emitted on the socket and `error` is passed as an argument to any listeners on the event.
  + [drop](https://bun.com/reference/node/http/IncomingMessage/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: 'close'

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

    [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/http/IncomingMessage/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/http/IncomingMessage/eventNames)(): string | symbol[];

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
  + [every](https://bun.com/reference/node/http/IncomingMessage/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/http/IncomingMessage/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/http/IncomingMessage/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/http/IncomingMessage/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/http/IncomingMessage/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/http/IncomingMessage/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/http/IncomingMessage/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/http/IncomingMessage/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/http/IncomingMessage/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/http/IncomingMessage/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http/IncomingMessage/listeners)<K>(

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
  + [map](https://bun.com/reference/node/http/IncomingMessage/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/http/IncomingMessage/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: 'close',

    listener: () => void

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

    [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/IncomingMessage/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: 'close',

    listener: () => void

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

    [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/IncomingMessage/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/http/IncomingMessage/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/http/IncomingMessage/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: 'close',

    listener: () => void

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

    [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/IncomingMessage/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: 'close',

    listener: () => void

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

    [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/IncomingMessage/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/http/IncomingMessage/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/http/IncomingMessage/rawListeners)<K>(

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
  + [read](https://bun.com/reference/node/http/IncomingMessage/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/http/IncomingMessage/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/http/IncomingMessage/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/http/IncomingMessage/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: 'close',

    listener: () => void

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

    [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/IncomingMessage/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/http/IncomingMessage/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setEncoding](https://bun.com/reference/node/http/IncomingMessage/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/http/IncomingMessage/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http/IncomingMessage/setTimeout)(

    msecs: number,

    callback?: () => void

    ): this;

    Calls `message.socket.setTimeout(msecs, callback)`.
  + [some](https://bun.com/reference/node/http/IncomingMessage/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/http/IncomingMessage/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/http/IncomingMessage/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [unpipe](https://bun.com/reference/node/http/IncomingMessage/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/http/IncomingMessage/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/http/IncomingMessage/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + static [addAbortListener](https://bun.com/reference/node/http/IncomingMessage/addAbortListener)(

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
  + static [from](https://bun.com/reference/node/http/IncomingMessage/from)(

    iterable: Iterable<any, any, any> | AsyncIterable<any, any, any>,

    options?: [ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    A utility method for creating Readable Streams out of iterators.

    @param iterable

    Object implementing the `Symbol.asyncIterator` or `Symbol.iterator` iterable protocol. Emits an 'error' event if a null value is passed.

    @param options

    Options provided to `new stream.Readable([options])`. By default, `Readable.from()` will set `options.objectMode` to `true`, unless this is explicitly opted out by setting `options.objectMode` to `false`.
  + static [fromWeb](https://bun.com/reference/node/http/IncomingMessage/fromWeb)(

    readableStream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream),

    options?: Pick<[ReadableOptions](https://bun.com/reference/node/stream/default/ReadableOptions)<[Readable](https://bun.com/reference/node/stream/default/Readable)>, 'signal' | 'encoding' | 'highWaterMark' | 'objectMode'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    A utility method for creating a `Readable` from a web `ReadableStream`.
  + static [getEventListeners](https://bun.com/reference/node/http/IncomingMessage/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/http/IncomingMessage/getMaxListeners)(

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
  + static [isDisturbed](https://bun.com/reference/node/http/IncomingMessage/isDisturbed)(

    stream: [Readable](https://bun.com/reference/node/stream/default/Readable) | ReadableStream

    ): boolean;

    Returns whether the stream has been read from or cancelled.
  + static [on](https://bun.com/reference/node/http/IncomingMessage/on)(

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

    static [on](https://bun.com/reference/node/http/IncomingMessage/on)(

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
  + static [once](https://bun.com/reference/node/http/IncomingMessage/once)(

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

    static [once](https://bun.com/reference/node/http/IncomingMessage/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/http/IncomingMessage/setMaxListeners)(

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
  + static [toWeb](https://bun.com/reference/node/http/IncomingMessage/toWeb)(

    streamReadable: [Readable](https://bun.com/reference/node/stream/default/Readable),

    options?: { strategy: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<any> }

    ): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream);

    A utility method for creating a web `ReadableStream` from a `Readable`.
* ### class [OutgoingMessage](https://bun.com/reference/node/http/OutgoingMessage)<Request extends [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)>

  This class serves as the parent class of ClientRequest and ServerResponse. It is an abstract outgoing message from the perspective of the participants of an HTTP transaction.

  + [chunkedEncoding](https://bun.com/reference/node/http/OutgoingMessage/chunkedEncoding): boolean
  + readonly [closed](https://bun.com/reference/node/http/OutgoingMessage/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/http/OutgoingMessage/destroyed): boolean

    Is `true` after `writable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/http/OutgoingMessage/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [headersSent](https://bun.com/reference/node/http/OutgoingMessage/headersSent): boolean

    Read-only. `true` if the headers were sent, otherwise `false`.
  + readonly [req](https://bun.com/reference/node/http/OutgoingMessage/req): Request
  + [sendDate](https://bun.com/reference/node/http/OutgoingMessage/sendDate): boolean
  + [shouldKeepAlive](https://bun.com/reference/node/http/OutgoingMessage/shouldKeepAlive): boolean
  + readonly [socket](https://bun.com/reference/node/http/OutgoingMessage/socket): null | [Socket](https://bun.com/reference/node/net/Socket)

    Reference to the underlying socket. Usually, users will not want to access this property.

    After calling `outgoingMessage.end()`, this property will be nulled.
  + [useChunkedEncodingByDefault](https://bun.com/reference/node/http/OutgoingMessage/useChunkedEncodingByDefault): boolean
  + readonly [writable](https://bun.com/reference/node/http/OutgoingMessage/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/http/OutgoingMessage/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/http/OutgoingMessage/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/http/OutgoingMessage/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/http/OutgoingMessage/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/http/OutgoingMessage/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/http/OutgoingMessage/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/http/OutgoingMessage/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/http/OutgoingMessage/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + static [captureRejections](https://bun.com/reference/node/http/OutgoingMessage/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http/OutgoingMessage/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http/OutgoingMessage/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/http/OutgoingMessage/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/http/OutgoingMessage/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http/OutgoingMessage/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/http/OutgoingMessage/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_write](https://bun.com/reference/node/http/OutgoingMessage/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/http/OutgoingMessage/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http/OutgoingMessage/[asyncDispose])(): Promise<void>;

    Calls `writable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http/OutgoingMessage/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http/OutgoingMessage/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/OutgoingMessage/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/OutgoingMessage/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/OutgoingMessage/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/OutgoingMessage/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/OutgoingMessage/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/OutgoingMessage/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe
  + [addTrailers](https://bun.com/reference/node/http/OutgoingMessage/addTrailers)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders) | readonly [string, string][]

    ): void;

    Adds HTTP trailers (headers but at the end of the message) to the message.

    Trailers will **only** be emitted if the message is chunked encoded. If not, the trailers will be silently discarded.

    HTTP requires the `Trailer` header to be sent to emit trailers, with a list of header field names in its value, e.g.

    ```
    message.writeHead(200, { 'Content-Type': 'text/plain',
                             'Trailer': 'Content-MD5' });
    message.write(fileData);
    message.addTrailers({ 'Content-MD5': '7895bf4b8828b55ceaf47747b4bca667' });
    message.end();
    ```

    Attempting to set a header field name or value that contains invalid characters will result in a `TypeError` being thrown.
  + [appendHeader](https://bun.com/reference/node/http/OutgoingMessage/appendHeader)(

    name: string,

    value: string | readonly string[]

    ): this;

    Append a single header value to the header object.

    If the value is an array, this is equivalent to calling this method multiple times.

    If there were no previous values for the header, this is equivalent to calling `outgoingMessage.setHeader(name, value)`.

    Depending of the value of `options.uniqueHeaders` when the client request or the server were created, this will end up in the header being sent multiple times or a single time with values joined using `;` .

    @param name

    Header name

    @param value

    Header value
  + [compose](https://bun.com/reference/node/http/OutgoingMessage/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/http/OutgoingMessage/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/http/OutgoingMessage/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the writable stream has ended and subsequent calls to `write()` or `end()` will result in an `ERR_STREAM_DESTROYED` error. This is a destructive and immediate way to destroy a stream. Previous calls to `write()` may not have drained, and may trigger an `ERR_STREAM_DESTROYED` error. Use `end()` instead of destroy if data should flush before close, or wait for the `'drain'` event before destroying the stream.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `writable._destroy()`.

    @param error

    Optional, an error to emit with `'error'` event.
  + [emit](https://bun.com/reference/node/http/OutgoingMessage/emit)(

    event: 'close'

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

    [emit](https://bun.com/reference/node/http/OutgoingMessage/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/http/OutgoingMessage/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http/OutgoingMessage/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/http/OutgoingMessage/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http/OutgoingMessage/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http/OutgoingMessage/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/http/OutgoingMessage/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/http/OutgoingMessage/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/http/OutgoingMessage/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/http/OutgoingMessage/eventNames)(): string | symbol[];

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
  + [flushHeaders](https://bun.com/reference/node/http/OutgoingMessage/flushHeaders)(): void;

    Flushes the message headers.

    For efficiency reason, Node.js normally buffers the message headers until `outgoingMessage.end()` is called or the first chunk of message data is written. It then tries to pack the headers and data into a single TCP packet.

    It is usually desired (it saves a TCP round-trip), but not when the first data is not sent until possibly much later. `outgoingMessage.flushHeaders()` bypasses the optimization and kickstarts the message.
  + [getHeader](https://bun.com/reference/node/http/OutgoingMessage/getHeader)(

    name: string

    ): undefined | string | number | string[];

    Gets the value of the HTTP header with the given name. If that header is not set, the returned value will be `undefined`.

    @param name

    Name of header
  + [getHeaderNames](https://bun.com/reference/node/http/OutgoingMessage/getHeaderNames)(): string[];

    Returns an array containing the unique names of the current outgoing headers. All names are lowercase.
  + [getHeaders](https://bun.com/reference/node/http/OutgoingMessage/getHeaders)(): [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders);

    Returns a shallow copy of the current outgoing headers. Since a shallow copy is used, array values may be mutated without additional calls to various header-related HTTP module methods. The keys of the returned object are the header names and the values are the respective header values. All header names are lowercase.

    The object returned by the `outgoingMessage.getHeaders()` method does not prototypically inherit from the JavaScript `Object`. This means that typical `Object` methods such as `obj.toString()`, `obj.hasOwnProperty()`, and others are not defined and will not work.

    ```
    outgoingMessage.setHeader('Foo', 'bar');
    outgoingMessage.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

    const headers = outgoingMessage.getHeaders();
    // headers === { foo: 'bar', 'set-cookie': ['foo=bar', 'bar=baz'] }
    ```
  + [getMaxListeners](https://bun.com/reference/node/http/OutgoingMessage/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [hasHeader](https://bun.com/reference/node/http/OutgoingMessage/hasHeader)(

    name: string

    ): boolean;

    Returns `true` if the header identified by `name` is currently set in the outgoing headers. The header name is case-insensitive.

    ```
    const hasContentType = outgoingMessage.hasHeader('content-type');
    ```
  + [listenerCount](https://bun.com/reference/node/http/OutgoingMessage/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http/OutgoingMessage/listeners)<K>(

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
  + [off](https://bun.com/reference/node/http/OutgoingMessage/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

    event: 'close',

    listener: () => void

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

    [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

    event: 'close',

    listener: () => void

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

    [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pipe](https://bun.com/reference/node/http/OutgoingMessage/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http/OutgoingMessage/prependListener)(

    event: 'close',

    listener: () => void

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

    [prependListener](https://bun.com/reference/node/http/OutgoingMessage/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/OutgoingMessage/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/OutgoingMessage/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/OutgoingMessage/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/OutgoingMessage/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/OutgoingMessage/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http/OutgoingMessage/prependOnceListener)(

    event: 'close',

    listener: () => void

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

    [prependOnceListener](https://bun.com/reference/node/http/OutgoingMessage/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/OutgoingMessage/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/OutgoingMessage/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/OutgoingMessage/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/OutgoingMessage/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/OutgoingMessage/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/http/OutgoingMessage/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/http/OutgoingMessage/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeHeader](https://bun.com/reference/node/http/OutgoingMessage/removeHeader)(

    name: string

    ): void;

    Removes a header that is queued for implicit sending.

    ```
    outgoingMessage.removeHeader('Content-Encoding');
    ```

    @param name

    Header name
  + [removeListener](https://bun.com/reference/node/http/OutgoingMessage/removeListener)(

    event: 'close',

    listener: () => void

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

    [removeListener](https://bun.com/reference/node/http/OutgoingMessage/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/OutgoingMessage/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/OutgoingMessage/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/OutgoingMessage/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/OutgoingMessage/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/OutgoingMessage/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [setDefaultEncoding](https://bun.com/reference/node/http/OutgoingMessage/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setHeader](https://bun.com/reference/node/http/OutgoingMessage/setHeader)(

    name: string,

    value: string | number | readonly string[]

    ): this;

    Sets a single header value. If the header already exists in the to-be-sent headers, its value will be replaced. Use an array of strings to send multiple headers with the same name.

    @param name

    Header name

    @param value

    Header value
  + [setHeaders](https://bun.com/reference/node/http/OutgoingMessage/setHeaders)(

    headers: [Headers](https://bun.com/reference/globals/Headers) | Map<string, string | number | readonly string[]>

    ): this;

    Sets multiple header values for implicit headers. headers must be an instance of `Headers` or `Map`, if a header already exists in the to-be-sent headers, its value will be replaced.

    ```
    const headers = new Headers({ foo: 'bar' });
    outgoingMessage.setHeaders(headers);
    ```

    or

    ```
    const headers = new Map([['foo', 'bar']]);
    outgoingMessage.setHeaders(headers);
    ```

    When headers have been set with `outgoingMessage.setHeaders()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    ```
    // Returns content-type = text/plain
    const server = http.createServer((req, res) => {
      const headers = new Headers({ 'Content-Type': 'text/html' });
      res.setHeaders(headers);
      res.writeHead(200, { 'Content-Type': 'text/plain' });
      res.end('ok');
    });
    ```
  + [setMaxListeners](https://bun.com/reference/node/http/OutgoingMessage/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http/OutgoingMessage/setTimeout)(

    msecs: number,

    callback?: () => void

    ): this;

    Once a socket is associated with the message and is connected, `socket.setTimeout()` will be called with `msecs` as the first parameter.

    @param callback

    Optional function to be called when a timeout occurs. Same as binding to the `timeout` event.
  + [uncork](https://bun.com/reference/node/http/OutgoingMessage/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [write](https://bun.com/reference/node/http/OutgoingMessage/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/http/OutgoingMessage/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
  + static [addAbortListener](https://bun.com/reference/node/http/OutgoingMessage/addAbortListener)(

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
  + static [fromWeb](https://bun.com/reference/node/http/OutgoingMessage/fromWeb)(

    writableStream: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream),

    options?: Pick<[WritableOptions](https://bun.com/reference/node/stream/default/WritableOptions)<[Writable](https://bun.com/reference/node/stream/default/Writable)>, 'signal' | 'decodeStrings' | 'highWaterMark' | 'objectMode'>

    ): [Writable](https://bun.com/reference/node/stream/default/Writable);

    A utility method for creating a `Writable` from a web `WritableStream`.
  + static [getEventListeners](https://bun.com/reference/node/http/OutgoingMessage/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/http/OutgoingMessage/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

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

    static [on](https://bun.com/reference/node/http/OutgoingMessage/on)(

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
  + static [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

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

    static [once](https://bun.com/reference/node/http/OutgoingMessage/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/http/OutgoingMessage/setMaxListeners)(

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
  + static [toWeb](https://bun.com/reference/node/http/OutgoingMessage/toWeb)(

    streamWritable: [Writable](https://bun.com/reference/node/stream/default/Writable)

    ): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream);

    A utility method for creating a web `WritableStream` from a `Writable`.
* ### class [Server](https://bun.com/reference/node/http/Server)<Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse)>

  + [connections](https://bun.com/reference/node/http/Server/connections): number
  + [headersTimeout](https://bun.com/reference/node/http/Server/headersTimeout): number

    Limit the amount of time the parser will wait to receive the complete HTTP headers.

    If the timeout expires, the server responds with status 408 without forwarding the request to the request listener and then closes the connection.

    It must be set to a non-zero value (e.g. 120 seconds) to protect against potential Denial-of-Service attacks in case the server is deployed without a reverse proxy in front.
  + [keepAliveTimeout](https://bun.com/reference/node/http/Server/keepAliveTimeout): number

    The number of milliseconds of inactivity a server needs to wait for additional incoming data, after it has finished writing the last response, before a socket will be destroyed.

    This timeout value is combined with the `server.keepAliveTimeoutBuffer` option to determine the actual socket timeout, calculated as: socketTimeout = keepAliveTimeout + keepAliveTimeoutBuffer If the server receives new data before the keep-alive timeout has fired, it will reset the regular inactivity timeout, i.e., `server.timeout`.

    A value of `0` will disable the keep-alive timeout behavior on incoming connections. A value of `0` makes the HTTP server behave similarly to Node.js versions prior to 8.0.0, which did not have a keep-alive timeout.

    The socket timeout logic is set up on connection, so changing this value only affects new connections to the server, not any existing connections.
  + [keepAliveTimeoutBuffer](https://bun.com/reference/node/http/Server/keepAliveTimeoutBuffer): number

    An additional buffer time added to the `server.keepAliveTimeout` to extend the internal socket timeout.

    This buffer helps reduce connection reset (`ECONNRESET`) errors by increasing the socket timeout slightly beyond the advertised keep-alive timeout.

    This option applies only to new incoming connections.
  + readonly [listening](https://bun.com/reference/node/http/Server/listening): boolean

    Indicates whether or not the server is listening for connections.
  + [maxConnections](https://bun.com/reference/node/http/Server/maxConnections): number

    Set this property to reject connections when the server's connection count gets high.

    It is not recommended to use this option once a socket has been sent to a child with `child_process.fork()`.
  + [maxHeadersCount](https://bun.com/reference/node/http/Server/maxHeadersCount): null | number

    Limits maximum incoming headers count. If set to 0, no limit will be applied.
  + [maxRequestsPerSocket](https://bun.com/reference/node/http/Server/maxRequestsPerSocket): null | number

    The maximum number of requests socket can handle before closing keep alive connection.

    A value of `0` will disable the limit.

    When the limit is reached it will set the `Connection` header value to `close`, but will not actually close the connection, subsequent requests sent after the limit is reached will get `503 Service Unavailable` as a response.
  + [requestTimeout](https://bun.com/reference/node/http/Server/requestTimeout): number

    Sets the timeout value in milliseconds for receiving the entire request from the client.

    If the timeout expires, the server responds with status 408 without forwarding the request to the request listener and then closes the connection.

    It must be set to a non-zero value (e.g. 120 seconds) to protect against potential Denial-of-Service attacks in case the server is deployed without a reverse proxy in front.
  + [timeout](https://bun.com/reference/node/http/Server/timeout): number

    The number of milliseconds of inactivity before a socket is presumed to have timed out.

    A value of `0` will disable the timeout behavior on incoming connections.

    The socket timeout logic is set up on connection, so changing this value only affects new connections to the server, not any existing connections.
  + static [captureRejections](https://bun.com/reference/node/http/Server/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http/Server/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http/Server/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/http/Server/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http/Server/[asyncDispose])(): Promise<void>;

    Calls () and returns a promise that fulfills when the server has closed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http/Server/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'listening',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'dropRequest',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [addListener](https://bun.com/reference/node/http/Server/addListener)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [address](https://bun.com/reference/node/http/Server/address)(): null | string | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

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
  + [close](https://bun.com/reference/node/http/Server/close)(

    callback?: (err?: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Stops the server from accepting new connections and keeps existing connections. This function is asynchronous, the server is finally closed when all connections are ended and the server emits a `'close'` event. The optional `callback` will be called once the `'close'` event occurs. Unlike that event, it will be called with an `Error` as its only argument if the server was not open when it was closed.

    @param callback

    Called when the server is closed.
  + [closeAllConnections](https://bun.com/reference/node/http/Server/closeAllConnections)(): void;

    Closes all connections connected to this server.
  + [closeIdleConnections](https://bun.com/reference/node/http/Server/closeIdleConnections)(): void;

    Closes all connections connected to this server which are not sending a request or waiting for a response.
  + [emit](https://bun.com/reference/node/http/Server/emit)(

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

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'connection',

    socket: [Socket](https://bun.com/reference/node/net/Socket)

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'listening'

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'checkContinue',

    req: InstanceType<Request>,

    res: InstanceType<Response> & { req: InstanceType<Request> }

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'checkExpectation',

    req: InstanceType<Request>,

    res: InstanceType<Response> & { req: InstanceType<Request> }

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'clientError',

    err: [Error](https://bun.com/reference/globals/Error),

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'connect',

    req: InstanceType<Request>,

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex),

    head: NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'dropRequest',

    req: InstanceType<Request>,

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'request',

    req: InstanceType<Request>,

    res: InstanceType<Response> & { req: InstanceType<Request> }

    ): boolean;

    [emit](https://bun.com/reference/node/http/Server/emit)(

    event: 'upgrade',

    req: InstanceType<Request>,

    socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex),

    head: NonSharedBuffer

    ): boolean;
  + [eventNames](https://bun.com/reference/node/http/Server/eventNames)(): string | symbol[];

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
  + [getConnections](https://bun.com/reference/node/http/Server/getConnections)(

    cb: (error: null | [Error](https://bun.com/reference/globals/Error), count: number) => void

    ): this;

    Asynchronously get the number of concurrent connections on the server. Works when sockets were sent to forks.

    Callback should take two arguments `err` and `count`.
  + [getMaxListeners](https://bun.com/reference/node/http/Server/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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

    [listen](https://bun.com/reference/node/http/Server/listen)(

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
  + [listenerCount](https://bun.com/reference/node/http/Server/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http/Server/listeners)<K>(

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
  + [off](https://bun.com/reference/node/http/Server/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http/Server/on)(

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

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'listening',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'dropRequest',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [on](https://bun.com/reference/node/http/Server/on)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [once](https://bun.com/reference/node/http/Server/once)(

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

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'listening',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'dropRequest',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [once](https://bun.com/reference/node/http/Server/once)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

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

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'dropRequest',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependListener](https://bun.com/reference/node/http/Server/prependListener)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'checkContinue',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'checkExpectation',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'clientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'connect',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'dropRequest',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'request',

    listener: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/Server/prependOnceListener)(

    event: 'upgrade',

    listener: (req: InstanceType<Request>, socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex), head: NonSharedBuffer) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/http/Server/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/http/Server/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed server will *not* let the program exit if it's the only server left (the default behavior). If the server is `ref`ed calling `ref()` again will have no effect.
  + [removeAllListeners](https://bun.com/reference/node/http/Server/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/http/Server/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/http/Server/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http/Server/setTimeout)(

    msecs?: number,

    callback?: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    Sets the timeout value for sockets, and emits a `'timeout'` event on the Server object, passing the socket as an argument, if a timeout occurs.

    If there is a `'timeout'` event listener on the Server object, then it will be called with the timed-out socket as an argument.

    By default, the Server does not timeout sockets. However, if a callback is assigned to the Server's `'timeout'` event, timeouts must be handled explicitly.

    [setTimeout](https://bun.com/reference/node/http/Server/setTimeout)(

    callback: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    Sets the timeout value for sockets, and emits a `'timeout'` event on the Server object, passing the socket as an argument, if a timeout occurs.

    If there is a `'timeout'` event listener on the Server object, then it will be called with the timed-out socket as an argument.

    By default, the Server does not timeout sockets. However, if a callback is assigned to the Server's `'timeout'` event, timeouts must be handled explicitly.
  + [unref](https://bun.com/reference/node/http/Server/unref)(): this;

    Calling `unref()` on a server will allow the program to exit if this is the only active server in the event system. If the server is already `unref`ed calling`unref()` again will have no effect.
  + static [addAbortListener](https://bun.com/reference/node/http/Server/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/http/Server/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/http/Server/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/http/Server/on)(

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

    static [on](https://bun.com/reference/node/http/Server/on)(

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
  + static [once](https://bun.com/reference/node/http/Server/once)(

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

    static [once](https://bun.com/reference/node/http/Server/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/http/Server/setMaxListeners)(

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
* ### class [ServerResponse](https://bun.com/reference/node/http/ServerResponse)<Request extends [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)>

  This object is created internally by an HTTP server, not by the user. It is passed as the second parameter to the `'request'` event.

  + [chunkedEncoding](https://bun.com/reference/node/http/ServerResponse/chunkedEncoding): boolean
  + readonly [closed](https://bun.com/reference/node/http/ServerResponse/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/http/ServerResponse/destroyed): boolean

    Is `true` after `writable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/http/ServerResponse/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [headersSent](https://bun.com/reference/node/http/ServerResponse/headersSent): boolean

    Read-only. `true` if the headers were sent, otherwise `false`.
  + readonly [req](https://bun.com/reference/node/http/ServerResponse/req): Request
  + [sendDate](https://bun.com/reference/node/http/ServerResponse/sendDate): boolean
  + [shouldKeepAlive](https://bun.com/reference/node/http/ServerResponse/shouldKeepAlive): boolean
  + readonly [socket](https://bun.com/reference/node/http/ServerResponse/socket): null | [Socket](https://bun.com/reference/node/net/Socket)

    Reference to the underlying socket. Usually, users will not want to access this property.

    After calling `outgoingMessage.end()`, this property will be nulled.
  + [statusCode](https://bun.com/reference/node/http/ServerResponse/statusCode): number

    When using implicit headers (not calling `response.writeHead()` explicitly), this property controls the status code that will be sent to the client when the headers get flushed.

    ```
    response.statusCode = 404;
    ```

    After response header was sent to the client, this property indicates the status code which was sent out.
  + [statusMessage](https://bun.com/reference/node/http/ServerResponse/statusMessage): string

    When using implicit headers (not calling `response.writeHead()` explicitly), this property controls the status message that will be sent to the client when the headers get flushed. If this is left as `undefined` then the standard message for the status code will be used.

    ```
    response.statusMessage = 'Not found';
    ```

    After response header was sent to the client, this property indicates the status message which was sent out.
  + [strictContentLength](https://bun.com/reference/node/http/ServerResponse/strictContentLength): boolean

    If set to `true`, Node.js will check whether the `Content-Length` header value and the size of the body, in bytes, are equal. Mismatching the `Content-Length` header value will result in an `Error` being thrown, identified by ``` code:``'ERR_HTTP_CONTENT_LENGTH_MISMATCH' ```.
  + [useChunkedEncodingByDefault](https://bun.com/reference/node/http/ServerResponse/useChunkedEncodingByDefault): boolean
  + readonly [writable](https://bun.com/reference/node/http/ServerResponse/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/http/ServerResponse/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/http/ServerResponse/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/http/ServerResponse/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/http/ServerResponse/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/http/ServerResponse/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/http/ServerResponse/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/http/ServerResponse/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/http/ServerResponse/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + static [captureRejections](https://bun.com/reference/node/http/ServerResponse/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/http/ServerResponse/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/http/ServerResponse/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/http/ServerResponse/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/http/ServerResponse/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/http/ServerResponse/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/http/ServerResponse/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_write](https://bun.com/reference/node/http/ServerResponse/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/http/ServerResponse/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/http/ServerResponse/[asyncDispose])(): Promise<void>;

    Calls `writable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/http/ServerResponse/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/http/ServerResponse/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/ServerResponse/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/ServerResponse/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/ServerResponse/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/ServerResponse/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/ServerResponse/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe

    [addListener](https://bun.com/reference/node/http/ServerResponse/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. drain
    3. error
    4. finish
    5. pipe
    6. unpipe
  + [addTrailers](https://bun.com/reference/node/http/ServerResponse/addTrailers)(

    headers: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders) | readonly [string, string][]

    ): void;

    Adds HTTP trailers (headers but at the end of the message) to the message.

    Trailers will **only** be emitted if the message is chunked encoded. If not, the trailers will be silently discarded.

    HTTP requires the `Trailer` header to be sent to emit trailers, with a list of header field names in its value, e.g.

    ```
    message.writeHead(200, { 'Content-Type': 'text/plain',
                             'Trailer': 'Content-MD5' });
    message.write(fileData);
    message.addTrailers({ 'Content-MD5': '7895bf4b8828b55ceaf47747b4bca667' });
    message.end();
    ```

    Attempting to set a header field name or value that contains invalid characters will result in a `TypeError` being thrown.
  + [appendHeader](https://bun.com/reference/node/http/ServerResponse/appendHeader)(

    name: string,

    value: string | readonly string[]

    ): this;

    Append a single header value to the header object.

    If the value is an array, this is equivalent to calling this method multiple times.

    If there were no previous values for the header, this is equivalent to calling `outgoingMessage.setHeader(name, value)`.

    Depending of the value of `options.uniqueHeaders` when the client request or the server were created, this will end up in the header being sent multiple times or a single time with values joined using `;` .

    @param name

    Header name

    @param value

    Header value
  + [assignSocket](https://bun.com/reference/node/http/ServerResponse/assignSocket)(

    socket: [Socket](https://bun.com/reference/node/net/Socket)

    ): void;
  + [compose](https://bun.com/reference/node/http/ServerResponse/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/http/ServerResponse/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/http/ServerResponse/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the writable stream has ended and subsequent calls to `write()` or `end()` will result in an `ERR_STREAM_DESTROYED` error. This is a destructive and immediate way to destroy a stream. Previous calls to `write()` may not have drained, and may trigger an `ERR_STREAM_DESTROYED` error. Use `end()` instead of destroy if data should flush before close, or wait for the `'drain'` event before destroying the stream.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `writable._destroy()`.

    @param error

    Optional, an error to emit with `'error'` event.
  + [detachSocket](https://bun.com/reference/node/http/ServerResponse/detachSocket)(

    socket: [Socket](https://bun.com/reference/node/net/Socket)

    ): void;
  + [emit](https://bun.com/reference/node/http/ServerResponse/emit)(

    event: 'close'

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

    [emit](https://bun.com/reference/node/http/ServerResponse/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/http/ServerResponse/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/http/ServerResponse/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/http/ServerResponse/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http/ServerResponse/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/http/ServerResponse/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/http/ServerResponse/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/http/ServerResponse/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/http/ServerResponse/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/http/ServerResponse/eventNames)(): string | symbol[];

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
  + [flushHeaders](https://bun.com/reference/node/http/ServerResponse/flushHeaders)(): void;

    Flushes the message headers.

    For efficiency reason, Node.js normally buffers the message headers until `outgoingMessage.end()` is called or the first chunk of message data is written. It then tries to pack the headers and data into a single TCP packet.

    It is usually desired (it saves a TCP round-trip), but not when the first data is not sent until possibly much later. `outgoingMessage.flushHeaders()` bypasses the optimization and kickstarts the message.
  + [getHeader](https://bun.com/reference/node/http/ServerResponse/getHeader)(

    name: string

    ): undefined | string | number | string[];

    Gets the value of the HTTP header with the given name. If that header is not set, the returned value will be `undefined`.

    @param name

    Name of header
  + [getHeaderNames](https://bun.com/reference/node/http/ServerResponse/getHeaderNames)(): string[];

    Returns an array containing the unique names of the current outgoing headers. All names are lowercase.
  + [getHeaders](https://bun.com/reference/node/http/ServerResponse/getHeaders)(): [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders);

    Returns a shallow copy of the current outgoing headers. Since a shallow copy is used, array values may be mutated without additional calls to various header-related HTTP module methods. The keys of the returned object are the header names and the values are the respective header values. All header names are lowercase.

    The object returned by the `outgoingMessage.getHeaders()` method does not prototypically inherit from the JavaScript `Object`. This means that typical `Object` methods such as `obj.toString()`, `obj.hasOwnProperty()`, and others are not defined and will not work.

    ```
    outgoingMessage.setHeader('Foo', 'bar');
    outgoingMessage.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

    const headers = outgoingMessage.getHeaders();
    // headers === { foo: 'bar', 'set-cookie': ['foo=bar', 'bar=baz'] }
    ```
  + [getMaxListeners](https://bun.com/reference/node/http/ServerResponse/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [hasHeader](https://bun.com/reference/node/http/ServerResponse/hasHeader)(

    name: string

    ): boolean;

    Returns `true` if the header identified by `name` is currently set in the outgoing headers. The header name is case-insensitive.

    ```
    const hasContentType = outgoingMessage.hasHeader('content-type');
    ```
  + [listenerCount](https://bun.com/reference/node/http/ServerResponse/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/http/ServerResponse/listeners)<K>(

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
  + [off](https://bun.com/reference/node/http/ServerResponse/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/http/ServerResponse/on)(

    event: 'close',

    listener: () => void

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

    [on](https://bun.com/reference/node/http/ServerResponse/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/ServerResponse/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/http/ServerResponse/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/http/ServerResponse/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http/ServerResponse/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/http/ServerResponse/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/http/ServerResponse/once)(

    event: 'close',

    listener: () => void

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

    [once](https://bun.com/reference/node/http/ServerResponse/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/ServerResponse/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/http/ServerResponse/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/http/ServerResponse/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http/ServerResponse/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/http/ServerResponse/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pipe](https://bun.com/reference/node/http/ServerResponse/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/http/ServerResponse/prependListener)(

    event: 'close',

    listener: () => void

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

    [prependListener](https://bun.com/reference/node/http/ServerResponse/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/ServerResponse/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/ServerResponse/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/ServerResponse/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/ServerResponse/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/http/ServerResponse/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/http/ServerResponse/prependOnceListener)(

    event: 'close',

    listener: () => void

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

    [prependOnceListener](https://bun.com/reference/node/http/ServerResponse/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/ServerResponse/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/ServerResponse/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/ServerResponse/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/ServerResponse/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/http/ServerResponse/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/http/ServerResponse/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/http/ServerResponse/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeHeader](https://bun.com/reference/node/http/ServerResponse/removeHeader)(

    name: string

    ): void;

    Removes a header that is queued for implicit sending.

    ```
    outgoingMessage.removeHeader('Content-Encoding');
    ```

    @param name

    Header name
  + [removeListener](https://bun.com/reference/node/http/ServerResponse/removeListener)(

    event: 'close',

    listener: () => void

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

    [removeListener](https://bun.com/reference/node/http/ServerResponse/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ServerResponse/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ServerResponse/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ServerResponse/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ServerResponse/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/http/ServerResponse/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [setDefaultEncoding](https://bun.com/reference/node/http/ServerResponse/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setHeader](https://bun.com/reference/node/http/ServerResponse/setHeader)(

    name: string,

    value: string | number | readonly string[]

    ): this;

    Sets a single header value. If the header already exists in the to-be-sent headers, its value will be replaced. Use an array of strings to send multiple headers with the same name.

    @param name

    Header name

    @param value

    Header value
  + [setHeaders](https://bun.com/reference/node/http/ServerResponse/setHeaders)(

    headers: [Headers](https://bun.com/reference/globals/Headers) | Map<string, string | number | readonly string[]>

    ): this;

    Sets multiple header values for implicit headers. headers must be an instance of `Headers` or `Map`, if a header already exists in the to-be-sent headers, its value will be replaced.

    ```
    const headers = new Headers({ foo: 'bar' });
    outgoingMessage.setHeaders(headers);
    ```

    or

    ```
    const headers = new Map([['foo', 'bar']]);
    outgoingMessage.setHeaders(headers);
    ```

    When headers have been set with `outgoingMessage.setHeaders()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    ```
    // Returns content-type = text/plain
    const server = http.createServer((req, res) => {
      const headers = new Headers({ 'Content-Type': 'text/html' });
      res.setHeaders(headers);
      res.writeHead(200, { 'Content-Type': 'text/plain' });
      res.end('ok');
    });
    ```
  + [setMaxListeners](https://bun.com/reference/node/http/ServerResponse/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setTimeout](https://bun.com/reference/node/http/ServerResponse/setTimeout)(

    msecs: number,

    callback?: () => void

    ): this;

    Once a socket is associated with the message and is connected, `socket.setTimeout()` will be called with `msecs` as the first parameter.

    @param callback

    Optional function to be called when a timeout occurs. Same as binding to the `timeout` event.
  + [uncork](https://bun.com/reference/node/http/ServerResponse/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [write](https://bun.com/reference/node/http/ServerResponse/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/http/ServerResponse/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
  + [writeContinue](https://bun.com/reference/node/http/ServerResponse/writeContinue)(

    callback?: () => void

    ): void;

    Sends an HTTP/1.1 100 Continue message to the client, indicating that the request body should be sent. See the `'checkContinue'` event on `Server`.
  + [writeEarlyHints](https://bun.com/reference/node/http/ServerResponse/writeEarlyHints)(

    hints: Record<string, string | string[]>,

    callback?: () => void

    ): void;

    Sends an HTTP/1.1 103 Early Hints message to the client with a Link header, indicating that the user agent can preload/preconnect the linked resources. The `hints` is an object containing the values of headers to be sent with early hints message. The optional `callback` argument will be called when the response message has been written.

    **Example**

    ```
    const earlyHintsLink = '</styles.css>; rel=preload; as=style';
    response.writeEarlyHints({
      'link': earlyHintsLink,
    });

    const earlyHintsLinks = [
      '</styles.css>; rel=preload; as=style',
      '</scripts.js>; rel=preload; as=script',
    ];
    response.writeEarlyHints({
      'link': earlyHintsLinks,
      'x-trace-id': 'id for diagnostics',
    });

    const earlyHintsCallback = () => console.log('early hints message sent');
    response.writeEarlyHints({
      'link': earlyHintsLinks,
    }, earlyHintsCallback);
    ```

    @param hints

    An object containing the values of headers

    @param callback

    Will be called when the response message has been written
  + [writeHead](https://bun.com/reference/node/http/ServerResponse/writeHead)(

    statusCode: number,

    statusMessage?: string,

    headers?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders) | [OutgoingHttpHeader](https://bun.com/reference/node/http/OutgoingHttpHeader)[]

    ): this;

    Sends a response header to the request. The status code is a 3-digit HTTP status code, like `404`. The last argument, `headers`, are the response headers. Optionally one can give a human-readable `statusMessage` as the second argument.

    `headers` may be an `Array` where the keys and values are in the same list. It is *not* a list of tuples. So, the even-numbered offsets are key values, and the odd-numbered offsets are the associated values. The array is in the same format as `request.rawHeaders`.

    Returns a reference to the `ServerResponse`, so that calls can be chained.

    ```
    const body = 'hello world';
    response
      .writeHead(200, {
        'Content-Length': Buffer.byteLength(body),
        'Content-Type': 'text/plain',
      })
      .end(body);
    ```

    This method must only be called once on a message and it must be called before `response.end()` is called.

    If `response.write()` or `response.end()` are called before calling this, the implicit/mutable headers will be calculated and call this function.

    When headers have been set with `response.setHeader()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    If this method is called and `response.setHeader()` has not been called, it will directly write the supplied header values onto the network channel without caching internally, and the `response.getHeader()` on the header will not yield the expected result. If progressive population of headers is desired with potential future retrieval and modification, use `response.setHeader()` instead.

    ```
    // Returns content-type = text/plain
    const server = http.createServer((req, res) => {
      res.setHeader('Content-Type', 'text/html');
      res.setHeader('X-Foo', 'bar');
      res.writeHead(200, { 'Content-Type': 'text/plain' });
      res.end('ok');
    });
    ```

    `Content-Length` is read in bytes, not characters. Use `Buffer.byteLength()` to determine the length of the body in bytes. Node.js will check whether `Content-Length` and the length of the body which has been transmitted are equal or not.

    Attempting to set a header field name or value that contains invalid characters will result in a [`Error`][] being thrown.

    [writeHead](https://bun.com/reference/node/http/ServerResponse/writeHead)(

    statusCode: number,

    headers?: [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders) | [OutgoingHttpHeader](https://bun.com/reference/node/http/OutgoingHttpHeader)[]

    ): this;

    Sends a response header to the request. The status code is a 3-digit HTTP status code, like `404`. The last argument, `headers`, are the response headers. Optionally one can give a human-readable `statusMessage` as the second argument.

    `headers` may be an `Array` where the keys and values are in the same list. It is *not* a list of tuples. So, the even-numbered offsets are key values, and the odd-numbered offsets are the associated values. The array is in the same format as `request.rawHeaders`.

    Returns a reference to the `ServerResponse`, so that calls can be chained.

    ```
    const body = 'hello world';
    response
      .writeHead(200, {
        'Content-Length': Buffer.byteLength(body),
        'Content-Type': 'text/plain',
      })
      .end(body);
    ```

    This method must only be called once on a message and it must be called before `response.end()` is called.

    If `response.write()` or `response.end()` are called before calling this, the implicit/mutable headers will be calculated and call this function.

    When headers have been set with `response.setHeader()`, they will be merged with any headers passed to `response.writeHead()`, with the headers passed to `response.writeHead()` given precedence.

    If this method is called and `response.setHeader()` has not been called, it will directly write the supplied header values onto the network channel without caching internally, and the `response.getHeader()` on the header will not yield the expected result. If progressive population of headers is desired with potential future retrieval and modification, use `response.setHeader()` instead.

    ```
    // Returns content-type = text/plain
    const server = http.createServer((req, res) => {
      res.setHeader('Content-Type', 'text/html');
      res.setHeader('X-Foo', 'bar');
      res.writeHead(200, { 'Content-Type': 'text/plain' });
      res.end('ok');
    });
    ```

    `Content-Length` is read in bytes, not characters. Use `Buffer.byteLength()` to determine the length of the body in bytes. Node.js will check whether `Content-Length` and the length of the body which has been transmitted are equal or not.

    Attempting to set a header field name or value that contains invalid characters will result in a [`Error`][] being thrown.
  + [writeProcessing](https://bun.com/reference/node/http/ServerResponse/writeProcessing)(

    callback?: () => void

    ): void;

    Sends a HTTP/1.1 102 Processing message to the client, indicating that the request body should be sent.
  + static [addAbortListener](https://bun.com/reference/node/http/ServerResponse/addAbortListener)(

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
  + static [fromWeb](https://bun.com/reference/node/http/ServerResponse/fromWeb)(

    writableStream: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream),

    options?: Pick<[WritableOptions](https://bun.com/reference/node/stream/default/WritableOptions)<[Writable](https://bun.com/reference/node/stream/default/Writable)>, 'signal' | 'decodeStrings' | 'highWaterMark' | 'objectMode'>

    ): [Writable](https://bun.com/reference/node/stream/default/Writable);

    A utility method for creating a `Writable` from a web `WritableStream`.
  + static [getEventListeners](https://bun.com/reference/node/http/ServerResponse/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/http/ServerResponse/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/http/ServerResponse/on)(

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

    static [on](https://bun.com/reference/node/http/ServerResponse/on)(

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
  + static [once](https://bun.com/reference/node/http/ServerResponse/once)(

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

    static [once](https://bun.com/reference/node/http/ServerResponse/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/http/ServerResponse/setMaxListeners)(

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
  + static [toWeb](https://bun.com/reference/node/http/ServerResponse/toWeb)(

    streamWritable: [Writable](https://bun.com/reference/node/stream/default/Writable)

    ): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream);

    A utility method for creating a web `WritableStream` from a `Writable`.
* const [CloseEvent](https://bun.com/reference/node/http/CloseEvent): CloseEvent
* const [globalAgent](https://bun.com/reference/node/http/globalAgent): [Agent](https://bun.com/reference/node/http/Agent)

  Global instance of `Agent` which is used as the default for all HTTP client requests. Diverges from a default `Agent` configuration by having `keepAlive` enabled and a `timeout` of 5 seconds.
* const [maxHeaderSize](https://bun.com/reference/node/http/maxHeaderSize): number

  Read-only property specifying the maximum allowed size of HTTP headers in bytes. Defaults to 16KB. Configurable using the `--max-http-header-size` CLI option.
* const [MessageEvent](https://bun.com/reference/node/http/MessageEvent): MessageEvent
* const [METHODS](https://bun.com/reference/node/http/METHODS): string[]
* const [STATUS\_CODES](https://bun.com/reference/node/http/STATUS_CODES): { 

  \_\_index[

  errorCode: number

  ]: undefined | string;

  \_\_index[

  errorCode: string

  ]: undefined | string;

   }
* const [WebSocket](https://bun.com/reference/node/http/WebSocket): WebSocket

  A browser-compatible implementation of `WebSocket`.
* function [createServer](https://bun.com/reference/node/http/createServer)<Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse)>(

  requestListener?: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

  ): [Server](https://bun.com/reference/node/http/Server)<Request, Response>;

  Returns a new instance of Server.

  The `requestListener` is a function which is automatically added to the `'request'` event.

  ```
  import http from 'node:http';

  // Create a local server to receive data from
  const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({
      data: 'Hello World!',
    }));
  });

  server.listen(8000);
  ```

  ```
  import http from 'node:http';

  // Create a local server to receive data from
  const server = http.createServer();

  // Listen to the request event
  server.on('request', (request, res) => {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({
      data: 'Hello World!',
    }));
  });

  server.listen(8000);
  ```

  function [createServer](https://bun.com/reference/node/http/createServer)<Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse)>(

  options: [ServerOptions](https://bun.com/reference/node/http/ServerOptions)<Request, Response>,

  requestListener?: [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request, Response>

  ): [Server](https://bun.com/reference/node/http/Server)<Request, Response>;

  Returns a new instance of Server.

  The `requestListener` is a function which is automatically added to the `'request'` event.

  ```
  import http from 'node:http';

  // Create a local server to receive data from
  const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({
      data: 'Hello World!',
    }));
  });

  server.listen(8000);
  ```

  ```
  import http from 'node:http';

  // Create a local server to receive data from
  const server = http.createServer();

  // Listen to the request event
  server.on('request', (request, res) => {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({
      data: 'Hello World!',
    }));
  });

  server.listen(8000);
  ```
* function [get](https://bun.com/reference/node/http/get)(

  options: string | [URL](https://bun.com/reference/node/url/URL) | [RequestOptions](https://bun.com/reference/node/http/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  Since most requests are GET requests without bodies, Node.js provides this convenience method. The only difference between this method and request is that it sets the method to GET by default and calls `req.end()` automatically. The callback must take care to consume the response data for reasons stated in ClientRequest section.

  The `callback` is invoked with a single argument that is an instance of IncomingMessage.

  JSON fetching example:

  ```
  http.get('http://localhost:8000/', (res) => {
    const { statusCode } = res;
    const contentType = res.headers['content-type'];

    let error;
    // Any 2xx status code signals a successful response but
    // here we're only checking for 200.
    if (statusCode !== 200) {
      error = new Error('Request Failed.\n' +
                        `Status Code: ${statusCode}`);
    } else if (!/^application/json/.test(contentType)) {
      error = new Error('Invalid content-type.\n' +
                        `Expected application/json but received ${contentType}`);
    }
    if (error) {
      console.error(error.message);
      // Consume response data to free up memory
      res.resume();
      return;
    }

    res.setEncoding('utf8');
    let rawData = '';
    res.on('data', (chunk) => { rawData += chunk; });
    res.on('end', () => {
      try {
        const parsedData = JSON.parse(rawData);
        console.log(parsedData);
      } catch (e) {
        console.error(e.message);
      }
    });
  }).on('error', (e) => {
    console.error(`Got error: ${e.message}`);
  });

  // Create a local server to receive data from
  const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({
      data: 'Hello World!',
    }));
  });

  server.listen(8000);
  ```

  @param options

  Accepts the same `options` as request, with the method set to GET by default.

  function [get](https://bun.com/reference/node/http/get)(

  url: string | [URL](https://bun.com/reference/node/url/URL),

  options: [RequestOptions](https://bun.com/reference/node/http/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  Since most requests are GET requests without bodies, Node.js provides this convenience method. The only difference between this method and request is that it sets the method to GET by default and calls `req.end()` automatically. The callback must take care to consume the response data for reasons stated in ClientRequest section.

  The `callback` is invoked with a single argument that is an instance of IncomingMessage.

  JSON fetching example:

  ```
  http.get('http://localhost:8000/', (res) => {
    const { statusCode } = res;
    const contentType = res.headers['content-type'];

    let error;
    // Any 2xx status code signals a successful response but
    // here we're only checking for 200.
    if (statusCode !== 200) {
      error = new Error('Request Failed.\n' +
                        `Status Code: ${statusCode}`);
    } else if (!/^application/json/.test(contentType)) {
      error = new Error('Invalid content-type.\n' +
                        `Expected application/json but received ${contentType}`);
    }
    if (error) {
      console.error(error.message);
      // Consume response data to free up memory
      res.resume();
      return;
    }

    res.setEncoding('utf8');
    let rawData = '';
    res.on('data', (chunk) => { rawData += chunk; });
    res.on('end', () => {
      try {
        const parsedData = JSON.parse(rawData);
        console.log(parsedData);
      } catch (e) {
        console.error(e.message);
      }
    });
  }).on('error', (e) => {
    console.error(`Got error: ${e.message}`);
  });

  // Create a local server to receive data from
  const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({
      data: 'Hello World!',
    }));
  });

  server.listen(8000);
  ```

  @param options

  Accepts the same `options` as request, with the method set to GET by default.
* function [request](https://bun.com/reference/node/http/request)(

  options: string | [URL](https://bun.com/reference/node/url/URL) | [RequestOptions](https://bun.com/reference/node/http/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  `options` in `socket.connect()` are also supported.

  Node.js maintains several connections per server to make HTTP requests. This function allows one to transparently issue requests.

  `url` can be a string or a `URL` object. If `url` is a string, it is automatically parsed with `new URL()`. If it is a `URL` object, it will be automatically converted to an ordinary `options` object.

  If both `url` and `options` are specified, the objects are merged, with the `options` properties taking precedence.

  The optional `callback` parameter will be added as a one-time listener for the `'response'` event.

  `http.request()` returns an instance of the ClientRequest class. The `ClientRequest` instance is a writable stream. If one needs to upload a file with a POST request, then write to the `ClientRequest` object.

  ```
  import http from 'node:http';
  import { Buffer } from 'node:buffer';

  const postData = JSON.stringify({
    'msg': 'Hello World!',
  });

  const options = {
    hostname: 'www.google.com',
    port: 80,
    path: '/upload',
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Content-Length': Buffer.byteLength(postData),
    },
  };

  const req = http.request(options, (res) => {
    console.log(`STATUS: ${res.statusCode}`);
    console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
    res.setEncoding('utf8');
    res.on('data', (chunk) => {
      console.log(`BODY: ${chunk}`);
    });
    res.on('end', () => {
      console.log('No more data in response.');
    });
  });

  req.on('error', (e) => {
    console.error(`problem with request: ${e.message}`);
  });

  // Write data to request body
  req.write(postData);
  req.end();
  ```

  In the example `req.end()` was called. With `http.request()` one must always call `req.end()` to signify the end of the request - even if there is no data being written to the request body.

  If any error is encountered during the request (be that with DNS resolution, TCP level errors, or actual HTTP parse errors) an `'error'` event is emitted on the returned request object. As with all `'error'` events, if no listeners are registered the error will be thrown.

  There are a few special headers that should be noted.

  + Sending a 'Connection: keep-alive' will notify Node.js that the connection to the server should be persisted until the next request.
  + Sending a 'Content-Length' header will disable the default chunked encoding.
  + Sending an 'Expect' header will immediately send the request headers. Usually, when sending 'Expect: 100-continue', both a timeout and a listener for the `'continue'` event should be set. See RFC 2616 Section 8.2.3 for more information.
  + Sending an Authorization header will override using the `auth` option to compute basic authentication.

  Example using a `URL` as `options`:

  ```
  const options = new URL('http://abc:xyz@example.com');

  const req = http.request(options, (res) => {
    // ...
  });
  ```

  In a successful request, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object (`'data'` will not be emitted at all if the response body is empty, for instance, in most redirects)
    - `'end'` on the `res` object
  + `'close'`

  In the case of a connection error, the following events will be emitted:

  + `'socket'`
  + `'error'`
  + `'close'`

  In the case of a premature connection close before the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`
  + `'close'`

  In the case of a premature connection close after the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object
  + (connection closed here)
  + `'aborted'` on the `res` object
  + `'close'`
  + `'error'` on the `res` object with an error with message `'Error: aborted'` and code `'ECONNRESET'`
  + `'close'` on the `res` object

  If `req.destroy()` is called before a socket is assigned, the following events will be emitted in the following order:

  + (`req.destroy()` called here)
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`, or the error with which `req.destroy()` was called
  + `'close'`

  If `req.destroy()` is called before the connection succeeds, the following events will be emitted in the following order:

  + `'socket'`
  + (`req.destroy()` called here)
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`, or the error with which `req.destroy()` was called
  + `'close'`

  If `req.destroy()` is called after the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object
  + (`req.destroy()` called here)
  + `'aborted'` on the `res` object
  + `'close'`
  + `'error'` on the `res` object with an error with message `'Error: aborted'` and code `'ECONNRESET'`, or the error with which `req.destroy()` was called
  + `'close'` on the `res` object

  If `req.abort()` is called before a socket is assigned, the following events will be emitted in the following order:

  + (`req.abort()` called here)
  + `'abort'`
  + `'close'`

  If `req.abort()` is called before the connection succeeds, the following events will be emitted in the following order:

  + `'socket'`
  + (`req.abort()` called here)
  + `'abort'`
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`
  + `'close'`

  If `req.abort()` is called after the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object
  + (`req.abort()` called here)
  + `'abort'`
  + `'aborted'` on the `res` object
  + `'error'` on the `res` object with an error with message `'Error: aborted'` and code `'ECONNRESET'`.
  + `'close'`
  + `'close'` on the `res` object

  Setting the `timeout` option or using the `setTimeout()` function will not abort the request or do anything besides add a `'timeout'` event.

  Passing an `AbortSignal` and then calling `abort()` on the corresponding `AbortController` will behave the same way as calling `.destroy()` on the request. Specifically, the `'error'` event will be emitted with an error with the message `'AbortError: The operation was aborted'`, the code `'ABORT_ERR'` and the `cause`, if one was provided.

  function [request](https://bun.com/reference/node/http/request)(

  url: string | [URL](https://bun.com/reference/node/url/URL),

  options: [RequestOptions](https://bun.com/reference/node/http/RequestOptions),

  callback?: (res: [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage)) => void

  ): [ClientRequest](https://bun.com/reference/node/http/ClientRequest);

  `options` in `socket.connect()` are also supported.

  Node.js maintains several connections per server to make HTTP requests. This function allows one to transparently issue requests.

  `url` can be a string or a `URL` object. If `url` is a string, it is automatically parsed with `new URL()`. If it is a `URL` object, it will be automatically converted to an ordinary `options` object.

  If both `url` and `options` are specified, the objects are merged, with the `options` properties taking precedence.

  The optional `callback` parameter will be added as a one-time listener for the `'response'` event.

  `http.request()` returns an instance of the ClientRequest class. The `ClientRequest` instance is a writable stream. If one needs to upload a file with a POST request, then write to the `ClientRequest` object.

  ```
  import http from 'node:http';
  import { Buffer } from 'node:buffer';

  const postData = JSON.stringify({
    'msg': 'Hello World!',
  });

  const options = {
    hostname: 'www.google.com',
    port: 80,
    path: '/upload',
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Content-Length': Buffer.byteLength(postData),
    },
  };

  const req = http.request(options, (res) => {
    console.log(`STATUS: ${res.statusCode}`);
    console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
    res.setEncoding('utf8');
    res.on('data', (chunk) => {
      console.log(`BODY: ${chunk}`);
    });
    res.on('end', () => {
      console.log('No more data in response.');
    });
  });

  req.on('error', (e) => {
    console.error(`problem with request: ${e.message}`);
  });

  // Write data to request body
  req.write(postData);
  req.end();
  ```

  In the example `req.end()` was called. With `http.request()` one must always call `req.end()` to signify the end of the request - even if there is no data being written to the request body.

  If any error is encountered during the request (be that with DNS resolution, TCP level errors, or actual HTTP parse errors) an `'error'` event is emitted on the returned request object. As with all `'error'` events, if no listeners are registered the error will be thrown.

  There are a few special headers that should be noted.

  + Sending a 'Connection: keep-alive' will notify Node.js that the connection to the server should be persisted until the next request.
  + Sending a 'Content-Length' header will disable the default chunked encoding.
  + Sending an 'Expect' header will immediately send the request headers. Usually, when sending 'Expect: 100-continue', both a timeout and a listener for the `'continue'` event should be set. See RFC 2616 Section 8.2.3 for more information.
  + Sending an Authorization header will override using the `auth` option to compute basic authentication.

  Example using a `URL` as `options`:

  ```
  const options = new URL('http://abc:xyz@example.com');

  const req = http.request(options, (res) => {
    // ...
  });
  ```

  In a successful request, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object (`'data'` will not be emitted at all if the response body is empty, for instance, in most redirects)
    - `'end'` on the `res` object
  + `'close'`

  In the case of a connection error, the following events will be emitted:

  + `'socket'`
  + `'error'`
  + `'close'`

  In the case of a premature connection close before the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`
  + `'close'`

  In the case of a premature connection close after the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object
  + (connection closed here)
  + `'aborted'` on the `res` object
  + `'close'`
  + `'error'` on the `res` object with an error with message `'Error: aborted'` and code `'ECONNRESET'`
  + `'close'` on the `res` object

  If `req.destroy()` is called before a socket is assigned, the following events will be emitted in the following order:

  + (`req.destroy()` called here)
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`, or the error with which `req.destroy()` was called
  + `'close'`

  If `req.destroy()` is called before the connection succeeds, the following events will be emitted in the following order:

  + `'socket'`
  + (`req.destroy()` called here)
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`, or the error with which `req.destroy()` was called
  + `'close'`

  If `req.destroy()` is called after the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object
  + (`req.destroy()` called here)
  + `'aborted'` on the `res` object
  + `'close'`
  + `'error'` on the `res` object with an error with message `'Error: aborted'` and code `'ECONNRESET'`, or the error with which `req.destroy()` was called
  + `'close'` on the `res` object

  If `req.abort()` is called before a socket is assigned, the following events will be emitted in the following order:

  + (`req.abort()` called here)
  + `'abort'`
  + `'close'`

  If `req.abort()` is called before the connection succeeds, the following events will be emitted in the following order:

  + `'socket'`
  + (`req.abort()` called here)
  + `'abort'`
  + `'error'` with an error with message `'Error: socket hang up'` and code `'ECONNRESET'`
  + `'close'`

  If `req.abort()` is called after the response is received, the following events will be emitted in the following order:

  + `'socket'`
  + `'response'`
    - `'data'` any number of times, on the `res` object
  + (`req.abort()` called here)
  + `'abort'`
  + `'aborted'` on the `res` object
  + `'error'` on the `res` object with an error with message `'Error: aborted'` and code `'ECONNRESET'`.
  + `'close'`
  + `'close'` on the `res` object

  Setting the `timeout` option or using the `setTimeout()` function will not abort the request or do anything besides add a `'timeout'` event.

  Passing an `AbortSignal` and then calling `abort()` on the corresponding `AbortController` will behave the same way as calling `.destroy()` on the request. Specifically, the `'error'` event will be emitted with an error with the message `'AbortError: The operation was aborted'`, the code `'ABORT_ERR'` and the `cause`, if one was provided.
* function [setMaxIdleHTTPParsers](https://bun.com/reference/node/http/setMaxIdleHTTPParsers)(

  max?: number

  ): void;

  Set the maximum number of idle HTTP parsers.
* function [validateHeaderName](https://bun.com/reference/node/http/validateHeaderName)(

  name: string

  ): void;

  Performs the low-level validations on the provided `name` that are done when `res.setHeader(name, value)` is called.

  Passing illegal value as `name` will result in a `TypeError` being thrown, identified by `code: 'ERR_INVALID_HTTP_TOKEN'`.

  It is not necessary to use this method before passing headers to an HTTP request or response. The HTTP module will automatically validate such headers.

  Example:

  ```
  import { validateHeaderName } from 'node:http';

  try {
    validateHeaderName('');
  } catch (err) {
    console.error(err instanceof TypeError); // --> true
    console.error(err.code); // --> 'ERR_INVALID_HTTP_TOKEN'
    console.error(err.message); // --> 'Header name must be a valid HTTP token [""]'
  }
  ```
* function [validateHeaderValue](https://bun.com/reference/node/http/validateHeaderValue)(

  name: string,

  value: string

  ): void;

  Performs the low-level validations on the provided `value` that are done when `res.setHeader(name, value)` is called.

  Passing illegal value as `value` will result in a `TypeError` being thrown.

  + Undefined value error is identified by `code: 'ERR_HTTP_INVALID_HEADER_VALUE'`.
  + Invalid value character error is identified by `code: 'ERR_INVALID_CHAR'`.

  It is not necessary to use this method before passing headers to an HTTP request or response. The HTTP module will automatically validate such headers.

  Examples:

  ```
  import { validateHeaderValue } from 'node:http';

  try {
    validateHeaderValue('x-my-header', undefined);
  } catch (err) {
    console.error(err instanceof TypeError); // --> true
    console.error(err.code === 'ERR_HTTP_INVALID_HEADER_VALUE'); // --> true
    console.error(err.message); // --> 'Invalid value "undefined" for header "x-my-header"'
  }

  try {
    validateHeaderValue('x-my-header', 'oʊmɪɡə');
  } catch (err) {
    console.error(err instanceof TypeError); // --> true
    console.error(err.code === 'ERR_INVALID_CHAR'); // --> true
    console.error(err.message); // --> 'Invalid character in header content ["x-my-header"]'
  }
  ```

  @param name

  Header name

  @param value

  Header value

## Type definitions

* ### interface [AgentOptions](https://bun.com/reference/node/http/AgentOptions)

  + [agentKeepAliveTimeoutBuffer](https://bun.com/reference/node/http/AgentOptions/agentKeepAliveTimeoutBuffer)?: number

    Milliseconds to subtract from the server-provided `keep-alive: timeout=...` hint when determining socket expiration time. This buffer helps ensure the agent closes the socket slightly before the server does, reducing the chance of sending a request on a socket that’s about to be closed by the server.
  + [autoSelectFamily](https://bun.com/reference/node/http/AgentOptions/autoSelectFamily)?: boolean
  + [autoSelectFamilyAttemptTimeout](https://bun.com/reference/node/http/AgentOptions/autoSelectFamilyAttemptTimeout)?: number
  + [blockList](https://bun.com/reference/node/http/AgentOptions/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)
  + [defaultPort](https://bun.com/reference/node/http/AgentOptions/defaultPort)?: number

    Default port to use when the port is not specified in requests.
  + [family](https://bun.com/reference/node/http/AgentOptions/family)?: number
  + [hints](https://bun.com/reference/node/http/AgentOptions/hints)?: number
  + [host](https://bun.com/reference/node/http/AgentOptions/host)?: string
  + [keepAlive](https://bun.com/reference/node/http/AgentOptions/keepAlive)?: boolean

    Keep sockets around in a pool to be used by other requests in the future. Default = false
  + [keepAliveInitialDelay](https://bun.com/reference/node/http/AgentOptions/keepAliveInitialDelay)?: number
  + [keepAliveMsecs](https://bun.com/reference/node/http/AgentOptions/keepAliveMsecs)?: number

    When using HTTP KeepAlive, how often to send TCP KeepAlive packets over sockets being kept alive. Default = 1000. Only relevant if keepAlive is set to true.
  + [localAddress](https://bun.com/reference/node/http/AgentOptions/localAddress)?: string
  + [localPort](https://bun.com/reference/node/http/AgentOptions/localPort)?: number
  + [lookup](https://bun.com/reference/node/http/AgentOptions/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxFreeSockets](https://bun.com/reference/node/http/AgentOptions/maxFreeSockets)?: number

    Maximum number of sockets to leave open in a free state. Only relevant if keepAlive is set to true. Default = 256.
  + [maxSockets](https://bun.com/reference/node/http/AgentOptions/maxSockets)?: number

    Maximum number of sockets to allow per host. Default for Node 0.10 is 5, default for Node 0.12 is Infinity
  + [maxTotalSockets](https://bun.com/reference/node/http/AgentOptions/maxTotalSockets)?: number

    Maximum number of sockets allowed for all hosts in total. Each request will use a new socket until the maximum is reached. Default: Infinity.
  + [noDelay](https://bun.com/reference/node/http/AgentOptions/noDelay)?: boolean
  + [port](https://bun.com/reference/node/http/AgentOptions/port)?: number
  + [proxyEnv](https://bun.com/reference/node/http/AgentOptions/proxyEnv)?: [ProxyEnv](https://bun.com/reference/node/http/ProxyEnv)

    Environment variables for proxy configuration. See [Built-in Proxy Support](https://nodejs.org/docs/latest-v24.x/api/http.html#built-in-proxy-support) for details.
  + [scheduling](https://bun.com/reference/node/http/AgentOptions/scheduling)?: 'fifo' | 'lifo'

    Scheduling strategy to apply when picking the next free socket to use.
  + [timeout](https://bun.com/reference/node/http/AgentOptions/timeout)?: number

    Socket timeout in milliseconds. This will set the timeout after the socket is connected.
* ### interface [ClientRequestArgs](https://bun.com/reference/node/http/ClientRequestArgs)

  + [\_defaultAgent](https://bun.com/reference/node/http/ClientRequestArgs/_defaultAgent)?: [Agent](https://bun.com/reference/node/http/Agent)
  + [agent](https://bun.com/reference/node/http/ClientRequestArgs/agent)?: boolean | [Agent](https://bun.com/reference/node/http/Agent)
  + [auth](https://bun.com/reference/node/http/ClientRequestArgs/auth)?: null | string
  + [createConnection](https://bun.com/reference/node/http/ClientRequestArgs/createConnection)?: (options: [ClientRequestArgs](https://bun.com/reference/node/http/ClientRequestArgs), oncreate: (err: null | [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void) => undefined | null | [Duplex](https://bun.com/reference/node/stream/default/Duplex)
  + [defaultPort](https://bun.com/reference/node/http/ClientRequestArgs/defaultPort)?: string | number
  + [family](https://bun.com/reference/node/http/ClientRequestArgs/family)?: number
  + [headers](https://bun.com/reference/node/http/ClientRequestArgs/headers)?: readonly string[] | [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)
  + [hints](https://bun.com/reference/node/http/ClientRequestArgs/hints)?: number

    One or more [supported `getaddrinfo`](https://nodejs.org/docs/latest-v24.x/api/dns.html#supported-getaddrinfo-flags) flags. Multiple flags may be passed by bitwise `OR`ing their values.
  + [host](https://bun.com/reference/node/http/ClientRequestArgs/host)?: null | string
  + [hostname](https://bun.com/reference/node/http/ClientRequestArgs/hostname)?: null | string
  + [insecureHTTPParser](https://bun.com/reference/node/http/ClientRequestArgs/insecureHTTPParser)?: boolean
  + [joinDuplicateHeaders](https://bun.com/reference/node/http/ClientRequestArgs/joinDuplicateHeaders)?: boolean
  + [localAddress](https://bun.com/reference/node/http/ClientRequestArgs/localAddress)?: string
  + [localPort](https://bun.com/reference/node/http/ClientRequestArgs/localPort)?: number
  + [lookup](https://bun.com/reference/node/http/ClientRequestArgs/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxHeaderSize](https://bun.com/reference/node/http/ClientRequestArgs/maxHeaderSize)?: number
  + [method](https://bun.com/reference/node/http/ClientRequestArgs/method)?: string
  + [path](https://bun.com/reference/node/http/ClientRequestArgs/path)?: null | string
  + [port](https://bun.com/reference/node/http/ClientRequestArgs/port)?: null | string | number
  + [setDefaultHeaders](https://bun.com/reference/node/http/ClientRequestArgs/setDefaultHeaders)?: boolean
  + [setHost](https://bun.com/reference/node/http/ClientRequestArgs/setHost)?: boolean
  + [signal](https://bun.com/reference/node/http/ClientRequestArgs/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [socketPath](https://bun.com/reference/node/http/ClientRequestArgs/socketPath)?: string
  + [timeout](https://bun.com/reference/node/http/ClientRequestArgs/timeout)?: number
  + [uniqueHeaders](https://bun.com/reference/node/http/ClientRequestArgs/uniqueHeaders)?: string | string[][]
* ### interface [IncomingHttpHeaders](https://bun.com/reference/node/http/IncomingHttpHeaders)

  + [accept](https://bun.com/reference/node/http/IncomingHttpHeaders/accept)?: string
  + [accept-encoding](https://bun.com/reference/node/http/IncomingHttpHeaders/accept-encoding)?: string
  + [accept-language](https://bun.com/reference/node/http/IncomingHttpHeaders/accept-language)?: string
  + [accept-patch](https://bun.com/reference/node/http/IncomingHttpHeaders/accept-patch)?: string
  + [accept-ranges](https://bun.com/reference/node/http/IncomingHttpHeaders/accept-ranges)?: string
  + [access-control-allow-credentials](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-allow-credentials)?: string
  + [access-control-allow-headers](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-allow-headers)?: string
  + [access-control-allow-methods](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-allow-methods)?: string
  + [access-control-allow-origin](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-allow-origin)?: string
  + [access-control-expose-headers](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-expose-headers)?: string
  + [access-control-max-age](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-max-age)?: string
  + [access-control-request-headers](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-request-headers)?: string
  + [access-control-request-method](https://bun.com/reference/node/http/IncomingHttpHeaders/access-control-request-method)?: string
  + [age](https://bun.com/reference/node/http/IncomingHttpHeaders/age)?: string
  + [allow](https://bun.com/reference/node/http/IncomingHttpHeaders/allow)?: string
  + [alt-svc](https://bun.com/reference/node/http/IncomingHttpHeaders/alt-svc)?: string
  + [authorization](https://bun.com/reference/node/http/IncomingHttpHeaders/authorization)?: string
  + [cache-control](https://bun.com/reference/node/http/IncomingHttpHeaders/cache-control)?: string
  + [connection](https://bun.com/reference/node/http/IncomingHttpHeaders/connection)?: string
  + [content-disposition](https://bun.com/reference/node/http/IncomingHttpHeaders/content-disposition)?: string
  + [content-encoding](https://bun.com/reference/node/http/IncomingHttpHeaders/content-encoding)?: string
  + [content-language](https://bun.com/reference/node/http/IncomingHttpHeaders/content-language)?: string
  + [content-length](https://bun.com/reference/node/http/IncomingHttpHeaders/content-length)?: string
  + [content-location](https://bun.com/reference/node/http/IncomingHttpHeaders/content-location)?: string
  + [content-range](https://bun.com/reference/node/http/IncomingHttpHeaders/content-range)?: string
  + [content-type](https://bun.com/reference/node/http/IncomingHttpHeaders/content-type)?: string
  + [cookie](https://bun.com/reference/node/http/IncomingHttpHeaders/cookie)?: string
  + [date](https://bun.com/reference/node/http/IncomingHttpHeaders/date)?: string
  + [etag](https://bun.com/reference/node/http/IncomingHttpHeaders/etag)?: string
  + [expect](https://bun.com/reference/node/http/IncomingHttpHeaders/expect)?: string
  + [expires](https://bun.com/reference/node/http/IncomingHttpHeaders/expires)?: string
  + [forwarded](https://bun.com/reference/node/http/IncomingHttpHeaders/forwarded)?: string
  + [from](https://bun.com/reference/node/http/IncomingHttpHeaders/from)?: string
  + [host](https://bun.com/reference/node/http/IncomingHttpHeaders/host)?: string
  + [if-match](https://bun.com/reference/node/http/IncomingHttpHeaders/if-match)?: string
  + [if-modified-since](https://bun.com/reference/node/http/IncomingHttpHeaders/if-modified-since)?: string
  + [if-none-match](https://bun.com/reference/node/http/IncomingHttpHeaders/if-none-match)?: string
  + [if-unmodified-since](https://bun.com/reference/node/http/IncomingHttpHeaders/if-unmodified-since)?: string
  + [last-modified](https://bun.com/reference/node/http/IncomingHttpHeaders/last-modified)?: string
  + [location](https://bun.com/reference/node/http/IncomingHttpHeaders/location)?: string
  + [origin](https://bun.com/reference/node/http/IncomingHttpHeaders/origin)?: string
  + [pragma](https://bun.com/reference/node/http/IncomingHttpHeaders/pragma)?: string
  + [proxy-authenticate](https://bun.com/reference/node/http/IncomingHttpHeaders/proxy-authenticate)?: string
  + [proxy-authorization](https://bun.com/reference/node/http/IncomingHttpHeaders/proxy-authorization)?: string
  + [public-key-pins](https://bun.com/reference/node/http/IncomingHttpHeaders/public-key-pins)?: string
  + [range](https://bun.com/reference/node/http/IncomingHttpHeaders/range)?: string
  + [referer](https://bun.com/reference/node/http/IncomingHttpHeaders/referer)?: string
  + [retry-after](https://bun.com/reference/node/http/IncomingHttpHeaders/retry-after)?: string
  + [sec-fetch-dest](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-fetch-dest)?: string
  + [sec-fetch-mode](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-fetch-mode)?: string
  + [sec-fetch-site](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-fetch-site)?: string
  + [sec-fetch-user](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-fetch-user)?: string
  + [sec-websocket-accept](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-websocket-accept)?: string
  + [sec-websocket-extensions](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-websocket-extensions)?: string
  + [sec-websocket-key](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-websocket-key)?: string
  + [sec-websocket-version](https://bun.com/reference/node/http/IncomingHttpHeaders/sec-websocket-version)?: string
  + [set-cookie](https://bun.com/reference/node/http/IncomingHttpHeaders/set-cookie)?: string[]
  + [strict-transport-security](https://bun.com/reference/node/http/IncomingHttpHeaders/strict-transport-security)?: string
  + [tk](https://bun.com/reference/node/http/IncomingHttpHeaders/tk)?: string
  + [trailer](https://bun.com/reference/node/http/IncomingHttpHeaders/trailer)?: string
  + [transfer-encoding](https://bun.com/reference/node/http/IncomingHttpHeaders/transfer-encoding)?: string
  + [upgrade](https://bun.com/reference/node/http/IncomingHttpHeaders/upgrade)?: string
  + [user-agent](https://bun.com/reference/node/http/IncomingHttpHeaders/user-agent)?: string
  + [vary](https://bun.com/reference/node/http/IncomingHttpHeaders/vary)?: string
  + [via](https://bun.com/reference/node/http/IncomingHttpHeaders/via)?: string
  + [warning](https://bun.com/reference/node/http/IncomingHttpHeaders/warning)?: string
  + [www-authenticate](https://bun.com/reference/node/http/IncomingHttpHeaders/www-authenticate)?: string
* ### interface [InformationEvent](https://bun.com/reference/node/http/InformationEvent)

  + [headers](https://bun.com/reference/node/http/InformationEvent/headers): [IncomingHttpHeaders](https://bun.com/reference/node/http/IncomingHttpHeaders)
  + [httpVersion](https://bun.com/reference/node/http/InformationEvent/httpVersion): string
  + [httpVersionMajor](https://bun.com/reference/node/http/InformationEvent/httpVersionMajor): number
  + [httpVersionMinor](https://bun.com/reference/node/http/InformationEvent/httpVersionMinor): number
  + [rawHeaders](https://bun.com/reference/node/http/InformationEvent/rawHeaders): string[]
  + [statusCode](https://bun.com/reference/node/http/InformationEvent/statusCode): number
  + [statusMessage](https://bun.com/reference/node/http/InformationEvent/statusMessage): string
* ### interface [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)

  + [accept](https://bun.com/reference/node/http/OutgoingHttpHeaders/accept)?: string | string[]
  + [accept-charset](https://bun.com/reference/node/http/OutgoingHttpHeaders/accept-charset)?: string | string[]
  + [accept-encoding](https://bun.com/reference/node/http/OutgoingHttpHeaders/accept-encoding)?: string | string[]
  + [accept-language](https://bun.com/reference/node/http/OutgoingHttpHeaders/accept-language)?: string | string[]
  + [accept-ranges](https://bun.com/reference/node/http/OutgoingHttpHeaders/accept-ranges)?: string
  + [access-control-allow-credentials](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-allow-credentials)?: string
  + [access-control-allow-headers](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-allow-headers)?: string
  + [access-control-allow-methods](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-allow-methods)?: string
  + [access-control-allow-origin](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-allow-origin)?: string
  + [access-control-expose-headers](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-expose-headers)?: string
  + [access-control-max-age](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-max-age)?: string
  + [access-control-request-headers](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-request-headers)?: string
  + [access-control-request-method](https://bun.com/reference/node/http/OutgoingHttpHeaders/access-control-request-method)?: string
  + [age](https://bun.com/reference/node/http/OutgoingHttpHeaders/age)?: string
  + [allow](https://bun.com/reference/node/http/OutgoingHttpHeaders/allow)?: string
  + [authorization](https://bun.com/reference/node/http/OutgoingHttpHeaders/authorization)?: string
  + [cache-control](https://bun.com/reference/node/http/OutgoingHttpHeaders/cache-control)?: string
  + [cdn-cache-control](https://bun.com/reference/node/http/OutgoingHttpHeaders/cdn-cache-control)?: string
  + [connection](https://bun.com/reference/node/http/OutgoingHttpHeaders/connection)?: string | string[]
  + [content-disposition](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-disposition)?: string
  + [content-encoding](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-encoding)?: string
  + [content-language](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-language)?: string
  + [content-length](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-length)?: string | number
  + [content-location](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-location)?: string
  + [content-range](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-range)?: string
  + [content-security-policy](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-security-policy)?: string
  + [content-security-policy-report-only](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-security-policy-report-only)?: string
  + [content-type](https://bun.com/reference/node/http/OutgoingHttpHeaders/content-type)?: string
  + [cookie](https://bun.com/reference/node/http/OutgoingHttpHeaders/cookie)?: string | string[]
  + [date](https://bun.com/reference/node/http/OutgoingHttpHeaders/date)?: string
  + [dav](https://bun.com/reference/node/http/OutgoingHttpHeaders/dav)?: string | string[]
  + [dnt](https://bun.com/reference/node/http/OutgoingHttpHeaders/dnt)?: string
  + [etag](https://bun.com/reference/node/http/OutgoingHttpHeaders/etag)?: string
  + [expect](https://bun.com/reference/node/http/OutgoingHttpHeaders/expect)?: string
  + [expires](https://bun.com/reference/node/http/OutgoingHttpHeaders/expires)?: string
  + [forwarded](https://bun.com/reference/node/http/OutgoingHttpHeaders/forwarded)?: string
  + [from](https://bun.com/reference/node/http/OutgoingHttpHeaders/from)?: string
  + [host](https://bun.com/reference/node/http/OutgoingHttpHeaders/host)?: string
  + [if-match](https://bun.com/reference/node/http/OutgoingHttpHeaders/if-match)?: string
  + [if-modified-since](https://bun.com/reference/node/http/OutgoingHttpHeaders/if-modified-since)?: string
  + [if-none-match](https://bun.com/reference/node/http/OutgoingHttpHeaders/if-none-match)?: string
  + [if-range](https://bun.com/reference/node/http/OutgoingHttpHeaders/if-range)?: string
  + [if-unmodified-since](https://bun.com/reference/node/http/OutgoingHttpHeaders/if-unmodified-since)?: string
  + [last-modified](https://bun.com/reference/node/http/OutgoingHttpHeaders/last-modified)?: string
  + [link](https://bun.com/reference/node/http/OutgoingHttpHeaders/link)?: string | string[]
  + [location](https://bun.com/reference/node/http/OutgoingHttpHeaders/location)?: string
  + [max-forwards](https://bun.com/reference/node/http/OutgoingHttpHeaders/max-forwards)?: string
  + [origin](https://bun.com/reference/node/http/OutgoingHttpHeaders/origin)?: string
  + [pragma](https://bun.com/reference/node/http/OutgoingHttpHeaders/pragma)?: string | string[]
  + [proxy-authenticate](https://bun.com/reference/node/http/OutgoingHttpHeaders/proxy-authenticate)?: string | string[]
  + [proxy-authorization](https://bun.com/reference/node/http/OutgoingHttpHeaders/proxy-authorization)?: string
  + [public-key-pins](https://bun.com/reference/node/http/OutgoingHttpHeaders/public-key-pins)?: string
  + [public-key-pins-report-only](https://bun.com/reference/node/http/OutgoingHttpHeaders/public-key-pins-report-only)?: string
  + [range](https://bun.com/reference/node/http/OutgoingHttpHeaders/range)?: string
  + [referer](https://bun.com/reference/node/http/OutgoingHttpHeaders/referer)?: string
  + [referrer-policy](https://bun.com/reference/node/http/OutgoingHttpHeaders/referrer-policy)?: string
  + [refresh](https://bun.com/reference/node/http/OutgoingHttpHeaders/refresh)?: string
  + [retry-after](https://bun.com/reference/node/http/OutgoingHttpHeaders/retry-after)?: string
  + [sec-websocket-accept](https://bun.com/reference/node/http/OutgoingHttpHeaders/sec-websocket-accept)?: string
  + [sec-websocket-extensions](https://bun.com/reference/node/http/OutgoingHttpHeaders/sec-websocket-extensions)?: string | string[]
  + [sec-websocket-key](https://bun.com/reference/node/http/OutgoingHttpHeaders/sec-websocket-key)?: string
  + [sec-websocket-version](https://bun.com/reference/node/http/OutgoingHttpHeaders/sec-websocket-version)?: string
  + [server](https://bun.com/reference/node/http/OutgoingHttpHeaders/server)?: string
  + [set-cookie](https://bun.com/reference/node/http/OutgoingHttpHeaders/set-cookie)?: string | string[]
  + [strict-transport-security](https://bun.com/reference/node/http/OutgoingHttpHeaders/strict-transport-security)?: string
  + [te](https://bun.com/reference/node/http/OutgoingHttpHeaders/te)?: string
  + [trailer](https://bun.com/reference/node/http/OutgoingHttpHeaders/trailer)?: string
  + [transfer-encoding](https://bun.com/reference/node/http/OutgoingHttpHeaders/transfer-encoding)?: string
  + [upgrade](https://bun.com/reference/node/http/OutgoingHttpHeaders/upgrade)?: string
  + [upgrade-insecure-requests](https://bun.com/reference/node/http/OutgoingHttpHeaders/upgrade-insecure-requests)?: string
  + [user-agent](https://bun.com/reference/node/http/OutgoingHttpHeaders/user-agent)?: string
  + [vary](https://bun.com/reference/node/http/OutgoingHttpHeaders/vary)?: string
  + [via](https://bun.com/reference/node/http/OutgoingHttpHeaders/via)?: string | string[]
  + [warning](https://bun.com/reference/node/http/OutgoingHttpHeaders/warning)?: string
  + [www-authenticate](https://bun.com/reference/node/http/OutgoingHttpHeaders/www-authenticate)?: string | string[]
  + [x-content-type-options](https://bun.com/reference/node/http/OutgoingHttpHeaders/x-content-type-options)?: string
  + [x-dns-prefetch-control](https://bun.com/reference/node/http/OutgoingHttpHeaders/x-dns-prefetch-control)?: string
  + [x-frame-options](https://bun.com/reference/node/http/OutgoingHttpHeaders/x-frame-options)?: string
  + [x-xss-protection](https://bun.com/reference/node/http/OutgoingHttpHeaders/x-xss-protection)?: string
* ### interface [ProxyEnv](https://bun.com/reference/node/http/ProxyEnv)

  + [http\_proxy](https://bun.com/reference/node/http/ProxyEnv/http_proxy)?: string
  + [HTTP\_PROXY](https://bun.com/reference/node/http/ProxyEnv/HTTP_PROXY)?: string
  + [https\_proxy](https://bun.com/reference/node/http/ProxyEnv/https_proxy)?: string
  + [HTTPS\_PROXY](https://bun.com/reference/node/http/ProxyEnv/HTTPS_PROXY)?: string
  + [no\_proxy](https://bun.com/reference/node/http/ProxyEnv/no_proxy)?: string
  + [NO\_PROXY](https://bun.com/reference/node/http/ProxyEnv/NO_PROXY)?: string
  + [NODE\_ENV](https://bun.com/reference/node/http/ProxyEnv/NODE_ENV)?: string
  + [TZ](https://bun.com/reference/node/http/ProxyEnv/TZ)?: string

    Can be used to change the default timezone at runtime
* ### interface [RequestOptions](https://bun.com/reference/node/http/RequestOptions)

  + [\_defaultAgent](https://bun.com/reference/node/http/RequestOptions/_defaultAgent)?: [Agent](https://bun.com/reference/node/http/Agent)
  + [agent](https://bun.com/reference/node/http/RequestOptions/agent)?: boolean | [Agent](https://bun.com/reference/node/http/Agent)
  + [auth](https://bun.com/reference/node/http/RequestOptions/auth)?: null | string
  + [createConnection](https://bun.com/reference/node/http/RequestOptions/createConnection)?: (options: [ClientRequestArgs](https://bun.com/reference/node/http/ClientRequestArgs), oncreate: (err: null | [Error](https://bun.com/reference/globals/Error), socket: [Duplex](https://bun.com/reference/node/stream/default/Duplex)) => void) => undefined | null | [Duplex](https://bun.com/reference/node/stream/default/Duplex)
  + [defaultPort](https://bun.com/reference/node/http/RequestOptions/defaultPort)?: string | number
  + [family](https://bun.com/reference/node/http/RequestOptions/family)?: number
  + [headers](https://bun.com/reference/node/http/RequestOptions/headers)?: readonly string[] | [OutgoingHttpHeaders](https://bun.com/reference/node/http/OutgoingHttpHeaders)
  + [hints](https://bun.com/reference/node/http/RequestOptions/hints)?: number

    One or more [supported `getaddrinfo`](https://nodejs.org/docs/latest-v24.x/api/dns.html#supported-getaddrinfo-flags) flags. Multiple flags may be passed by bitwise `OR`ing their values.
  + [host](https://bun.com/reference/node/http/RequestOptions/host)?: null | string
  + [hostname](https://bun.com/reference/node/http/RequestOptions/hostname)?: null | string
  + [insecureHTTPParser](https://bun.com/reference/node/http/RequestOptions/insecureHTTPParser)?: boolean
  + [joinDuplicateHeaders](https://bun.com/reference/node/http/RequestOptions/joinDuplicateHeaders)?: boolean
  + [localAddress](https://bun.com/reference/node/http/RequestOptions/localAddress)?: string
  + [localPort](https://bun.com/reference/node/http/RequestOptions/localPort)?: number
  + [lookup](https://bun.com/reference/node/http/RequestOptions/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxHeaderSize](https://bun.com/reference/node/http/RequestOptions/maxHeaderSize)?: number
  + [method](https://bun.com/reference/node/http/RequestOptions/method)?: string
  + [path](https://bun.com/reference/node/http/RequestOptions/path)?: null | string
  + [port](https://bun.com/reference/node/http/RequestOptions/port)?: null | string | number
  + [setDefaultHeaders](https://bun.com/reference/node/http/RequestOptions/setDefaultHeaders)?: boolean
  + [setHost](https://bun.com/reference/node/http/RequestOptions/setHost)?: boolean
  + [signal](https://bun.com/reference/node/http/RequestOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [socketPath](https://bun.com/reference/node/http/RequestOptions/socketPath)?: string
  + [timeout](https://bun.com/reference/node/http/RequestOptions/timeout)?: number
  + [uniqueHeaders](https://bun.com/reference/node/http/RequestOptions/uniqueHeaders)?: string | string[][]
* ### interface [ServerOptions](https://bun.com/reference/node/http/ServerOptions)<Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse)>

  + [connectionsCheckingInterval](https://bun.com/reference/node/http/ServerOptions/connectionsCheckingInterval)?: number

    Sets the interval value in milliseconds to check for request and headers timeout in incomplete requests.
  + [headersTimeout](https://bun.com/reference/node/http/ServerOptions/headersTimeout)?: number

    Sets the timeout value in milliseconds for receiving the complete HTTP headers from the client. See Server.headersTimeout for more information.
  + [highWaterMark](https://bun.com/reference/node/http/ServerOptions/highWaterMark)?: number

    Optionally overrides all `socket`s' `readableHighWaterMark` and `writableHighWaterMark`. This affects `highWaterMark` property of both `IncomingMessage` and `ServerResponse`. Default:
  + [IncomingMessage](https://bun.com/reference/node/http/ServerOptions/IncomingMessage)?: Request

    Specifies the `IncomingMessage` class to be used. Useful for extending the original `IncomingMessage`.
  + [insecureHTTPParser](https://bun.com/reference/node/http/ServerOptions/insecureHTTPParser)?: boolean

    Use an insecure HTTP parser that accepts invalid HTTP headers when `true`. Using the insecure parser should be avoided. See --insecure-http-parser for more information.
  + [joinDuplicateHeaders](https://bun.com/reference/node/http/ServerOptions/joinDuplicateHeaders)?: boolean

    It joins the field line values of multiple headers in a request with `,`  instead of discarding the duplicates.
  + [keepAlive](https://bun.com/reference/node/http/ServerOptions/keepAlive)?: boolean

    If set to `true`, it enables keep-alive functionality on the socket immediately after a new incoming connection is received, similarly on what is done in `socket.setKeepAlive([enable][, initialDelay])`.
  + [keepAliveInitialDelay](https://bun.com/reference/node/http/ServerOptions/keepAliveInitialDelay)?: number

    If set to a positive number, it sets the initial delay before the first keepalive probe is sent on an idle socket.
  + [keepAliveTimeout](https://bun.com/reference/node/http/ServerOptions/keepAliveTimeout)?: number

    The number of milliseconds of inactivity a server needs to wait for additional incoming data, after it has finished writing the last response, before a socket will be destroyed.
  + [keepAliveTimeoutBuffer](https://bun.com/reference/node/http/ServerOptions/keepAliveTimeoutBuffer)?: number

    An additional buffer time added to the `server.keepAliveTimeout` to extend the internal socket timeout.
  + [maxHeaderSize](https://bun.com/reference/node/http/ServerOptions/maxHeaderSize)?: number

    Optionally overrides the value of `--max-http-header-size` for requests received by this server, i.e. the maximum length of request headers in bytes.
  + [noDelay](https://bun.com/reference/node/http/ServerOptions/noDelay)?: boolean

    If set to `true`, it disables the use of Nagle's algorithm immediately after a new incoming connection is received.
  + [rejectNonStandardBodyWrites](https://bun.com/reference/node/http/ServerOptions/rejectNonStandardBodyWrites)?: boolean

    If set to `true`, an error is thrown when writing to an HTTP response which does not have a body.
  + [requestTimeout](https://bun.com/reference/node/http/ServerOptions/requestTimeout)?: number

    Sets the timeout value in milliseconds for receiving the entire request from the client.
  + [requireHostHeader](https://bun.com/reference/node/http/ServerOptions/requireHostHeader)?: boolean

    If set to `true`, it forces the server to respond with a 400 (Bad Request) status code to any HTTP/1.1 request message that lacks a Host header (as mandated by the specification).
  + [ServerResponse](https://bun.com/reference/node/http/ServerOptions/ServerResponse)?: Response

    Specifies the `ServerResponse` class to be used. Useful for extending the original `ServerResponse`.
  + [shouldUpgradeCallback](https://bun.com/reference/node/http/ServerOptions/shouldUpgradeCallback)?: (request: InstanceType<Request>) => boolean

    A callback which receives an incoming request and returns a boolean, to control which upgrade attempts should be accepted. Accepted upgrades will fire an `'upgrade'` event (or their sockets will be destroyed, if no listener is registered) while rejected upgrades will fire a `'request'` event like any non-upgrade request.
  + [uniqueHeaders](https://bun.com/reference/node/http/ServerOptions/uniqueHeaders)?: string | string[][]

    A list of response headers that should be sent only once. If the header's value is an array, the items will be joined using `;` .
* type [OutgoingHttpHeader](https://bun.com/reference/node/http/OutgoingHttpHeader) = number | string | string[]
* type [RequestListener](https://bun.com/reference/node/http/RequestListener)<Request extends typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage) = typeof [IncomingMessage](https://bun.com/reference/node/http/IncomingMessage), Response extends typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse) = typeof [ServerResponse](https://bun.com/reference/node/http/ServerResponse)> = (req: InstanceType<Request>, res: InstanceType<Response> & { req: InstanceType<Request> }) => void