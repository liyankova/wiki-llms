---
url: https://bun.com/reference/node/cluster
title: Node.js cluster module | API Reference | Bun
source_domain: bun.com
---

# Node.js cluster module | API Reference | Bun

Node.js module

# [cluster](https://bun.com/reference/node/cluster)

The `'node:cluster'` module provides a way to create a small network of processes to share server ports and distribute workload across CPU cores. It uses the `fork()` mechanism to spawn worker processes that share the same server handles.

Clustered applications can handle more concurrent connections by distributing requests among workers. The module includes utilities for worker management, messaging, and graceful shutdown.

Works in Bun

Implemented but not battle-tested. Handles and file descriptors cannot be passed between workers, limiting TCP server load-balancing across processes to Linux (via SO\_REUSEPORT).

* ### class [Worker](https://bun.com/reference/node/cluster/Worker)

  A `Worker` object contains all public information and method about a worker. In the primary it can be obtained using `cluster.workers`. In a worker it can be obtained using `cluster.worker`.

  + [exitedAfterDisconnect](https://bun.com/reference/node/cluster/Worker/exitedAfterDisconnect): boolean

    This property is `true` if the worker exited due to `.disconnect()`. If the worker exited any other way, it is `false`. If the worker has not exited, it is `undefined`.

    The boolean `worker.exitedAfterDisconnect` allows distinguishing between voluntary and accidental exit, the primary may choose not to respawn a worker based on this value.

    ```
    cluster.on('exit', (worker, code, signal) => {
      if (worker.exitedAfterDisconnect === true) {
        console.log('Oh, it was just voluntary – no need to worry');
      }
    });

    // kill worker
    worker.kill();
    ```
  + [id](https://bun.com/reference/node/cluster/Worker/id): number

    Each new worker is given its own unique id, this id is stored in the `id`.

    While a worker is alive, this is the key that indexes it in `cluster.workers`.
  + [process](https://bun.com/reference/node/cluster/Worker/process): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess)

    All workers are created using [`child_process.fork()`](https://nodejs.org/docs/latest-v24.x/api/child_process.html#child_processforkmodulepath-args-options), the returned object from this function is stored as `.process`. In a worker, the global `process` is stored.

    See: [Child Process module](https://nodejs.org/docs/latest-v24.x/api/child_process.html#child_processforkmodulepath-args-options).

    Workers will call `process.exit(0)` if the `'disconnect'` event occurs on `process` and `.exitedAfterDisconnect` is not `true`. This protects against accidental disconnection.
  + static [captureRejections](https://bun.com/reference/node/cluster/Worker/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/cluster/Worker/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/cluster/Worker/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/cluster/Worker/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/cluster/Worker/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/cluster/Worker/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. error
    3. exit
    4. listening
    5. message
    6. online

    [addListener](https://bun.com/reference/node/cluster/Worker/addListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. error
    3. exit
    4. listening
    5. message
    6. online

    [addListener](https://bun.com/reference/node/cluster/Worker/addListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. error
    3. exit
    4. listening
    5. message
    6. online

    [addListener](https://bun.com/reference/node/cluster/Worker/addListener)(

    event: 'exit',

    listener: (code: number, signal: string) => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. error
    3. exit
    4. listening
    5. message
    6. online

    [addListener](https://bun.com/reference/node/cluster/Worker/addListener)(

    event: 'listening',

    listener: (address: [Address](https://bun.com/reference/node/cluster/Address)) => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. error
    3. exit
    4. listening
    5. message
    6. online

    [addListener](https://bun.com/reference/node/cluster/Worker/addListener)(

    event: 'message',

    listener: (message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. error
    3. exit
    4. listening
    5. message
    6. online

    [addListener](https://bun.com/reference/node/cluster/Worker/addListener)(

    event: 'online',

    listener: () => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. error
    3. exit
    4. listening
    5. message
    6. online
  + [destroy](https://bun.com/reference/node/cluster/Worker/destroy)(

    signal?: string

    ): void;
  + [disconnect](https://bun.com/reference/node/cluster/Worker/disconnect)(): this;

    In a worker, this function will close all servers, wait for the `'close'` event on those servers, and then disconnect the IPC channel.

    In the primary, an internal message is sent to the worker causing it to call `.disconnect()` on itself.

    Causes `.exitedAfterDisconnect` to be set.

    After a server is closed, it will no longer accept new connections, but connections may be accepted by any other listening worker. Existing connections will be allowed to close as usual. When no more connections exist, see `server.close()`, the IPC channel to the worker will close allowing it to die gracefully.

    The above applies *only* to server connections, client connections are not automatically closed by workers, and disconnect does not wait for them to close before exiting.

    In a worker, `process.disconnect` exists, but it is not this function; it is `disconnect()`.

    Because long living server connections may block workers from disconnecting, it may be useful to send a message, so application specific actions may be taken to close them. It also may be useful to implement a timeout, killing a worker if the `'disconnect'` event has not been emitted after some time.

    ```
    import net from 'node:net';

    if (cluster.isPrimary) {
      const worker = cluster.fork();
      let timeout;

      worker.on('listening', (address) => {
        worker.send('shutdown');
        worker.disconnect();
        timeout = setTimeout(() => {
          worker.kill();
        }, 2000);
      });

      worker.on('disconnect', () => {
        clearTimeout(timeout);
      });

    } else if (cluster.isWorker) {
      const server = net.createServer((socket) => {
        // Connections never end
      });

      server.listen(8000);

      process.on('message', (msg) => {
        if (msg === 'shutdown') {
          // Initiate graceful close of any connections to server
        }
      });
    }
    ```

    @returns

    A reference to `worker`.
  + [emit](https://bun.com/reference/node/cluster/Worker/emit)(

    event: string | symbol,

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

    [emit](https://bun.com/reference/node/cluster/Worker/emit)(

    event: 'disconnect'

    ): boolean;

    [emit](https://bun.com/reference/node/cluster/Worker/emit)(

    event: 'error',

    error: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/cluster/Worker/emit)(

    event: 'exit',

    code: number,

    signal: string

    ): boolean;

    [emit](https://bun.com/reference/node/cluster/Worker/emit)(

    event: 'listening',

    address: [Address](https://bun.com/reference/node/cluster/Address)

    ): boolean;

    [emit](https://bun.com/reference/node/cluster/Worker/emit)(

    event: 'message',

    message: any,

    handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)

    ): boolean;

    [emit](https://bun.com/reference/node/cluster/Worker/emit)(

    event: 'online'

    ): boolean;
  + [eventNames](https://bun.com/reference/node/cluster/Worker/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/cluster/Worker/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isConnected](https://bun.com/reference/node/cluster/Worker/isConnected)(): boolean;

    This function returns `true` if the worker is connected to its primary via its IPC channel, `false` otherwise. A worker is connected to its primary after it has been created. It is disconnected after the `'disconnect'` event is emitted.
  + [isDead](https://bun.com/reference/node/cluster/Worker/isDead)(): boolean;

    This function returns `true` if the worker's process has terminated (either because of exiting or being signaled). Otherwise, it returns `false`.

    ```
    import cluster from 'node:cluster';
    import http from 'node:http';
    import { availableParallelism } from 'node:os';
    import process from 'node:process';

    const numCPUs = availableParallelism();

    if (cluster.isPrimary) {
      console.log(`Primary ${process.pid} is running`);

      // Fork workers.
      for (let i = 0; i < numCPUs; i++) {
        cluster.fork();
      }

      cluster.on('fork', (worker) => {
        console.log('worker is dead:', worker.isDead());
      });

      cluster.on('exit', (worker, code, signal) => {
        console.log('worker is dead:', worker.isDead());
      });
    } else {
      // Workers can share any TCP connection. In this case, it is an HTTP server.
      http.createServer((req, res) => {
        res.writeHead(200);
        res.end(`Current process\n ${process.pid}`);
        process.kill(process.pid);
      }).listen(8000);
    }
    ```
  + [kill](https://bun.com/reference/node/cluster/Worker/kill)(

    signal?: string

    ): void;

    This function will kill the worker. In the primary worker, it does this by disconnecting the `worker.process`, and once disconnected, killing with `signal`. In the worker, it does it by killing the process with `signal`.

    The `kill()` function kills the worker process without waiting for a graceful disconnect, it has the same behavior as `worker.process.kill()`.

    This method is aliased as `worker.destroy()` for backwards compatibility.

    In a worker, `process.kill()` exists, but it is not this function; it is [`kill()`](https://nodejs.org/docs/latest-v24.x/api/process.html#processkillpid-signal).

    @param signal

    Name of the kill signal to send to the worker process.
  + [listenerCount](https://bun.com/reference/node/cluster/Worker/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/cluster/Worker/listeners)<K>(

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
  + [off](https://bun.com/reference/node/cluster/Worker/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/cluster/Worker/on)(

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

    [on](https://bun.com/reference/node/cluster/Worker/on)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/cluster/Worker/on)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/cluster/Worker/on)(

    event: 'exit',

    listener: (code: number, signal: string) => void

    ): this;

    [on](https://bun.com/reference/node/cluster/Worker/on)(

    event: 'listening',

    listener: (address: [Address](https://bun.com/reference/node/cluster/Address)) => void

    ): this;

    [on](https://bun.com/reference/node/cluster/Worker/on)(

    event: 'message',

    listener: (message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

    ): this;

    [on](https://bun.com/reference/node/cluster/Worker/on)(

    event: 'online',

    listener: () => void

    ): this;
  + [once](https://bun.com/reference/node/cluster/Worker/once)(

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

    [once](https://bun.com/reference/node/cluster/Worker/once)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/cluster/Worker/once)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/cluster/Worker/once)(

    event: 'exit',

    listener: (code: number, signal: string) => void

    ): this;

    [once](https://bun.com/reference/node/cluster/Worker/once)(

    event: 'listening',

    listener: (address: [Address](https://bun.com/reference/node/cluster/Address)) => void

    ): this;

    [once](https://bun.com/reference/node/cluster/Worker/once)(

    event: 'message',

    listener: (message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

    ): this;

    [once](https://bun.com/reference/node/cluster/Worker/once)(

    event: 'online',

    listener: () => void

    ): this;
  + [prependListener](https://bun.com/reference/node/cluster/Worker/prependListener)(

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

    [prependListener](https://bun.com/reference/node/cluster/Worker/prependListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/cluster/Worker/prependListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/cluster/Worker/prependListener)(

    event: 'exit',

    listener: (code: number, signal: string) => void

    ): this;

    [prependListener](https://bun.com/reference/node/cluster/Worker/prependListener)(

    event: 'listening',

    listener: (address: [Address](https://bun.com/reference/node/cluster/Address)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/cluster/Worker/prependListener)(

    event: 'message',

    listener: (message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/cluster/Worker/prependListener)(

    event: 'online',

    listener: () => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/cluster/Worker/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Worker/prependOnceListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/cluster/Worker/prependOnceListener)(

    event: 'error',

    listener: (error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/cluster/Worker/prependOnceListener)(

    event: 'exit',

    listener: (code: number, signal: string) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/cluster/Worker/prependOnceListener)(

    event: 'listening',

    listener: (address: [Address](https://bun.com/reference/node/cluster/Address)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/cluster/Worker/prependOnceListener)(

    event: 'message',

    listener: (message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/cluster/Worker/prependOnceListener)(

    event: 'online',

    listener: () => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/cluster/Worker/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/cluster/Worker/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/cluster/Worker/removeListener)<K>(

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
  + [send](https://bun.com/reference/node/cluster/Worker/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    Send a message to a worker or primary, optionally with a handle.

    In the primary, this sends a message to a specific worker. It is identical to [`ChildProcess.send()`](https://nodejs.org/docs/latest-v24.x/api/child_process.html#subprocesssendmessage-sendhandle-options-callback).

    In a worker, this sends a message to the primary. It is identical to `process.send()`.

    This example will echo back all messages from the primary:

    ```
    if (cluster.isPrimary) {
      const worker = cluster.fork();
      worker.send('hi there');

    } else if (cluster.isWorker) {
      process.on('message', (msg) => {
        process.send(msg);
      });
    }
    ```

    [send](https://bun.com/reference/node/cluster/Worker/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    Send a message to a worker or primary, optionally with a handle.

    In the primary, this sends a message to a specific worker. It is identical to [`ChildProcess.send()`](https://nodejs.org/docs/latest-v24.x/api/child_process.html#subprocesssendmessage-sendhandle-options-callback).

    In a worker, this sends a message to the primary. It is identical to `process.send()`.

    This example will echo back all messages from the primary:

    ```
    if (cluster.isPrimary) {
      const worker = cluster.fork();
      worker.send('hi there');

    } else if (cluster.isWorker) {
      process.on('message', (msg) => {
        process.send(msg);
      });
    }
    ```

    [send](https://bun.com/reference/node/cluster/Worker/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    options?: [MessageOptions](https://bun.com/reference/node/child_process/MessageOptions),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    Send a message to a worker or primary, optionally with a handle.

    In the primary, this sends a message to a specific worker. It is identical to [`ChildProcess.send()`](https://nodejs.org/docs/latest-v24.x/api/child_process.html#subprocesssendmessage-sendhandle-options-callback).

    In a worker, this sends a message to the primary. It is identical to `process.send()`.

    This example will echo back all messages from the primary:

    ```
    if (cluster.isPrimary) {
      const worker = cluster.fork();
      worker.send('hi there');

    } else if (cluster.isWorker) {
      process.on('message', (msg) => {
        process.send(msg);
      });
    }
    ```

    @param options

    The `options` argument, if present, is an object used to parameterize the sending of certain types of handles.
  + [setMaxListeners](https://bun.com/reference/node/cluster/Worker/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/cluster/Worker/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/cluster/Worker/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/cluster/Worker/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/cluster/Worker/on)(

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

    static [on](https://bun.com/reference/node/cluster/Worker/on)(

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
  + static [once](https://bun.com/reference/node/cluster/Worker/once)(

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

    static [once](https://bun.com/reference/node/cluster/Worker/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/cluster/Worker/setMaxListeners)(

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

## Type definitions

* ### interface [Address](https://bun.com/reference/node/cluster/Address)

  + [address](https://bun.com/reference/node/cluster/Address/address): string
  + [addressType](https://bun.com/reference/node/cluster/Address/addressType): 4 | 6 | -1 | 'udp4' | 'udp6'

    The `addressType` is one of:

    - `4` (TCPv4)
    - `6` (TCPv6)
    - `-1` (Unix domain socket)
    - `'udp4'` or `'udp6'` (UDPv4 or UDPv6)
  + [port](https://bun.com/reference/node/cluster/Address/port): number
* ### interface [Cluster](https://bun.com/reference/node/cluster/Cluster)

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + readonly [isPrimary](https://bun.com/reference/node/cluster/Cluster/isPrimary): boolean

    True if the process is a primary. This is determined by the `process.env.NODE_UNIQUE_ID`. If `process.env.NODE_UNIQUE_ID` is undefined, then `isPrimary` is `true`.
  + readonly [isWorker](https://bun.com/reference/node/cluster/Cluster/isWorker): boolean

    True if the process is not a primary (it is the negation of `cluster.isPrimary`).
  + readonly [SCHED\_NONE](https://bun.com/reference/node/cluster/Cluster/SCHED_NONE): number
  + readonly [SCHED\_RR](https://bun.com/reference/node/cluster/Cluster/SCHED_RR): number
  + [schedulingPolicy](https://bun.com/reference/node/cluster/Cluster/schedulingPolicy): number

    The scheduling policy, either `cluster.SCHED_RR` for round-robin or `cluster.SCHED_NONE` to leave it to the operating system. This is a global setting and effectively frozen once either the first worker is spawned, or [`.setupPrimary()`](https://nodejs.org/docs/latest-v24.x/api/cluster.html#clustersetupprimarysettings) is called, whichever comes first.

    `SCHED_RR` is the default on all operating systems except Windows. Windows will change to `SCHED_RR` once libuv is able to effectively distribute IOCP handles without incurring a large performance hit.

    `cluster.schedulingPolicy` can also be set through the `NODE_CLUSTER_SCHED_POLICY` environment variable. Valid values are `'rr'` and `'none'`.
  + readonly [settings](https://bun.com/reference/node/cluster/Cluster/settings): [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)

    After calling [`.setupPrimary()`](https://nodejs.org/docs/latest-v24.x/api/cluster.html#clustersetupprimarysettings) (or [`.fork()`](https://nodejs.org/docs/latest-v24.x/api/cluster.html#clusterforkenv)) this settings object will contain the settings, including the default values.

    This object is not intended to be changed or set manually.
  + readonly [worker](https://bun.com/reference/node/cluster/Cluster/worker)?: [Worker](https://bun.com/reference/node/cluster/Worker)

    A reference to the current worker object. Not available in the primary process.

    ```
    import cluster from 'node:cluster';

    if (cluster.isPrimary) {
      console.log('I am primary');
      cluster.fork();
      cluster.fork();
    } else if (cluster.isWorker) {
      console.log(`I am worker #${cluster.worker.id}`);
    }
    ```
  + readonly [workers](https://bun.com/reference/node/cluster/Cluster/workers)?: Dict<[Worker](https://bun.com/reference/node/cluster/Worker)>

    A hash that stores the active worker objects, keyed by `id` field. This makes it easy to loop through all the workers. It is only available in the primary process.

    A worker is removed from `cluster.workers` after the worker has disconnected *and* exited. The order between these two events cannot be determined in advance. However, it is guaranteed that the removal from the `cluster.workers` list happens before the last `'disconnect'` or `'exit'` event is emitted.

    ```
    import cluster from 'node:cluster';

    for (const worker of Object.values(cluster.workers)) {
      worker.send('big announcement to all workers');
    }
    ```
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/cluster/Cluster/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. disconnect
    2. exit
    3. fork
    4. listening
    5. message
    6. online
    7. setup

    [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: 'disconnect',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: 'exit',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), code: number, signal: string) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: 'fork',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: 'listening',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), address: [Address](https://bun.com/reference/node/cluster/Address)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: 'message',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: 'online',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.

    [addListener](https://bun.com/reference/node/cluster/Cluster/addListener)(

    event: 'setup',

    listener: (settings: [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [disconnect](https://bun.com/reference/node/cluster/Cluster/disconnect)(

    callback?: () => void

    ): void;
  + [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: string | symbol,

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

    [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: 'disconnect',

    worker: [Worker](https://bun.com/reference/node/cluster/Worker)

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

    [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: 'exit',

    worker: [Worker](https://bun.com/reference/node/cluster/Worker),

    code: number,

    signal: string

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

    [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: 'fork',

    worker: [Worker](https://bun.com/reference/node/cluster/Worker)

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

    [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: 'listening',

    worker: [Worker](https://bun.com/reference/node/cluster/Worker),

    address: [Address](https://bun.com/reference/node/cluster/Address)

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

    [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: 'message',

    worker: [Worker](https://bun.com/reference/node/cluster/Worker),

    message: any,

    handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)

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

    [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: 'online',

    worker: [Worker](https://bun.com/reference/node/cluster/Worker)

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

    [emit](https://bun.com/reference/node/cluster/Cluster/emit)(

    event: 'setup',

    settings: [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)

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
  + [eventNames](https://bun.com/reference/node/cluster/Cluster/eventNames)(): string | symbol[];

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
  + [fork](https://bun.com/reference/node/cluster/Cluster/fork)(

    env?: any

    ): [Worker](https://bun.com/reference/node/cluster/Worker);

    Spawn a new worker process.

    This can only be called from the primary process.

    @param env

    Key/value pairs to add to worker process environment.
  + [getMaxListeners](https://bun.com/reference/node/cluster/Cluster/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/cluster/Cluster/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/cluster/Cluster/listeners)<K>(

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
  + [off](https://bun.com/reference/node/cluster/Cluster/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/cluster/Cluster/on)(

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

    [on](https://bun.com/reference/node/cluster/Cluster/on)(

    event: 'disconnect',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [on](https://bun.com/reference/node/cluster/Cluster/on)(

    event: 'exit',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), code: number, signal: string) => void

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

    [on](https://bun.com/reference/node/cluster/Cluster/on)(

    event: 'fork',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [on](https://bun.com/reference/node/cluster/Cluster/on)(

    event: 'listening',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), address: [Address](https://bun.com/reference/node/cluster/Address)) => void

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

    [on](https://bun.com/reference/node/cluster/Cluster/on)(

    event: 'message',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

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

    [on](https://bun.com/reference/node/cluster/Cluster/on)(

    event: 'online',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [on](https://bun.com/reference/node/cluster/Cluster/on)(

    event: 'setup',

    listener: (settings: [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)) => void

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
  + [once](https://bun.com/reference/node/cluster/Cluster/once)(

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

    [once](https://bun.com/reference/node/cluster/Cluster/once)(

    event: 'disconnect',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [once](https://bun.com/reference/node/cluster/Cluster/once)(

    event: 'exit',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), code: number, signal: string) => void

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

    [once](https://bun.com/reference/node/cluster/Cluster/once)(

    event: 'fork',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [once](https://bun.com/reference/node/cluster/Cluster/once)(

    event: 'listening',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), address: [Address](https://bun.com/reference/node/cluster/Address)) => void

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

    [once](https://bun.com/reference/node/cluster/Cluster/once)(

    event: 'message',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

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

    [once](https://bun.com/reference/node/cluster/Cluster/once)(

    event: 'online',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [once](https://bun.com/reference/node/cluster/Cluster/once)(

    event: 'setup',

    listener: (settings: [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)) => void

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
  + [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

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

    [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

    event: 'disconnect',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

    event: 'exit',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), code: number, signal: string) => void

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

    [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

    event: 'fork',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

    event: 'listening',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), address: [Address](https://bun.com/reference/node/cluster/Address)) => void

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

    [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

    event: 'message',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

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

    [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

    event: 'online',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [prependListener](https://bun.com/reference/node/cluster/Cluster/prependListener)(

    event: 'setup',

    listener: (settings: [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)) => void

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
  + [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

    event: 'disconnect',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

    event: 'exit',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), code: number, signal: string) => void

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

    event: 'fork',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

    event: 'listening',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), address: [Address](https://bun.com/reference/node/cluster/Address)) => void

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

    event: 'message',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker), message: any, handle: [Socket](https://bun.com/reference/node/net/Socket) | [Server](https://bun.com/reference/node/net/Server)) => void

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

    event: 'online',

    listener: (worker: [Worker](https://bun.com/reference/node/cluster/Worker)) => void

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

    [prependOnceListener](https://bun.com/reference/node/cluster/Cluster/prependOnceListener)(

    event: 'setup',

    listener: (settings: [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)) => void

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
  + [rawListeners](https://bun.com/reference/node/cluster/Cluster/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/cluster/Cluster/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/cluster/Cluster/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/cluster/Cluster/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setupPrimary](https://bun.com/reference/node/cluster/Cluster/setupPrimary)(

    settings?: [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)

    ): void;

    `setupPrimary` is used to change the default 'fork' behavior. Once called, the settings will be present in `cluster.settings`.

    Any settings changes only affect future calls to [`.fork()`](https://nodejs.org/docs/latest-v24.x/api/cluster.html#clusterforkenv) and have no effect on workers that are already running.

    The only attribute of a worker that cannot be set via `.setupPrimary()` is the `env` passed to [`.fork()`](https://nodejs.org/docs/latest-v24.x/api/cluster.html#clusterforkenv).

    The defaults above apply to the first call only; the defaults for later calls are the current values at the time of `cluster.setupPrimary()` is called.

    ```
    import cluster from 'node:cluster';

    cluster.setupPrimary({
      exec: 'worker.js',
      args: ['--use', 'https'],
      silent: true,
    });
    cluster.fork(); // https worker
    cluster.setupPrimary({
      exec: 'worker.js',
      args: ['--use', 'http'],
    });
    cluster.fork(); // http worker
    ```

    This can only be called from the primary process.
* ### interface [ClusterSettings](https://bun.com/reference/node/cluster/ClusterSettings)

  + [args](https://bun.com/reference/node/cluster/ClusterSettings/args)?: readonly string[]

    String arguments passed to worker.
  + [cwd](https://bun.com/reference/node/cluster/ClusterSettings/cwd)?: string

    Current working directory of the worker process.
  + [exec](https://bun.com/reference/node/cluster/ClusterSettings/exec)?: string

    File path to worker file.
  + [execArgv](https://bun.com/reference/node/cluster/ClusterSettings/execArgv)?: string[]

    List of string arguments passed to the Node.js executable.
  + [gid](https://bun.com/reference/node/cluster/ClusterSettings/gid)?: number

    Sets the group identity of the process. (See [`setgid(2)`](https://man7.org/linux/man-pages/man2/setgid.2.html).)
  + [inspectPort](https://bun.com/reference/node/cluster/ClusterSettings/inspectPort)?: number | () => number

    Sets inspector port of worker. This can be a number, or a function that takes no arguments and returns a number. By default each worker gets its own port, incremented from the primary's `process.debugPort`.
  + [serialization](https://bun.com/reference/node/cluster/ClusterSettings/serialization)?: SerializationType

    Specify the kind of serialization used for sending messages between processes. Possible values are `'json'` and `'advanced'`. See [Advanced serialization for `child_process`](https://nodejs.org/docs/latest-v24.x/api/child_process.html#advanced-serialization) for more details.
  + [silent](https://bun.com/reference/node/cluster/ClusterSettings/silent)?: boolean

    Whether or not to send output to parent's stdio.
  + [stdio](https://bun.com/reference/node/cluster/ClusterSettings/stdio)?: any[]

    Configures the stdio of forked processes. Because the cluster module relies on IPC to function, this configuration must contain an `'ipc'` entry. When this option is provided, it overrides `silent`. See [`child_prcess.spawn()`](https://nodejs.org/docs/latest-v24.x/api/child_process.html#child_processspawncommand-args-options)'s [`stdio`](https://nodejs.org/docs/latest-v24.x/api/child_process.html#optionsstdio).
  + [uid](https://bun.com/reference/node/cluster/ClusterSettings/uid)?: number

    Sets the user identity of the process. (See [`setuid(2)`](https://man7.org/linux/man-pages/man2/setuid.2.html).)
  + [windowsHide](https://bun.com/reference/node/cluster/ClusterSettings/windowsHide)?: boolean

    Hide the forked processes console window that would normally be created on Windows systems.