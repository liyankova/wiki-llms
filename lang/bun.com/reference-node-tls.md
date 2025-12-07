---
url: https://bun.com/reference/node/tls
title: Node.js tls module | API Reference | Bun
source_domain: bun.com
---

# Node.js tls module | API Reference | Bun

Node.js module

# [tls](https://bun.com/reference/node/tls)

The `'node:tls'` module provides an API for implementing TLS and SSL secure network communication. It wraps OpenSSL to create secure TCP connections via `tls.createServer` and `tls.connect`.

Features include certificate parsing, client authorization, secure context management, and TLS session resumption.

Works in Bun

Core TLS/SSL functionality works. The deprecated `tls.createSecurePair` method is missing.

* ### class [Server](https://bun.com/reference/node/tls/Server)

  Accepts encrypted connections using TLS or SSL.

  + [connections](https://bun.com/reference/node/tls/Server/connections): number
  + readonly [listening](https://bun.com/reference/node/tls/Server/listening): boolean

    Indicates whether or not the server is listening for connections.
  + [maxConnections](https://bun.com/reference/node/tls/Server/maxConnections): number

    Set this property to reject connections when the server's connection count gets high.

    It is not recommended to use this option once a socket has been sent to a child with `child_process.fork()`.
  + static [captureRejections](https://bun.com/reference/node/tls/Server/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/tls/Server/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/tls/Server/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/tls/Server/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/tls/Server/[asyncDispose])(): Promise<void>;

    Calls () and returns a promise that fulfills when the server has closed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/tls/Server/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addContext](https://bun.com/reference/node/tls/Server/addContext)(

    hostname: string,

    context: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions) | [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    ): void;

    The `server.addContext()` method adds a secure context that will be used if the client request's SNI name matches the supplied `hostname` (or wildcard).

    When there are multiple matching contexts, the most recently added one is used.

    @param hostname

    A SNI host name or wildcard (e.g. `'*'`)

    @param context

    An object containing any of the possible properties from the createSecureContext `options` arguments (e.g. `key`, `cert`, `ca`, etc), or a TLS context object created with createSecureContext itself.
  + [addListener](https://bun.com/reference/node/tls/Server/addListener)(

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

    [addListener](https://bun.com/reference/node/tls/Server/addListener)(

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

    [addListener](https://bun.com/reference/node/tls/Server/addListener)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/tls/Server/addListener)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/tls/Server/addListener)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/tls/Server/addListener)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog

    [addListener](https://bun.com/reference/node/tls/Server/addListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    events.EventEmitter

    1. tlsClientError
    2. newSession
    3. OCSPRequest
    4. resumeSession
    5. secureConnection
    6. keylog
  + [address](https://bun.com/reference/node/tls/Server/address)(): null | string | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

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
  + [close](https://bun.com/reference/node/tls/Server/close)(

    callback?: (err?: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Stops the server from accepting new connections and keeps existing connections. This function is asynchronous, the server is finally closed when all connections are ended and the server emits a `'close'` event. The optional `callback` will be called once the `'close'` event occurs. Unlike that event, it will be called with an `Error` as its only argument if the server was not open when it was closed.

    @param callback

    Called when the server is closed.
  + [emit](https://bun.com/reference/node/tls/Server/emit)(

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

    [emit](https://bun.com/reference/node/tls/Server/emit)(

    event: 'tlsClientError',

    err: [Error](https://bun.com/reference/globals/Error),

    tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    [emit](https://bun.com/reference/node/tls/Server/emit)(

    event: 'newSession',

    sessionId: NonSharedBuffer,

    sessionData: NonSharedBuffer,

    callback: () => void

    ): boolean;

    [emit](https://bun.com/reference/node/tls/Server/emit)(

    event: 'OCSPRequest',

    certificate: NonSharedBuffer,

    issuer: NonSharedBuffer,

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): boolean;

    [emit](https://bun.com/reference/node/tls/Server/emit)(

    event: 'resumeSession',

    sessionId: NonSharedBuffer,

    callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void

    ): boolean;

    [emit](https://bun.com/reference/node/tls/Server/emit)(

    event: 'secureConnection',

    tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;

    [emit](https://bun.com/reference/node/tls/Server/emit)(

    event: 'keylog',

    line: NonSharedBuffer,

    tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

    ): boolean;
  + [eventNames](https://bun.com/reference/node/tls/Server/eventNames)(): string | symbol[];

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
  + [getConnections](https://bun.com/reference/node/tls/Server/getConnections)(

    cb: (error: null | [Error](https://bun.com/reference/globals/Error), count: number) => void

    ): this;

    Asynchronously get the number of concurrent connections on the server. Works when sockets were sent to forks.

    Callback should take two arguments `err` and `count`.
  + [getMaxListeners](https://bun.com/reference/node/tls/Server/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getTicketKeys](https://bun.com/reference/node/tls/Server/getTicketKeys)(): NonSharedBuffer;

    Returns the session ticket keys.

    See `Session Resumption` for more information.

    @returns

    A 48-byte buffer containing the session ticket keys.
  + [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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

    [listen](https://bun.com/reference/node/tls/Server/listen)(

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
  + [listenerCount](https://bun.com/reference/node/tls/Server/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/tls/Server/listeners)<K>(

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
  + [off](https://bun.com/reference/node/tls/Server/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/tls/Server/on)(

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

    [on](https://bun.com/reference/node/tls/Server/on)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [on](https://bun.com/reference/node/tls/Server/on)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [on](https://bun.com/reference/node/tls/Server/on)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [on](https://bun.com/reference/node/tls/Server/on)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [on](https://bun.com/reference/node/tls/Server/on)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [on](https://bun.com/reference/node/tls/Server/on)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;
  + [once](https://bun.com/reference/node/tls/Server/once)(

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

    [once](https://bun.com/reference/node/tls/Server/once)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [once](https://bun.com/reference/node/tls/Server/once)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [once](https://bun.com/reference/node/tls/Server/once)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [once](https://bun.com/reference/node/tls/Server/once)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [once](https://bun.com/reference/node/tls/Server/once)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [once](https://bun.com/reference/node/tls/Server/once)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/tls/Server/prependListener)(

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

    [prependListener](https://bun.com/reference/node/tls/Server/prependListener)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/Server/prependListener)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/Server/prependListener)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/Server/prependListener)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/Server/prependListener)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/Server/prependListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/tls/Server/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/tls/Server/prependOnceListener)(

    event: 'tlsClientError',

    listener: (err: [Error](https://bun.com/reference/globals/Error), tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/Server/prependOnceListener)(

    event: 'newSession',

    listener: (sessionId: NonSharedBuffer, sessionData: NonSharedBuffer, callback: () => void) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/Server/prependOnceListener)(

    event: 'OCSPRequest',

    listener: (certificate: NonSharedBuffer, issuer: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), resp: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/Server/prependOnceListener)(

    event: 'resumeSession',

    listener: (sessionId: NonSharedBuffer, callback: (err: null | [Error](https://bun.com/reference/globals/Error), sessionData: null | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>) => void) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/Server/prependOnceListener)(

    event: 'secureConnection',

    listener: (tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/Server/prependOnceListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer, tlsSocket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/tls/Server/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/tls/Server/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed server will *not* let the program exit if it's the only server left (the default behavior). If the server is `ref`ed calling `ref()` again will have no effect.
  + [removeAllListeners](https://bun.com/reference/node/tls/Server/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/tls/Server/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/tls/Server/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setSecureContext](https://bun.com/reference/node/tls/Server/setSecureContext)(

    options: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions)

    ): void;

    The `server.setSecureContext()` method replaces the secure context of an existing server. Existing connections to the server are not interrupted.

    @param options

    An object containing any of the possible properties from the createSecureContext `options` arguments (e.g. `key`, `cert`, `ca`, etc).
  + [setTicketKeys](https://bun.com/reference/node/tls/Server/setTicketKeys)(

    keys: [Buffer](https://bun.com/reference/node/buffer/Buffer)

    ): void;

    Sets the session ticket keys.

    Changes to the ticket keys are effective only for future server connections. Existing or currently pending server connections will use the previous keys.

    See `Session Resumption` for more information.

    @param keys

    A 48-byte buffer containing the session ticket keys.
  + [unref](https://bun.com/reference/node/tls/Server/unref)(): this;

    Calling `unref()` on a server will allow the program to exit if this is the only active server in the event system. If the server is already `unref`ed calling`unref()` again will have no effect.
  + static [addAbortListener](https://bun.com/reference/node/tls/Server/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/tls/Server/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/tls/Server/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/tls/Server/on)(

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

    static [on](https://bun.com/reference/node/tls/Server/on)(

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
  + static [once](https://bun.com/reference/node/tls/Server/once)(

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

    static [once](https://bun.com/reference/node/tls/Server/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/tls/Server/setMaxListeners)(

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
* ### class [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)

  Performs transparent encryption of written data and all required TLS negotiation.

  Instances of `tls.TLSSocket` implement the duplex `Stream` interface.

  Methods that return TLS connection metadata (e.g.TLSSocket.getPeerCertificate) will only return data while the connection is open.

  + [allowHalfOpen](https://bun.com/reference/node/tls/TLSSocket/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + [authorizationError](https://bun.com/reference/node/tls/TLSSocket/authorizationError): [Error](https://bun.com/reference/globals/Error)

    Returns the reason why the peer's certificate was not been verified. This property is set only when `tlsSocket.authorized === false`.
  + [authorized](https://bun.com/reference/node/tls/TLSSocket/authorized): boolean

    This property is `true` if the peer certificate was signed by one of the CAs specified when creating the `tls.TLSSocket` instance, otherwise `false`.
  + readonly [autoSelectFamilyAttemptedAddresses](https://bun.com/reference/node/tls/TLSSocket/autoSelectFamilyAttemptedAddresses): string[]

    This property is only present if the family autoselection algorithm is enabled in `socket.connect(options)` and it is an array of the addresses that have been attempted.

    Each address is a string in the form of `$IP:$PORT`. If the connection was successful, then the last address is the one that the socket is currently connected to.
  + readonly [bytesRead](https://bun.com/reference/node/tls/TLSSocket/bytesRead): number

    The amount of received bytes.
  + readonly [bytesWritten](https://bun.com/reference/node/tls/TLSSocket/bytesWritten): number

    The amount of bytes sent.
  + readonly [closed](https://bun.com/reference/node/tls/TLSSocket/closed): boolean

    Is `true` after `'close'` has been emitted.
  + readonly [connecting](https://bun.com/reference/node/tls/TLSSocket/connecting): boolean

    If `true`, `socket.connect(options[, connectListener])` was called and has not yet finished. It will stay `true` until the socket becomes connected, then it is set to `false` and the `'connect'` event is emitted. Note that the `socket.connect(options[, connectListener])` callback is a listener for the `'connect'` event.
  + readonly [destroyed](https://bun.com/reference/node/tls/TLSSocket/destroyed): boolean

    See `writable.destroyed` for further details.
  + [encrypted](https://bun.com/reference/node/tls/TLSSocket/encrypted): true

    Always returns `true`. This may be used to distinguish TLS sockets from regular`net.Socket` instances.
  + readonly [errored](https://bun.com/reference/node/tls/TLSSocket/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [localAddress](https://bun.com/reference/node/tls/TLSSocket/localAddress)?: string

    The string representation of the local IP address the remote client is connecting on. For example, in a server listening on `'0.0.0.0'`, if a client connects on `'192.168.1.1'`, the value of `socket.localAddress` would be`'192.168.1.1'`.
  + readonly [localFamily](https://bun.com/reference/node/tls/TLSSocket/localFamily)?: string

    The string representation of the local IP family. `'IPv4'` or `'IPv6'`.
  + readonly [localPort](https://bun.com/reference/node/tls/TLSSocket/localPort)?: number

    The numeric representation of the local port. For example, `80` or `21`.
  + readonly [pending](https://bun.com/reference/node/tls/TLSSocket/pending): boolean

    This is `true` if the socket is not connected yet, either because `.connect()`has not yet been called or because it is still in the process of connecting (see `socket.connecting`).
  + [readable](https://bun.com/reference/node/tls/TLSSocket/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/tls/TLSSocket/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/tls/TLSSocket/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/tls/TLSSocket/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/tls/TLSSocket/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/tls/TLSSocket/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/tls/TLSSocket/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/tls/TLSSocket/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/tls/TLSSocket/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + readonly [readyState](https://bun.com/reference/node/tls/TLSSocket/readyState): [SocketReadyState](https://bun.com/reference/node/net/SocketReadyState)

    This property represents the state of the connection as a string.

    - If the stream is connecting `socket.readyState` is `opening`.
    - If the stream is readable and writable, it is `open`.
    - If the stream is readable and not writable, it is `readOnly`.
    - If the stream is not readable and writable, it is `writeOnly`.
  + readonly [remoteAddress](https://bun.com/reference/node/tls/TLSSocket/remoteAddress): undefined | string

    The string representation of the remote IP address. For example,`'74.125.127.100'` or `'2001:4860:a005::68'`. Value may be `undefined` if the socket is destroyed (for example, if the client disconnected).
  + readonly [remoteFamily](https://bun.com/reference/node/tls/TLSSocket/remoteFamily): undefined | string

    The string representation of the remote IP family. `'IPv4'` or `'IPv6'`. Value may be `undefined` if the socket is destroyed (for example, if the client disconnected).
  + readonly [remotePort](https://bun.com/reference/node/tls/TLSSocket/remotePort): undefined | number

    The numeric representation of the remote port. For example, `80` or `21`. Value may be `undefined` if the socket is destroyed (for example, if the client disconnected).
  + readonly [timeout](https://bun.com/reference/node/tls/TLSSocket/timeout)?: number

    The socket timeout in milliseconds as set by `socket.setTimeout()`. It is `undefined` if a timeout has not been set.
  + readonly [writable](https://bun.com/reference/node/tls/TLSSocket/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/tls/TLSSocket/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/tls/TLSSocket/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/tls/TLSSocket/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/tls/TLSSocket/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/tls/TLSSocket/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/tls/TLSSocket/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/tls/TLSSocket/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/tls/TLSSocket/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + static [captureRejections](https://bun.com/reference/node/tls/TLSSocket/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/tls/TLSSocket/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/tls/TLSSocket/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/tls/TLSSocket/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/tls/TLSSocket/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/tls/TLSSocket/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/tls/TLSSocket/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/tls/TLSSocket/_read)(

    size: number

    ): void;
  + [\_write](https://bun.com/reference/node/tls/TLSSocket/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/tls/TLSSocket/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/tls/TLSSocket/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/tls/TLSSocket/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/tls/TLSSocket/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/tls/TLSSocket/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. connectionAttempt
    4. connectionAttemptFailed
    5. connectionAttemptTimeout
    6. data
    7. drain
    8. end
    9. error
    10. lookup
    11. ready
    12. timeout

    [addListener](https://bun.com/reference/node/tls/TLSSocket/addListener)(

    event: 'OCSPResponse',

    listener: (response: NonSharedBuffer) => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. connectionAttempt
    4. connectionAttemptFailed
    5. connectionAttemptTimeout
    6. data
    7. drain
    8. end
    9. error
    10. lookup
    11. ready
    12. timeout

    [addListener](https://bun.com/reference/node/tls/TLSSocket/addListener)(

    event: 'secureConnect',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. connectionAttempt
    4. connectionAttemptFailed
    5. connectionAttemptTimeout
    6. data
    7. drain
    8. end
    9. error
    10. lookup
    11. ready
    12. timeout

    [addListener](https://bun.com/reference/node/tls/TLSSocket/addListener)(

    event: 'session',

    listener: (session: NonSharedBuffer) => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. connectionAttempt
    4. connectionAttemptFailed
    5. connectionAttemptTimeout
    6. data
    7. drain
    8. end
    9. error
    10. lookup
    11. ready
    12. timeout

    [addListener](https://bun.com/reference/node/tls/TLSSocket/addListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer) => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. connectionAttempt
    4. connectionAttemptFailed
    5. connectionAttemptTimeout
    6. data
    7. drain
    8. end
    9. error
    10. lookup
    11. ready
    12. timeout
  + [address](https://bun.com/reference/node/tls/TLSSocket/address)(): {} | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

    Returns the bound `address`, the address `family` name and `port` of the socket as reported by the operating system:`{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`
  + [asIndexedPairs](https://bun.com/reference/node/tls/TLSSocket/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [compose](https://bun.com/reference/node/tls/TLSSocket/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [connect](https://bun.com/reference/node/tls/TLSSocket/connect)(

    options: [SocketConnectOpts](https://bun.com/reference/node/net/SocketConnectOpts),

    connectionListener?: () => void

    ): this;

    Initiate a connection on a given socket.

    Possible signatures:

    - `socket.connect(options[, connectListener])`
    - `socket.connect(path[, connectListener])` for `IPC` connections.
    - `socket.connect(port[, host][, connectListener])` for TCP connections.
    - Returns: `net.Socket` The socket itself.

    This function is asynchronous. When the connection is established, the `'connect'` event will be emitted. If there is a problem connecting, instead of a `'connect'` event, an `'error'` event will be emitted with the error passed to the `'error'` listener. The last parameter `connectListener`, if supplied, will be added as a listener for the `'connect'` event **once**.

    This function should only be used for reconnecting a socket after`'close'` has been emitted or otherwise it may lead to undefined behavior.

    [connect](https://bun.com/reference/node/tls/TLSSocket/connect)(

    port: number,

    host: string,

    connectionListener?: () => void

    ): this;

    Initiate a connection on a given socket.

    Possible signatures:

    - `socket.connect(options[, connectListener])`
    - `socket.connect(path[, connectListener])` for `IPC` connections.
    - `socket.connect(port[, host][, connectListener])` for TCP connections.
    - Returns: `net.Socket` The socket itself.

    This function is asynchronous. When the connection is established, the `'connect'` event will be emitted. If there is a problem connecting, instead of a `'connect'` event, an `'error'` event will be emitted with the error passed to the `'error'` listener. The last parameter `connectListener`, if supplied, will be added as a listener for the `'connect'` event **once**.

    This function should only be used for reconnecting a socket after`'close'` has been emitted or otherwise it may lead to undefined behavior.

    [connect](https://bun.com/reference/node/tls/TLSSocket/connect)(

    port: number,

    connectionListener?: () => void

    ): this;

    Initiate a connection on a given socket.

    Possible signatures:

    - `socket.connect(options[, connectListener])`
    - `socket.connect(path[, connectListener])` for `IPC` connections.
    - `socket.connect(port[, host][, connectListener])` for TCP connections.
    - Returns: `net.Socket` The socket itself.

    This function is asynchronous. When the connection is established, the `'connect'` event will be emitted. If there is a problem connecting, instead of a `'connect'` event, an `'error'` event will be emitted with the error passed to the `'error'` listener. The last parameter `connectListener`, if supplied, will be added as a listener for the `'connect'` event **once**.

    This function should only be used for reconnecting a socket after`'close'` has been emitted or otherwise it may lead to undefined behavior.

    [connect](https://bun.com/reference/node/tls/TLSSocket/connect)(

    path: string,

    connectionListener?: () => void

    ): this;

    Initiate a connection on a given socket.

    Possible signatures:

    - `socket.connect(options[, connectListener])`
    - `socket.connect(path[, connectListener])` for `IPC` connections.
    - `socket.connect(port[, host][, connectListener])` for TCP connections.
    - Returns: `net.Socket` The socket itself.

    This function is asynchronous. When the connection is established, the `'connect'` event will be emitted. If there is a problem connecting, instead of a `'connect'` event, an `'error'` event will be emitted with the error passed to the `'error'` listener. The last parameter `connectListener`, if supplied, will be added as a listener for the `'connect'` event **once**.

    This function should only be used for reconnecting a socket after`'close'` has been emitted or otherwise it may lead to undefined behavior.
  + [cork](https://bun.com/reference/node/tls/TLSSocket/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/tls/TLSSocket/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [destroySoon](https://bun.com/reference/node/tls/TLSSocket/destroySoon)(): void;

    Destroys the socket after all data is written. If the `finish` event was already emitted the socket is destroyed immediately. If the socket is still writable it implicitly calls `socket.end()`.
  + [disableRenegotiation](https://bun.com/reference/node/tls/TLSSocket/disableRenegotiation)(): void;

    Disables TLS renegotiation for this `TLSSocket` instance. Once called, attempts to renegotiate will trigger an `'error'` event on the `TLSSocket`.
  + [drop](https://bun.com/reference/node/tls/TLSSocket/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/tls/TLSSocket/emit)(

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

    [emit](https://bun.com/reference/node/tls/TLSSocket/emit)(

    event: 'OCSPResponse',

    response: NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/tls/TLSSocket/emit)(

    event: 'secureConnect'

    ): boolean;

    [emit](https://bun.com/reference/node/tls/TLSSocket/emit)(

    event: 'session',

    session: NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/tls/TLSSocket/emit)(

    event: 'keylog',

    line: NonSharedBuffer

    ): boolean;
  + [enableTrace](https://bun.com/reference/node/tls/TLSSocket/enableTrace)(): void;

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.

    The format of the output is identical to the output of`openssl s_client -trace` or `openssl s_server -trace`. While it is produced by OpenSSL's `SSL_trace()` function, the format is undocumented, can change without notice, and should not be relied on.
  + [end](https://bun.com/reference/node/tls/TLSSocket/end)(

    callback?: () => void

    ): this;

    Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data.

    See `writable.end()` for further details.

    @param callback

    Optional callback for when the socket is finished.

    @returns

    The socket itself.

    [end](https://bun.com/reference/node/tls/TLSSocket/end)(

    buffer: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    callback?: () => void

    ): this;

    Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data.

    See `writable.end()` for further details.

    @param callback

    Optional callback for when the socket is finished.

    @returns

    The socket itself.

    [end](https://bun.com/reference/node/tls/TLSSocket/end)(

    str: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    encoding?: BufferEncoding,

    callback?: () => void

    ): this;

    Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data.

    See `writable.end()` for further details.

    @param encoding

    Only used when data is `string`.

    @param callback

    Optional callback for when the socket is finished.

    @returns

    The socket itself.
  + [eventNames](https://bun.com/reference/node/tls/TLSSocket/eventNames)(): string | symbol[];

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
  + [every](https://bun.com/reference/node/tls/TLSSocket/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [exportKeyingMaterial](https://bun.com/reference/node/tls/TLSSocket/exportKeyingMaterial)(

    length: number,

    label: string,

    context: [Buffer](https://bun.com/reference/node/buffer/Buffer)

    ): NonSharedBuffer;

    Keying material is used for validations to prevent different kind of attacks in network protocols, for example in the specifications of IEEE 802.1X.

    Example

    ```
    const keyingMaterial = tlsSocket.exportKeyingMaterial(
      128,
      'client finished');

    /*
     Example return value of keyingMaterial:
     <Buffer 76 26 af 99 c5 56 8e 42 09 91 ef 9f 93 cb ad 6c 7b 65 f8 53 f1 d8 d9
        12 5a 33 b8 b5 25 df 7b 37 9f e0 e2 4f b8 67 83 a3 2f cd 5d 41 42 4c 91
        74 ef 2c ... 78 more bytes>
    ```

    See the OpenSSL [`SSL_export_keying_material`](https://www.openssl.org/docs/man1.1.1/man3/SSL_export_keying_material.html) documentation for more information.

    @param length

    number of bytes to retrieve from keying material

    @param label

    an application specific label, typically this will be a value from the [IANA Exporter Label Registry](https://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#exporter-labels).

    @param context

    Optionally provide a context.

    @returns

    requested bytes of the keying material
  + [filter](https://bun.com/reference/node/tls/TLSSocket/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/tls/TLSSocket/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/tls/TLSSocket/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/tls/TLSSocket/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/tls/TLSSocket/forEach)(

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
  + [getCertificate](https://bun.com/reference/node/tls/TLSSocket/getCertificate)(): null | object | [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate);

    Returns an object representing the local certificate. The returned object has some properties corresponding to the fields of the certificate.

    See TLSSocket.getPeerCertificate for an example of the certificate structure.

    If there is no local certificate, an empty object will be returned. If the socket has been destroyed, `null` will be returned.
  + [getCipher](https://bun.com/reference/node/tls/TLSSocket/getCipher)(): [CipherNameAndProtocol](https://bun.com/reference/node/tls/CipherNameAndProtocol);

    Returns an object containing information on the negotiated cipher suite.

    For example, a TLSv1.2 protocol with AES256-SHA cipher:

    ```
    {
        "name": "AES256-SHA",
        "standardName": "TLS_RSA_WITH_AES_256_CBC_SHA",
        "version": "SSLv3"
    }
    ```

    See [SSL\_CIPHER\_get\_name](https://www.openssl.org/docs/man1.1.1/man3/SSL_CIPHER_get_name.html) for more information.
  + [getEphemeralKeyInfo](https://bun.com/reference/node/tls/TLSSocket/getEphemeralKeyInfo)(): null | object | [EphemeralKeyInfo](https://bun.com/reference/node/tls/EphemeralKeyInfo);

    Returns an object representing the type, name, and size of parameter of an ephemeral key exchange in `perfect forward secrecy` on a client connection. It returns an empty object when the key exchange is not ephemeral. As this is only supported on a client socket; `null` is returned if called on a server socket. The supported types are `'DH'` and `'ECDH'`. The `name` property is available only when type is `'ECDH'`.

    For example: `{ type: 'ECDH', name: 'prime256v1', size: 256 }`.
  + [getFinished](https://bun.com/reference/node/tls/TLSSocket/getFinished)(): undefined | NonSharedBuffer;

    As the `Finished` messages are message digests of the complete handshake (with a total of 192 bits for TLS 1.0 and more for SSL 3.0), they can be used for external authentication procedures when the authentication provided by SSL/TLS is not desired or is not enough.

    Corresponds to the `SSL_get_finished` routine in OpenSSL and may be used to implement the `tls-unique` channel binding from [RFC 5929](https://tools.ietf.org/html/rfc5929).

    @returns

    The latest `Finished` message that has been sent to the socket as part of a SSL/TLS handshake, or `undefined` if no `Finished` message has been sent yet.
  + [getMaxListeners](https://bun.com/reference/node/tls/TLSSocket/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getPeerCertificate](https://bun.com/reference/node/tls/TLSSocket/getPeerCertificate)(

    detailed: true

    ): [DetailedPeerCertificate](https://bun.com/reference/node/tls/DetailedPeerCertificate);

    Returns an object representing the peer's certificate. If the peer does not provide a certificate, an empty object will be returned. If the socket has been destroyed, `null` will be returned.

    If the full certificate chain was requested, each certificate will include an`issuerCertificate` property containing an object representing its issuer's certificate.

    @param detailed

    Include the full certificate chain if `true`, otherwise include just the peer's certificate.

    @returns

    A certificate object.

    [getPeerCertificate](https://bun.com/reference/node/tls/TLSSocket/getPeerCertificate)(

    detailed?: false

    ): [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate);

    Returns an object representing the peer's certificate. If the peer does not provide a certificate, an empty object will be returned. If the socket has been destroyed, `null` will be returned.

    If the full certificate chain was requested, each certificate will include an`issuerCertificate` property containing an object representing its issuer's certificate.

    @param detailed

    Include the full certificate chain if `true`, otherwise include just the peer's certificate.

    @returns

    A certificate object.

    [getPeerCertificate](https://bun.com/reference/node/tls/TLSSocket/getPeerCertificate)(

    detailed?: boolean

    ): [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate) | [DetailedPeerCertificate](https://bun.com/reference/node/tls/DetailedPeerCertificate);

    Returns an object representing the peer's certificate. If the peer does not provide a certificate, an empty object will be returned. If the socket has been destroyed, `null` will be returned.

    If the full certificate chain was requested, each certificate will include an`issuerCertificate` property containing an object representing its issuer's certificate.

    @param detailed

    Include the full certificate chain if `true`, otherwise include just the peer's certificate.

    @returns

    A certificate object.
  + [getPeerFinished](https://bun.com/reference/node/tls/TLSSocket/getPeerFinished)(): undefined | NonSharedBuffer;

    As the `Finished` messages are message digests of the complete handshake (with a total of 192 bits for TLS 1.0 and more for SSL 3.0), they can be used for external authentication procedures when the authentication provided by SSL/TLS is not desired or is not enough.

    Corresponds to the `SSL_get_peer_finished` routine in OpenSSL and may be used to implement the `tls-unique` channel binding from [RFC 5929](https://tools.ietf.org/html/rfc5929).

    @returns

    The latest `Finished` message that is expected or has actually been received from the socket as part of a SSL/TLS handshake, or `undefined` if there is no `Finished` message so far.
  + [getPeerX509Certificate](https://bun.com/reference/node/tls/TLSSocket/getPeerX509Certificate)(): undefined | [X509Certificate](https://bun.com/reference/node/crypto/X509Certificate);

    Returns the peer certificate as an `X509Certificate` object.

    If there is no peer certificate, or the socket has been destroyed,`undefined` will be returned.
  + [getSession](https://bun.com/reference/node/tls/TLSSocket/getSession)(): undefined | NonSharedBuffer;

    Returns the TLS session data or `undefined` if no session was negotiated. On the client, the data can be provided to the `session` option of connect to resume the connection. On the server, it may be useful for debugging.

    See `Session Resumption` for more information.

    Note: `getSession()` works only for TLSv1.2 and below. For TLSv1.3, applications must use the `'session'` event (it also works for TLSv1.2 and below).
  + [getSharedSigalgs](https://bun.com/reference/node/tls/TLSSocket/getSharedSigalgs)(): string[];

    See [SSL\_get\_shared\_sigalgs](https://www.openssl.org/docs/man1.1.1/man3/SSL_get_shared_sigalgs.html) for more information.

    @returns

    List of signature algorithms shared between the server and the client in the order of decreasing preference.
  + [getTLSTicket](https://bun.com/reference/node/tls/TLSSocket/getTLSTicket)(): undefined | NonSharedBuffer;

    For a client, returns the TLS session ticket if one is available, or`undefined`. For a server, always returns `undefined`.

    It may be useful for debugging.

    See `Session Resumption` for more information.
  + [getX509Certificate](https://bun.com/reference/node/tls/TLSSocket/getX509Certificate)(): undefined | [X509Certificate](https://bun.com/reference/node/crypto/X509Certificate);

    Returns the local certificate as an `X509Certificate` object.

    If there is no local certificate, or the socket has been destroyed,`undefined` will be returned.
  + [isPaused](https://bun.com/reference/node/tls/TLSSocket/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [isSessionReused](https://bun.com/reference/node/tls/TLSSocket/isSessionReused)(): boolean;

    See `Session Resumption` for more information.

    @returns

    `true` if the session was reused, `false` otherwise.
  + [iterator](https://bun.com/reference/node/tls/TLSSocket/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/tls/TLSSocket/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/tls/TLSSocket/listeners)<K>(

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
  + [map](https://bun.com/reference/node/tls/TLSSocket/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/tls/TLSSocket/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/tls/TLSSocket/on)(

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

    [on](https://bun.com/reference/node/tls/TLSSocket/on)(

    event: 'OCSPResponse',

    listener: (response: NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/tls/TLSSocket/on)(

    event: 'secureConnect',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/tls/TLSSocket/on)(

    event: 'session',

    listener: (session: NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/tls/TLSSocket/on)(

    event: 'keylog',

    listener: (line: NonSharedBuffer) => void

    ): this;
  + [once](https://bun.com/reference/node/tls/TLSSocket/once)(

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

    [once](https://bun.com/reference/node/tls/TLSSocket/once)(

    event: 'OCSPResponse',

    listener: (response: NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/tls/TLSSocket/once)(

    event: 'secureConnect',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/tls/TLSSocket/once)(

    event: 'session',

    listener: (session: NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/tls/TLSSocket/once)(

    event: 'keylog',

    listener: (line: NonSharedBuffer) => void

    ): this;
  + [pause](https://bun.com/reference/node/tls/TLSSocket/pause)(): this;

    Pauses the reading of data. That is, `'data'` events will not be emitted. Useful to throttle back an upload.

    @returns

    The socket itself.
  + [pipe](https://bun.com/reference/node/tls/TLSSocket/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/tls/TLSSocket/prependListener)(

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

    [prependListener](https://bun.com/reference/node/tls/TLSSocket/prependListener)(

    event: 'OCSPResponse',

    listener: (response: NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/TLSSocket/prependListener)(

    event: 'secureConnect',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/TLSSocket/prependListener)(

    event: 'session',

    listener: (session: NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/tls/TLSSocket/prependListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/tls/TLSSocket/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/tls/TLSSocket/prependOnceListener)(

    event: 'OCSPResponse',

    listener: (response: NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/TLSSocket/prependOnceListener)(

    event: 'secureConnect',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/TLSSocket/prependOnceListener)(

    event: 'session',

    listener: (session: NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/tls/TLSSocket/prependOnceListener)(

    event: 'keylog',

    listener: (line: NonSharedBuffer) => void

    ): this;
  + [push](https://bun.com/reference/node/tls/TLSSocket/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/tls/TLSSocket/rawListeners)<K>(

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
  + [read](https://bun.com/reference/node/tls/TLSSocket/read)(

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
  + [reduce](https://bun.com/reference/node/tls/TLSSocket/reduce)<T = any>(

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

    [reduce](https://bun.com/reference/node/tls/TLSSocket/reduce)<T = any>(

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
  + [ref](https://bun.com/reference/node/tls/TLSSocket/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed socket will *not* let the program exit if it's the only socket left (the default behavior). If the socket is `ref`ed calling `ref` again will have no effect.

    @returns

    The socket itself.
  + [removeAllListeners](https://bun.com/reference/node/tls/TLSSocket/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

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

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/tls/TLSSocket/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [renegotiate](https://bun.com/reference/node/tls/TLSSocket/renegotiate)(

    options: { rejectUnauthorized: boolean; requestCert: boolean },

    callback: (err: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): undefined | boolean;

    The `tlsSocket.renegotiate()` method initiates a TLS renegotiation process. Upon completion, the `callback` function will be passed a single argument that is either an `Error` (if the request failed) or `null`.

    This method can be used to request a peer's certificate after the secure connection has been established.

    When running as the server, the socket will be destroyed with an error after `handshakeTimeout` timeout.

    For TLSv1.3, renegotiation cannot be initiated, it is not supported by the protocol.

    @param callback

    If `renegotiate()` returned `true`, callback is attached once to the `'secure'` event. If `renegotiate()` returned `false`, `callback` will be called in the next tick with an error, unless the `tlsSocket` has been destroyed, in which case `callback` will not be called at all.

    @returns

    `true` if renegotiation was initiated, `false` otherwise.
  + [resetAndDestroy](https://bun.com/reference/node/tls/TLSSocket/resetAndDestroy)(): this;

    Close the TCP connection by sending an RST packet and destroy the stream. If this TCP socket is in connecting status, it will send an RST packet and destroy this TCP socket once it is connected. Otherwise, it will call `socket.destroy` with an `ERR_SOCKET_CLOSED` Error. If this is not a TCP socket (for example, a pipe), calling this method will immediately throw an `ERR_INVALID_HANDLE_TYPE` Error.
  + [resume](https://bun.com/reference/node/tls/TLSSocket/resume)(): this;

    Resumes reading after a call to `socket.pause()`.

    @returns

    The socket itself.
  + [setDefaultEncoding](https://bun.com/reference/node/tls/TLSSocket/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/tls/TLSSocket/setEncoding)(

    encoding?: BufferEncoding

    ): this;

    Set the encoding for the socket as a `Readable Stream`. See `readable.setEncoding()` for more information.

    @returns

    The socket itself.
  + [setKeepAlive](https://bun.com/reference/node/tls/TLSSocket/setKeepAlive)(

    enable?: boolean,

    initialDelay?: number

    ): this;

    Enable/disable keep-alive functionality, and optionally set the initial delay before the first keepalive probe is sent on an idle socket.

    Set `initialDelay` (in milliseconds) to set the delay between the last data packet received and the first keepalive probe. Setting `0` for`initialDelay` will leave the value unchanged from the default (or previous) setting.

    Enabling the keep-alive functionality will set the following socket options:

    - `SO_KEEPALIVE=1`
    - `TCP_KEEPIDLE=initialDelay`
    - `TCP_KEEPCNT=10`
    - `TCP_KEEPINTVL=1`

    @returns

    The socket itself.
  + [setKeyCert](https://bun.com/reference/node/tls/TLSSocket/setKeyCert)(

    context: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions) | [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    ): void;

    The `tlsSocket.setKeyCert()` method sets the private key and certificate to use for the socket. This is mainly useful if you wish to select a server certificate from a TLS server's `ALPNCallback`.

    @param context

    An object containing at least `key` and `cert` properties from the () `options`, or a TLS context object created with () itself.
  + [setMaxListeners](https://bun.com/reference/node/tls/TLSSocket/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setMaxSendFragment](https://bun.com/reference/node/tls/TLSSocket/setMaxSendFragment)(

    size?: number

    ): boolean;

    The `tlsSocket.setMaxSendFragment()` method sets the maximum TLS fragment size. Returns `true` if setting the limit succeeded; `false` otherwise.

    Smaller fragment sizes decrease the buffering latency on the client: larger fragments are buffered by the TLS layer until the entire fragment is received and its integrity is verified; large fragments can span multiple roundtrips and their processing can be delayed due to packet loss or reordering. However, smaller fragments add extra TLS framing bytes and CPU overhead, which may decrease overall server throughput.

    @param size

    The maximum TLS fragment size. The maximum value is `16384`.
  + [setNoDelay](https://bun.com/reference/node/tls/TLSSocket/setNoDelay)(

    noDelay?: boolean

    ): this;

    Enable/disable the use of Nagle's algorithm.

    When a TCP connection is created, it will have Nagle's algorithm enabled.

    Nagle's algorithm delays data before it is sent via the network. It attempts to optimize throughput at the expense of latency.

    Passing `true` for `noDelay` or not passing an argument will disable Nagle's algorithm for the socket. Passing `false` for `noDelay` will enable Nagle's algorithm.

    @returns

    The socket itself.
  + [setTimeout](https://bun.com/reference/node/tls/TLSSocket/setTimeout)(

    timeout: number,

    callback?: () => void

    ): this;

    Sets the socket to timeout after `timeout` milliseconds of inactivity on the socket. By default `net.Socket` do not have a timeout.

    When an idle timeout is triggered the socket will receive a `'timeout'` event but the connection will not be severed. The user must manually call `socket.end()` or `socket.destroy()` to end the connection.

    ```
    socket.setTimeout(3000);
    socket.on('timeout', () => {
      console.log('socket timeout');
      socket.end();
    });
    ```

    If `timeout` is 0, then the existing idle timeout is disabled.

    The optional `callback` parameter will be added as a one-time listener for the `'timeout'` event.

    @returns

    The socket itself.
  + [some](https://bun.com/reference/node/tls/TLSSocket/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/tls/TLSSocket/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/tls/TLSSocket/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/tls/TLSSocket/uncork)(): void;

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
  + [unpipe](https://bun.com/reference/node/tls/TLSSocket/unpipe)(

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
  + [unref](https://bun.com/reference/node/tls/TLSSocket/unref)(): this;

    Calling `unref()` on a socket will allow the program to exit if this is the only active socket in the event system. If the socket is already `unref`ed calling`unref()` again will have no effect.

    @returns

    The socket itself.
  + [unshift](https://bun.com/reference/node/tls/TLSSocket/unshift)(

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
  + [wrap](https://bun.com/reference/node/tls/TLSSocket/wrap)(

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
  + [write](https://bun.com/reference/node/tls/TLSSocket/write)(

    buffer: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    cb?: (err?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    Sends data on the socket. The second parameter specifies the encoding in the case of a string. It defaults to UTF8 encoding.

    Returns `true` if the entire data was flushed successfully to the kernel buffer. Returns `false` if all or part of the data was queued in user memory.`'drain'` will be emitted when the buffer is again free.

    The optional `callback` parameter will be executed when the data is finally written out, which may not be immediately.

    See `Writable` stream `write()` method for more information.

    [write](https://bun.com/reference/node/tls/TLSSocket/write)(

    str: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    encoding?: BufferEncoding,

    cb?: (err?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    Sends data on the socket. The second parameter specifies the encoding in the case of a string. It defaults to UTF8 encoding.

    Returns `true` if the entire data was flushed successfully to the kernel buffer. Returns `false` if all or part of the data was queued in user memory.`'drain'` will be emitted when the buffer is again free.

    The optional `callback` parameter will be executed when the data is finally written out, which may not be immediately.

    See `Writable` stream `write()` method for more information.

    @param encoding

    Only used when data is `string`.
  + static [addAbortListener](https://bun.com/reference/node/tls/TLSSocket/addAbortListener)(

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
  + static [from](https://bun.com/reference/node/tls/TLSSocket/from)(

    src: string | Object | [Stream](https://bun.com/reference/node/stream/default) | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | [Blob](https://bun.com/reference/node/buffer/Blob) | Promise<any> | Iterable<any, any, any> | AsyncIterable<any, any, any> | AsyncGeneratorFunction

    ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

    A utility method for creating duplex streams.

    - `Stream` converts writable stream into writable `Duplex` and readable stream to `Duplex`.
    - `Blob` converts into readable `Duplex`.
    - `string` converts into readable `Duplex`.
    - `ArrayBuffer` converts into readable `Duplex`.
    - `AsyncIterable` converts into a readable `Duplex`. Cannot yield `null`.
    - `AsyncGeneratorFunction` converts into a readable/writable transform `Duplex`. Must take a source `AsyncIterable` as first parameter. Cannot yield `null`.
    - `AsyncFunction` converts into a writable `Duplex`. Must return either `null` or `undefined`
    - `Object ({ writable, readable })` converts `readable` and `writable` into `Stream` and then combines them into `Duplex` where the `Duplex` will write to the `writable` and read from the `readable`.
    - `Promise` converts into readable `Duplex`. Value `null` is ignored.
  + static [fromWeb](https://bun.com/reference/node/tls/TLSSocket/fromWeb)(

    duplexStream: { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) },

    options?: Pick<[DuplexOptions](https://bun.com/reference/node/stream/default/DuplexOptions)<[Duplex](https://bun.com/reference/node/stream/default/Duplex)>, 'signal' | 'allowHalfOpen' | 'decodeStrings' | 'encoding' | 'highWaterMark' | 'objectMode'>

    ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

    A utility method for creating a `Duplex` from a web `ReadableStream` and `WritableStream`.
  + static [getEventListeners](https://bun.com/reference/node/tls/TLSSocket/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/tls/TLSSocket/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/tls/TLSSocket/on)(

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

    static [on](https://bun.com/reference/node/tls/TLSSocket/on)(

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
  + static [once](https://bun.com/reference/node/tls/TLSSocket/once)(

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

    static [once](https://bun.com/reference/node/tls/TLSSocket/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/tls/TLSSocket/setMaxListeners)(

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
  + static [toWeb](https://bun.com/reference/node/tls/TLSSocket/toWeb)(

    streamDuplex: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    ): { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) };

    A utility method for creating a web `ReadableStream` and `WritableStream` from a `Duplex`.
* const [CLIENT\_RENEG\_LIMIT](https://bun.com/reference/node/tls/CLIENT_RENEG_LIMIT): number
* const [CLIENT\_RENEG\_WINDOW](https://bun.com/reference/node/tls/CLIENT_RENEG_WINDOW): number
* const [DEFAULT\_CIPHERS](https://bun.com/reference/node/tls/DEFAULT_CIPHERS): string

  The default value of the `ciphers` option of `{@link createSecureContext()}`. It can be assigned any of the supported OpenSSL ciphers. Defaults to the content of `crypto.constants.defaultCoreCipherList`, unless changed using CLI options using `--tls-default-ciphers`.
* const [DEFAULT\_ECDH\_CURVE](https://bun.com/reference/node/tls/DEFAULT_ECDH_CURVE): string

  The default curve name to use for ECDH key agreement in a tls server. The default value is `'auto'`. See `{@link createSecureContext()}` for further information.
* const [DEFAULT\_MAX\_VERSION](https://bun.com/reference/node/tls/DEFAULT_MAX_VERSION): [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

  The default value of the `maxVersion` option of `{@link createSecureContext()}`. It can be assigned any of the supported TLS protocol versions, `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
* const [DEFAULT\_MIN\_VERSION](https://bun.com/reference/node/tls/DEFAULT_MIN_VERSION): [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

  The default value of the `minVersion` option of `{@link createSecureContext()}`. It can be assigned any of the supported TLS protocol versions, `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-min-v1.0` sets the default to `'TLSv1'`. Using `--tls-min-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the lowest minimum is used.
* const [rootCertificates](https://bun.com/reference/node/tls/rootCertificates): readonly string[]

  An immutable array of strings representing the root certificates (in PEM format) from the bundled Mozilla CA store as supplied by the current Node.js version.

  The bundled CA store, as supplied by Node.js, is a snapshot of Mozilla CA store that is fixed at release time. It is identical on all supported platforms.
* function [checkServerIdentity](https://bun.com/reference/node/tls/checkServerIdentity)(

  hostname: string,

  cert: [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate)

  ): undefined | [Error](https://bun.com/reference/globals/Error);

  Verifies the certificate `cert` is issued to `hostname`.

  Returns [Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) object, populating it with `reason`, `host`, and `cert` on failure. On success, returns [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Undefined_type).

  This function is intended to be used in combination with the`checkServerIdentity` option that can be passed to connect and as such operates on a `certificate object`. For other purposes, consider using `x509.checkHost()` instead.

  This function can be overwritten by providing an alternative function as the `options.checkServerIdentity` option that is passed to `tls.connect()`. The overwriting function can call `tls.checkServerIdentity()` of course, to augment the checks done with additional verification.

  This function is only called if the certificate passed all other checks, such as being issued by trusted CA (`options.ca`).

  Earlier versions of Node.js incorrectly accepted certificates for a given`hostname` if a matching `uniformResourceIdentifier` subject alternative name was present (see [CVE-2021-44531](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44531)). Applications that wish to accept`uniformResourceIdentifier` subject alternative names can use a custom `options.checkServerIdentity` function that implements the desired behavior.

  @param hostname

  The host name or IP address to verify the certificate against.

  @param cert

  A `certificate object` representing the peer's certificate.
* function [connect](https://bun.com/reference/node/tls/connect)(

  options: [ConnectionOptions](https://bun.com/reference/node/tls/ConnectionOptions),

  secureConnectListener?: () => void

  ): [TLSSocket](https://bun.com/reference/node/tls/TLSSocket);

  The `callback` function, if specified, will be added as a listener for the `'secureConnect'` event.

  `tls.connect()` returns a TLSSocket object.

  Unlike the `https` API, `tls.connect()` does not enable the SNI (Server Name Indication) extension by default, which may cause some servers to return an incorrect certificate or reject the connection altogether. To enable SNI, set the `servername` option in addition to `host`.

  The following illustrates a client for the echo server example from createServer:

  ```
  // Assumes an echo server that is listening on port 8000.
  import tls from 'node:tls';
  import fs from 'node:fs';

  const options = {
    // Necessary only if the server requires client certificate authentication.
    key: fs.readFileSync('client-key.pem'),
    cert: fs.readFileSync('client-cert.pem'),

    // Necessary only if the server uses a self-signed certificate.
    ca: [ fs.readFileSync('server-cert.pem') ],

    // Necessary only if the server's cert isn't for "localhost".
    checkServerIdentity: () => { return null; },
  };

  const socket = tls.connect(8000, options, () => {
    console.log('client connected',
                socket.authorized ? 'authorized' : 'unauthorized');
    process.stdin.pipe(socket);
    process.stdin.resume();
  });
  socket.setEncoding('utf8');
  socket.on('data', (data) => {
    console.log(data);
  });
  socket.on('end', () => {
    console.log('server ends connection');
  });
  ```

  function [connect](https://bun.com/reference/node/tls/connect)(

  port: number,

  host?: string,

  options?: [ConnectionOptions](https://bun.com/reference/node/tls/ConnectionOptions),

  secureConnectListener?: () => void

  ): [TLSSocket](https://bun.com/reference/node/tls/TLSSocket);

  The `callback` function, if specified, will be added as a listener for the `'secureConnect'` event.

  `tls.connect()` returns a TLSSocket object.

  Unlike the `https` API, `tls.connect()` does not enable the SNI (Server Name Indication) extension by default, which may cause some servers to return an incorrect certificate or reject the connection altogether. To enable SNI, set the `servername` option in addition to `host`.

  The following illustrates a client for the echo server example from createServer:

  ```
  // Assumes an echo server that is listening on port 8000.
  import tls from 'node:tls';
  import fs from 'node:fs';

  const options = {
    // Necessary only if the server requires client certificate authentication.
    key: fs.readFileSync('client-key.pem'),
    cert: fs.readFileSync('client-cert.pem'),

    // Necessary only if the server uses a self-signed certificate.
    ca: [ fs.readFileSync('server-cert.pem') ],

    // Necessary only if the server's cert isn't for "localhost".
    checkServerIdentity: () => { return null; },
  };

  const socket = tls.connect(8000, options, () => {
    console.log('client connected',
                socket.authorized ? 'authorized' : 'unauthorized');
    process.stdin.pipe(socket);
    process.stdin.resume();
  });
  socket.setEncoding('utf8');
  socket.on('data', (data) => {
    console.log(data);
  });
  socket.on('end', () => {
    console.log('server ends connection');
  });
  ```

  function [connect](https://bun.com/reference/node/tls/connect)(

  port: number,

  options?: [ConnectionOptions](https://bun.com/reference/node/tls/ConnectionOptions),

  secureConnectListener?: () => void

  ): [TLSSocket](https://bun.com/reference/node/tls/TLSSocket);

  The `callback` function, if specified, will be added as a listener for the `'secureConnect'` event.

  `tls.connect()` returns a TLSSocket object.

  Unlike the `https` API, `tls.connect()` does not enable the SNI (Server Name Indication) extension by default, which may cause some servers to return an incorrect certificate or reject the connection altogether. To enable SNI, set the `servername` option in addition to `host`.

  The following illustrates a client for the echo server example from createServer:

  ```
  // Assumes an echo server that is listening on port 8000.
  import tls from 'node:tls';
  import fs from 'node:fs';

  const options = {
    // Necessary only if the server requires client certificate authentication.
    key: fs.readFileSync('client-key.pem'),
    cert: fs.readFileSync('client-cert.pem'),

    // Necessary only if the server uses a self-signed certificate.
    ca: [ fs.readFileSync('server-cert.pem') ],

    // Necessary only if the server's cert isn't for "localhost".
    checkServerIdentity: () => { return null; },
  };

  const socket = tls.connect(8000, options, () => {
    console.log('client connected',
                socket.authorized ? 'authorized' : 'unauthorized');
    process.stdin.pipe(socket);
    process.stdin.resume();
  });
  socket.setEncoding('utf8');
  socket.on('data', (data) => {
    console.log(data);
  });
  socket.on('end', () => {
    console.log('server ends connection');
  });
  ```

  function [connect](https://bun.com/reference/node/tls/connect)(

  options: [BunConnectionOptions](https://bun.com/reference/node/tls/BunConnectionOptions),

  secureConnectListener?: () => void

  ): [TLSSocket](https://bun.com/reference/node/tls/TLSSocket);

  The `callback` function, if specified, will be added as a listener for the `'secureConnect'` event.

  `tls.connect()` returns a TLSSocket object.

  Unlike the `https` API, `tls.connect()` does not enable the SNI (Server Name Indication) extension by default, which may cause some servers to return an incorrect certificate or reject the connection altogether. To enable SNI, set the `servername` option in addition to `host`.

  The following illustrates a client for the echo server example from createServer:

  ```
  // Assumes an echo server that is listening on port 8000.
  import tls from 'node:tls';
  import fs from 'node:fs';

  const options = {
    // Necessary only if the server requires client certificate authentication.
    key: fs.readFileSync('client-key.pem'),
    cert: fs.readFileSync('client-cert.pem'),

    // Necessary only if the server uses a self-signed certificate.
    ca: [ fs.readFileSync('server-cert.pem') ],

    // Necessary only if the server's cert isn't for "localhost".
    checkServerIdentity: () => { return null; },
  };

  const socket = tls.connect(8000, options, () => {
    console.log('client connected',
                socket.authorized ? 'authorized' : 'unauthorized');
    process.stdin.pipe(socket);
    process.stdin.resume();
  });
  socket.setEncoding('utf8');
  socket.on('data', (data) => {
    console.log(data);
  });
  socket.on('end', () => {
    console.log('server ends connection');
  });
  ```
* function [createSecureContext](https://bun.com/reference/node/tls/createSecureContext)(

  options?: [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions)

  ): [SecureContext](https://bun.com/reference/node/tls/SecureContext);

  `{@link createServer}` sets the default value of the `honorCipherOrder` option to `true`, other APIs that create secure contexts leave it unset.

  `{@link createServer}` uses a 128 bit truncated SHA1 hash value generated from `process.argv` as the default value of the `sessionIdContext` option, other APIs that create secure contexts have no default value.

  The `tls.createSecureContext()` method creates a `SecureContext` object. It is usable as an argument to several `tls` APIs, such as `server.addContext()`, but has no public methods. The Server constructor and the createServer method do not support the `secureContext` option.

  A key is *required* for ciphers that use certificates. Either `key` or `pfx` can be used to provide it.

  If the `ca` option is not given, then Node.js will default to using [Mozilla's publicly trusted list of CAs](https://hg.mozilla.org/mozilla-central/raw-file/tip/security/nss/lib/ckfw/builtins/certdata.txt).

  Custom DHE parameters are discouraged in favor of the new `dhparam: 'auto'` option. When set to `'auto'`, well-known DHE parameters of sufficient strength will be selected automatically. Otherwise, if necessary, `openssl dhparam` can be used to create custom parameters. The key length must be greater than or equal to 1024 bits or else an error will be thrown. Although 1024 bits is permissible, use 2048 bits or larger for stronger security.
* function [createServer](https://bun.com/reference/node/tls/createServer)(

  secureConnectionListener?: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

  ): [Server](https://bun.com/reference/node/tls/Server);

  Creates a new Server. The `secureConnectionListener`, if provided, is automatically set as a listener for the `'secureConnection'` event.

  The `ticketKeys` options is automatically shared between `node:cluster` module workers.

  The following illustrates a simple echo server:

  ```
  import tls from 'node:tls';
  import fs from 'node:fs';

  const options = {
    key: fs.readFileSync('server-key.pem'),
    cert: fs.readFileSync('server-cert.pem'),

    // This is necessary only if using client certificate authentication.
    requestCert: true,

    // This is necessary only if the client uses a self-signed certificate.
    ca: [ fs.readFileSync('client-cert.pem') ],
  };

  const server = tls.createServer(options, (socket) => {
    console.log('server connected',
                socket.authorized ? 'authorized' : 'unauthorized');
    socket.write('welcome!\n');
    socket.setEncoding('utf8');
    socket.pipe(socket);
  });
  server.listen(8000, () => {
    console.log('server bound');
  });
  ```

  The server can be tested by connecting to it using the example client from connect.

  function [createServer](https://bun.com/reference/node/tls/createServer)(

  options: [TlsOptions](https://bun.com/reference/node/tls/TlsOptions),

  secureConnectionListener?: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket)) => void

  ): [Server](https://bun.com/reference/node/tls/Server);

  Creates a new Server. The `secureConnectionListener`, if provided, is automatically set as a listener for the `'secureConnection'` event.

  The `ticketKeys` options is automatically shared between `node:cluster` module workers.

  The following illustrates a simple echo server:

  ```
  import tls from 'node:tls';
  import fs from 'node:fs';

  const options = {
    key: fs.readFileSync('server-key.pem'),
    cert: fs.readFileSync('server-cert.pem'),

    // This is necessary only if using client certificate authentication.
    requestCert: true,

    // This is necessary only if the client uses a self-signed certificate.
    ca: [ fs.readFileSync('client-cert.pem') ],
  };

  const server = tls.createServer(options, (socket) => {
    console.log('server connected',
                socket.authorized ? 'authorized' : 'unauthorized');
    socket.write('welcome!\n');
    socket.setEncoding('utf8');
    socket.pipe(socket);
  });
  server.listen(8000, () => {
    console.log('server bound');
  });
  ```

  The server can be tested by connecting to it using the example client from connect.
* function [getCACertificates](https://bun.com/reference/node/tls/getCACertificates)(

  type?: 'default' | 'system' | 'bundled' | 'extra'

  ): string[];

  Returns an array containing the CA certificates from various sources, depending on `type`:

  + `"default"`: return the CA certificates that will be used by the Node.js TLS clients by default.
    - When `--use-bundled-ca` is enabled (default), or `--use-openssl-ca` is not enabled, this would include CA certificates from the bundled Mozilla CA store.
    - When `--use-system-ca` is enabled, this would also include certificates from the system's trusted store.
    - When `NODE_EXTRA_CA_CERTS` is used, this would also include certificates loaded from the specified file.
  + `"system"`: return the CA certificates that are loaded from the system's trusted store, according to rules set by `--use-system-ca`. This can be used to get the certificates from the system when `--use-system-ca` is not enabled.
  + `"bundled"`: return the CA certificates from the bundled Mozilla CA store. This would be the same as `tls.rootCertificates`.
  + `"extra"`: return the CA certificates loaded from `NODE_EXTRA_CA_CERTS`. It's an empty array if `NODE_EXTRA_CA_CERTS` is not set.

  @param type

  The type of CA certificates that will be returned. Valid values are `"default"`, `"system"`, `"bundled"` and `"extra"`. **Default:** `"default"`.

  @returns

  An array of PEM-encoded certificates. The array may contain duplicates if the same certificate is repeatedly stored in multiple sources.
* function [getCiphers](https://bun.com/reference/node/tls/getCiphers)(): string[];

  Returns an array with the names of the supported TLS ciphers. The names are lower-case for historical reasons, but must be uppercased to be used in the `ciphers` option of `{@link createSecureContext}`.

  Not all supported ciphers are enabled by default. See [Modifying the default TLS cipher suite](https://nodejs.org/docs/latest-v24.x/api/tls.html#modifying-the-default-tls-cipher-suite).

  Cipher names that start with `'tls_'` are for TLSv1.3, all the others are for TLSv1.2 and below.

  ```
  console.log(tls.getCiphers()); // ['aes128-gcm-sha256', 'aes128-sha', ...]
  ```
* function [setDefaultCACertificates](https://bun.com/reference/node/tls/setDefaultCACertificates)(

  certs: readonly string | ArrayBufferView<ArrayBufferLike>[]

  ): void;

  Sets the default CA certificates used by Node.js TLS clients. If the provided certificates are parsed successfully, they will become the default CA certificate list returned by getCACertificates and used by subsequent TLS connections that don't specify their own CA certificates. The certificates will be deduplicated before being set as the default.

  This function only affects the current Node.js thread. Previous sessions cached by the HTTPS agent won't be affected by this change, so this method should be called before any unwanted cachable TLS connections are made.

  To use system CA certificates as the default:

  ```
  import tls from 'node:tls';
  tls.setDefaultCACertificates(tls.getCACertificates('system'));
  ```

  This function completely replaces the default CA certificate list. To add additional certificates to the existing defaults, get the current certificates and append to them:

  ```
  import tls from 'node:tls';
  const currentCerts = tls.getCACertificates('default');
  const additionalCerts = ['-----BEGIN CERTIFICATE-----\n...'];
  tls.setDefaultCACertificates([...currentCerts, ...additionalCerts]);
  ```

  @param certs

  An array of CA certificates in PEM format.

## Type definitions

* ### interface [BunConnectionOptions](https://bun.com/reference/node/tls/BunConnectionOptions)

  + [allowPartialTrustChain](https://bun.com/reference/node/tls/BunConnectionOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/tls/BunConnectionOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [ca](https://bun.com/reference/node/tls/BunConnectionOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | TypedArray<ArrayBufferLike> | [BunFile](https://bun.com/reference/bun/BunFile) | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [BunFile](https://bun.com/reference/bun/BunFile)[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/tls/BunConnectionOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | TypedArray<ArrayBufferLike> | [BunFile](https://bun.com/reference/bun/BunFile) | unknown[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [checkServerIdentity](https://bun.com/reference/node/tls/BunConnectionOptions/checkServerIdentity)?: (hostname: string, cert: [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate)) => undefined | [Error](https://bun.com/reference/globals/Error)
  + [ciphers](https://bun.com/reference/node/tls/BunConnectionOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/tls/BunConnectionOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/tls/BunConnectionOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/tls/BunConnectionOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/tls/BunConnectionOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [honorCipherOrder](https://bun.com/reference/node/tls/BunConnectionOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [host](https://bun.com/reference/node/tls/BunConnectionOptions/host)?: string
  + [key](https://bun.com/reference/node/tls/BunConnectionOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | TypedArray<ArrayBufferLike> | [BunFile](https://bun.com/reference/bun/BunFile) | unknown[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [lookup](https://bun.com/reference/node/tls/BunConnectionOptions/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxVersion](https://bun.com/reference/node/tls/BunConnectionOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minDHSize](https://bun.com/reference/node/tls/BunConnectionOptions/minDHSize)?: number
  + [minVersion](https://bun.com/reference/node/tls/BunConnectionOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [passphrase](https://bun.com/reference/node/tls/BunConnectionOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [path](https://bun.com/reference/node/tls/BunConnectionOptions/path)?: string
  + [pfx](https://bun.com/reference/node/tls/BunConnectionOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [port](https://bun.com/reference/node/tls/BunConnectionOptions/port)?: number
  + [pskCallback](https://bun.com/reference/node/tls/BunConnectionOptions/pskCallback)?: (hint: null | string) => null | [PSKCallbackNegotation](https://bun.com/reference/node/tls/PSKCallbackNegotation)

    When negotiating TLS-PSK (pre-shared keys), this function is called with optional identity `hint` provided by the server or `null` in case of TLS 1.3 where `hint` was removed. It will be necessary to provide a custom `tls.checkServerIdentity()` for the connection as the default one will try to check hostname/IP of the server against the certificate but that's not applicable for PSK because there won't be a certificate present. More information can be found in the RFC 4279.
  + [rejectUnauthorized](https://bun.com/reference/node/tls/BunConnectionOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [requestCert](https://bun.com/reference/node/tls/BunConnectionOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [secureContext](https://bun.com/reference/node/tls/BunConnectionOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/tls/BunConnectionOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [servername](https://bun.com/reference/node/tls/BunConnectionOptions/servername)?: string
  + [session](https://bun.com/reference/node/tls/BunConnectionOptions/session)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>
  + [sessionIdContext](https://bun.com/reference/node/tls/BunConnectionOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/tls/BunConnectionOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [sigalgs](https://bun.com/reference/node/tls/BunConnectionOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/tls/BunConnectionOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [socket](https://bun.com/reference/node/tls/BunConnectionOptions/socket)?: [Duplex](https://bun.com/reference/node/stream/default/Duplex)
  + [ticketKeys](https://bun.com/reference/node/tls/BunConnectionOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data. See Session Resumption for more information.
  + [timeout](https://bun.com/reference/node/tls/BunConnectionOptions/timeout)?: number
* ### interface [Certificate](https://bun.com/reference/node/tls/Certificate)

  + [C](https://bun.com/reference/node/tls/Certificate/C): string

    Country code.
  + [CN](https://bun.com/reference/node/tls/Certificate/CN): string

    Common name.
  + [L](https://bun.com/reference/node/tls/Certificate/L): string

    Locality.
  + [O](https://bun.com/reference/node/tls/Certificate/O): string

    Organization.
  + [OU](https://bun.com/reference/node/tls/Certificate/OU): string

    Organizational unit.
  + [ST](https://bun.com/reference/node/tls/Certificate/ST): string

    Street.
* ### interface [CommonConnectionOptions](https://bun.com/reference/node/tls/CommonConnectionOptions)

  + [enableTrace](https://bun.com/reference/node/tls/CommonConnectionOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [rejectUnauthorized](https://bun.com/reference/node/tls/CommonConnectionOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [requestCert](https://bun.com/reference/node/tls/CommonConnectionOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [secureContext](https://bun.com/reference/node/tls/CommonConnectionOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [SNICallback](https://bun.com/reference/node/tls/CommonConnectionOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
* ### interface [ConnectionOptions](https://bun.com/reference/node/tls/ConnectionOptions)

  + [allowPartialTrustChain](https://bun.com/reference/node/tls/ConnectionOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/tls/ConnectionOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [ca](https://bun.com/reference/node/tls/ConnectionOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/tls/ConnectionOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [checkServerIdentity](https://bun.com/reference/node/tls/ConnectionOptions/checkServerIdentity)?: (hostname: string, cert: [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate)) => undefined | [Error](https://bun.com/reference/globals/Error)
  + [ciphers](https://bun.com/reference/node/tls/ConnectionOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/tls/ConnectionOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/tls/ConnectionOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/tls/ConnectionOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/tls/ConnectionOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [honorCipherOrder](https://bun.com/reference/node/tls/ConnectionOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [host](https://bun.com/reference/node/tls/ConnectionOptions/host)?: string
  + [key](https://bun.com/reference/node/tls/ConnectionOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [lookup](https://bun.com/reference/node/tls/ConnectionOptions/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [maxVersion](https://bun.com/reference/node/tls/ConnectionOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minDHSize](https://bun.com/reference/node/tls/ConnectionOptions/minDHSize)?: number
  + [minVersion](https://bun.com/reference/node/tls/ConnectionOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [passphrase](https://bun.com/reference/node/tls/ConnectionOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [path](https://bun.com/reference/node/tls/ConnectionOptions/path)?: string
  + [pfx](https://bun.com/reference/node/tls/ConnectionOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [port](https://bun.com/reference/node/tls/ConnectionOptions/port)?: number
  + [pskCallback](https://bun.com/reference/node/tls/ConnectionOptions/pskCallback)?: (hint: null | string) => null | [PSKCallbackNegotation](https://bun.com/reference/node/tls/PSKCallbackNegotation)

    When negotiating TLS-PSK (pre-shared keys), this function is called with optional identity `hint` provided by the server or `null` in case of TLS 1.3 where `hint` was removed. It will be necessary to provide a custom `tls.checkServerIdentity()` for the connection as the default one will try to check hostname/IP of the server against the certificate but that's not applicable for PSK because there won't be a certificate present. More information can be found in the RFC 4279.
  + [rejectUnauthorized](https://bun.com/reference/node/tls/ConnectionOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [requestCert](https://bun.com/reference/node/tls/ConnectionOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [secureContext](https://bun.com/reference/node/tls/ConnectionOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/tls/ConnectionOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [servername](https://bun.com/reference/node/tls/ConnectionOptions/servername)?: string
  + [session](https://bun.com/reference/node/tls/ConnectionOptions/session)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>
  + [sessionIdContext](https://bun.com/reference/node/tls/ConnectionOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/tls/ConnectionOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [sigalgs](https://bun.com/reference/node/tls/ConnectionOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/tls/ConnectionOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [socket](https://bun.com/reference/node/tls/ConnectionOptions/socket)?: [Duplex](https://bun.com/reference/node/stream/default/Duplex)
  + [ticketKeys](https://bun.com/reference/node/tls/ConnectionOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data. See Session Resumption for more information.
  + [timeout](https://bun.com/reference/node/tls/ConnectionOptions/timeout)?: number
* ### interface [DetailedPeerCertificate](https://bun.com/reference/node/tls/DetailedPeerCertificate)

  + [asn1Curve](https://bun.com/reference/node/tls/DetailedPeerCertificate/asn1Curve)?: string

    The ASN.1 name of the OID of the elliptic curve. Well-known curves are identified by an OID. While it is unusual, it is possible that the curve is identified by its mathematical properties, in which case it will not have an OID.
  + [bits](https://bun.com/reference/node/tls/DetailedPeerCertificate/bits)?: number

    For RSA keys: The RSA bit size.

    For EC keys: The key size in bits.
  + [ca](https://bun.com/reference/node/tls/DetailedPeerCertificate/ca): boolean

    `true` if a Certificate Authority (CA), `false` otherwise.
  + [exponent](https://bun.com/reference/node/tls/DetailedPeerCertificate/exponent)?: string

    The RSA exponent, as a string in hexadecimal number notation.
  + [ext\_key\_usage](https://bun.com/reference/node/tls/DetailedPeerCertificate/ext_key_usage)?: string[]

    The extended key usage, a set of OIDs.
  + [fingerprint](https://bun.com/reference/node/tls/DetailedPeerCertificate/fingerprint): string

    The SHA-1 digest of the DER encoded certificate. It is returned as a `:` separated hexadecimal string.
  + [fingerprint256](https://bun.com/reference/node/tls/DetailedPeerCertificate/fingerprint256): string

    The SHA-256 digest of the DER encoded certificate. It is returned as a `:` separated hexadecimal string.
  + [fingerprint512](https://bun.com/reference/node/tls/DetailedPeerCertificate/fingerprint512): string

    The SHA-512 digest of the DER encoded certificate. It is returned as a `:` separated hexadecimal string.
  + [infoAccess](https://bun.com/reference/node/tls/DetailedPeerCertificate/infoAccess)?: Dict<string[]>

    An array describing the AuthorityInfoAccess, used with OCSP.
  + [issuer](https://bun.com/reference/node/tls/DetailedPeerCertificate/issuer): [Certificate](https://bun.com/reference/node/tls/Certificate)

    The certificate issuer, described in the same terms as the `subject`.
  + [issuerCertificate](https://bun.com/reference/node/tls/DetailedPeerCertificate/issuerCertificate): [DetailedPeerCertificate](https://bun.com/reference/node/tls/DetailedPeerCertificate)

    The issuer certificate object. For self-signed certificates, this may be a circular reference.
  + [modulus](https://bun.com/reference/node/tls/DetailedPeerCertificate/modulus)?: string

    The RSA modulus, as a hexadecimal string.
  + [nistCurve](https://bun.com/reference/node/tls/DetailedPeerCertificate/nistCurve)?: string

    The NIST name for the elliptic curve, if it has one (not all well-known curves have been assigned names by NIST).
  + [pubkey](https://bun.com/reference/node/tls/DetailedPeerCertificate/pubkey)?: NonSharedBuffer

    The public key.
  + [raw](https://bun.com/reference/node/tls/DetailedPeerCertificate/raw): NonSharedBuffer

    The DER encoded X.509 certificate data.
  + [serialNumber](https://bun.com/reference/node/tls/DetailedPeerCertificate/serialNumber): string

    The certificate serial number, as a hex string.
  + [subject](https://bun.com/reference/node/tls/DetailedPeerCertificate/subject): [Certificate](https://bun.com/reference/node/tls/Certificate)

    The certificate subject.
  + [subjectaltname](https://bun.com/reference/node/tls/DetailedPeerCertificate/subjectaltname)?: string

    A string containing concatenated names for the subject, an alternative to the `subject` names.
  + [valid\_from](https://bun.com/reference/node/tls/DetailedPeerCertificate/valid_from): string

    The date-time the certificate is valid from.
  + [valid\_to](https://bun.com/reference/node/tls/DetailedPeerCertificate/valid_to): string

    The date-time the certificate is valid to.
* ### interface [EphemeralKeyInfo](https://bun.com/reference/node/tls/EphemeralKeyInfo)

  + [name](https://bun.com/reference/node/tls/EphemeralKeyInfo/name)?: string

    The name property is available only when type is 'ECDH'.
  + [size](https://bun.com/reference/node/tls/EphemeralKeyInfo/size): number

    The size of parameter of an ephemeral key exchange.
  + [type](https://bun.com/reference/node/tls/EphemeralKeyInfo/type): string

    The supported types are 'DH' and 'ECDH'.
* ### interface [KeyObject](https://bun.com/reference/node/tls/KeyObject)

  + [passphrase](https://bun.com/reference/node/tls/KeyObject/passphrase)?: string

    Optional passphrase.
  + [pem](https://bun.com/reference/node/tls/KeyObject/pem): string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    Private keys in PEM format.
* ### interface [PeerCertificate](https://bun.com/reference/node/tls/PeerCertificate)

  + [asn1Curve](https://bun.com/reference/node/tls/PeerCertificate/asn1Curve)?: string

    The ASN.1 name of the OID of the elliptic curve. Well-known curves are identified by an OID. While it is unusual, it is possible that the curve is identified by its mathematical properties, in which case it will not have an OID.
  + [bits](https://bun.com/reference/node/tls/PeerCertificate/bits)?: number

    For RSA keys: The RSA bit size.

    For EC keys: The key size in bits.
  + [ca](https://bun.com/reference/node/tls/PeerCertificate/ca): boolean

    `true` if a Certificate Authority (CA), `false` otherwise.
  + [exponent](https://bun.com/reference/node/tls/PeerCertificate/exponent)?: string

    The RSA exponent, as a string in hexadecimal number notation.
  + [ext\_key\_usage](https://bun.com/reference/node/tls/PeerCertificate/ext_key_usage)?: string[]

    The extended key usage, a set of OIDs.
  + [fingerprint](https://bun.com/reference/node/tls/PeerCertificate/fingerprint): string

    The SHA-1 digest of the DER encoded certificate. It is returned as a `:` separated hexadecimal string.
  + [fingerprint256](https://bun.com/reference/node/tls/PeerCertificate/fingerprint256): string

    The SHA-256 digest of the DER encoded certificate. It is returned as a `:` separated hexadecimal string.
  + [fingerprint512](https://bun.com/reference/node/tls/PeerCertificate/fingerprint512): string

    The SHA-512 digest of the DER encoded certificate. It is returned as a `:` separated hexadecimal string.
  + [infoAccess](https://bun.com/reference/node/tls/PeerCertificate/infoAccess)?: Dict<string[]>

    An array describing the AuthorityInfoAccess, used with OCSP.
  + [issuer](https://bun.com/reference/node/tls/PeerCertificate/issuer): [Certificate](https://bun.com/reference/node/tls/Certificate)

    The certificate issuer, described in the same terms as the `subject`.
  + [modulus](https://bun.com/reference/node/tls/PeerCertificate/modulus)?: string

    The RSA modulus, as a hexadecimal string.
  + [nistCurve](https://bun.com/reference/node/tls/PeerCertificate/nistCurve)?: string

    The NIST name for the elliptic curve, if it has one (not all well-known curves have been assigned names by NIST).
  + [pubkey](https://bun.com/reference/node/tls/PeerCertificate/pubkey)?: NonSharedBuffer

    The public key.
  + [raw](https://bun.com/reference/node/tls/PeerCertificate/raw): NonSharedBuffer

    The DER encoded X.509 certificate data.
  + [serialNumber](https://bun.com/reference/node/tls/PeerCertificate/serialNumber): string

    The certificate serial number, as a hex string.
  + [subject](https://bun.com/reference/node/tls/PeerCertificate/subject): [Certificate](https://bun.com/reference/node/tls/Certificate)

    The certificate subject.
  + [subjectaltname](https://bun.com/reference/node/tls/PeerCertificate/subjectaltname)?: string

    A string containing concatenated names for the subject, an alternative to the `subject` names.
  + [valid\_from](https://bun.com/reference/node/tls/PeerCertificate/valid_from): string

    The date-time the certificate is valid from.
  + [valid\_to](https://bun.com/reference/node/tls/PeerCertificate/valid_to): string

    The date-time the certificate is valid to.
* ### interface [PSKCallbackNegotation](https://bun.com/reference/node/tls/PSKCallbackNegotation)

  + [identity](https://bun.com/reference/node/tls/PSKCallbackNegotation/identity): string
  + [psk](https://bun.com/reference/node/tls/PSKCallbackNegotation/psk): ArrayBufferView
* ### interface [PxfObject](https://bun.com/reference/node/tls/PxfObject)

  + [buf](https://bun.com/reference/node/tls/PxfObject/buf): string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    PFX or PKCS12 encoded private key and certificate chain.
  + [passphrase](https://bun.com/reference/node/tls/PxfObject/passphrase)?: string

    Optional passphrase.
* ### interface [SecureContext](https://bun.com/reference/node/tls/SecureContext)

  + [context](https://bun.com/reference/node/tls/SecureContext/context): any
* ### interface [SecureContextOptions](https://bun.com/reference/node/tls/SecureContextOptions)

  + [allowPartialTrustChain](https://bun.com/reference/node/tls/SecureContextOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/tls/SecureContextOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [ca](https://bun.com/reference/node/tls/SecureContextOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/tls/SecureContextOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [ciphers](https://bun.com/reference/node/tls/SecureContextOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/tls/SecureContextOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/tls/SecureContextOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/tls/SecureContextOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [honorCipherOrder](https://bun.com/reference/node/tls/SecureContextOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [key](https://bun.com/reference/node/tls/SecureContextOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [maxVersion](https://bun.com/reference/node/tls/SecureContextOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minVersion](https://bun.com/reference/node/tls/SecureContextOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [passphrase](https://bun.com/reference/node/tls/SecureContextOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [pfx](https://bun.com/reference/node/tls/SecureContextOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [secureOptions](https://bun.com/reference/node/tls/SecureContextOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [sessionIdContext](https://bun.com/reference/node/tls/SecureContextOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/tls/SecureContextOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [sigalgs](https://bun.com/reference/node/tls/SecureContextOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [ticketKeys](https://bun.com/reference/node/tls/SecureContextOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data. See Session Resumption for more information.
* ### interface [TlsOptions](https://bun.com/reference/node/tls/TlsOptions)

  + [allowHalfOpen](https://bun.com/reference/node/tls/TlsOptions/allowHalfOpen)?: boolean

    Indicates whether half-opened TCP connections are allowed.
  + [allowPartialTrustChain](https://bun.com/reference/node/tls/TlsOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/tls/TlsOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [blockList](https://bun.com/reference/node/tls/TlsOptions/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)

    `blockList` can be used for disabling inbound access to specific IP addresses, IP ranges, or IP subnets. This does not work if the server is behind a reverse proxy, NAT, etc. because the address checked against the block list is the address of the proxy, or the one specified by the NAT.
  + [ca](https://bun.com/reference/node/tls/TlsOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/tls/TlsOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [ciphers](https://bun.com/reference/node/tls/TlsOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/tls/TlsOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/tls/TlsOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/tls/TlsOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/tls/TlsOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [handshakeTimeout](https://bun.com/reference/node/tls/TlsOptions/handshakeTimeout)?: number

    Abort the connection if the SSL/TLS handshake does not finish in the specified number of milliseconds. A 'tlsClientError' is emitted on the tls.Server object whenever a handshake times out. Default: 120000 (120 seconds).
  + [highWaterMark](https://bun.com/reference/node/tls/TlsOptions/highWaterMark)?: number

    Optionally overrides all `net.Socket`s' `readableHighWaterMark` and `writableHighWaterMark`.
  + [honorCipherOrder](https://bun.com/reference/node/tls/TlsOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [keepAlive](https://bun.com/reference/node/tls/TlsOptions/keepAlive)?: boolean

    If set to `true`, it enables keep-alive functionality on the socket immediately after a new incoming connection is received, similarly on what is done in `socket.setKeepAlive([enable][, initialDelay])`.
  + [keepAliveInitialDelay](https://bun.com/reference/node/tls/TlsOptions/keepAliveInitialDelay)?: number

    If set to a positive number, it sets the initial delay before the first keepalive probe is sent on an idle socket.
  + [key](https://bun.com/reference/node/tls/TlsOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [maxVersion](https://bun.com/reference/node/tls/TlsOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minVersion](https://bun.com/reference/node/tls/TlsOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [noDelay](https://bun.com/reference/node/tls/TlsOptions/noDelay)?: boolean

    If set to `true`, it disables the use of Nagle's algorithm immediately after a new incoming connection is received.
  + [passphrase](https://bun.com/reference/node/tls/TlsOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [pauseOnConnect](https://bun.com/reference/node/tls/TlsOptions/pauseOnConnect)?: boolean

    Indicates whether the socket should be paused on incoming connections.
  + [pfx](https://bun.com/reference/node/tls/TlsOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [pskCallback](https://bun.com/reference/node/tls/TlsOptions/pskCallback)?: (socket: [TLSSocket](https://bun.com/reference/node/tls/TLSSocket), identity: string) => null | ArrayBufferView<ArrayBufferLike>
  + [pskIdentityHint](https://bun.com/reference/node/tls/TlsOptions/pskIdentityHint)?: string

    hint to send to a client to help with selecting the identity during TLS-PSK negotiation. Will be ignored in TLS 1.3. Upon failing to set pskIdentityHint `tlsClientError` will be emitted with `ERR_TLS_PSK_SET_IDENTIY_HINT_FAILED` code.
  + [rejectUnauthorized](https://bun.com/reference/node/tls/TlsOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [requestCert](https://bun.com/reference/node/tls/TlsOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [secureContext](https://bun.com/reference/node/tls/TlsOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/tls/TlsOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [sessionIdContext](https://bun.com/reference/node/tls/TlsOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/tls/TlsOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [sigalgs](https://bun.com/reference/node/tls/TlsOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/tls/TlsOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [ticketKeys](https://bun.com/reference/node/tls/TlsOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data.
* ### interface [TLSSocketOptions](https://bun.com/reference/node/tls/TLSSocketOptions)

  + [allowPartialTrustChain](https://bun.com/reference/node/tls/TLSSocketOptions/allowPartialTrustChain)?: boolean

    Treat intermediate (non-self-signed) certificates in the trust CA certificate list as trusted.
  + [ALPNCallback](https://bun.com/reference/node/tls/TLSSocketOptions/ALPNCallback)?: (arg: { protocols: string[]; servername: string }) => undefined | string

    If set, this will be called when a client opens a connection using the ALPN extension. One argument will be passed to the callback: an object containing `servername` and `protocols` fields, respectively containing the server name from the SNI extension (if any) and an array of ALPN protocol name strings. The callback must return either one of the strings listed in `protocols`, which will be returned to the client as the selected ALPN protocol, or `undefined`, to reject the connection with a fatal alert. If a string is returned that does not match one of the client's ALPN protocols, an error will be thrown. This option cannot be used with the `ALPNProtocols` option, and setting both options will throw an error.
  + [ca](https://bun.com/reference/node/tls/TLSSocketOptions/ca)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Optionally override the trusted CA certificates. Default is to trust the well-known CAs curated by Mozilla. Mozilla's CAs are completely replaced when CAs are explicitly specified using this option.
  + [cert](https://bun.com/reference/node/tls/TLSSocketOptions/cert)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    Cert chains in PEM format. One cert chain should be provided per private key. Each cert chain should consist of the PEM formatted certificate for a provided private key, followed by the PEM formatted intermediate certificates (if any), in order, and not including the root CA (the root CA must be pre-known to the peer, see ca). When providing multiple cert chains, they do not have to be in the same order as their private keys in key. If the intermediate certificates are not provided, the peer will not be able to validate the certificate, and the handshake will fail.
  + [ciphers](https://bun.com/reference/node/tls/TLSSocketOptions/ciphers)?: string

    Cipher suite specification, replacing the default. For more information, see modifying the default cipher suite. Permitted ciphers can be obtained via tls.getCiphers(). Cipher names must be uppercased in order for OpenSSL to accept them.
  + [crl](https://bun.com/reference/node/tls/TLSSocketOptions/crl)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>[]

    PEM formatted CRLs (Certificate Revocation Lists).
  + [dhparam](https://bun.com/reference/node/tls/TLSSocketOptions/dhparam)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    `'auto'` or custom Diffie-Hellman parameters, required for non-ECDHE perfect forward secrecy. If omitted or invalid, the parameters are silently discarded and DHE ciphers will not be available. ECDHE-based perfect forward secrecy will still be available.
  + [ecdhCurve](https://bun.com/reference/node/tls/TLSSocketOptions/ecdhCurve)?: string

    A string describing a named curve or a colon separated list of curve NIDs or names, for example P-521:P-384:P-256, to use for ECDH key agreement. Set to auto to select the curve automatically. Use crypto.getCurves() to obtain a list of available curve names. On recent releases, openssl ecparam -list\_curves will also display the name and description of each available elliptic curve. Default: tls.DEFAULT\_ECDH\_CURVE.
  + [enableTrace](https://bun.com/reference/node/tls/TLSSocketOptions/enableTrace)?: boolean

    When enabled, TLS packet trace information is written to `stderr`. This can be used to debug TLS connection problems.
  + [honorCipherOrder](https://bun.com/reference/node/tls/TLSSocketOptions/honorCipherOrder)?: boolean

    Attempt to use the server's cipher suite preferences instead of the client's. When true, causes SSL\_OP\_CIPHER\_SERVER\_PREFERENCE to be set in secureOptions
  + [isServer](https://bun.com/reference/node/tls/TLSSocketOptions/isServer)?: boolean

    If true the TLS socket will be instantiated in server-mode. Defaults to false.
  + [key](https://bun.com/reference/node/tls/TLSSocketOptions/key)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [KeyObject](https://bun.com/reference/node/tls/KeyObject)[]

    Private keys in PEM format. PEM allows the option of private keys being encrypted. Encrypted keys will be decrypted with options.passphrase. Multiple keys using different algorithms can be provided either as an array of unencrypted key strings or buffers, or an array of objects in the form {pem: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted keys will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [maxVersion](https://bun.com/reference/node/tls/TLSSocketOptions/maxVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the maximum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. **Default:** `'TLSv1.3'`, unless changed using CLI options. Using `--tls-max-v1.2` sets the default to `'TLSv1.2'`. Using `--tls-max-v1.3` sets the default to `'TLSv1.3'`. If multiple of the options are provided, the highest maximum is used.
  + [minVersion](https://bun.com/reference/node/tls/TLSSocketOptions/minVersion)?: [SecureVersion](https://bun.com/reference/node/tls/SecureVersion)

    Optionally set the minimum TLS version to allow. One of `'TLSv1.3'`, `'TLSv1.2'`, `'TLSv1.1'`, or `'TLSv1'`. Cannot be specified along with the `secureProtocol` option, use one or the other. It is not recommended to use less than TLSv1.2, but it may be required for interoperability. **Default:** `'TLSv1.2'`, unless changed using CLI options. Using `--tls-v1.0` sets the default to `'TLSv1'`. Using `--tls-v1.1` sets the default to `'TLSv1.1'`. Using `--tls-min-v1.3` sets the default to 'TLSv1.3'. If multiple of the options are provided, the lowest minimum is used.
  + [passphrase](https://bun.com/reference/node/tls/TLSSocketOptions/passphrase)?: string

    Shared passphrase used for a single private key and/or a PFX.
  + [pfx](https://bun.com/reference/node/tls/TLSSocketOptions/pfx)?: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike> | [PxfObject](https://bun.com/reference/node/tls/PxfObject)[]

    PFX or PKCS12 encoded private key and certificate chain. pfx is an alternative to providing key and cert individually. PFX is usually encrypted, if it is, passphrase will be used to decrypt it. Multiple PFX can be provided either as an array of unencrypted PFX buffers, or an array of objects in the form {buf: <string|buffer>[, passphrase: <string>]}. The object form can only occur in an array. object.passphrase is optional. Encrypted PFX will be decrypted with object.passphrase if provided, or options.passphrase if it is not.
  + [rejectUnauthorized](https://bun.com/reference/node/tls/TLSSocketOptions/rejectUnauthorized)?: boolean

    If true the server will reject any connection which is not authorized with the list of supplied CAs. This option only has an effect if requestCert is true.
  + [requestCert](https://bun.com/reference/node/tls/TLSSocketOptions/requestCert)?: boolean

    If true the server will request a certificate from clients that connect and attempt to verify that certificate. Defaults to false.
  + [requestOCSP](https://bun.com/reference/node/tls/TLSSocketOptions/requestOCSP)?: boolean

    If true, specifies that the OCSP status request extension will be added to the client hello and an 'OCSPResponse' event will be emitted on the socket before establishing a secure communication
  + [secureContext](https://bun.com/reference/node/tls/TLSSocketOptions/secureContext)?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)

    An optional TLS context object from tls.createSecureContext()
  + [secureOptions](https://bun.com/reference/node/tls/TLSSocketOptions/secureOptions)?: number

    Optionally affect the OpenSSL protocol behavior, which is not usually necessary. This should be used carefully if at all! Value is a numeric bitmask of the SSL\_OP\_\* options from OpenSSL Options
  + [server](https://bun.com/reference/node/tls/TLSSocketOptions/server)?: [Server](https://bun.com/reference/node/net/Server)

    An optional net.Server instance.
  + [session](https://bun.com/reference/node/tls/TLSSocketOptions/session)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    An optional Buffer instance containing a TLS session.
  + [sessionIdContext](https://bun.com/reference/node/tls/TLSSocketOptions/sessionIdContext)?: string

    Opaque identifier used by servers to ensure session state is not shared between applications. Unused by clients.
  + [sessionTimeout](https://bun.com/reference/node/tls/TLSSocketOptions/sessionTimeout)?: number

    The number of seconds after which a TLS session created by the server will no longer be resumable. See Session Resumption for more information. Default: 300.
  + [sigalgs](https://bun.com/reference/node/tls/TLSSocketOptions/sigalgs)?: string

    Colon-separated list of supported signature algorithms. The list can contain digest algorithms (SHA256, MD5 etc.), public key algorithms (RSA-PSS, ECDSA etc.), combination of both (e.g 'RSA+SHA384') or TLS v1.3 scheme names (e.g. rsa\_pss\_pss\_sha512).
  + [SNICallback](https://bun.com/reference/node/tls/TLSSocketOptions/SNICallback)?: (servername: string, cb: (err: null | [Error](https://bun.com/reference/globals/Error), ctx?: [SecureContext](https://bun.com/reference/node/tls/SecureContext)) => void) => void

    SNICallback(servername, cb) <Function> A function that will be called if the client supports SNI TLS extension. Two arguments will be passed when called: servername and cb. SNICallback should invoke cb(null, ctx), where ctx is a SecureContext instance. (tls.createSecureContext(...) can be used to get a proper SecureContext.) If SNICallback wasn't provided the default callback with high-level API will be used (see below).
  + [ticketKeys](https://bun.com/reference/node/tls/TLSSocketOptions/ticketKeys)?: [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>

    48-bytes of cryptographically strong pseudo-random data. See Session Resumption for more information.
* type [SecureVersion](https://bun.com/reference/node/tls/SecureVersion) = 'TLSv1.3' | 'TLSv1.2' | 'TLSv1.1' | 'TLSv1'