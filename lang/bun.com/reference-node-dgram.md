---
url: https://bun.com/reference/node/dgram
title: Node.js dgram module | API Reference | Bun
source_domain: bun.com
---

# Node.js dgram module | API Reference | Bun

Node.js module

# [dgram](https://bun.com/reference/node/dgram)

The `'node:dgram'` module provides an implementation of UDP datagram sockets. It allows sending and receiving UDP packets, creating both IPv4 and IPv6 sockets.

This module is used for lightweight, connectionless communication, such as DNS queries, syslog, and real-time streaming protocols that favor speed over reliability.

Works in Bun

Fully implemented. > 90% of Node.js's test suite passes.

* ### class [Socket](https://bun.com/reference/node/dgram/Socket)

  Encapsulates the datagram functionality.

  New instances of `dgram.Socket` are created using createSocket. The `new` keyword is not to be used to create `dgram.Socket` instances.

  + static [captureRejections](https://bun.com/reference/node/dgram/Socket/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/dgram/Socket/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/dgram/Socket/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/dgram/Socket/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/dgram/Socket/[asyncDispose])(): Promise<void>;

    Calls `socket.close()` and returns a promise that fulfills when the socket has closed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/dgram/Socket/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/dgram/Socket/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. error
    4. listening
    5. message

    [addListener](https://bun.com/reference/node/dgram/Socket/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. error
    4. listening
    5. message

    [addListener](https://bun.com/reference/node/dgram/Socket/addListener)(

    event: 'connect',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. error
    4. listening
    5. message

    [addListener](https://bun.com/reference/node/dgram/Socket/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. error
    4. listening
    5. message

    [addListener](https://bun.com/reference/node/dgram/Socket/addListener)(

    event: 'listening',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. error
    4. listening
    5. message

    [addListener](https://bun.com/reference/node/dgram/Socket/addListener)(

    event: 'message',

    listener: (msg: NonSharedBuffer, rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)) => void

    ): this;

    events.EventEmitter

    1. close
    2. connect
    3. error
    4. listening
    5. message
  + [addMembership](https://bun.com/reference/node/dgram/Socket/addMembership)(

    multicastAddress: string,

    multicastInterface?: string

    ): void;

    Tells the kernel to join a multicast group at the given `multicastAddress` and `multicastInterface` using the `IP_ADD_MEMBERSHIP` socket option. If the `multicastInterface` argument is not specified, the operating system will choose one interface and will add membership to it. To add membership to every available interface, call `addMembership` multiple times, once per interface.

    When called on an unbound socket, this method will implicitly bind to a random port, listening on all interfaces.

    When sharing a UDP socket across multiple `cluster` workers, the`socket.addMembership()` function must be called only once or an`EADDRINUSE` error will occur:

    ```
    import cluster from 'node:cluster';
    import dgram from 'node:dgram';

    if (cluster.isPrimary) {
      cluster.fork(); // Works ok.
      cluster.fork(); // Fails with EADDRINUSE.
    } else {
      const s = dgram.createSocket('udp4');
      s.bind(1234, () => {
        s.addMembership('224.0.0.114');
      });
    }
    ```
  + [address](https://bun.com/reference/node/dgram/Socket/address)(): [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

    Returns an object containing the address information for a socket. For UDP sockets, this object will contain `address`, `family`, and `port` properties.

    This method throws `EBADF` if called on an unbound socket.
  + [addSourceSpecificMembership](https://bun.com/reference/node/dgram/Socket/addSourceSpecificMembership)(

    sourceAddress: string,

    groupAddress: string,

    multicastInterface?: string

    ): void;

    Tells the kernel to join a source-specific multicast channel at the given `sourceAddress` and `groupAddress`, using the `multicastInterface` with the `IP_ADD_SOURCE_MEMBERSHIP` socket option. If the `multicastInterface` argument is not specified, the operating system will choose one interface and will add membership to it. To add membership to every available interface, call `socket.addSourceSpecificMembership()` multiple times, once per interface.

    When called on an unbound socket, this method will implicitly bind to a random port, listening on all interfaces.
  + [bind](https://bun.com/reference/node/dgram/Socket/bind)(

    port?: number,

    address?: string,

    callback?: () => void

    ): this;

    For UDP sockets, causes the `dgram.Socket` to listen for datagram messages on a named `port` and optional `address`. If `port` is not specified or is `0`, the operating system will attempt to bind to a random port. If `address` is not specified, the operating system will attempt to listen on all addresses. Once binding is complete, a `'listening'` event is emitted and the optional `callback` function is called.

    Specifying both a `'listening'` event listener and passing a `callback` to the `socket.bind()` method is not harmful but not very useful.

    A bound datagram socket keeps the Node.js process running to receive datagram messages.

    If binding fails, an `'error'` event is generated. In rare case (e.g. attempting to bind with a closed socket), an `Error` may be thrown.

    Example of a UDP server listening on port 41234:

    ```
    import dgram from 'node:dgram';

    const server = dgram.createSocket('udp4');

    server.on('error', (err) => {
      console.error(`server error:\n${err.stack}`);
      server.close();
    });

    server.on('message', (msg, rinfo) => {
      console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
    });

    server.on('listening', () => {
      const address = server.address();
      console.log(`server listening ${address.address}:${address.port}`);
    });

    server.bind(41234);
    // Prints: server listening 0.0.0.0:41234
    ```

    @param callback

    with no parameters. Called when binding is complete.

    [bind](https://bun.com/reference/node/dgram/Socket/bind)(

    port?: number,

    callback?: () => void

    ): this;

    For UDP sockets, causes the `dgram.Socket` to listen for datagram messages on a named `port` and optional `address`. If `port` is not specified or is `0`, the operating system will attempt to bind to a random port. If `address` is not specified, the operating system will attempt to listen on all addresses. Once binding is complete, a `'listening'` event is emitted and the optional `callback` function is called.

    Specifying both a `'listening'` event listener and passing a `callback` to the `socket.bind()` method is not harmful but not very useful.

    A bound datagram socket keeps the Node.js process running to receive datagram messages.

    If binding fails, an `'error'` event is generated. In rare case (e.g. attempting to bind with a closed socket), an `Error` may be thrown.

    Example of a UDP server listening on port 41234:

    ```
    import dgram from 'node:dgram';

    const server = dgram.createSocket('udp4');

    server.on('error', (err) => {
      console.error(`server error:\n${err.stack}`);
      server.close();
    });

    server.on('message', (msg, rinfo) => {
      console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
    });

    server.on('listening', () => {
      const address = server.address();
      console.log(`server listening ${address.address}:${address.port}`);
    });

    server.bind(41234);
    // Prints: server listening 0.0.0.0:41234
    ```

    @param callback

    with no parameters. Called when binding is complete.

    [bind](https://bun.com/reference/node/dgram/Socket/bind)(

    callback?: () => void

    ): this;

    For UDP sockets, causes the `dgram.Socket` to listen for datagram messages on a named `port` and optional `address`. If `port` is not specified or is `0`, the operating system will attempt to bind to a random port. If `address` is not specified, the operating system will attempt to listen on all addresses. Once binding is complete, a `'listening'` event is emitted and the optional `callback` function is called.

    Specifying both a `'listening'` event listener and passing a `callback` to the `socket.bind()` method is not harmful but not very useful.

    A bound datagram socket keeps the Node.js process running to receive datagram messages.

    If binding fails, an `'error'` event is generated. In rare case (e.g. attempting to bind with a closed socket), an `Error` may be thrown.

    Example of a UDP server listening on port 41234:

    ```
    import dgram from 'node:dgram';

    const server = dgram.createSocket('udp4');

    server.on('error', (err) => {
      console.error(`server error:\n${err.stack}`);
      server.close();
    });

    server.on('message', (msg, rinfo) => {
      console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
    });

    server.on('listening', () => {
      const address = server.address();
      console.log(`server listening ${address.address}:${address.port}`);
    });

    server.bind(41234);
    // Prints: server listening 0.0.0.0:41234
    ```

    @param callback

    with no parameters. Called when binding is complete.

    [bind](https://bun.com/reference/node/dgram/Socket/bind)(

    options: [BindOptions](https://bun.com/reference/node/dgram/BindOptions),

    callback?: () => void

    ): this;

    For UDP sockets, causes the `dgram.Socket` to listen for datagram messages on a named `port` and optional `address`. If `port` is not specified or is `0`, the operating system will attempt to bind to a random port. If `address` is not specified, the operating system will attempt to listen on all addresses. Once binding is complete, a `'listening'` event is emitted and the optional `callback` function is called.

    Specifying both a `'listening'` event listener and passing a `callback` to the `socket.bind()` method is not harmful but not very useful.

    A bound datagram socket keeps the Node.js process running to receive datagram messages.

    If binding fails, an `'error'` event is generated. In rare case (e.g. attempting to bind with a closed socket), an `Error` may be thrown.

    Example of a UDP server listening on port 41234:

    ```
    import dgram from 'node:dgram';

    const server = dgram.createSocket('udp4');

    server.on('error', (err) => {
      console.error(`server error:\n${err.stack}`);
      server.close();
    });

    server.on('message', (msg, rinfo) => {
      console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
    });

    server.on('listening', () => {
      const address = server.address();
      console.log(`server listening ${address.address}:${address.port}`);
    });

    server.bind(41234);
    // Prints: server listening 0.0.0.0:41234
    ```

    @param callback

    with no parameters. Called when binding is complete.
  + [close](https://bun.com/reference/node/dgram/Socket/close)(

    callback?: () => void

    ): this;

    Close the underlying socket and stop listening for data on it. If a callback is provided, it is added as a listener for the `'close'` event.

    @param callback

    Called when the socket has been closed.
  + [connect](https://bun.com/reference/node/dgram/Socket/connect)(

    port: number,

    address?: string,

    callback?: () => void

    ): void;

    Associates the `dgram.Socket` to a remote address and port. Every message sent by this handle is automatically sent to that destination. Also, the socket will only receive messages from that remote peer. Trying to call `connect()` on an already connected socket will result in an `ERR_SOCKET_DGRAM_IS_CONNECTED` exception. If `address` is not provided, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default. Once the connection is complete, a `'connect'` event is emitted and the optional `callback` function is called. In case of failure, the `callback` is called or, failing this, an `'error'` event is emitted.

    @param callback

    Called when the connection is completed or on error.

    [connect](https://bun.com/reference/node/dgram/Socket/connect)(

    port: number,

    callback: () => void

    ): void;

    Associates the `dgram.Socket` to a remote address and port. Every message sent by this handle is automatically sent to that destination. Also, the socket will only receive messages from that remote peer. Trying to call `connect()` on an already connected socket will result in an `ERR_SOCKET_DGRAM_IS_CONNECTED` exception. If `address` is not provided, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default. Once the connection is complete, a `'connect'` event is emitted and the optional `callback` function is called. In case of failure, the `callback` is called or, failing this, an `'error'` event is emitted.

    @param callback

    Called when the connection is completed or on error.
  + [disconnect](https://bun.com/reference/node/dgram/Socket/disconnect)(): void;

    A synchronous function that disassociates a connected `dgram.Socket` from its remote address. Trying to call `disconnect()` on an unbound or already disconnected socket will result in an `ERR_SOCKET_DGRAM_NOT_CONNECTED` exception.
  + [dropMembership](https://bun.com/reference/node/dgram/Socket/dropMembership)(

    multicastAddress: string,

    multicastInterface?: string

    ): void;

    Instructs the kernel to leave a multicast group at `multicastAddress` using the `IP_DROP_MEMBERSHIP` socket option. This method is automatically called by the kernel when the socket is closed or the process terminates, so most apps will never have reason to call this.

    If `multicastInterface` is not specified, the operating system will attempt to drop membership on all valid interfaces.
  + [dropSourceSpecificMembership](https://bun.com/reference/node/dgram/Socket/dropSourceSpecificMembership)(

    sourceAddress: string,

    groupAddress: string,

    multicastInterface?: string

    ): void;

    Instructs the kernel to leave a source-specific multicast channel at the given `sourceAddress` and `groupAddress` using the `IP_DROP_SOURCE_MEMBERSHIP` socket option. This method is automatically called by the kernel when the socket is closed or the process terminates, so most apps will never have reason to call this.

    If `multicastInterface` is not specified, the operating system will attempt to drop membership on all valid interfaces.
  + [emit](https://bun.com/reference/node/dgram/Socket/emit)(

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

    [emit](https://bun.com/reference/node/dgram/Socket/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/dgram/Socket/emit)(

    event: 'connect'

    ): boolean;

    [emit](https://bun.com/reference/node/dgram/Socket/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/dgram/Socket/emit)(

    event: 'listening'

    ): boolean;

    [emit](https://bun.com/reference/node/dgram/Socket/emit)(

    event: 'message',

    msg: NonSharedBuffer,

    rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)

    ): boolean;
  + [eventNames](https://bun.com/reference/node/dgram/Socket/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/dgram/Socket/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getRecvBufferSize](https://bun.com/reference/node/dgram/Socket/getRecvBufferSize)(): number;

    This method throws `ERR_SOCKET_BUFFER_SIZE` if called on an unbound socket.

    @returns

    the `SO_RCVBUF` socket receive buffer size in bytes.
  + [getSendBufferSize](https://bun.com/reference/node/dgram/Socket/getSendBufferSize)(): number;

    This method throws `ERR_SOCKET_BUFFER_SIZE` if called on an unbound socket.

    @returns

    the `SO_SNDBUF` socket send buffer size in bytes.
  + [getSendQueueCount](https://bun.com/reference/node/dgram/Socket/getSendQueueCount)(): number;

    @returns

    Number of send requests currently in the queue awaiting to be processed.
  + [getSendQueueSize](https://bun.com/reference/node/dgram/Socket/getSendQueueSize)(): number;

    @returns

    Number of bytes queued for sending.
  + [listenerCount](https://bun.com/reference/node/dgram/Socket/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/dgram/Socket/listeners)<K>(

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
  + [off](https://bun.com/reference/node/dgram/Socket/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/dgram/Socket/on)(

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

    [on](https://bun.com/reference/node/dgram/Socket/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/dgram/Socket/on)(

    event: 'connect',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/dgram/Socket/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/dgram/Socket/on)(

    event: 'listening',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/dgram/Socket/on)(

    event: 'message',

    listener: (msg: NonSharedBuffer, rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)) => void

    ): this;
  + [once](https://bun.com/reference/node/dgram/Socket/once)(

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

    [once](https://bun.com/reference/node/dgram/Socket/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/dgram/Socket/once)(

    event: 'connect',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/dgram/Socket/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/dgram/Socket/once)(

    event: 'listening',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/dgram/Socket/once)(

    event: 'message',

    listener: (msg: NonSharedBuffer, rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)) => void

    ): this;
  + [prependListener](https://bun.com/reference/node/dgram/Socket/prependListener)(

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

    [prependListener](https://bun.com/reference/node/dgram/Socket/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/dgram/Socket/prependListener)(

    event: 'connect',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/dgram/Socket/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/dgram/Socket/prependListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/dgram/Socket/prependListener)(

    event: 'message',

    listener: (msg: NonSharedBuffer, rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/dgram/Socket/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/dgram/Socket/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/dgram/Socket/prependOnceListener)(

    event: 'connect',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/dgram/Socket/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/dgram/Socket/prependOnceListener)(

    event: 'listening',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/dgram/Socket/prependOnceListener)(

    event: 'message',

    listener: (msg: NonSharedBuffer, rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)) => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/dgram/Socket/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/dgram/Socket/ref)(): this;

    By default, binding a socket will cause it to block the Node.js process from exiting as long as the socket is open. The `socket.unref()` method can be used to exclude the socket from the reference counting that keeps the Node.js process active. The `socket.ref()` method adds the socket back to the reference counting and restores the default behavior.

    Calling `socket.ref()` multiples times will have no additional effect.

    The `socket.ref()` method returns a reference to the socket so calls can be chained.
  + [remoteAddress](https://bun.com/reference/node/dgram/Socket/remoteAddress)(): [AddressInfo](https://bun.com/reference/node/net/AddressInfo);

    Returns an object containing the `address`, `family`, and `port` of the remote endpoint. This method throws an `ERR_SOCKET_DGRAM_NOT_CONNECTED` exception if the socket is not connected.
  + [removeAllListeners](https://bun.com/reference/node/dgram/Socket/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/dgram/Socket/removeListener)<K>(

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
  + [send](https://bun.com/reference/node/dgram/Socket/send)(

    msg: string | readonly any[] | ArrayBufferView<ArrayBufferLike>,

    port?: number,

    address?: string,

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error), bytes: number) => void

    ): void;

    Broadcasts a datagram on the socket. For connectionless sockets, the destination `port` and `address` must be specified. Connected sockets, on the other hand, will use their associated remote endpoint, so the `port` and `address` arguments must not be set.

    The `msg` argument contains the message to be sent. Depending on its type, different behavior can apply. If `msg` is a `Buffer`, any `TypedArray` or a `DataView`, the `offset` and `length` specify the offset within the `Buffer` where the message begins and the number of bytes in the message, respectively. If `msg` is a `String`, then it is automatically converted to a `Buffer` with `'utf8'` encoding. With messages that contain multi-byte characters, `offset` and `length` will be calculated with respect to `byte length` and not the character position. If `msg` is an array, `offset` and `length` must not be specified.

    The `address` argument is a string. If the value of `address` is a host name, DNS will be used to resolve the address of the host. If `address` is not provided or otherwise nullish, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default.

    If the socket has not been previously bound with a call to `bind`, the socket is assigned a random port number and is bound to the "all interfaces" address (`'0.0.0.0'` for `udp4` sockets, `'::0'` for `udp6` sockets.)

    An optional `callback` function may be specified to as a way of reporting DNS errors or for determining when it is safe to reuse the `buf` object. DNS lookups delay the time to send for at least one tick of the Node.js event loop.

    The only way to know for sure that the datagram has been sent is by using a `callback`. If an error occurs and a `callback` is given, the error will be passed as the first argument to the `callback`. If a `callback` is not given, the error is emitted as an `'error'` event on the `socket` object.

    Offset and length are optional but both *must* be set if either are used. They are supported only when the first argument is a `Buffer`, a `TypedArray`, or a `DataView`.

    This method throws `ERR_SOCKET_BAD_PORT` if called on an unbound socket.

    Example of sending a UDP packet to a port on `localhost`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.send(message, 41234, 'localhost', (err) => {
      client.close();
    });
    ```

    Example of sending a UDP packet composed of multiple buffers to a port on`127.0.0.1`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('Some ');
    const buf2 = Buffer.from('bytes');
    const client = dgram.createSocket('udp4');
    client.send([buf1, buf2], 41234, (err) => {
      client.close();
    });
    ```

    Sending multiple buffers might be faster or slower depending on the application and operating system. Run benchmarks to determine the optimal strategy on a case-by-case basis. Generally speaking, however, sending multiple buffers is faster.

    Example of sending a UDP packet using a socket connected to a port on `localhost`:

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.connect(41234, 'localhost', (err) => {
      client.send(message, (err) => {
        client.close();
      });
    });
    ```

    @param msg

    Message to be sent.

    @param port

    Destination port.

    @param address

    Destination host name or IP address.

    @param callback

    Called when the message has been sent.

    [send](https://bun.com/reference/node/dgram/Socket/send)(

    msg: string | readonly any[] | ArrayBufferView<ArrayBufferLike>,

    port?: number,

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error), bytes: number) => void

    ): void;

    Broadcasts a datagram on the socket. For connectionless sockets, the destination `port` and `address` must be specified. Connected sockets, on the other hand, will use their associated remote endpoint, so the `port` and `address` arguments must not be set.

    The `msg` argument contains the message to be sent. Depending on its type, different behavior can apply. If `msg` is a `Buffer`, any `TypedArray` or a `DataView`, the `offset` and `length` specify the offset within the `Buffer` where the message begins and the number of bytes in the message, respectively. If `msg` is a `String`, then it is automatically converted to a `Buffer` with `'utf8'` encoding. With messages that contain multi-byte characters, `offset` and `length` will be calculated with respect to `byte length` and not the character position. If `msg` is an array, `offset` and `length` must not be specified.

    The `address` argument is a string. If the value of `address` is a host name, DNS will be used to resolve the address of the host. If `address` is not provided or otherwise nullish, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default.

    If the socket has not been previously bound with a call to `bind`, the socket is assigned a random port number and is bound to the "all interfaces" address (`'0.0.0.0'` for `udp4` sockets, `'::0'` for `udp6` sockets.)

    An optional `callback` function may be specified to as a way of reporting DNS errors or for determining when it is safe to reuse the `buf` object. DNS lookups delay the time to send for at least one tick of the Node.js event loop.

    The only way to know for sure that the datagram has been sent is by using a `callback`. If an error occurs and a `callback` is given, the error will be passed as the first argument to the `callback`. If a `callback` is not given, the error is emitted as an `'error'` event on the `socket` object.

    Offset and length are optional but both *must* be set if either are used. They are supported only when the first argument is a `Buffer`, a `TypedArray`, or a `DataView`.

    This method throws `ERR_SOCKET_BAD_PORT` if called on an unbound socket.

    Example of sending a UDP packet to a port on `localhost`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.send(message, 41234, 'localhost', (err) => {
      client.close();
    });
    ```

    Example of sending a UDP packet composed of multiple buffers to a port on`127.0.0.1`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('Some ');
    const buf2 = Buffer.from('bytes');
    const client = dgram.createSocket('udp4');
    client.send([buf1, buf2], 41234, (err) => {
      client.close();
    });
    ```

    Sending multiple buffers might be faster or slower depending on the application and operating system. Run benchmarks to determine the optimal strategy on a case-by-case basis. Generally speaking, however, sending multiple buffers is faster.

    Example of sending a UDP packet using a socket connected to a port on `localhost`:

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.connect(41234, 'localhost', (err) => {
      client.send(message, (err) => {
        client.close();
      });
    });
    ```

    @param msg

    Message to be sent.

    @param port

    Destination port.

    @param callback

    Called when the message has been sent.

    [send](https://bun.com/reference/node/dgram/Socket/send)(

    msg: string | readonly any[] | ArrayBufferView<ArrayBufferLike>,

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error), bytes: number) => void

    ): void;

    Broadcasts a datagram on the socket. For connectionless sockets, the destination `port` and `address` must be specified. Connected sockets, on the other hand, will use their associated remote endpoint, so the `port` and `address` arguments must not be set.

    The `msg` argument contains the message to be sent. Depending on its type, different behavior can apply. If `msg` is a `Buffer`, any `TypedArray` or a `DataView`, the `offset` and `length` specify the offset within the `Buffer` where the message begins and the number of bytes in the message, respectively. If `msg` is a `String`, then it is automatically converted to a `Buffer` with `'utf8'` encoding. With messages that contain multi-byte characters, `offset` and `length` will be calculated with respect to `byte length` and not the character position. If `msg` is an array, `offset` and `length` must not be specified.

    The `address` argument is a string. If the value of `address` is a host name, DNS will be used to resolve the address of the host. If `address` is not provided or otherwise nullish, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default.

    If the socket has not been previously bound with a call to `bind`, the socket is assigned a random port number and is bound to the "all interfaces" address (`'0.0.0.0'` for `udp4` sockets, `'::0'` for `udp6` sockets.)

    An optional `callback` function may be specified to as a way of reporting DNS errors or for determining when it is safe to reuse the `buf` object. DNS lookups delay the time to send for at least one tick of the Node.js event loop.

    The only way to know for sure that the datagram has been sent is by using a `callback`. If an error occurs and a `callback` is given, the error will be passed as the first argument to the `callback`. If a `callback` is not given, the error is emitted as an `'error'` event on the `socket` object.

    Offset and length are optional but both *must* be set if either are used. They are supported only when the first argument is a `Buffer`, a `TypedArray`, or a `DataView`.

    This method throws `ERR_SOCKET_BAD_PORT` if called on an unbound socket.

    Example of sending a UDP packet to a port on `localhost`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.send(message, 41234, 'localhost', (err) => {
      client.close();
    });
    ```

    Example of sending a UDP packet composed of multiple buffers to a port on`127.0.0.1`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('Some ');
    const buf2 = Buffer.from('bytes');
    const client = dgram.createSocket('udp4');
    client.send([buf1, buf2], 41234, (err) => {
      client.close();
    });
    ```

    Sending multiple buffers might be faster or slower depending on the application and operating system. Run benchmarks to determine the optimal strategy on a case-by-case basis. Generally speaking, however, sending multiple buffers is faster.

    Example of sending a UDP packet using a socket connected to a port on `localhost`:

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.connect(41234, 'localhost', (err) => {
      client.send(message, (err) => {
        client.close();
      });
    });
    ```

    @param msg

    Message to be sent.

    @param callback

    Called when the message has been sent.

    [send](https://bun.com/reference/node/dgram/Socket/send)(

    msg: string | ArrayBufferView<ArrayBufferLike>,

    offset: number,

    length: number,

    port?: number,

    address?: string,

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error), bytes: number) => void

    ): void;

    Broadcasts a datagram on the socket. For connectionless sockets, the destination `port` and `address` must be specified. Connected sockets, on the other hand, will use their associated remote endpoint, so the `port` and `address` arguments must not be set.

    The `msg` argument contains the message to be sent. Depending on its type, different behavior can apply. If `msg` is a `Buffer`, any `TypedArray` or a `DataView`, the `offset` and `length` specify the offset within the `Buffer` where the message begins and the number of bytes in the message, respectively. If `msg` is a `String`, then it is automatically converted to a `Buffer` with `'utf8'` encoding. With messages that contain multi-byte characters, `offset` and `length` will be calculated with respect to `byte length` and not the character position. If `msg` is an array, `offset` and `length` must not be specified.

    The `address` argument is a string. If the value of `address` is a host name, DNS will be used to resolve the address of the host. If `address` is not provided or otherwise nullish, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default.

    If the socket has not been previously bound with a call to `bind`, the socket is assigned a random port number and is bound to the "all interfaces" address (`'0.0.0.0'` for `udp4` sockets, `'::0'` for `udp6` sockets.)

    An optional `callback` function may be specified to as a way of reporting DNS errors or for determining when it is safe to reuse the `buf` object. DNS lookups delay the time to send for at least one tick of the Node.js event loop.

    The only way to know for sure that the datagram has been sent is by using a `callback`. If an error occurs and a `callback` is given, the error will be passed as the first argument to the `callback`. If a `callback` is not given, the error is emitted as an `'error'` event on the `socket` object.

    Offset and length are optional but both *must* be set if either are used. They are supported only when the first argument is a `Buffer`, a `TypedArray`, or a `DataView`.

    This method throws `ERR_SOCKET_BAD_PORT` if called on an unbound socket.

    Example of sending a UDP packet to a port on `localhost`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.send(message, 41234, 'localhost', (err) => {
      client.close();
    });
    ```

    Example of sending a UDP packet composed of multiple buffers to a port on`127.0.0.1`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('Some ');
    const buf2 = Buffer.from('bytes');
    const client = dgram.createSocket('udp4');
    client.send([buf1, buf2], 41234, (err) => {
      client.close();
    });
    ```

    Sending multiple buffers might be faster or slower depending on the application and operating system. Run benchmarks to determine the optimal strategy on a case-by-case basis. Generally speaking, however, sending multiple buffers is faster.

    Example of sending a UDP packet using a socket connected to a port on `localhost`:

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.connect(41234, 'localhost', (err) => {
      client.send(message, (err) => {
        client.close();
      });
    });
    ```

    @param msg

    Message to be sent.

    @param offset

    Offset in the buffer where the message starts.

    @param length

    Number of bytes in the message.

    @param port

    Destination port.

    @param address

    Destination host name or IP address.

    @param callback

    Called when the message has been sent.

    [send](https://bun.com/reference/node/dgram/Socket/send)(

    msg: string | ArrayBufferView<ArrayBufferLike>,

    offset: number,

    length: number,

    port?: number,

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error), bytes: number) => void

    ): void;

    Broadcasts a datagram on the socket. For connectionless sockets, the destination `port` and `address` must be specified. Connected sockets, on the other hand, will use their associated remote endpoint, so the `port` and `address` arguments must not be set.

    The `msg` argument contains the message to be sent. Depending on its type, different behavior can apply. If `msg` is a `Buffer`, any `TypedArray` or a `DataView`, the `offset` and `length` specify the offset within the `Buffer` where the message begins and the number of bytes in the message, respectively. If `msg` is a `String`, then it is automatically converted to a `Buffer` with `'utf8'` encoding. With messages that contain multi-byte characters, `offset` and `length` will be calculated with respect to `byte length` and not the character position. If `msg` is an array, `offset` and `length` must not be specified.

    The `address` argument is a string. If the value of `address` is a host name, DNS will be used to resolve the address of the host. If `address` is not provided or otherwise nullish, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default.

    If the socket has not been previously bound with a call to `bind`, the socket is assigned a random port number and is bound to the "all interfaces" address (`'0.0.0.0'` for `udp4` sockets, `'::0'` for `udp6` sockets.)

    An optional `callback` function may be specified to as a way of reporting DNS errors or for determining when it is safe to reuse the `buf` object. DNS lookups delay the time to send for at least one tick of the Node.js event loop.

    The only way to know for sure that the datagram has been sent is by using a `callback`. If an error occurs and a `callback` is given, the error will be passed as the first argument to the `callback`. If a `callback` is not given, the error is emitted as an `'error'` event on the `socket` object.

    Offset and length are optional but both *must* be set if either are used. They are supported only when the first argument is a `Buffer`, a `TypedArray`, or a `DataView`.

    This method throws `ERR_SOCKET_BAD_PORT` if called on an unbound socket.

    Example of sending a UDP packet to a port on `localhost`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.send(message, 41234, 'localhost', (err) => {
      client.close();
    });
    ```

    Example of sending a UDP packet composed of multiple buffers to a port on`127.0.0.1`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('Some ');
    const buf2 = Buffer.from('bytes');
    const client = dgram.createSocket('udp4');
    client.send([buf1, buf2], 41234, (err) => {
      client.close();
    });
    ```

    Sending multiple buffers might be faster or slower depending on the application and operating system. Run benchmarks to determine the optimal strategy on a case-by-case basis. Generally speaking, however, sending multiple buffers is faster.

    Example of sending a UDP packet using a socket connected to a port on `localhost`:

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.connect(41234, 'localhost', (err) => {
      client.send(message, (err) => {
        client.close();
      });
    });
    ```

    @param msg

    Message to be sent.

    @param offset

    Offset in the buffer where the message starts.

    @param length

    Number of bytes in the message.

    @param port

    Destination port.

    @param callback

    Called when the message has been sent.

    [send](https://bun.com/reference/node/dgram/Socket/send)(

    msg: string | ArrayBufferView<ArrayBufferLike>,

    offset: number,

    length: number,

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error), bytes: number) => void

    ): void;

    Broadcasts a datagram on the socket. For connectionless sockets, the destination `port` and `address` must be specified. Connected sockets, on the other hand, will use their associated remote endpoint, so the `port` and `address` arguments must not be set.

    The `msg` argument contains the message to be sent. Depending on its type, different behavior can apply. If `msg` is a `Buffer`, any `TypedArray` or a `DataView`, the `offset` and `length` specify the offset within the `Buffer` where the message begins and the number of bytes in the message, respectively. If `msg` is a `String`, then it is automatically converted to a `Buffer` with `'utf8'` encoding. With messages that contain multi-byte characters, `offset` and `length` will be calculated with respect to `byte length` and not the character position. If `msg` is an array, `offset` and `length` must not be specified.

    The `address` argument is a string. If the value of `address` is a host name, DNS will be used to resolve the address of the host. If `address` is not provided or otherwise nullish, `'127.0.0.1'` (for `udp4` sockets) or `'::1'` (for `udp6` sockets) will be used by default.

    If the socket has not been previously bound with a call to `bind`, the socket is assigned a random port number and is bound to the "all interfaces" address (`'0.0.0.0'` for `udp4` sockets, `'::0'` for `udp6` sockets.)

    An optional `callback` function may be specified to as a way of reporting DNS errors or for determining when it is safe to reuse the `buf` object. DNS lookups delay the time to send for at least one tick of the Node.js event loop.

    The only way to know for sure that the datagram has been sent is by using a `callback`. If an error occurs and a `callback` is given, the error will be passed as the first argument to the `callback`. If a `callback` is not given, the error is emitted as an `'error'` event on the `socket` object.

    Offset and length are optional but both *must* be set if either are used. They are supported only when the first argument is a `Buffer`, a `TypedArray`, or a `DataView`.

    This method throws `ERR_SOCKET_BAD_PORT` if called on an unbound socket.

    Example of sending a UDP packet to a port on `localhost`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.send(message, 41234, 'localhost', (err) => {
      client.close();
    });
    ```

    Example of sending a UDP packet composed of multiple buffers to a port on`127.0.0.1`;

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('Some ');
    const buf2 = Buffer.from('bytes');
    const client = dgram.createSocket('udp4');
    client.send([buf1, buf2], 41234, (err) => {
      client.close();
    });
    ```

    Sending multiple buffers might be faster or slower depending on the application and operating system. Run benchmarks to determine the optimal strategy on a case-by-case basis. Generally speaking, however, sending multiple buffers is faster.

    Example of sending a UDP packet using a socket connected to a port on `localhost`:

    ```
    import dgram from 'node:dgram';
    import { Buffer } from 'node:buffer';

    const message = Buffer.from('Some bytes');
    const client = dgram.createSocket('udp4');
    client.connect(41234, 'localhost', (err) => {
      client.send(message, (err) => {
        client.close();
      });
    });
    ```

    @param msg

    Message to be sent.

    @param offset

    Offset in the buffer where the message starts.

    @param length

    Number of bytes in the message.

    @param callback

    Called when the message has been sent.
  + [setBroadcast](https://bun.com/reference/node/dgram/Socket/setBroadcast)(

    flag: boolean

    ): void;

    Sets or clears the `SO_BROADCAST` socket option. When set to `true`, UDP packets may be sent to a local interface's broadcast address.

    This method throws `EBADF` if called on an unbound socket.
  + [setMaxListeners](https://bun.com/reference/node/dgram/Socket/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setMulticastInterface](https://bun.com/reference/node/dgram/Socket/setMulticastInterface)(

    multicastInterface: string

    ): void;

    *All references to scope in this section are referring to [IPv6 Zone Indices](https://en.wikipedia.org/wiki/IPv6_address#Scoped_literal_IPv6_addresses), which are defined by [RFC 4007](https://tools.ietf.org/html/rfc4007). In string form, an IP* *with a scope index is written as `'IP%scope'` where scope is an interface name* *or interface number.*

    Sets the default outgoing multicast interface of the socket to a chosen interface or back to system interface selection. The `multicastInterface` must be a valid string representation of an IP from the socket's family.

    For IPv4 sockets, this should be the IP configured for the desired physical interface. All packets sent to multicast on the socket will be sent on the interface determined by the most recent successful use of this call.

    For IPv6 sockets, `multicastInterface` should include a scope to indicate the interface as in the examples that follow. In IPv6, individual `send` calls can also use explicit scope in addresses, so only packets sent to a multicast address without specifying an explicit scope are affected by the most recent successful use of this call.

    This method throws `EBADF` if called on an unbound socket.

    #### Example: IPv6 outgoing multicast interface

    On most systems, where scope format uses the interface name:

    ```
    const socket = dgram.createSocket('udp6');

    socket.bind(1234, () => {
      socket.setMulticastInterface('::%eth1');
    });
    ```

    On Windows, where scope format uses an interface number:

    ```
    const socket = dgram.createSocket('udp6');

    socket.bind(1234, () => {
      socket.setMulticastInterface('::%2');
    });
    ```

    #### Example: IPv4 outgoing multicast interface

    All systems use an IP of the host on the desired physical interface:

    ```
    const socket = dgram.createSocket('udp4');

    socket.bind(1234, () => {
      socket.setMulticastInterface('10.0.0.2');
    });
    ```
  + [setMulticastLoopback](https://bun.com/reference/node/dgram/Socket/setMulticastLoopback)(

    flag: boolean

    ): boolean;

    Sets or clears the `IP_MULTICAST_LOOP` socket option. When set to `true`, multicast packets will also be received on the local interface.

    This method throws `EBADF` if called on an unbound socket.
  + [setMulticastTTL](https://bun.com/reference/node/dgram/Socket/setMulticastTTL)(

    ttl: number

    ): number;

    Sets the `IP_MULTICAST_TTL` socket option. While TTL generally stands for "Time to Live", in this context it specifies the number of IP hops that a packet is allowed to travel through, specifically for multicast traffic. Each router or gateway that forwards a packet decrements the TTL. If the TTL is decremented to 0 by a router, it will not be forwarded.

    The `ttl` argument may be between 0 and 255. The default on most systems is `1`.

    This method throws `EBADF` if called on an unbound socket.
  + [setRecvBufferSize](https://bun.com/reference/node/dgram/Socket/setRecvBufferSize)(

    size: number

    ): void;

    Sets the `SO_RCVBUF` socket option. Sets the maximum socket receive buffer in bytes.

    This method throws `ERR_SOCKET_BUFFER_SIZE` if called on an unbound socket.
  + [setSendBufferSize](https://bun.com/reference/node/dgram/Socket/setSendBufferSize)(

    size: number

    ): void;

    Sets the `SO_SNDBUF` socket option. Sets the maximum socket send buffer in bytes.

    This method throws `ERR_SOCKET_BUFFER_SIZE` if called on an unbound socket.
  + [setTTL](https://bun.com/reference/node/dgram/Socket/setTTL)(

    ttl: number

    ): number;

    Sets the `IP_TTL` socket option. While TTL generally stands for "Time to Live", in this context it specifies the number of IP hops that a packet is allowed to travel through. Each router or gateway that forwards a packet decrements the TTL. If the TTL is decremented to 0 by a router, it will not be forwarded. Changing TTL values is typically done for network probes or when multicasting.

    The `ttl` argument may be between 1 and 255. The default on most systems is 64.

    This method throws `EBADF` if called on an unbound socket.
  + [unref](https://bun.com/reference/node/dgram/Socket/unref)(): this;

    By default, binding a socket will cause it to block the Node.js process from exiting as long as the socket is open. The `socket.unref()` method can be used to exclude the socket from the reference counting that keeps the Node.js process active, allowing the process to exit even if the socket is still listening.

    Calling `socket.unref()` multiple times will have no additional effect.

    The `socket.unref()` method returns a reference to the socket so calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/dgram/Socket/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/dgram/Socket/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/dgram/Socket/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/dgram/Socket/on)(

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

    static [on](https://bun.com/reference/node/dgram/Socket/on)(

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
  + static [once](https://bun.com/reference/node/dgram/Socket/once)(

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

    static [once](https://bun.com/reference/node/dgram/Socket/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/dgram/Socket/setMaxListeners)(

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
* function [createSocket](https://bun.com/reference/node/dgram/createSocket)(

  type: [SocketType](https://bun.com/reference/node/dgram/SocketType),

  callback?: (msg: NonSharedBuffer, rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)) => void

  ): [Socket](https://bun.com/reference/node/dgram/Socket);

  Creates a `dgram.Socket` object. Once the socket is created, calling `socket.bind()` will instruct the socket to begin listening for datagram messages. When `address` and `port` are not passed to `socket.bind()` the method will bind the socket to the "all interfaces" address on a random port (it does the right thing for both `udp4` and `udp6` sockets). The bound address and port can be retrieved using `socket.address().address` and `socket.address().port`.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.close()` on the socket:

  ```
  const controller = new AbortController();
  const { signal } = controller;
  const server = dgram.createSocket({ type: 'udp4', signal });
  server.on('message', (msg, rinfo) => {
    console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
  });
  // Later, when you want to close the server.
  controller.abort();
  ```

  @param callback

  Attached as a listener for `'message'` events. Optional.

  function [createSocket](https://bun.com/reference/node/dgram/createSocket)(

  options: [SocketOptions](https://bun.com/reference/node/dgram/SocketOptions),

  callback?: (msg: NonSharedBuffer, rinfo: [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)) => void

  ): [Socket](https://bun.com/reference/node/dgram/Socket);

  Creates a `dgram.Socket` object. Once the socket is created, calling `socket.bind()` will instruct the socket to begin listening for datagram messages. When `address` and `port` are not passed to `socket.bind()` the method will bind the socket to the "all interfaces" address on a random port (it does the right thing for both `udp4` and `udp6` sockets). The bound address and port can be retrieved using `socket.address().address` and `socket.address().port`.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.close()` on the socket:

  ```
  const controller = new AbortController();
  const { signal } = controller;
  const server = dgram.createSocket({ type: 'udp4', signal });
  server.on('message', (msg, rinfo) => {
    console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
  });
  // Later, when you want to close the server.
  controller.abort();
  ```

  @param options

  Available options are:

  @param callback

  Attached as a listener for `'message'` events. Optional.

## Type definitions

* ### interface [BindOptions](https://bun.com/reference/node/dgram/BindOptions)

  + [address](https://bun.com/reference/node/dgram/BindOptions/address)?: string
  + [exclusive](https://bun.com/reference/node/dgram/BindOptions/exclusive)?: boolean
  + [fd](https://bun.com/reference/node/dgram/BindOptions/fd)?: number
  + [port](https://bun.com/reference/node/dgram/BindOptions/port)?: number
* ### interface [RemoteInfo](https://bun.com/reference/node/dgram/RemoteInfo)

  + [address](https://bun.com/reference/node/dgram/RemoteInfo/address): string
  + [family](https://bun.com/reference/node/dgram/RemoteInfo/family): 'IPv4' | 'IPv6'
  + [port](https://bun.com/reference/node/dgram/RemoteInfo/port): number
  + [size](https://bun.com/reference/node/dgram/RemoteInfo/size): number
* ### interface [SocketOptions](https://bun.com/reference/node/dgram/SocketOptions)

  + [ipv6Only](https://bun.com/reference/node/dgram/SocketOptions/ipv6Only)?: boolean
  + [lookup](https://bun.com/reference/node/dgram/SocketOptions/lookup)?: (hostname: string, options: [LookupOneOptions](https://bun.com/reference/node/dns/LookupOneOptions), callback: (err: null | ErrnoException, address: string, family: number) => void) => void
  + [receiveBlockList](https://bun.com/reference/node/dgram/SocketOptions/receiveBlockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)
  + [recvBufferSize](https://bun.com/reference/node/dgram/SocketOptions/recvBufferSize)?: number
  + [reuseAddr](https://bun.com/reference/node/dgram/SocketOptions/reuseAddr)?: boolean
  + [reusePort](https://bun.com/reference/node/dgram/SocketOptions/reusePort)?: boolean
  + [sendBlockList](https://bun.com/reference/node/dgram/SocketOptions/sendBlockList)?: [BlockList](https://bun.com/reference/node/net/BlockList)
  + [sendBufferSize](https://bun.com/reference/node/dgram/SocketOptions/sendBufferSize)?: number
  + [signal](https://bun.com/reference/node/dgram/SocketOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [type](https://bun.com/reference/node/dgram/SocketOptions/type): [SocketType](https://bun.com/reference/node/dgram/SocketType)
* type [SocketType](https://bun.com/reference/node/dgram/SocketType) = 'udp4' | 'udp6'