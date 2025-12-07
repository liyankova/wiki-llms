---
url: https://bun.com/reference/node/net
title: Node.js net module | API Reference | Bun
source_domain: bun.com
---

# Node.js net module | API Reference | Bun

Node.js module

# [net](https://bun.com/reference/node/net)

The `'node:net'` module provides an asynchronous network API for creating TCP servers and clients. It exposes `Socket` and `Server` classes for handling raw network connections.

Works in Bun

Core TCP socket functionality works. The SocketAddress class is implemented internally but not exposed. BlockList exists but is currently a no-op.

* ### class [BlockList](https://bun.com/reference/node/net/BlockList)

  The `BlockList` object can be used with some network APIs to specify rules for disabling inbound or outbound access to specific IP addresses, IP ranges, or IP subnets.

  + [rules](https://bun.com/reference/node/net/BlockList/rules): readonly string[]

    The list of rules added to the blocklist.
  + [addAddress](https://bun.com/reference/node/net/BlockList/addAddress)(

    address: string,

    type?: [IPVersion](https://bun.com/reference/node/net/IPVersion)

    ): void;

    Adds a rule to block the given IP address.

    @param address

    An IPv4 or IPv6 address.

    @param type

    Either `'ipv4'` or `'ipv6'`.

    [addAddress](https://bun.com/reference/node/net/BlockList/addAddress)(

    address: [SocketAddress](https://bun.com/reference/node/net/SocketAddress)

    ): void;

    Adds a rule to block the given IP address.

    @param address

    An IPv4 or IPv6 address.
  + [addRange](https://bun.com/reference/node/net/BlockList/addRange)(

    start: string,

    end: string,

    type?: [IPVersion](https://bun.com/reference/node/net/IPVersion)

    ): void;

    Adds a rule to block a range of IP addresses from `start` (inclusive) to`end` (inclusive).

    @param start

    The starting IPv4 or IPv6 address in the range.

    @param end

    The ending IPv4 or IPv6 address in the range.

    @param type

    Either `'ipv4'` or `'ipv6'`.

    [addRange](https://bun.com/reference/node/net/BlockList/addRange)(

    start: [SocketAddress](https://bun.com/reference/node/net/SocketAddress),

    end: [SocketAddress](https://bun.com/reference/node/net/SocketAddress)

    ): void;

    Adds a rule to block a range of IP addresses from `start` (inclusive) to`end` (inclusive).

    @param start

    The starting IPv4 or IPv6 address in the range.

    @param end

    The ending IPv4 or IPv6 address in the range.
  + [addSubnet](https://bun.com/reference/node/net/BlockList/addSubnet)(

    net: [SocketAddress](https://bun.com/reference/node/net/SocketAddress),

    prefix: number

    ): void;

    Adds a rule to block a range of IP addresses specified as a subnet mask.

    @param net

    The network IPv4 or IPv6 address.

    @param prefix

    The number of CIDR prefix bits. For IPv4, this must be a value between `0` and `32`. For IPv6, this must be between `0` and `128`.

    [addSubnet](https://bun.com/reference/node/net/BlockList/addSubnet)(

    net: string,

    prefix: number,

    type?: [IPVersion](https://bun.com/reference/node/net/IPVersion)

    ): void;

    Adds a rule to block a range of IP addresses specified as a subnet mask.

    @param net

    The network IPv4 or IPv6 address.

    @param prefix

    The number of CIDR prefix bits. For IPv4, this must be a value between `0` and `32`. For IPv6, this must be between `0` and `128`.

    @param type

    Either `'ipv4'` or `'ipv6'`.
  + [check](https://bun.com/reference/node/net/BlockList/check)(

    address: [SocketAddress](https://bun.com/reference/node/net/SocketAddress)

    ): boolean;

    Returns `true` if the given IP address matches any of the rules added to the`BlockList`.

    ```
    const blockList = new net.BlockList();
    blockList.addAddress('123.123.123.123');
    blockList.addRange('10.0.0.1', '10.0.0.10');
    blockList.addSubnet('8592:757c:efae:4e45::', 64, 'ipv6');

    console.log(blockList.check('123.123.123.123'));  // Prints: true
    console.log(blockList.check('10.0.0.3'));  // Prints: true
    console.log(blockList.check('222.111.111.222'));  // Prints: false

    // IPv6 notation for IPv4 addresses works:
    console.log(blockList.check('::ffff:7b7b:7b7b', 'ipv6')); // Prints: true
    console.log(blockList.check('::ffff:123.123.123.123', 'ipv6')); // Prints: true
    ```

    @param address

    The IP address to check

    [check](https://bun.com/reference/node/net/BlockList/check)(

    address: string,

    type?: [IPVersion](https://bun.com/reference/node/net/IPVersion)

    ): boolean;

    Returns `true` if the given IP address matches any of the rules added to the`BlockList`.

    ```
    const blockList = new net.BlockList();
    blockList.addAddress('123.123.123.123');
    blockList.addRange('10.0.0.1', '10.0.0.10');
    blockList.addSubnet('8592:757c:efae:4e45::', 64, 'ipv6');

    console.log(blockList.check('123.123.123.123'));  // Prints: true
    console.log(blockList.check('10.0.0.3'));  // Prints: true
    console.log(blockList.check('222.111.111.222'));  // Prints: false

    // IPv6 notation for IPv4 addresses works:
    console.log(blockList.check('::ffff:7b7b:7b7b', 'ipv6')); // Prints: true
    console.log(blockList.check('::ffff:123.123.123.123', 'ipv6')); // Prints: true
    ```

    @param address

    The IP address to check

    @param type

    Either `'ipv4'` or `'ipv6'`.
  + [fromJSON](https://bun.com/reference/node/net/BlockList/fromJSON)(

    data: string | readonly string[]

    ): void;

    ```
    const blockList = new net.BlockList();
    const data = [
      'Subnet: IPv4 192.168.1.0/24',
      'Address: IPv4 10.0.0.5',
      'Range: IPv4 192.168.2.1-192.168.2.10',
      'Range: IPv4 10.0.0.1-10.0.0.10',
    ];
    blockList.fromJSON(data);
    blockList.fromJSON(JSON.stringify(data));
    ```
  + [toJSON](https://bun.com/reference/node/net/BlockList/toJSON)(): readonly string[];
  + static [isBlockList](https://bun.com/reference/node/net/BlockList/isBlockList)(

    value: unknown

    ): value is [BlockList](https://bun.com/reference/node/net/BlockList);

    Returns `true` if the `value` is a `net.BlockList`.

    @param value

    Any JS value
* ### class [Server](https://bun.com/reference/node/net/Server)

  This class is used to create a TCP or `IPC` server.

  + [connections](https://bun.com/reference/node/net/Server/connections): number
  + readonly [listening](https://bun.com/reference/node/net/Server/listening): boolean

    Indicates whether or not the server is listening for connections.
  + [maxConnections](https://bun.com/reference/node/net/Server/maxConnections): number

    Set this property to reject connections when the server's connection count gets high.

    It is not recommended to use this option once a socket has been sent to a child with `child_process.fork()`.
  + static [captureRejections](https://bun.com/reference/node/net/Server/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/net/Server/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/net/Server/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/net/Server/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/net/Server/[asyncDispose])(): Promise<void>;

    Calls () and returns a promise that fulfills when the server has closed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/net/Server/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/net/Server/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/net/Server/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/net/Server/addListener)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/net/Server/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/net/Server/addListener)(

    event: 'listening',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop

    [addListener](https://bun.com/reference/node/net/Server/addListener)(

    event: 'drop',

    listener: (data?: [DropArgument](https://bun.com/reference/node/net/DropArgument)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connection
    3. error
    4. listening
    5. drop
  + [address](https://bun.com/reference/node/net/Server/address)(): null | string | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

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
  + [close](https://bun.com/reference/node/net/Server/close)(

    callback?: (err?: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Stops the server from accepting new connections and keeps existing connections. This function is asynchronous, the server is finally closed when all connections are ended and the server emits a `'close'` event. The optional `callback` will be called once the `'close'` event occurs. Unlike that event, it will be called with an `Error` as its only argument if the server was not open when it was closed.

    @param callback

    Called when the server is closed.
  + [emit](https://bun.com/reference/node/net/Server/emit)(

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

    [emit](https://bun.com/reference/node/net/Server/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/net/Server/emit)(

    event: 'connection',

    socket: [Socket](https://bun.com/reference/node/net/Socket)

    ): boolean;

    [emit](https://bun.com/reference/node/net/Server/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/net/Server/emit)(

    event: 'listening'

    ): boolean;

    [emit](https://bun.com/reference/node/net/Server/emit)(

    event: 'drop',

    data?: [DropArgument](https://bun.com/reference/node/net/DropArgument)

    ): boolean;
  + [eventNames](https://bun.com/reference/node/net/Server/eventNames)(): string | symbol[];

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
  + [getConnections](https://bun.com/reference/node/net/Server/getConnections)(

    cb: (error: null | [Error](https://bun.com/reference/globals/Error), count: number) => void

    ): this;

    Asynchronously get the number of concurrent connections on the server. Works when sockets were sent to forks.

    Callback should take two arguments `err` and `count`.
  + [getMaxListeners](https://bun.com/reference/node/net/Server/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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

    [listen](https://bun.com/reference/node/net/Server/listen)(

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
  + [listenerCount](https://bun.com/reference/node/net/Server/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/net/Server/listeners)<K>(

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
  + [off](https://bun.com/reference/node/net/Server/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/net/Server/on)(

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

    [on](https://bun.com/reference/node/net/Server/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/net/Server/on)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [on](https://bun.com/reference/node/net/Server/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/net/Server/on)(

    event: 'listening',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/net/Server/on)(

    event: 'drop',

    listener: (data?: [DropArgument](https://bun.com/reference/node/net/DropArgument)) => void

    ): this;
  + [once](https://bun.com/reference/node/net/Server/once)(

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

    [once](https://bun.com/reference/node/net/Server/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/net/Server/once)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [once](https://bun.com/reference/node/net/Server/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/net/Server/once)(

    event: 'listening',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/net/Server/once)(

    event: 'drop',

    listener: (data?: [DropArgument](https://bun.com/reference/node/net/DropArgument)) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/net/Server/prependListener)(

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

    [prependListener](https://bun.com/reference/node/net/Server/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Server/prependListener)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Server/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Server/prependListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Server/prependListener)(

    event: 'drop',

    listener: (data?: [DropArgument](https://bun.com/reference/node/net/DropArgument)) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/net/Server/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/net/Server/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Server/prependOnceListener)(

    event: 'connection',

    listener: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Server/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Server/prependOnceListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Server/prependOnceListener)(

    event: 'drop',

    listener: (data?: [DropArgument](https://bun.com/reference/node/net/DropArgument)) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/net/Server/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/net/Server/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed server will *not* let the program exit if it's the only server left (the default behavior). If the server is `ref`ed calling `ref()` again will have no effect.
  + [removeAllListeners](https://bun.com/reference/node/net/Server/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/net/Server/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/net/Server/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [unref](https://bun.com/reference/node/net/Server/unref)(): this;

    Calling `unref()` on a server will allow the program to exit if this is the only active server in the event system. If the server is already `unref`ed calling`unref()` again will have no effect.
  + static [addAbortListener](https://bun.com/reference/node/net/Server/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/net/Server/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/net/Server/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/net/Server/on)(

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

    static [on](https://bun.com/reference/node/net/Server/on)(

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
  + static [once](https://bun.com/reference/node/net/Server/once)(

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

    static [once](https://bun.com/reference/node/net/Server/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/net/Server/setMaxListeners)(

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
* ### class [Socket](https://bun.com/reference/node/net/Socket)

  This class is an abstraction of a TCP socket or a streaming `IPC` endpoint (uses named pipes on Windows, and Unix domain sockets otherwise). It is also an `EventEmitter`.

  A `net.Socket` can be created by the user and used directly to interact with a server. For example, it is returned by createConnection, so the user can use it to talk to the server.

  It can also be created by Node.js and passed to the user when a connection is received. For example, it is passed to the listeners of a `'connection'` event emitted on a Server, so the user can use it to interact with the client.

  + [allowHalfOpen](https://bun.com/reference/node/net/Socket/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [autoSelectFamilyAttemptedAddresses](https://bun.com/reference/node/net/Socket/autoSelectFamilyAttemptedAddresses): string[]

    This property is only present if the family autoselection algorithm is enabled in `socket.connect(options)` and it is an array of the addresses that have been attempted.

    Each address is a string in the form of `$IP:$PORT`. If the connection was successful, then the last address is the one that the socket is currently connected to.
  + readonly [bytesRead](https://bun.com/reference/node/net/Socket/bytesRead): number

    The amount of received bytes.
  + readonly [bytesWritten](https://bun.com/reference/node/net/Socket/bytesWritten): number

    The amount of bytes sent.
  + readonly [closed](https://bun.com/reference/node/net/Socket/closed): boolean

    Is `true` after `'close'` has been emitted.
  + readonly [connecting](https://bun.com/reference/node/net/Socket/connecting): boolean

    If `true`, `socket.connect(options[, connectListener])` was called and has not yet finished. It will stay `true` until the socket becomes connected, then it is set to `false` and the `'connect'` event is emitted. Note that the `socket.connect(options[, connectListener])` callback is a listener for the `'connect'` event.
  + readonly [destroyed](https://bun.com/reference/node/net/Socket/destroyed): boolean

    See `writable.destroyed` for further details.
  + readonly [errored](https://bun.com/reference/node/net/Socket/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + readonly [localAddress](https://bun.com/reference/node/net/Socket/localAddress)?: string

    The string representation of the local IP address the remote client is connecting on. For example, in a server listening on `'0.0.0.0'`, if a client connects on `'192.168.1.1'`, the value of `socket.localAddress` would be`'192.168.1.1'`.
  + readonly [localFamily](https://bun.com/reference/node/net/Socket/localFamily)?: string

    The string representation of the local IP family. `'IPv4'` or `'IPv6'`.
  + readonly [localPort](https://bun.com/reference/node/net/Socket/localPort)?: number

    The numeric representation of the local port. For example, `80` or `21`.
  + readonly [pending](https://bun.com/reference/node/net/Socket/pending): boolean

    This is `true` if the socket is not connected yet, either because `.connect()`has not yet been called or because it is still in the process of connecting (see `socket.connecting`).
  + [readable](https://bun.com/reference/node/net/Socket/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/net/Socket/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/net/Socket/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/net/Socket/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/net/Socket/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/net/Socket/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/net/Socket/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/net/Socket/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/net/Socket/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + readonly [readyState](https://bun.com/reference/node/net/Socket/readyState): [SocketReadyState](https://bun.com/reference/node/net/SocketReadyState)

    This property represents the state of the connection as a string.

    - If the stream is connecting `socket.readyState` is `opening`.
    - If the stream is readable and writable, it is `open`.
    - If the stream is readable and not writable, it is `readOnly`.
    - If the stream is not readable and writable, it is `writeOnly`.
  + readonly [remoteAddress](https://bun.com/reference/node/net/Socket/remoteAddress): undefined | string

    The string representation of the remote IP address. For example,`'74.125.127.100'` or `'2001:4860:a005::68'`. Value may be `undefined` if the socket is destroyed (for example, if the client disconnected).
  + readonly [remoteFamily](https://bun.com/reference/node/net/Socket/remoteFamily): undefined | string

    The string representation of the remote IP family. `'IPv4'` or `'IPv6'`. Value may be `undefined` if the socket is destroyed (for example, if the client disconnected).
  + readonly [remotePort](https://bun.com/reference/node/net/Socket/remotePort): undefined | number

    The numeric representation of the remote port. For example, `80` or `21`. Value may be `undefined` if the socket is destroyed (for example, if the client disconnected).
  + readonly [timeout](https://bun.com/reference/node/net/Socket/timeout)?: number

    The socket timeout in milliseconds as set by `socket.setTimeout()`. It is `undefined` if a timeout has not been set.
  + readonly [writable](https://bun.com/reference/node/net/Socket/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/net/Socket/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/net/Socket/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/net/Socket/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/net/Socket/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/net/Socket/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/net/Socket/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/net/Socket/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/net/Socket/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + static [captureRejections](https://bun.com/reference/node/net/Socket/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/net/Socket/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/net/Socket/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/net/Socket/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [\_construct](https://bun.com/reference/node/net/Socket/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/net/Socket/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/net/Socket/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_read](https://bun.com/reference/node/net/Socket/_read)(

    size: number

    ): void;
  + [\_write](https://bun.com/reference/node/net/Socket/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/net/Socket/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/net/Socket/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/net/Socket/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/net/Socket/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/net/Socket/addListener)(

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'close',

    listener: (hadError: boolean) => void

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'connect',

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'connectionAttempt',

    listener: (ip: string, port: number, family: number) => void

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'connectionAttemptFailed',

    listener: (ip: string, port: number, family: number, error: [Error](https://bun.com/reference/globals/Error)) => void

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'connectionAttemptTimeout',

    listener: (ip: string, port: number, family: number) => void

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'data',

    listener: (data: NonSharedBuffer) => void

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'drain',

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'end',

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'lookup',

    listener: (err: [Error](https://bun.com/reference/globals/Error), address: string, family: string | number, host: string) => void

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'ready',

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

    [addListener](https://bun.com/reference/node/net/Socket/addListener)(

    event: 'timeout',

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
  + [address](https://bun.com/reference/node/net/Socket/address)(): {} | [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

    Returns the bound `address`, the address `family` name and `port` of the socket as reported by the operating system:`{ port: 12346, family: 'IPv4', address: '127.0.0.1' }`
  + [asIndexedPairs](https://bun.com/reference/node/net/Socket/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [compose](https://bun.com/reference/node/net/Socket/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [connect](https://bun.com/reference/node/net/Socket/connect)(

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

    [connect](https://bun.com/reference/node/net/Socket/connect)(

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

    [connect](https://bun.com/reference/node/net/Socket/connect)(

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

    [connect](https://bun.com/reference/node/net/Socket/connect)(

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
  + [cork](https://bun.com/reference/node/net/Socket/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/net/Socket/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [destroySoon](https://bun.com/reference/node/net/Socket/destroySoon)(): void;

    Destroys the socket after all data is written. If the `finish` event was already emitted the socket is destroyed immediately. If the socket is still writable it implicitly calls `socket.end()`.
  + [drop](https://bun.com/reference/node/net/Socket/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/net/Socket/emit)(

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

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'close',

    hadError: boolean

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'connect'

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'connectionAttempt',

    ip: string,

    port: number,

    family: number

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'connectionAttemptFailed',

    ip: string,

    port: number,

    family: number,

    error: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'connectionAttemptTimeout',

    ip: string,

    port: number,

    family: number

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'data',

    data: NonSharedBuffer

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'lookup',

    err: [Error](https://bun.com/reference/globals/Error),

    address: string,

    family: string | number,

    host: string

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'ready'

    ): boolean;

    [emit](https://bun.com/reference/node/net/Socket/emit)(

    event: 'timeout'

    ): boolean;
  + [end](https://bun.com/reference/node/net/Socket/end)(

    callback?: () => void

    ): this;

    Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data.

    See `writable.end()` for further details.

    @param callback

    Optional callback for when the socket is finished.

    @returns

    The socket itself.

    [end](https://bun.com/reference/node/net/Socket/end)(

    buffer: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    callback?: () => void

    ): this;

    Half-closes the socket. i.e., it sends a FIN packet. It is possible the server will still send some data.

    See `writable.end()` for further details.

    @param callback

    Optional callback for when the socket is finished.

    @returns

    The socket itself.

    [end](https://bun.com/reference/node/net/Socket/end)(

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
  + [eventNames](https://bun.com/reference/node/net/Socket/eventNames)(): string | symbol[];

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
  + [every](https://bun.com/reference/node/net/Socket/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/net/Socket/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/net/Socket/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/net/Socket/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/net/Socket/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [forEach](https://bun.com/reference/node/net/Socket/forEach)(

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
  + [getMaxListeners](https://bun.com/reference/node/net/Socket/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/net/Socket/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/net/Socket/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/net/Socket/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/net/Socket/listeners)<K>(

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
  + [map](https://bun.com/reference/node/net/Socket/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/net/Socket/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/net/Socket/on)(

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

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'close',

    listener: (hadError: boolean) => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'connect',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'connectionAttempt',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'connectionAttemptFailed',

    listener: (ip: string, port: number, family: number, error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'connectionAttemptTimeout',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'data',

    listener: (data: NonSharedBuffer) => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'lookup',

    listener: (err: [Error](https://bun.com/reference/globals/Error), address: string, family: string | number, host: string) => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'ready',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/net/Socket/on)(

    event: 'timeout',

    listener: () => void

    ): this;
  + [once](https://bun.com/reference/node/net/Socket/once)(

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

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'close',

    listener: (hadError: boolean) => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'connectionAttempt',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'connectionAttemptFailed',

    listener: (ip: string, port: number, family: number, error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'connectionAttemptTimeout',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'connect',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'data',

    listener: (data: NonSharedBuffer) => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'lookup',

    listener: (err: [Error](https://bun.com/reference/globals/Error), address: string, family: string | number, host: string) => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'ready',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/net/Socket/once)(

    event: 'timeout',

    listener: () => void

    ): this;
  + [pause](https://bun.com/reference/node/net/Socket/pause)(): this;

    Pauses the reading of data. That is, `'data'` events will not be emitted. Useful to throttle back an upload.

    @returns

    The socket itself.
  + [pipe](https://bun.com/reference/node/net/Socket/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

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

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'close',

    listener: (hadError: boolean) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'connect',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'connectionAttempt',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'connectionAttemptFailed',

    listener: (ip: string, port: number, family: number, error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'connectionAttemptTimeout',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'data',

    listener: (data: NonSharedBuffer) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'lookup',

    listener: (err: [Error](https://bun.com/reference/globals/Error), address: string, family: string | number, host: string) => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'ready',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/net/Socket/prependListener)(

    event: 'timeout',

    listener: () => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'close',

    listener: (hadError: boolean) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'connect',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'connectionAttempt',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'connectionAttemptFailed',

    listener: (ip: string, port: number, family: number, error: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'connectionAttemptTimeout',

    listener: (ip: string, port: number, family: number) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'data',

    listener: (data: NonSharedBuffer) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'lookup',

    listener: (err: [Error](https://bun.com/reference/globals/Error), address: string, family: string | number, host: string) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'ready',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/net/Socket/prependOnceListener)(

    event: 'timeout',

    listener: () => void

    ): this;
  + [push](https://bun.com/reference/node/net/Socket/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/net/Socket/rawListeners)<K>(

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
  + [read](https://bun.com/reference/node/net/Socket/read)(

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
  + [reduce](https://bun.com/reference/node/net/Socket/reduce)<T = any>(

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

    [reduce](https://bun.com/reference/node/net/Socket/reduce)<T = any>(

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
  + [ref](https://bun.com/reference/node/net/Socket/ref)(): this;

    Opposite of `unref()`, calling `ref()` on a previously `unref`ed socket will *not* let the program exit if it's the only socket left (the default behavior). If the socket is `ref`ed calling `ref` again will have no effect.

    @returns

    The socket itself.
  + [removeAllListeners](https://bun.com/reference/node/net/Socket/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

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

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/net/Socket/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resetAndDestroy](https://bun.com/reference/node/net/Socket/resetAndDestroy)(): this;

    Close the TCP connection by sending an RST packet and destroy the stream. If this TCP socket is in connecting status, it will send an RST packet and destroy this TCP socket once it is connected. Otherwise, it will call `socket.destroy` with an `ERR_SOCKET_CLOSED` Error. If this is not a TCP socket (for example, a pipe), calling this method will immediately throw an `ERR_INVALID_HANDLE_TYPE` Error.
  + [resume](https://bun.com/reference/node/net/Socket/resume)(): this;

    Resumes reading after a call to `socket.pause()`.

    @returns

    The socket itself.
  + [setDefaultEncoding](https://bun.com/reference/node/net/Socket/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/net/Socket/setEncoding)(

    encoding?: BufferEncoding

    ): this;

    Set the encoding for the socket as a `Readable Stream`. See `readable.setEncoding()` for more information.

    @returns

    The socket itself.
  + [setKeepAlive](https://bun.com/reference/node/net/Socket/setKeepAlive)(

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
  + [setMaxListeners](https://bun.com/reference/node/net/Socket/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setNoDelay](https://bun.com/reference/node/net/Socket/setNoDelay)(

    noDelay?: boolean

    ): this;

    Enable/disable the use of Nagle's algorithm.

    When a TCP connection is created, it will have Nagle's algorithm enabled.

    Nagle's algorithm delays data before it is sent via the network. It attempts to optimize throughput at the expense of latency.

    Passing `true` for `noDelay` or not passing an argument will disable Nagle's algorithm for the socket. Passing `false` for `noDelay` will enable Nagle's algorithm.

    @returns

    The socket itself.
  + [setTimeout](https://bun.com/reference/node/net/Socket/setTimeout)(

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
  + [some](https://bun.com/reference/node/net/Socket/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/net/Socket/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/net/Socket/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/net/Socket/uncork)(): void;

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
  + [unpipe](https://bun.com/reference/node/net/Socket/unpipe)(

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
  + [unref](https://bun.com/reference/node/net/Socket/unref)(): this;

    Calling `unref()` on a socket will allow the program to exit if this is the only active socket in the event system. If the socket is already `unref`ed calling`unref()` again will have no effect.

    @returns

    The socket itself.
  + [unshift](https://bun.com/reference/node/net/Socket/unshift)(

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
  + [wrap](https://bun.com/reference/node/net/Socket/wrap)(

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
  + [write](https://bun.com/reference/node/net/Socket/write)(

    buffer: string | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    cb?: (err?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    Sends data on the socket. The second parameter specifies the encoding in the case of a string. It defaults to UTF8 encoding.

    Returns `true` if the entire data was flushed successfully to the kernel buffer. Returns `false` if all or part of the data was queued in user memory.`'drain'` will be emitted when the buffer is again free.

    The optional `callback` parameter will be executed when the data is finally written out, which may not be immediately.

    See `Writable` stream `write()` method for more information.

    [write](https://bun.com/reference/node/net/Socket/write)(

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
  + static [addAbortListener](https://bun.com/reference/node/net/Socket/addAbortListener)(

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
  + static [from](https://bun.com/reference/node/net/Socket/from)(

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
  + static [fromWeb](https://bun.com/reference/node/net/Socket/fromWeb)(

    duplexStream: { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) },

    options?: Pick<[DuplexOptions](https://bun.com/reference/node/stream/default/DuplexOptions)<[Duplex](https://bun.com/reference/node/stream/default/Duplex)>, 'signal' | 'allowHalfOpen' | 'decodeStrings' | 'encoding' | 'highWaterMark' | 'objectMode'>

    ): [Duplex](https://bun.com/reference/node/stream/default/Duplex);

    A utility method for creating a `Duplex` from a web `ReadableStream` and `WritableStream`.
  + static [getEventListeners](https://bun.com/reference/node/net/Socket/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/net/Socket/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/net/Socket/on)(

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

    static [on](https://bun.com/reference/node/net/Socket/on)(

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
  + static [once](https://bun.com/reference/node/net/Socket/once)(

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

    static [once](https://bun.com/reference/node/net/Socket/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/net/Socket/setMaxListeners)(

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
  + static [toWeb](https://bun.com/reference/node/net/Socket/toWeb)(

    streamDuplex: [Duplex](https://bun.com/reference/node/stream/default/Duplex)

    ): { readable: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream); writable: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream) };

    A utility method for creating a web `ReadableStream` and `WritableStream` from a `Duplex`.
* ### class [SocketAddress](https://bun.com/reference/node/net/SocketAddress)

  + readonly [address](https://bun.com/reference/node/net/SocketAddress/address): string

    Either `'ipv4'` or `'ipv6'`.
  + readonly [family](https://bun.com/reference/node/net/SocketAddress/family): [IPVersion](https://bun.com/reference/node/net/IPVersion)

    Either `'ipv4'` or `'ipv6'`.
  + readonly [flowlabel](https://bun.com/reference/node/net/SocketAddress/flowlabel): number
  + readonly [port](https://bun.com/reference/node/net/SocketAddress/port): number
  + static [parse](https://bun.com/reference/node/net/SocketAddress/parse)(

    input: string

    ): undefined | [SocketAddress](https://bun.com/reference/node/net/SocketAddress);

    @param input

    An input string containing an IP address and optional port, e.g. `123.1.2.3:1234` or `[1::1]:1234`.

    @returns

    Returns a `SocketAddress` if parsing was successful. Otherwise returns `undefined`.
* function [connect](https://bun.com/reference/node/net/connect)(

  options: [NetConnectOpts](https://bun.com/reference/node/net/NetConnectOpts),

  connectionListener?: () => void

  ): [Socket](https://bun.com/reference/node/net/Socket);

  Aliases to createConnection.

  Possible signatures:

  + connect
  + connect for `IPC` connections.
  + connect for TCP connections.

  function [connect](https://bun.com/reference/node/net/connect)(

  port: number,

  host?: string,

  connectionListener?: () => void

  ): [Socket](https://bun.com/reference/node/net/Socket);

  Aliases to createConnection.

  Possible signatures:

  + connect
  + connect for `IPC` connections.
  + connect for TCP connections.

  function [connect](https://bun.com/reference/node/net/connect)(

  path: string,

  connectionListener?: () => void

  ): [Socket](https://bun.com/reference/node/net/Socket);

  Aliases to createConnection.

  Possible signatures:

  + connect
  + connect for `IPC` connections.
  + connect for TCP connections.
* function [createConnection](https://bun.com/reference/node/net/createConnection)(

  options: [NetConnectOpts](https://bun.com/reference/node/net/NetConnectOpts),

  connectionListener?: () => void

  ): [Socket](https://bun.com/reference/node/net/Socket);

  A factory function, which creates a new Socket, immediately initiates connection with `socket.connect()`, then returns the `net.Socket` that starts the connection.

  When the connection is established, a `'connect'` event will be emitted on the returned socket. The last parameter `connectListener`, if supplied, will be added as a listener for the `'connect'` event **once**.

  Possible signatures:

  + createConnection
  + createConnection for `IPC` connections.
  + createConnection for TCP connections.

  The connect function is an alias to this function.

  function [createConnection](https://bun.com/reference/node/net/createConnection)(

  port: number,

  host?: string,

  connectionListener?: () => void

  ): [Socket](https://bun.com/reference/node/net/Socket);

  A factory function, which creates a new Socket, immediately initiates connection with `socket.connect()`, then returns the `net.Socket` that starts the connection.

  When the connection is established, a `'connect'` event will be emitted on the returned socket. The last parameter `connectListener`, if supplied, will be added as a listener for the `'connect'` event **once**.

  Possible signatures:

  + createConnection
  + createConnection for `IPC` connections.
  + createConnection for TCP connections.

  The connect function is an alias to this function.

  function [createConnection](https://bun.com/reference/node/net/createConnection)(

  path: string,

  connectionListener?: () => void

  ): [Socket](https://bun.com/reference/node/net/Socket);

  A factory function, which creates a new Socket, immediately initiates connection with `socket.connect()`, then returns the `net.Socket` that starts the connection.

  When the connection is established, a `'connect'` event will be emitted on the returned socket. The last parameter `connectListener`, if supplied, will be added as a listener for the `'connect'` event **once**.

  Possible signatures:

  + createConnection
  + createConnection for `IPC` connections.
  + createConnection for TCP connections.

  The connect function is an alias to this function.
* function [createServer](https://bun.com/reference/node/net/createServer)(

  connectionListener?: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

  ): [Server](https://bun.com/reference/node/net/Server);

  Creates a new TCP or `IPC` server.

  If `allowHalfOpen` is set to `true`, when the other end of the socket signals the end of transmission, the server will only send back the end of transmission when `socket.end()` is explicitly called. For example, in the context of TCP, when a FIN packed is received, a FIN packed is sent back only when `socket.end()` is explicitly called. Until then the connection is half-closed (non-readable but still writable). See `'end'` event and [RFC 1122](https://tools.ietf.org/html/rfc1122) (section 4.2.2.13) for more information.

  If `pauseOnConnect` is set to `true`, then the socket associated with each incoming connection will be paused, and no data will be read from its handle. This allows connections to be passed between processes without any data being read by the original process. To begin reading data from a paused socket, call `socket.resume()`.

  The server can be a TCP server or an `IPC` server, depending on what it `listen()` to.

  Here is an example of a TCP echo server which listens for connections on port 8124:

  ```
  import net from 'node:net';
  const server = net.createServer((c) => {
    // 'connection' listener.
    console.log('client connected');
    c.on('end', () => {
      console.log('client disconnected');
    });
    c.write('hello\r\n');
    c.pipe(c);
  });
  server.on('error', (err) => {
    throw err;
  });
  server.listen(8124, () => {
    console.log('server bound');
  });
  ```

  Test this by using `telnet`:

  ```
  telnet localhost 8124
  ```

  To listen on the socket `/tmp/echo.sock`:

  ```
  server.listen('/tmp/echo.sock', () => {
    console.log('server bound');
  });
  ```

  Use `nc` to connect to a Unix domain socket server:

  ```
  nc -U /tmp/echo.sock
  ```

  @param connectionListener

  Automatically set as a listener for the 'connection' event.

  function [createServer](https://bun.com/reference/node/net/createServer)(

  options?: [ServerOpts](https://bun.com/reference/node/net/ServerOpts),

  connectionListener?: (socket: [Socket](https://bun.com/reference/node/net/Socket)) => void

  ): [Server](https://bun.com/reference/node/net/Server);

  Creates a new TCP or `IPC` server.

  If `allowHalfOpen` is set to `true`, when the other end of the socket signals the end of transmission, the server will only send back the end of transmission when `socket.end()` is explicitly called. For example, in the context of TCP, when a FIN packed is received, a FIN packed is sent back only when `socket.end()` is explicitly called. Until then the connection is half-closed (non-readable but still writable). See `'end'` event and [RFC 1122](https://tools.ietf.org/html/rfc1122) (section 4.2.2.13) for more information.

  If `pauseOnConnect` is set to `true`, then the socket associated with each incoming connection will be paused, and no data will be read from its handle. This allows connections to be passed between processes without any data being read by the original process. To begin reading data from a paused socket, call `socket.resume()`.

  The server can be a TCP server or an `IPC` server, depending on what it `listen()` to.

  Here is an example of a TCP echo server which listens for connections on port 8124:

  ```
  import net from 'node:net';
  const server = net.createServer((c) => {
    // 'connection' listener.
    console.log('client connected');
    c.on('end', () => {
      console.log('client disconnected');
    });
    c.write('hello\r\n');
    c.pipe(c);
  });
  server.on('error', (err) => {
    throw err;
  });
  server.listen(8124, () => {
    console.log('server bound');
  });
  ```

  Test this by using `telnet`:

  ```
  telnet localhost 8124
  ```

  To listen on the socket `/tmp/echo.sock`:

  ```
  server.listen('/tmp/echo.sock', () => {
    console.log('server bound');
  });
  ```

  Use `nc` to connect to a Unix domain socket server:

  ```
  nc -U /tmp/echo.sock
  ```

  @param connectionListener

  Automatically set as a listener for the 'connection' event.
* function [getDefaultAutoSelectFamily](https://bun.com/reference/node/net/getDefaultAutoSelectFamily)(): boolean;

  Gets the current default value of the `autoSelectFamily` option of `socket.connect(options)`. The initial default value is `true`, unless the command line option`--no-network-family-autoselection` is provided.
* function [getDefaultAutoSelectFamilyAttemptTimeout](https://bun.com/reference/node/net/getDefaultAutoSelectFamilyAttemptTimeout)(): number;

  Gets the current default value of the `autoSelectFamilyAttemptTimeout` option of `socket.connect(options)`. The initial default value is `250` or the value specified via the command line option `--network-family-autoselection-attempt-timeout`.

  @returns

  The current default value of the `autoSelectFamilyAttemptTimeout` option.
* function [isIP](https://bun.com/reference/node/net/isIP)(

  input: string

  ): number;

  Returns `6` if `input` is an IPv6 address. Returns `4` if `input` is an IPv4 address in [dot-decimal notation](https://en.wikipedia.org/wiki/Dot-decimal_notation) with no leading zeroes. Otherwise, returns`0`.

  ```
  net.isIP('::1'); // returns 6
  net.isIP('127.0.0.1'); // returns 4
  net.isIP('127.000.000.001'); // returns 0
  net.isIP('127.0.0.1/24'); // returns 0
  net.isIP('fhqwhgads'); // returns 0
  ```
* function [isIPv4](https://bun.com/reference/node/net/isIPv4)(

  input: string

  ): boolean;

  Returns `true` if `input` is an IPv4 address in [dot-decimal notation](https://en.wikipedia.org/wiki/Dot-decimal_notation) with no leading zeroes. Otherwise, returns `false`.

  ```
  net.isIPv4('127.0.0.1'); // returns true
  net.isIPv4('127.000.000.001'); // returns false
  net.isIPv4('127.0.0.1/24'); // returns false
  net.isIPv4('fhqwhgads'); // returns false
  ```
* function [isIPv6](https://bun.com/reference/node/net/isIPv6)(

  input: string

  ): boolean;

  Returns `true` if `input` is an IPv6 address. Otherwise, returns `false`.

  ```
  net.isIPv6('::1'); // returns true
  net.isIPv6('fhqwhgads'); // returns false
  ```
* function [setDefaultAutoSelectFamily](https://bun.com/reference/node/net/setDefaultAutoSelectFamily)(

  value: boolean

  ): void;

  Sets the default value of the `autoSelectFamily` option of `socket.connect(options)`.

  @param value

  The new default value. The initial default value is `true`, unless the command line option `--no-network-family-autoselection` is provided.
* function [setDefaultAutoSelectFamilyAttemptTimeout](https://bun.com/reference/node/net/setDefaultAutoSelectFamilyAttemptTimeout)(

  value: number

  ): void;

  Sets the default value of the `autoSelectFamilyAttemptTimeout` option of `socket.connect(options)`.

  @param value

  The new default value, which must be a positive number. If the number is less than `10`, the value `10` is used instead. The initial default value is `250` or the value specified via the command line option `--network-family-autoselection-attempt-timeout`.

## Type definitions

* ### interface [AddressInfo](https://bun.com/reference/node/net/AddressInfo)

  + [address](https://bun.com/reference/node/net/AddressInfo/address): string
  + [family](https://bun.com/reference/node/net/AddressInfo/family): string
  + [port](https://bun.com/reference/node/net/AddressInfo/port): number
* ### interface [DropArgument](https://bun.com/reference/node/net/DropArgument)

  + [localAddress](https://bun.com/reference/node/net/DropArgument/localAddress)?: string
  + [localFamily](https://bun.com/reference/node/net/DropArgument/localFamily)?: string
  + [localPort](https://bun.com/reference/node/net/DropArgument/localPort)?: number
  + [remoteAddress](https://bun.com/reference/node/net/DropArgument/remoteAddress)?: string
  + [remoteFamily](https://bun.com/reference/node/net/DropArgument/remoteFamily)?: string
  + [remotePort](https://bun.com/reference/node/net/DropArgument/remotePort)?: number
* ### interface [IpcNetConnectOpts](https://bun.com/reference/node/net/IpcNetConnectOpts)

  + [allowHalfOpen](https://bun.com/reference/node/net/IpcNetConnectOpts/allowHalfOpen)?: boolean
  + [fd](https://bun.com/reference/node/net/IpcNetConnectOpts/fd)?: number
  + [onread](https://bun.com/reference/node/net/IpcNetConnectOpts/onread)?: [OnReadOpts](https://bun.com/reference/node/net/OnReadOpts)
  + [path](https://bun.com/reference/node/net/IpcNetConnectOpts/path): string
  + [readable](https://bun.com/reference/node/net/IpcNetConnectOpts/readable)?: boolean
  + [signal](https://bun.com/reference/node/net/IpcNetConnectOpts/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [timeout](https://bun.com/reference/node/net/IpcNetConnectOpts/timeout)?: number
  + [writable](https://bun.com/reference/node/net/IpcNetConnectOpts/writable)?: boolean
* ### interface [IpcSocketConnectOpts](https://bun.com/reference/node/net/IpcSocketConnectOpts)

  + [path](https://bun.com/reference/node/net/IpcSocketConnectOpts/path): string
* ### interface [ListenOptions](https://bun.com/reference/node/net/ListenOptions)

  + [backlog](https://bun.com/reference/node/net/ListenOptions/backlog)?: number
  + [exclusive](https://bun.com/reference/node/net/ListenOptions/exclusive)?: boolean
  + [host](https://bun.com/reference/node/net/ListenOptions/host)?: string
  + [ipv6Only](https://bun.com/reference/node/net/ListenOptions/ipv6Only)?: boolean
  + [path](https://bun.com/reference/node/net/ListenOptions/path)?: string
  + [port](https://bun.com/reference/node/net/ListenOptions/port)?: number
  + [readableAll](https://bun.com/reference/node/net/ListenOptions/readableAll)?: boolean
  + [reusePort](https://bun.com/reference/node/net/ListenOptions/reusePort)?: boolean
  + [signal](https://bun.com/reference/node/net/ListenOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [writableAll](https://bun.com/reference/node/net/ListenOptions/writableAll)?: boolean
* ### interface [OnReadOpts](https://bun.com/reference/node/net/OnReadOpts)

  + [buffer](https://bun.com/reference/node/net/OnReadOpts/buffer): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike> | () => [Uint8Array](https://bun.com/reference/globals/Uint8Array)
  + [callback](https://bun.com/reference/node/net/OnReadOpts/callback)(

    bytesWritten: number,

    buffer: [Uint8Array](https://bun.com/reference/globals/Uint8Array)

    ): boolean;

    This function is called for every chunk of incoming data. Two arguments are passed to it: the number of bytes written to `buffer` and a reference to `buffer`. Return `false` from this function to implicitly `pause()` the socket.
* ### interface [ServerOpts](https://bun.com/reference/node/net/ServerOpts)

  + [allowHalfOpen](https://bun.com/reference/node/net/ServerOpts/allowHalfOpen)?: boolean

    Indicates whether half-opened TCP connections are allowed.
  + [blockList](https://bun.com/reference/node/net/ServerOpts/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)

    `blockList` can be used for disabling inbound access to specific IP addresses, IP ranges, or IP subnets. This does not work if the server is behind a reverse proxy, NAT, etc. because the address checked against the block list is the address of the proxy, or the one specified by the NAT.
  + [highWaterMark](https://bun.com/reference/node/net/ServerOpts/highWaterMark)?: number

    Optionally overrides all `net.Socket`s' `readableHighWaterMark` and `writableHighWaterMark`.
  + [keepAlive](https://bun.com/reference/node/net/ServerOpts/keepAlive)?: boolean

    If set to `true`, it enables keep-alive functionality on the socket immediately after a new incoming connection is received, similarly on what is done in `socket.setKeepAlive([enable][, initialDelay])`.
  + [keepAliveInitialDelay](https://bun.com/reference/node/net/ServerOpts/keepAliveInitialDelay)?: number

    If set to a positive number, it sets the initial delay before the first keepalive probe is sent on an idle socket.
  + [noDelay](https://bun.com/reference/node/net/ServerOpts/noDelay)?: boolean

    If set to `true`, it disables the use of Nagle's algorithm immediately after a new incoming connection is received.
  + [pauseOnConnect](https://bun.com/reference/node/net/ServerOpts/pauseOnConnect)?: boolean

    Indicates whether the socket should be paused on incoming connections.
* ### interface [SocketAddressInitOptions](https://bun.com/reference/node/net/SocketAddressInitOptions)

  + [address](https://bun.com/reference/node/net/SocketAddressInitOptions/address)?: string

    The network address as either an IPv4 or IPv6 string.
  + [family](https://bun.com/reference/node/net/SocketAddressInitOptions/family)?: [IPVersion](https://bun.com/reference/node/net/IPVersion)
  + [flowlabel](https://bun.com/reference/node/net/SocketAddressInitOptions/flowlabel)?: number

    An IPv6 flow-label used only if `family` is `'ipv6'`.
  + [port](https://bun.com/reference/node/net/SocketAddressInitOptions/port)?: number

    An IP port.
* ### interface [SocketConstructorOpts](https://bun.com/reference/node/net/SocketConstructorOpts)

  + [allowHalfOpen](https://bun.com/reference/node/net/SocketConstructorOpts/allowHalfOpen)?: boolean
  + [fd](https://bun.com/reference/node/net/SocketConstructorOpts/fd)?: number
  + [onread](https://bun.com/reference/node/net/SocketConstructorOpts/onread)?: [OnReadOpts](https://bun.com/reference/node/net/OnReadOpts)
  + [readable](https://bun.com/reference/node/net/SocketConstructorOpts/readable)?: boolean
  + [signal](https://bun.com/reference/node/net/SocketConstructorOpts/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [writable](https://bun.com/reference/node/net/SocketConstructorOpts/writable)?: boolean
* ### interface [TcpNetConnectOpts](https://bun.com/reference/node/net/TcpNetConnectOpts)

  + [allowHalfOpen](https://bun.com/reference/node/net/TcpNetConnectOpts/allowHalfOpen)?: boolean
  + [autoSelectFamily](https://bun.com/reference/node/net/TcpNetConnectOpts/autoSelectFamily)?: boolean
  + [autoSelectFamilyAttemptTimeout](https://bun.com/reference/node/net/TcpNetConnectOpts/autoSelectFamilyAttemptTimeout)?: number
  + [blockList](https://bun.com/reference/node/net/TcpNetConnectOpts/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)
  + [family](https://bun.com/reference/node/net/TcpNetConnectOpts/family)?: number
  + [fd](https://bun.com/reference/node/net/TcpNetConnectOpts/fd)?: number
  + [hints](https://bun.com/reference/node/net/TcpNetConnectOpts/hints)?: number
  + [host](https://bun.com/reference/node/net/TcpNetConnectOpts/host)?: string
  + [keepAlive](https://bun.com/reference/node/net/TcpNetConnectOpts/keepAlive)?: boolean
  + [keepAliveInitialDelay](https://bun.com/reference/node/net/TcpNetConnectOpts/keepAliveInitialDelay)?: number
  + [localAddress](https://bun.com/reference/node/net/TcpNetConnectOpts/localAddress)?: string
  + [localPort](https://bun.com/reference/node/net/TcpNetConnectOpts/localPort)?: number
  + [lookup](https://bun.com/reference/node/net/TcpNetConnectOpts/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [noDelay](https://bun.com/reference/node/net/TcpNetConnectOpts/noDelay)?: boolean
  + [onread](https://bun.com/reference/node/net/TcpNetConnectOpts/onread)?: [OnReadOpts](https://bun.com/reference/node/net/OnReadOpts)
  + [port](https://bun.com/reference/node/net/TcpNetConnectOpts/port): number
  + [readable](https://bun.com/reference/node/net/TcpNetConnectOpts/readable)?: boolean
  + [signal](https://bun.com/reference/node/net/TcpNetConnectOpts/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [timeout](https://bun.com/reference/node/net/TcpNetConnectOpts/timeout)?: number
  + [writable](https://bun.com/reference/node/net/TcpNetConnectOpts/writable)?: boolean
* ### interface [TcpSocketConnectOpts](https://bun.com/reference/node/net/TcpSocketConnectOpts)

  + [autoSelectFamily](https://bun.com/reference/node/net/TcpSocketConnectOpts/autoSelectFamily)?: boolean
  + [autoSelectFamilyAttemptTimeout](https://bun.com/reference/node/net/TcpSocketConnectOpts/autoSelectFamilyAttemptTimeout)?: number
  + [blockList](https://bun.com/reference/node/net/TcpSocketConnectOpts/blockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)
  + [family](https://bun.com/reference/node/net/TcpSocketConnectOpts/family)?: number
  + [hints](https://bun.com/reference/node/net/TcpSocketConnectOpts/hints)?: number
  + [host](https://bun.com/reference/node/net/TcpSocketConnectOpts/host)?: string
  + [keepAlive](https://bun.com/reference/node/net/TcpSocketConnectOpts/keepAlive)?: boolean
  + [keepAliveInitialDelay](https://bun.com/reference/node/net/TcpSocketConnectOpts/keepAliveInitialDelay)?: number
  + [localAddress](https://bun.com/reference/node/net/TcpSocketConnectOpts/localAddress)?: string
  + [localPort](https://bun.com/reference/node/net/TcpSocketConnectOpts/localPort)?: number
  + [lookup](https://bun.com/reference/node/net/TcpSocketConnectOpts/lookup)?: [LookupFunction](https://bun.com/reference/node/net/LookupFunction)
  + [noDelay](https://bun.com/reference/node/net/TcpSocketConnectOpts/noDelay)?: boolean
  + [port](https://bun.com/reference/node/net/TcpSocketConnectOpts/port): number
* type [IPVersion](https://bun.com/reference/node/net/IPVersion) = 'ipv4' | 'ipv6'
* type [LookupFunction](https://bun.com/reference/node/net/LookupFunction) = (hostname: string, options: [dns.LookupOptions](https://bun.com/reference/node/dns/LookupOptions), callback: (err: NodeJS.ErrnoException | null, address: string | [dns.LookupAddress](https://bun.com/reference/node/dns/LookupAddress)[], family?: number) => void) => void
* type [NetConnectOpts](https://bun.com/reference/node/net/NetConnectOpts) = [TcpNetConnectOpts](https://bun.com/reference/node/net/TcpNetConnectOpts) | [IpcNetConnectOpts](https://bun.com/reference/node/net/IpcNetConnectOpts)
* type [SocketConnectOpts](https://bun.com/reference/node/net/SocketConnectOpts) = [TcpSocketConnectOpts](https://bun.com/reference/node/net/TcpSocketConnectOpts) | [IpcSocketConnectOpts](https://bun.com/reference/node/net/IpcSocketConnectOpts)
* type [SocketReadyState](https://bun.com/reference/node/net/SocketReadyState) = 'opening' | 'open' | 'readOnly' | 'writeOnly' | 'closed'