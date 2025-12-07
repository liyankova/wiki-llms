---
url: https://bun.com/reference/node/child_process
title: Node.js child_process module | API Reference | Bun
source_domain: bun.com
---

# Node.js child_process module | API Reference | Bun

Node.js module

# [child\_process](https://bun.com/reference/node/child_process)

The `'node:child_process'` module enables spawning and controlling subprocesses from Node.js. It supports synchronous and asynchronous execution via `exec`, `execFile`, `spawn`, and `fork` functions.

Child processes can inherit stdio, communicate via IPC channels, and return exit codes. This module is essential for leveraging external commands, implementing parallel work, and managing worker processes.

Works in Bun

Core functionality works. The Stream class is not exported. IPC cannot send socket handles between processes; Node.js <> Bun IPC can be used with JSON serialization. Some process properties are missing.

* ### class [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess)

  Instances of the `ChildProcess` represent spawned child processes.

  Instances of `ChildProcess` are not intended to be created directly. Rather, use the spawn, exec,execFile, or fork methods to create instances of `ChildProcess`.

  + readonly [channel](https://bun.com/reference/node/child_process/ChildProcess/channel)?: null | [Control](https://bun.com/reference/node/child_process/Control)

    The `subprocess.channel` property is a reference to the child's IPC channel. If no IPC channel exists, this property is `undefined`.
  + readonly [connected](https://bun.com/reference/node/child_process/ChildProcess/connected): boolean

    The `subprocess.connected` property indicates whether it is still possible to send and receive messages from a child process. When `subprocess.connected` is `false`, it is no longer possible to send or receive messages.
  + readonly [exitCode](https://bun.com/reference/node/child_process/ChildProcess/exitCode): null | number

    The `subprocess.exitCode` property indicates the exit code of the child process. If the child process is still running, the field will be `null`.
  + readonly [killed](https://bun.com/reference/node/child_process/ChildProcess/killed): boolean

    The `subprocess.killed` property indicates whether the child process successfully received a signal from `subprocess.kill()`. The `killed` property does not indicate that the child process has been terminated.
  + readonly [pid](https://bun.com/reference/node/child_process/ChildProcess/pid)?: number

    Returns the process identifier (PID) of the child process. If the child process fails to spawn due to errors, then the value is `undefined` and `error` is emitted.

    ```
    import { spawn } from 'node:child_process';
    const grep = spawn('grep', ['ssh']);

    console.log(`Spawned child pid: ${grep.pid}`);
    grep.stdin.end();
    ```
  + readonly [signalCode](https://bun.com/reference/node/child_process/ChildProcess/signalCode): null | Signals

    The `subprocess.signalCode` property indicates the signal received by the child process if any, else `null`.
  + readonly [spawnargs](https://bun.com/reference/node/child_process/ChildProcess/spawnargs): string[]

    The `subprocess.spawnargs` property represents the full list of command-line arguments the child process was launched with.
  + readonly [spawnfile](https://bun.com/reference/node/child_process/ChildProcess/spawnfile): string

    The `subprocess.spawnfile` property indicates the executable file name of the child process that is launched.

    For fork, its value will be equal to `process.execPath`. For spawn, its value will be the name of the executable file. For exec, its value will be the name of the shell in which the child process is launched.
  + [stderr](https://bun.com/reference/node/child_process/ChildProcess/stderr): null | [Readable](https://bun.com/reference/node/stream/default/Readable)

    A `Readable Stream` that represents the child process's `stderr`.

    If the child was spawned with `stdio[2]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stderr` is an alias for `subprocess.stdio[2]`. Both properties will refer to the same value.

    The `subprocess.stderr` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + [stdin](https://bun.com/reference/node/child_process/ChildProcess/stdin): null | [Writable](https://bun.com/reference/node/stream/default/Writable)

    A `Writable Stream` that represents the child process's `stdin`.

    If a child process waits to read all of its input, the child will not continue until this stream has been closed via `end()`.

    If the child was spawned with `stdio[0]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stdin` is an alias for `subprocess.stdio[0]`. Both properties will refer to the same value.

    The `subprocess.stdin` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + readonly [stdio](https://bun.com/reference/node/child_process/ChildProcess/stdio): [null | [Writable](https://bun.com/reference/node/stream/default/Writable), null | [Readable](https://bun.com/reference/node/stream/default/Readable), null | [Readable](https://bun.com/reference/node/stream/default/Readable), undefined | null | [Writable](https://bun.com/reference/node/stream/default/Writable) | [Readable](https://bun.com/reference/node/stream/default/Readable), undefined | null | [Writable](https://bun.com/reference/node/stream/default/Writable) | [Readable](https://bun.com/reference/node/stream/default/Readable)]

    A sparse array of pipes to the child process, corresponding with positions in the `stdio` option passed to spawn that have been set to the value `'pipe'`. `subprocess.stdio[0]`, `subprocess.stdio[1]`, and `subprocess.stdio[2]` are also available as `subprocess.stdin`, `subprocess.stdout`, and `subprocess.stderr`, respectively.

    In the following example, only the child's fd `1` (stdout) is configured as a pipe, so only the parent's `subprocess.stdio[1]` is a stream, all other values in the array are `null`.

    ```
    import assert from 'node:assert';
    import fs from 'node:fs';
    import child_process from 'node:child_process';

    const subprocess = child_process.spawn('ls', {
      stdio: [
        0, // Use parent's stdin for child.
        'pipe', // Pipe child's stdout to parent.
        fs.openSync('err.out', 'w'), // Direct child's stderr to a file.
      ],
    });

    assert.strictEqual(subprocess.stdio[0], null);
    assert.strictEqual(subprocess.stdio[0], subprocess.stdin);

    assert(subprocess.stdout);
    assert.strictEqual(subprocess.stdio[1], subprocess.stdout);

    assert.strictEqual(subprocess.stdio[2], null);
    assert.strictEqual(subprocess.stdio[2], subprocess.stderr);
    ```

    The `subprocess.stdio` property can be `undefined` if the child process could not be successfully spawned.
  + [stdout](https://bun.com/reference/node/child_process/ChildProcess/stdout): null | [Readable](https://bun.com/reference/node/stream/default/Readable)

    A `Readable Stream` that represents the child process's `stdout`.

    If the child was spawned with `stdio[1]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stdout` is an alias for `subprocess.stdio[1]`. Both properties will refer to the same value.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn('ls');

    subprocess.stdout.on('data', (data) => {
      console.log(`Received chunk ${data}`);
    });
    ```

    The `subprocess.stdout` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + static [captureRejections](https://bun.com/reference/node/child_process/ChildProcess/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/child_process/ChildProcess/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/child_process/ChildProcess/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/child_process/ChildProcess/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/child_process/ChildProcess/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [[Symbol.dispose]](https://bun.com/reference/node/child_process/ChildProcess/[dispose])(): void;

    Calls ChildProcess.kill with `'SIGTERM'`.
  + [addListener](https://bun.com/reference/node/child_process/ChildProcess/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcess/addListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcess/addListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcess/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcess/addListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcess/addListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcess/addListener)(

    event: 'spawn',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn
  + [disconnect](https://bun.com/reference/node/child_process/ChildProcess/disconnect)(): void;

    Closes the IPC channel between parent and child, allowing the child to exit gracefully once there are no other connections keeping it alive. After calling this method the `subprocess.connected` and `process.connected` properties in both the parent and child (respectively) will be set to `false`, and it will be no longer possible to pass messages between the processes.

    The `'disconnect'` event will be emitted when there are no messages in the process of being received. This will most often be triggered immediately after calling `subprocess.disconnect()`.

    When the child process is a Node.js instance (e.g. spawned using fork), the `process.disconnect()` method can be invoked within the child process to close the IPC channel as well.
  + [emit](https://bun.com/reference/node/child_process/ChildProcess/emit)(

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

    [emit](https://bun.com/reference/node/child_process/ChildProcess/emit)(

    event: 'close',

    code: null | number,

    signal: null | Signals

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcess/emit)(

    event: 'disconnect'

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcess/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcess/emit)(

    event: 'exit',

    code: null | number,

    signal: null | Signals

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcess/emit)(

    event: 'message',

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcess/emit)(

    event: 'spawn',

    listener: () => void

    ): boolean;
  + [eventNames](https://bun.com/reference/node/child_process/ChildProcess/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/child_process/ChildProcess/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [kill](https://bun.com/reference/node/child_process/ChildProcess/kill)(

    signal?: number | Signals

    ): boolean;

    The `subprocess.kill()` method sends a signal to the child process. If no argument is given, the process will be sent the `'SIGTERM'` signal. See [`signal(7)`](http://man7.org/linux/man-pages/man7/signal.7.html) for a list of available signals. This function returns `true` if [`kill(2)`](http://man7.org/linux/man-pages/man2/kill.2.html) succeeds, and `false` otherwise.

    ```
    import { spawn } from 'node:child_process';
    const grep = spawn('grep', ['ssh']);

    grep.on('close', (code, signal) => {
      console.log(
        `child process terminated due to receipt of signal ${signal}`);
    });

    // Send SIGHUP to process.
    grep.kill('SIGHUP');
    ```

    The `ChildProcess` object may emit an `'error'` event if the signal cannot be delivered. Sending a signal to a child process that has already exited is not an error but may have unforeseen consequences. Specifically, if the process identifier (PID) has been reassigned to another process, the signal will be delivered to that process instead which can have unexpected results.

    While the function is called `kill`, the signal delivered to the child process may not actually terminate the process.

    See [`kill(2)`](http://man7.org/linux/man-pages/man2/kill.2.html) for reference.

    On Windows, where POSIX signals do not exist, the `signal` argument will be ignored, and the process will be killed forcefully and abruptly (similar to `'SIGKILL'`). See `Signal Events` for more details.

    On Linux, child processes of child processes will not be terminated when attempting to kill their parent. This is likely to happen when running a new process in a shell or with the use of the `shell` option of `ChildProcess`:

    ```
    'use strict';
    import { spawn } from 'node:child_process';

    const subprocess = spawn(
      'sh',
      [
        '-c',
        `node -e "setInterval(() => {
          console.log(process.pid, 'is alive')
        }, 500);"`,
      ], {
        stdio: ['inherit', 'inherit', 'inherit'],
      },
    );

    setTimeout(() => {
      subprocess.kill(); // Does not terminate the Node.js process in the shell.
    }, 2000);
    ```
  + [listenerCount](https://bun.com/reference/node/child_process/ChildProcess/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/child_process/ChildProcess/listeners)<K>(

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
  + [off](https://bun.com/reference/node/child_process/ChildProcess/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

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

    [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

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

    [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [prependListener](https://bun.com/reference/node/child_process/ChildProcess/prependListener)(

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

    [prependListener](https://bun.com/reference/node/child_process/ChildProcess/prependListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcess/prependListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcess/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcess/prependListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcess/prependListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcess/prependListener)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcess/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcess/prependOnceListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcess/prependOnceListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcess/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcess/prependOnceListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcess/prependOnceListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcess/prependOnceListener)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/child_process/ChildProcess/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/child_process/ChildProcess/ref)(): void;

    Calling `subprocess.ref()` after making a call to `subprocess.unref()` will restore the removed reference count for the child process, forcing the parent to wait for the child to exit before exiting itself.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn(process.argv[0], ['child_program.js'], {
      detached: true,
      stdio: 'ignore',
    });

    subprocess.unref();
    subprocess.ref();
    ```
  + [removeAllListeners](https://bun.com/reference/node/child_process/ChildProcess/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/child_process/ChildProcess/removeListener)<K>(

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
  + [send](https://bun.com/reference/node/child_process/ChildProcess/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    [send](https://bun.com/reference/node/child_process/ChildProcess/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle?: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    @param sendHandle

    `undefined`, or a [`net.Socket`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netsocket), [`net.Server`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netserver), or [`dgram.Socket`](https://nodejs.org/docs/latest-v24.x/api/dgram.html#class-dgramsocket) object.

    [send](https://bun.com/reference/node/child_process/ChildProcess/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle?: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    options?: [MessageOptions](https://bun.com/reference/node/child_process/MessageOptions),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    @param sendHandle

    `undefined`, or a [`net.Socket`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netsocket), [`net.Server`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netserver), or [`dgram.Socket`](https://nodejs.org/docs/latest-v24.x/api/dgram.html#class-dgramsocket) object.

    @param options

    The `options` argument, if present, is an object used to parameterize the sending of certain types of handles. `options` supports the following properties:
  + [setMaxListeners](https://bun.com/reference/node/child_process/ChildProcess/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [unref](https://bun.com/reference/node/child_process/ChildProcess/unref)(): void;

    By default, the parent will wait for the detached child to exit. To prevent the parent from waiting for a given `subprocess` to exit, use the `subprocess.unref()` method. Doing so will cause the parent's event loop to not include the child in its reference count, allowing the parent to exit independently of the child, unless there is an established IPC channel between the child and the parent.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn(process.argv[0], ['child_program.js'], {
      detached: true,
      stdio: 'ignore',
    });

    subprocess.unref();
    ```
  + static [addAbortListener](https://bun.com/reference/node/child_process/ChildProcess/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/child_process/ChildProcess/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/child_process/ChildProcess/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

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

    static [on](https://bun.com/reference/node/child_process/ChildProcess/on)(

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
  + static [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

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

    static [once](https://bun.com/reference/node/child_process/ChildProcess/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/child_process/ChildProcess/setMaxListeners)(

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
* function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.

  function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  options: [ExecOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding),

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: NonSharedBuffer, stderr: NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.

  function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  options: [ExecOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding),

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.

  function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  options: undefined | null | [ExecOptions](https://bun.com/reference/node/child_process/ExecOptions),

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: string | NonSharedBuffer, stderr: string | NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.
* function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  options: [ExecFileOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: NonSharedBuffer, stderr: NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  options: [ExecFileOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: NonSharedBuffer, stderr: NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  options: [ExecFileOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  options: [ExecFileOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  options: undefined | null | [ExecFileOptions](https://bun.com/reference/node/child_process/ExecFileOptions),

  callback: undefined | null | (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string | NonSharedBuffer, stderr: string | NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  options: undefined | null | [ExecFileOptions](https://bun.com/reference/node/child_process/ExecFileOptions),

  callback: undefined | null | (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string | NonSharedBuffer, stderr: string | NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.
* function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string

  ): NonSharedBuffer;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @returns

  The stdout from the command.

  function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string,

  options: [ExecFileSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding)

  ): string;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @returns

  The stdout from the command.

  function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string,

  options: [ExecFileSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding)

  ): NonSharedBuffer;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @returns

  The stdout from the command.

  function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string,

  options?: [ExecFileSyncOptions](https://bun.com/reference/node/child_process/ExecFileSyncOptions)

  ): string | NonSharedBuffer;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @returns

  The stdout from the command.

  function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string,

  args: readonly string[]

  ): NonSharedBuffer;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @returns

  The stdout from the command.

  function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string,

  args: readonly string[],

  options: [ExecFileSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding)

  ): string;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @returns

  The stdout from the command.

  function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string,

  args: readonly string[],

  options: [ExecFileSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding)

  ): NonSharedBuffer;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @returns

  The stdout from the command.

  function [execFileSync](https://bun.com/reference/node/child_process/execFileSync)(

  file: string,

  args?: readonly string[],

  options?: [ExecFileSyncOptions](https://bun.com/reference/node/child_process/ExecFileSyncOptions)

  ): string | NonSharedBuffer;

  The `child_process.execFileSync()` method is generally identical to execFile with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited.

  If the child process intercepts and handles the `SIGTERM` signal and does not exit, the parent process will still wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw an `Error` that will include the full result of the underlying spawnSync.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @returns

  The stdout from the command.
* function [execSync](https://bun.com/reference/node/child_process/execSync)(

  command: string

  ): NonSharedBuffer;

  The `child_process.execSync()` method is generally identical to exec with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the child process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw. The `Error` object will contain the entire result from spawnSync.

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  @param command

  The command to run.

  @returns

  The stdout from the command.

  function [execSync](https://bun.com/reference/node/child_process/execSync)(

  command: string,

  options: [ExecSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding)

  ): string;

  The `child_process.execSync()` method is generally identical to exec with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the child process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw. The `Error` object will contain the entire result from spawnSync.

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  @param command

  The command to run.

  @returns

  The stdout from the command.

  function [execSync](https://bun.com/reference/node/child_process/execSync)(

  command: string,

  options: [ExecSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding)

  ): NonSharedBuffer;

  The `child_process.execSync()` method is generally identical to exec with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the child process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw. The `Error` object will contain the entire result from spawnSync.

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  @param command

  The command to run.

  @returns

  The stdout from the command.

  function [execSync](https://bun.com/reference/node/child_process/execSync)(

  command: string,

  options?: [ExecSyncOptions](https://bun.com/reference/node/child_process/ExecSyncOptions)

  ): string | NonSharedBuffer;

  The `child_process.execSync()` method is generally identical to exec with the exception that the method will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the child process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  If the process times out or has a non-zero exit code, this method will throw. The `Error` object will contain the entire result from spawnSync.

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  @param command

  The command to run.

  @returns

  The stdout from the command.
* function [fork](https://bun.com/reference/node/child_process/fork)(

  modulePath: string | [URL](https://bun.com/reference/node/url/URL),

  options?: [ForkOptions](https://bun.com/reference/node/child_process/ForkOptions)

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.fork()` method is a special case of spawn used specifically to spawn new Node.js processes. Like spawn, a `ChildProcess` object is returned. The returned `ChildProcess` will have an additional communication channel built-in that allows messages to be passed back and forth between the parent and child. See `subprocess.send()` for details.

  Keep in mind that spawned Node.js child processes are independent of the parent with exception of the IPC communication channel that is established between the two. Each process has its own memory, with their own V8 instances. Because of the additional resource allocations required, spawning a large number of child Node.js processes is not recommended.

  By default, `child_process.fork()` will spawn new Node.js instances using the `process.execPath` of the parent process. The `execPath` property in the `options` object allows for an alternative execution path to be used.

  Node.js processes launched with a custom `execPath` will communicate with the parent process using the file descriptor (fd) identified using the environment variable `NODE_CHANNEL_FD` on the child process.

  Unlike the [`fork(2)`](http://man7.org/linux/man-pages/man2/fork.2.html) POSIX system call, `child_process.fork()` does not clone the current process.

  The `shell` option available in spawn is not supported by `child_process.fork()` and will be ignored if set.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  if (process.argv[2] === 'child') {
    setTimeout(() => {
      console.log(`Hello from ${process.argv[2]}!`);
    }, 1_000);
  } else {
    import { fork } from 'node:child_process';
    const controller = new AbortController();
    const { signal } = controller;
    const child = fork(__filename, ['child'], { signal });
    child.on('error', (err) => {
      // This will be called with err being an AbortError if the controller aborts
    });
    controller.abort(); // Stops the child process
  }
  ```

  @param modulePath

  The module to run in the child.

  function [fork](https://bun.com/reference/node/child_process/fork)(

  modulePath: string | [URL](https://bun.com/reference/node/url/URL),

  args?: readonly string[],

  options?: [ForkOptions](https://bun.com/reference/node/child_process/ForkOptions)

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.fork()` method is a special case of spawn used specifically to spawn new Node.js processes. Like spawn, a `ChildProcess` object is returned. The returned `ChildProcess` will have an additional communication channel built-in that allows messages to be passed back and forth between the parent and child. See `subprocess.send()` for details.

  Keep in mind that spawned Node.js child processes are independent of the parent with exception of the IPC communication channel that is established between the two. Each process has its own memory, with their own V8 instances. Because of the additional resource allocations required, spawning a large number of child Node.js processes is not recommended.

  By default, `child_process.fork()` will spawn new Node.js instances using the `process.execPath` of the parent process. The `execPath` property in the `options` object allows for an alternative execution path to be used.

  Node.js processes launched with a custom `execPath` will communicate with the parent process using the file descriptor (fd) identified using the environment variable `NODE_CHANNEL_FD` on the child process.

  Unlike the [`fork(2)`](http://man7.org/linux/man-pages/man2/fork.2.html) POSIX system call, `child_process.fork()` does not clone the current process.

  The `shell` option available in spawn is not supported by `child_process.fork()` and will be ignored if set.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  if (process.argv[2] === 'child') {
    setTimeout(() => {
      console.log(`Hello from ${process.argv[2]}!`);
    }, 1_000);
  } else {
    import { fork } from 'node:child_process';
    const controller = new AbortController();
    const { signal } = controller;
    const child = fork(__filename, ['child'], { signal });
    child.on('error', (err) => {
      // This will be called with err being an AbortError if the controller aborts
    });
    controller.abort(); // Stops the child process
  }
  ```

  @param modulePath

  The module to run in the child.

  @param args

  List of string arguments.
* function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options?: [SpawnOptionsWithoutStdio](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio)

  ): [ChildProcessWithoutNullStreams](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams);

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), [Readable](https://bun.com/reference/node/stream/default/Readable), [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), [Readable](https://bun.com/reference/node/stream/default/Readable), null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), null, [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, [Readable](https://bun.com/reference/node/stream/default/Readable), [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), null, null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, [Readable](https://bun.com/reference/node/stream/default/Readable), null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, null, [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, null, null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  options: [SpawnOptions](https://bun.com/reference/node/child_process/SpawnOptions)

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args?: readonly string[],

  options?: [SpawnOptionsWithoutStdio](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio)

  ): [ChildProcessWithoutNullStreams](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams);

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), [Readable](https://bun.com/reference/node/stream/default/Readable), [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), [Readable](https://bun.com/reference/node/stream/default/Readable), null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), null, [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, [Readable](https://bun.com/reference/node/stream/default/Readable), [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<[Writable](https://bun.com/reference/node/stream/default/Writable), null, null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, [Readable](https://bun.com/reference/node/stream/default/Readable), null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, null, [Readable](https://bun.com/reference/node/stream/default/Readable)>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<[StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull), [StdioNull](https://bun.com/reference/node/child_process/StdioNull)>

  ): [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<null, null, null>;

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawn](https://bun.com/reference/node/child_process/spawn)(

  command: string,

  args: readonly string[],

  options: [SpawnOptions](https://bun.com/reference/node/child_process/SpawnOptions)

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  A third argument may be used to specify additional options, with these defaults:

  ```
  const defaults = {
    cwd: undefined,
    env: process.env,
  };
  ```

  Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

  Use `env` to specify environment variables that will be visible to the new process, the default is `process.env`.

  `undefined` values in `env` will be ignored.

  Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

  ```
  import { spawn } from 'node:child_process';
  const ls = spawn('ls', ['-lh', '/usr']);

  ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
  });

  ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
  });

  ls.on('close', (code) => {
    console.log(`child process exited with code ${code}`);
  });
  ```

  Example: A very elaborate way to run `ps ax | grep ssh`

  ```
  import { spawn } from 'node:child_process';
  const ps = spawn('ps', ['ax']);
  const grep = spawn('grep', ['ssh']);

  ps.stdout.on('data', (data) => {
    grep.stdin.write(data);
  });

  ps.stderr.on('data', (data) => {
    console.error(`ps stderr: ${data}`);
  });

  ps.on('close', (code) => {
    if (code !== 0) {
      console.log(`ps process exited with code ${code}`);
    }
    grep.stdin.end();
  });

  grep.stdout.on('data', (data) => {
    console.log(data.toString());
  });

  grep.stderr.on('data', (data) => {
    console.error(`grep stderr: ${data}`);
  });

  grep.on('close', (code) => {
    if (code !== 0) {
      console.log(`grep process exited with code ${code}`);
    }
  });
  ```

  Example of checking for failed `spawn`:

  ```
  import { spawn } from 'node:child_process';
  const subprocess = spawn('bad_command');

  subprocess.on('error', (err) => {
    console.error('Failed to start subprocess.');
  });
  ```

  Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

  Node.js overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent. Retrieve it with the `process.argv0` property instead.

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { spawn } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const grep = spawn('grep', ['ssh'], { signal });
  grep.on('error', (err) => {
    // This will be called with err being an AbortError if the controller aborts
  });
  controller.abort(); // Stops the child process
  ```

  @param command

  The command to run.

  @param args

  List of string arguments.
* function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<NonSharedBuffer>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string,

  options: [SpawnSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding)

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<string>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string,

  options: [SpawnSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding)

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<NonSharedBuffer>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string,

  options?: [SpawnSyncOptions](https://bun.com/reference/node/child_process/SpawnSyncOptions)

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<string | NonSharedBuffer>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string,

  args: readonly string[]

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<NonSharedBuffer>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string,

  args: readonly string[],

  options: [SpawnSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding)

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<string>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string,

  args: readonly string[],

  options: [SpawnSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding)

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<NonSharedBuffer>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  @param args

  List of string arguments.

  function [spawnSync](https://bun.com/reference/node/child_process/spawnSync)(

  command: string,

  args?: readonly string[],

  options?: [SpawnSyncOptions](https://bun.com/reference/node/child_process/SpawnSyncOptions)

  ): [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<string | NonSharedBuffer>;

  The `child_process.spawnSync()` method is generally identical to spawn with the exception that the function will not return until the child process has fully closed. When a timeout has been encountered and `killSignal` is sent, the method won't return until the process has completely exited. If the process intercepts and handles the `SIGTERM` signal and doesn't exit, the parent process will wait until the child process has exited.

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  @param command

  The command to run.

  @param args

  List of string arguments.

## Type definitions

* function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.

  function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  options: [ExecOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding),

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: NonSharedBuffer, stderr: NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.

  function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  options: [ExecOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding),

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.

  function [exec](https://bun.com/reference/node/child_process/exec)(

  command: string,

  options: undefined | null | [ExecOptions](https://bun.com/reference/node/child_process/ExecOptions),

  callback?: (error: null | [ExecException](https://bun.com/reference/node/child_process/ExecException), stdout: string | NonSharedBuffer, stderr: string | NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  Spawns a shell then executes the `command` within that shell, buffering any generated output. The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

  ```
  import { exec } from 'node:child_process';

  exec('"/path/to/test file/test.sh" arg1 arg2');
  // Double quotes are used so that the space in the path is not interpreted as
  // a delimiter of multiple arguments.

  exec('echo "The \\$HOME variable is $HOME"');
  // The $HOME variable is escaped in the first instance, but not in the second.
  ```

  **Never pass unsanitized user input to this function. Any input containing shell** **metacharacters may be used to trigger arbitrary command execution.**

  If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. On error, `error` will be an instance of `Error`. The `error.code` property will be the exit code of the process. By convention, any exit code other than `0` indicates an error. `error.signal` will be the signal that terminated the process.

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  ```
  import { exec } from 'node:child_process';
  exec('cat *.js missing_file | wc -l', (error, stdout, stderr) => {
    if (error) {
      console.error(`exec error: ${error}`);
      return;
    }
    console.log(`stdout: ${stdout}`);
    console.error(`stderr: ${stderr}`);
  });
  ```

  If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

  Unlike the [`exec(3)`](http://man7.org/linux/man-pages/man3/exec.3.html) POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const exec = util.promisify(child_process.exec);

  async function lsExample() {
    const { stdout, stderr } = await exec('ls');
    console.log('stdout:', stdout);
    console.error('stderr:', stderr);
  }
  lsExample();
  ```

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { exec } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = exec('grep ssh', { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param command

  The command to run, with space-separated arguments.

  @param callback

  called with the output when process terminates.

  ### namespace [exec](https://bun.com/reference/node/child_process/exec)
* function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  options: [ExecFileOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: NonSharedBuffer, stderr: NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  options: [ExecFileOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: NonSharedBuffer, stderr: NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  options: [ExecFileOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  options: [ExecFileOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding),

  callback?: (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string, stderr: string) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  options: undefined | null | [ExecFileOptions](https://bun.com/reference/node/child_process/ExecFileOptions),

  callback: undefined | null | (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string | NonSharedBuffer, stderr: string | NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param callback

  Called with the output when process terminates.

  function [execFile](https://bun.com/reference/node/child_process/execFile)(

  file: string,

  args: undefined | null | readonly string[],

  options: undefined | null | [ExecFileOptions](https://bun.com/reference/node/child_process/ExecFileOptions),

  callback: undefined | null | (error: null | [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException), stdout: string | NonSharedBuffer, stderr: string | NonSharedBuffer) => void

  ): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess);

  The `child_process.execFile()` function is similar to exec except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than exec.

  The same options as exec are supported. Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

  ```
  import { execFile } from 'node:child_process';
  const child = execFile('node', ['--version'], (error, stdout, stderr) => {
    if (error) {
      throw error;
    }
    console.log(stdout);
  });
  ```

  The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. By default, Node.js will decode the output as UTF-8 and pass strings to the callback. The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

  If this method is invoked as its `util.promisify()` ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties. The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

  ```
  import util from 'node:util';
  import child_process from 'node:child_process';
  const execFile = util.promisify(child_process.execFile);
  async function getVersion() {
    const { stdout } = await execFile('node', ['--version']);
    console.log(stdout);
  }
  getVersion();
  ```

  **If the `shell` option is enabled, do not pass unsanitized user input to this** **function. Any input containing shell metacharacters may be used to trigger** **arbitrary command execution.**

  If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

  ```
  import { execFile } from 'node:child_process';
  const controller = new AbortController();
  const { signal } = controller;
  const child = execFile('node', ['--version'], { signal }, (error) => {
    console.error(error); // an AbortError
  });
  controller.abort();
  ```

  @param file

  The name or path of the executable file to run.

  @param args

  List of string arguments.

  @param callback

  Called with the output when process terminates.

  ### namespace [execFile](https://bun.com/reference/node/child_process/execFile)
* ### interface [ChildProcessByStdio](https://bun.com/reference/node/child_process/ChildProcessByStdio)<I extends null | [Writable](https://bun.com/reference/node/stream/default/Writable), O extends null | [Readable](https://bun.com/reference/node/stream/default/Readable), E extends null | [Readable](https://bun.com/reference/node/stream/default/Readable)>

  Instances of the `ChildProcess` represent spawned child processes.

  Instances of `ChildProcess` are not intended to be created directly. Rather, use the spawn, exec,execFile, or fork methods to create instances of `ChildProcess`.

  + readonly [channel](https://bun.com/reference/node/child_process/ChildProcessByStdio/channel)?: null | [Control](https://bun.com/reference/node/child_process/Control)

    The `subprocess.channel` property is a reference to the child's IPC channel. If no IPC channel exists, this property is `undefined`.
  + readonly [connected](https://bun.com/reference/node/child_process/ChildProcessByStdio/connected): boolean

    The `subprocess.connected` property indicates whether it is still possible to send and receive messages from a child process. When `subprocess.connected` is `false`, it is no longer possible to send or receive messages.
  + readonly [exitCode](https://bun.com/reference/node/child_process/ChildProcessByStdio/exitCode): null | number

    The `subprocess.exitCode` property indicates the exit code of the child process. If the child process is still running, the field will be `null`.
  + readonly [killed](https://bun.com/reference/node/child_process/ChildProcessByStdio/killed): boolean

    The `subprocess.killed` property indicates whether the child process successfully received a signal from `subprocess.kill()`. The `killed` property does not indicate that the child process has been terminated.
  + readonly [pid](https://bun.com/reference/node/child_process/ChildProcessByStdio/pid)?: number

    Returns the process identifier (PID) of the child process. If the child process fails to spawn due to errors, then the value is `undefined` and `error` is emitted.

    ```
    import { spawn } from 'node:child_process';
    const grep = spawn('grep', ['ssh']);

    console.log(`Spawned child pid: ${grep.pid}`);
    grep.stdin.end();
    ```
  + readonly [signalCode](https://bun.com/reference/node/child_process/ChildProcessByStdio/signalCode): null | Signals

    The `subprocess.signalCode` property indicates the signal received by the child process if any, else `null`.
  + readonly [spawnargs](https://bun.com/reference/node/child_process/ChildProcessByStdio/spawnargs): string[]

    The `subprocess.spawnargs` property represents the full list of command-line arguments the child process was launched with.
  + readonly [spawnfile](https://bun.com/reference/node/child_process/ChildProcessByStdio/spawnfile): string

    The `subprocess.spawnfile` property indicates the executable file name of the child process that is launched.

    For fork, its value will be equal to `process.execPath`. For spawn, its value will be the name of the executable file. For exec, its value will be the name of the shell in which the child process is launched.
  + [stderr](https://bun.com/reference/node/child_process/ChildProcessByStdio/stderr): E

    A `Readable Stream` that represents the child process's `stderr`.

    If the child was spawned with `stdio[2]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stderr` is an alias for `subprocess.stdio[2]`. Both properties will refer to the same value.

    The `subprocess.stderr` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + [stdin](https://bun.com/reference/node/child_process/ChildProcessByStdio/stdin): I

    A `Writable Stream` that represents the child process's `stdin`.

    If a child process waits to read all of its input, the child will not continue until this stream has been closed via `end()`.

    If the child was spawned with `stdio[0]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stdin` is an alias for `subprocess.stdio[0]`. Both properties will refer to the same value.

    The `subprocess.stdin` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + readonly [stdio](https://bun.com/reference/node/child_process/ChildProcessByStdio/stdio): [I, O, E, undefined | null | [Writable](https://bun.com/reference/node/stream/default/Writable) | [Readable](https://bun.com/reference/node/stream/default/Readable), undefined | null | [Writable](https://bun.com/reference/node/stream/default/Writable) | [Readable](https://bun.com/reference/node/stream/default/Readable)]

    A sparse array of pipes to the child process, corresponding with positions in the `stdio` option passed to spawn that have been set to the value `'pipe'`. `subprocess.stdio[0]`, `subprocess.stdio[1]`, and `subprocess.stdio[2]` are also available as `subprocess.stdin`, `subprocess.stdout`, and `subprocess.stderr`, respectively.

    In the following example, only the child's fd `1` (stdout) is configured as a pipe, so only the parent's `subprocess.stdio[1]` is a stream, all other values in the array are `null`.

    ```
    import assert from 'node:assert';
    import fs from 'node:fs';
    import child_process from 'node:child_process';

    const subprocess = child_process.spawn('ls', {
      stdio: [
        0, // Use parent's stdin for child.
        'pipe', // Pipe child's stdout to parent.
        fs.openSync('err.out', 'w'), // Direct child's stderr to a file.
      ],
    });

    assert.strictEqual(subprocess.stdio[0], null);
    assert.strictEqual(subprocess.stdio[0], subprocess.stdin);

    assert(subprocess.stdout);
    assert.strictEqual(subprocess.stdio[1], subprocess.stdout);

    assert.strictEqual(subprocess.stdio[2], null);
    assert.strictEqual(subprocess.stdio[2], subprocess.stderr);
    ```

    The `subprocess.stdio` property can be `undefined` if the child process could not be successfully spawned.
  + [stdout](https://bun.com/reference/node/child_process/ChildProcessByStdio/stdout): O

    A `Readable Stream` that represents the child process's `stdout`.

    If the child was spawned with `stdio[1]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stdout` is an alias for `subprocess.stdio[1]`. Both properties will refer to the same value.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn('ls');

    subprocess.stdout.on('data', (data) => {
      console.log(`Received chunk ${data}`);
    });
    ```

    The `subprocess.stdout` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/child_process/ChildProcessByStdio/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [[Symbol.dispose]](https://bun.com/reference/node/child_process/ChildProcessByStdio/[dispose])(): void;

    Calls ChildProcess.kill with `'SIGTERM'`.
  + [addListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/addListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/addListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/addListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/addListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/addListener)(

    event: 'spawn',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn
  + [disconnect](https://bun.com/reference/node/child_process/ChildProcessByStdio/disconnect)(): void;

    Closes the IPC channel between parent and child, allowing the child to exit gracefully once there are no other connections keeping it alive. After calling this method the `subprocess.connected` and `process.connected` properties in both the parent and child (respectively) will be set to `false`, and it will be no longer possible to pass messages between the processes.

    The `'disconnect'` event will be emitted when there are no messages in the process of being received. This will most often be triggered immediately after calling `subprocess.disconnect()`.

    When the child process is a Node.js instance (e.g. spawned using fork), the `process.disconnect()` method can be invoked within the child process to close the IPC channel as well.
  + [emit](https://bun.com/reference/node/child_process/ChildProcessByStdio/emit)(

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

    [emit](https://bun.com/reference/node/child_process/ChildProcessByStdio/emit)(

    event: 'close',

    code: null | number,

    signal: null | Signals

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessByStdio/emit)(

    event: 'disconnect'

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessByStdio/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessByStdio/emit)(

    event: 'exit',

    code: null | number,

    signal: null | Signals

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessByStdio/emit)(

    event: 'message',

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessByStdio/emit)(

    event: 'spawn',

    listener: () => void

    ): boolean;
  + [eventNames](https://bun.com/reference/node/child_process/ChildProcessByStdio/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/child_process/ChildProcessByStdio/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [kill](https://bun.com/reference/node/child_process/ChildProcessByStdio/kill)(

    signal?: number | Signals

    ): boolean;

    The `subprocess.kill()` method sends a signal to the child process. If no argument is given, the process will be sent the `'SIGTERM'` signal. See [`signal(7)`](http://man7.org/linux/man-pages/man7/signal.7.html) for a list of available signals. This function returns `true` if [`kill(2)`](http://man7.org/linux/man-pages/man2/kill.2.html) succeeds, and `false` otherwise.

    ```
    import { spawn } from 'node:child_process';
    const grep = spawn('grep', ['ssh']);

    grep.on('close', (code, signal) => {
      console.log(
        `child process terminated due to receipt of signal ${signal}`);
    });

    // Send SIGHUP to process.
    grep.kill('SIGHUP');
    ```

    The `ChildProcess` object may emit an `'error'` event if the signal cannot be delivered. Sending a signal to a child process that has already exited is not an error but may have unforeseen consequences. Specifically, if the process identifier (PID) has been reassigned to another process, the signal will be delivered to that process instead which can have unexpected results.

    While the function is called `kill`, the signal delivered to the child process may not actually terminate the process.

    See [`kill(2)`](http://man7.org/linux/man-pages/man2/kill.2.html) for reference.

    On Windows, where POSIX signals do not exist, the `signal` argument will be ignored, and the process will be killed forcefully and abruptly (similar to `'SIGKILL'`). See `Signal Events` for more details.

    On Linux, child processes of child processes will not be terminated when attempting to kill their parent. This is likely to happen when running a new process in a shell or with the use of the `shell` option of `ChildProcess`:

    ```
    'use strict';
    import { spawn } from 'node:child_process';

    const subprocess = spawn(
      'sh',
      [
        '-c',
        `node -e "setInterval(() => {
          console.log(process.pid, 'is alive')
        }, 500);"`,
      ], {
        stdio: ['inherit', 'inherit', 'inherit'],
      },
    );

    setTimeout(() => {
      subprocess.kill(); // Does not terminate the Node.js process in the shell.
    }, 2000);
    ```
  + [listenerCount](https://bun.com/reference/node/child_process/ChildProcessByStdio/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/child_process/ChildProcessByStdio/listeners)<K>(

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
  + [off](https://bun.com/reference/node/child_process/ChildProcessByStdio/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/child_process/ChildProcessByStdio/on)(

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

    [on](https://bun.com/reference/node/child_process/ChildProcessByStdio/on)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessByStdio/on)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessByStdio/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessByStdio/on)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessByStdio/on)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessByStdio/on)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [once](https://bun.com/reference/node/child_process/ChildProcessByStdio/once)(

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

    [once](https://bun.com/reference/node/child_process/ChildProcessByStdio/once)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessByStdio/once)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessByStdio/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessByStdio/once)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessByStdio/once)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessByStdio/once)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [prependListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependListener)(

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

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependListener)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependOnceListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependOnceListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependOnceListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependOnceListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/prependOnceListener)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/child_process/ChildProcessByStdio/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/child_process/ChildProcessByStdio/ref)(): void;

    Calling `subprocess.ref()` after making a call to `subprocess.unref()` will restore the removed reference count for the child process, forcing the parent to wait for the child to exit before exiting itself.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn(process.argv[0], ['child_program.js'], {
      detached: true,
      stdio: 'ignore',
    });

    subprocess.unref();
    subprocess.ref();
    ```
  + [removeAllListeners](https://bun.com/reference/node/child_process/ChildProcessByStdio/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/child_process/ChildProcessByStdio/removeListener)<K>(

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
  + [send](https://bun.com/reference/node/child_process/ChildProcessByStdio/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    [send](https://bun.com/reference/node/child_process/ChildProcessByStdio/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle?: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    @param sendHandle

    `undefined`, or a [`net.Socket`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netsocket), [`net.Server`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netserver), or [`dgram.Socket`](https://nodejs.org/docs/latest-v24.x/api/dgram.html#class-dgramsocket) object.

    [send](https://bun.com/reference/node/child_process/ChildProcessByStdio/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle?: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    options?: [MessageOptions](https://bun.com/reference/node/child_process/MessageOptions),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    @param sendHandle

    `undefined`, or a [`net.Socket`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netsocket), [`net.Server`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netserver), or [`dgram.Socket`](https://nodejs.org/docs/latest-v24.x/api/dgram.html#class-dgramsocket) object.

    @param options

    The `options` argument, if present, is an object used to parameterize the sending of certain types of handles. `options` supports the following properties:
  + [setMaxListeners](https://bun.com/reference/node/child_process/ChildProcessByStdio/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [unref](https://bun.com/reference/node/child_process/ChildProcessByStdio/unref)(): void;

    By default, the parent will wait for the detached child to exit. To prevent the parent from waiting for a given `subprocess` to exit, use the `subprocess.unref()` method. Doing so will cause the parent's event loop to not include the child in its reference count, allowing the parent to exit independently of the child, unless there is an established IPC channel between the child and the parent.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn(process.argv[0], ['child_program.js'], {
      detached: true,
      stdio: 'ignore',
    });

    subprocess.unref();
    ```
* ### interface [ChildProcessWithoutNullStreams](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams)

  Instances of the `ChildProcess` represent spawned child processes.

  Instances of `ChildProcess` are not intended to be created directly. Rather, use the spawn, exec,execFile, or fork methods to create instances of `ChildProcess`.

  + readonly [channel](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/channel)?: null | [Control](https://bun.com/reference/node/child_process/Control)

    The `subprocess.channel` property is a reference to the child's IPC channel. If no IPC channel exists, this property is `undefined`.
  + readonly [connected](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/connected): boolean

    The `subprocess.connected` property indicates whether it is still possible to send and receive messages from a child process. When `subprocess.connected` is `false`, it is no longer possible to send or receive messages.
  + readonly [exitCode](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/exitCode): null | number

    The `subprocess.exitCode` property indicates the exit code of the child process. If the child process is still running, the field will be `null`.
  + readonly [killed](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/killed): boolean

    The `subprocess.killed` property indicates whether the child process successfully received a signal from `subprocess.kill()`. The `killed` property does not indicate that the child process has been terminated.
  + readonly [pid](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/pid)?: number

    Returns the process identifier (PID) of the child process. If the child process fails to spawn due to errors, then the value is `undefined` and `error` is emitted.

    ```
    import { spawn } from 'node:child_process';
    const grep = spawn('grep', ['ssh']);

    console.log(`Spawned child pid: ${grep.pid}`);
    grep.stdin.end();
    ```
  + readonly [signalCode](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/signalCode): null | Signals

    The `subprocess.signalCode` property indicates the signal received by the child process if any, else `null`.
  + readonly [spawnargs](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/spawnargs): string[]

    The `subprocess.spawnargs` property represents the full list of command-line arguments the child process was launched with.
  + readonly [spawnfile](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/spawnfile): string

    The `subprocess.spawnfile` property indicates the executable file name of the child process that is launched.

    For fork, its value will be equal to `process.execPath`. For spawn, its value will be the name of the executable file. For exec, its value will be the name of the shell in which the child process is launched.
  + [stderr](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/stderr): [Readable](https://bun.com/reference/node/stream/default/Readable)

    A `Readable Stream` that represents the child process's `stderr`.

    If the child was spawned with `stdio[2]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stderr` is an alias for `subprocess.stdio[2]`. Both properties will refer to the same value.

    The `subprocess.stderr` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + [stdin](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/stdin): [Writable](https://bun.com/reference/node/stream/default/Writable)

    A `Writable Stream` that represents the child process's `stdin`.

    If a child process waits to read all of its input, the child will not continue until this stream has been closed via `end()`.

    If the child was spawned with `stdio[0]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stdin` is an alias for `subprocess.stdio[0]`. Both properties will refer to the same value.

    The `subprocess.stdin` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + readonly [stdio](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/stdio): [[Writable](https://bun.com/reference/node/stream/default/Writable), [Readable](https://bun.com/reference/node/stream/default/Readable), [Readable](https://bun.com/reference/node/stream/default/Readable), undefined | null | [Writable](https://bun.com/reference/node/stream/default/Writable) | [Readable](https://bun.com/reference/node/stream/default/Readable), undefined | null | [Writable](https://bun.com/reference/node/stream/default/Writable) | [Readable](https://bun.com/reference/node/stream/default/Readable)]

    A sparse array of pipes to the child process, corresponding with positions in the `stdio` option passed to spawn that have been set to the value `'pipe'`. `subprocess.stdio[0]`, `subprocess.stdio[1]`, and `subprocess.stdio[2]` are also available as `subprocess.stdin`, `subprocess.stdout`, and `subprocess.stderr`, respectively.

    In the following example, only the child's fd `1` (stdout) is configured as a pipe, so only the parent's `subprocess.stdio[1]` is a stream, all other values in the array are `null`.

    ```
    import assert from 'node:assert';
    import fs from 'node:fs';
    import child_process from 'node:child_process';

    const subprocess = child_process.spawn('ls', {
      stdio: [
        0, // Use parent's stdin for child.
        'pipe', // Pipe child's stdout to parent.
        fs.openSync('err.out', 'w'), // Direct child's stderr to a file.
      ],
    });

    assert.strictEqual(subprocess.stdio[0], null);
    assert.strictEqual(subprocess.stdio[0], subprocess.stdin);

    assert(subprocess.stdout);
    assert.strictEqual(subprocess.stdio[1], subprocess.stdout);

    assert.strictEqual(subprocess.stdio[2], null);
    assert.strictEqual(subprocess.stdio[2], subprocess.stderr);
    ```

    The `subprocess.stdio` property can be `undefined` if the child process could not be successfully spawned.
  + [stdout](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/stdout): [Readable](https://bun.com/reference/node/stream/default/Readable)

    A `Readable Stream` that represents the child process's `stdout`.

    If the child was spawned with `stdio[1]` set to anything other than `'pipe'`, then this will be `null`.

    `subprocess.stdout` is an alias for `subprocess.stdio[1]`. Both properties will refer to the same value.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn('ls');

    subprocess.stdout.on('data', (data) => {
      console.log(`Received chunk ${data}`);
    });
    ```

    The `subprocess.stdout` property can be `null` or `undefined` if the child process could not be successfully spawned.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [[Symbol.dispose]](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/[dispose])(): void;

    Calls ChildProcess.kill with `'SIGTERM'`.
  + [addListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/addListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/addListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/addListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/addListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn

    [addListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/addListener)(

    event: 'spawn',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. disconnect
    3. error
    4. exit
    5. message
    6. spawn
  + [disconnect](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/disconnect)(): void;

    Closes the IPC channel between parent and child, allowing the child to exit gracefully once there are no other connections keeping it alive. After calling this method the `subprocess.connected` and `process.connected` properties in both the parent and child (respectively) will be set to `false`, and it will be no longer possible to pass messages between the processes.

    The `'disconnect'` event will be emitted when there are no messages in the process of being received. This will most often be triggered immediately after calling `subprocess.disconnect()`.

    When the child process is a Node.js instance (e.g. spawned using fork), the `process.disconnect()` method can be invoked within the child process to close the IPC channel as well.
  + [emit](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/emit)(

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

    [emit](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/emit)(

    event: 'close',

    code: null | number,

    signal: null | Signals

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/emit)(

    event: 'disconnect'

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/emit)(

    event: 'exit',

    code: null | number,

    signal: null | Signals

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/emit)(

    event: 'message',

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)

    ): boolean;

    [emit](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/emit)(

    event: 'spawn',

    listener: () => void

    ): boolean;
  + [eventNames](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [kill](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/kill)(

    signal?: number | Signals

    ): boolean;

    The `subprocess.kill()` method sends a signal to the child process. If no argument is given, the process will be sent the `'SIGTERM'` signal. See [`signal(7)`](http://man7.org/linux/man-pages/man7/signal.7.html) for a list of available signals. This function returns `true` if [`kill(2)`](http://man7.org/linux/man-pages/man2/kill.2.html) succeeds, and `false` otherwise.

    ```
    import { spawn } from 'node:child_process';
    const grep = spawn('grep', ['ssh']);

    grep.on('close', (code, signal) => {
      console.log(
        `child process terminated due to receipt of signal ${signal}`);
    });

    // Send SIGHUP to process.
    grep.kill('SIGHUP');
    ```

    The `ChildProcess` object may emit an `'error'` event if the signal cannot be delivered. Sending a signal to a child process that has already exited is not an error but may have unforeseen consequences. Specifically, if the process identifier (PID) has been reassigned to another process, the signal will be delivered to that process instead which can have unexpected results.

    While the function is called `kill`, the signal delivered to the child process may not actually terminate the process.

    See [`kill(2)`](http://man7.org/linux/man-pages/man2/kill.2.html) for reference.

    On Windows, where POSIX signals do not exist, the `signal` argument will be ignored, and the process will be killed forcefully and abruptly (similar to `'SIGKILL'`). See `Signal Events` for more details.

    On Linux, child processes of child processes will not be terminated when attempting to kill their parent. This is likely to happen when running a new process in a shell or with the use of the `shell` option of `ChildProcess`:

    ```
    'use strict';
    import { spawn } from 'node:child_process';

    const subprocess = spawn(
      'sh',
      [
        '-c',
        `node -e "setInterval(() => {
          console.log(process.pid, 'is alive')
        }, 500);"`,
      ], {
        stdio: ['inherit', 'inherit', 'inherit'],
      },
    );

    setTimeout(() => {
      subprocess.kill(); // Does not terminate the Node.js process in the shell.
    }, 2000);
    ```
  + [listenerCount](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/listeners)<K>(

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
  + [off](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/on)(

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

    [on](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/on)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/on)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/on)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/on)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [on](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/on)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [once](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/once)(

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

    [once](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/once)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/once)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/once)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/once)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [once](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/once)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [prependListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependListener)(

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

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependListener)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependOnceListener)(

    event: 'close',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependOnceListener)(

    event: 'disconnect',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependOnceListener)(

    event: 'exit',

    listener: (code: null | number, signal: null | Signals) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependOnceListener)(

    event: 'message',

    listener: (message: [Serializable](https://bun.com/reference/node/child_process/Serializable), sendHandle: [SendHandle](https://bun.com/reference/node/child_process/SendHandle)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/prependOnceListener)(

    event: 'spawn',

    listener: () => void

    ): this;
  + [rawListeners](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/ref)(): void;

    Calling `subprocess.ref()` after making a call to `subprocess.unref()` will restore the removed reference count for the child process, forcing the parent to wait for the child to exit before exiting itself.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn(process.argv[0], ['child_program.js'], {
      detached: true,
      stdio: 'ignore',
    });

    subprocess.unref();
    subprocess.ref();
    ```
  + [removeAllListeners](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/removeListener)<K>(

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
  + [send](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    [send](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle?: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    @param sendHandle

    `undefined`, or a [`net.Socket`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netsocket), [`net.Server`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netserver), or [`dgram.Socket`](https://nodejs.org/docs/latest-v24.x/api/dgram.html#class-dgramsocket) object.

    [send](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/send)(

    message: [Serializable](https://bun.com/reference/node/child_process/Serializable),

    sendHandle?: [SendHandle](https://bun.com/reference/node/child_process/SendHandle),

    options?: [MessageOptions](https://bun.com/reference/node/child_process/MessageOptions),

    callback?: (error: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    When an IPC channel has been established between the parent and child ( i.e. when using fork), the `subprocess.send()` method can be used to send messages to the child process. When the child process is a Node.js instance, these messages can be received via the `'message'` event.

    The message goes through serialization and parsing. The resulting message might not be the same as what is originally sent.

    For example, in the parent script:

    ```
    import cp from 'node:child_process';
    const n = cp.fork(`${__dirname}/sub.js`);

    n.on('message', (m) => {
      console.log('PARENT got message:', m);
    });

    // Causes the child to print: CHILD got message: { hello: 'world' }
    n.send({ hello: 'world' });
    ```

    And then the child script, `'sub.js'` might look like this:

    ```
    process.on('message', (m) => {
      console.log('CHILD got message:', m);
    });

    // Causes the parent to print: PARENT got message: { foo: 'bar', baz: null }
    process.send({ foo: 'bar', baz: NaN });
    ```

    Child Node.js processes will have a `process.send()` method of their own that allows the child to send messages back to the parent.

    There is a special case when sending a `{cmd: 'NODE_foo'}` message. Messages containing a `NODE_` prefix in the `cmd` property are reserved for use within Node.js core and will not be emitted in the child's `'message'` event. Rather, such messages are emitted using the `'internalMessage'` event and are consumed internally by Node.js. Applications should avoid using such messages or listening for `'internalMessage'` events as it is subject to change without notice.

    The optional `sendHandle` argument that may be passed to `subprocess.send()` is for passing a TCP server or socket object to the child process. The child will receive the object as the second argument passed to the callback function registered on the `'message'` event. Any data that is received and buffered in the socket will not be sent to the child. Sending IPC sockets is not supported on Windows.

    The optional `callback` is a function that is invoked after the message is sent but before the child may have received it. The function is called with a single argument: `null` on success, or an `Error` object on failure.

    If no `callback` function is provided and the message cannot be sent, an `'error'` event will be emitted by the `ChildProcess` object. This can happen, for instance, when the child process has already exited.

    `subprocess.send()` will return `false` if the channel has closed or when the backlog of unsent messages exceeds a threshold that makes it unwise to send more. Otherwise, the method returns `true`. The `callback` function can be used to implement flow control.

    #### Example: sending a server object

    The `sendHandle` argument can be used, for instance, to pass the handle of a TCP server object to the child process as illustrated in the example below:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const subprocess = fork('subprocess.js');

    // Open up the server object and send the handle.
    const server = createServer();
    server.on('connection', (socket) => {
      socket.end('handled by parent');
    });
    server.listen(1337, () => {
      subprocess.send('server', server);
    });
    ```

    The child would then receive the server object as:

    ```
    process.on('message', (m, server) => {
      if (m === 'server') {
        server.on('connection', (socket) => {
          socket.end('handled by child');
        });
      }
    });
    ```

    Once the server is now shared between the parent and child, some connections can be handled by the parent and some by the child.

    While the example above uses a server created using the `node:net` module, `node:dgram` module servers use exactly the same workflow with the exceptions of listening on a `'message'` event instead of `'connection'` and using `server.bind()` instead of `server.listen()`. This is, however, only supported on Unix platforms.

    #### Example: sending a socket object

    Similarly, the `sendHandler` argument can be used to pass the handle of a socket to the child process. The example below spawns two children that each handle connections with "normal" or "special" priority:

    ```
    import { createServer } from 'node:net';
    import { fork } from 'node:child_process';
    const normal = fork('subprocess.js', ['normal']);
    const special = fork('subprocess.js', ['special']);

    // Open up the server and send sockets to child. Use pauseOnConnect to prevent
    // the sockets from being read before they are sent to the child process.
    const server = createServer({ pauseOnConnect: true });
    server.on('connection', (socket) => {

      // If this is special priority...
      if (socket.remoteAddress === '74.125.127.100') {
        special.send('socket', socket);
        return;
      }
      // This is normal priority.
      normal.send('socket', socket);
    });
    server.listen(1337);
    ```

    The `subprocess.js` would receive the socket handle as the second argument passed to the event callback function:

    ```
    process.on('message', (m, socket) => {
      if (m === 'socket') {
        if (socket) {
          // Check that the client socket exists.
          // It is possible for the socket to be closed between the time it is
          // sent and the time it is received in the child process.
          socket.end(`Request handled with ${process.argv[2]} priority`);
        }
      }
    });
    ```

    Do not use `.maxConnections` on a socket that has been passed to a subprocess. The parent cannot track when the socket is destroyed.

    Any `'message'` handlers in the subprocess should verify that `socket` exists, as the connection may have been closed during the time it takes to send the connection to the child.

    @param sendHandle

    `undefined`, or a [`net.Socket`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netsocket), [`net.Server`](https://nodejs.org/docs/latest-v24.x/api/net.html#class-netserver), or [`dgram.Socket`](https://nodejs.org/docs/latest-v24.x/api/dgram.html#class-dgramsocket) object.

    @param options

    The `options` argument, if present, is an object used to parameterize the sending of certain types of handles. `options` supports the following properties:
  + [setMaxListeners](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [unref](https://bun.com/reference/node/child_process/ChildProcessWithoutNullStreams/unref)(): void;

    By default, the parent will wait for the detached child to exit. To prevent the parent from waiting for a given `subprocess` to exit, use the `subprocess.unref()` method. Doing so will cause the parent's event loop to not include the child in its reference count, allowing the parent to exit independently of the child, unless there is an established IPC channel between the child and the parent.

    ```
    import { spawn } from 'node:child_process';

    const subprocess = spawn(process.argv[0], ['child_program.js'], {
      detached: true,
      stdio: 'ignore',
    });

    subprocess.unref();
    ```
* ### interface [CommonExecOptions](https://bun.com/reference/node/child_process/CommonExecOptions)

  + [cwd](https://bun.com/reference/node/child_process/CommonExecOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/CommonExecOptions/encoding)?: null | BufferEncoding | 'buffer'
  + [env](https://bun.com/reference/node/child_process/CommonExecOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/CommonExecOptions/gid)?: number
  + [input](https://bun.com/reference/node/child_process/CommonExecOptions/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/CommonExecOptions/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/CommonExecOptions/maxBuffer)?: number
  + [stdio](https://bun.com/reference/node/child_process/CommonExecOptions/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit, or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/CommonExecOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/CommonExecOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/CommonExecOptions/windowsHide)?: boolean
* ### interface [CommonOptions](https://bun.com/reference/node/child_process/CommonOptions)

  + [cwd](https://bun.com/reference/node/child_process/CommonOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [env](https://bun.com/reference/node/child_process/CommonOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/CommonOptions/gid)?: number
  + [timeout](https://bun.com/reference/node/child_process/CommonOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/CommonOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/CommonOptions/windowsHide)?: boolean
* ### interface [CommonSpawnOptions](https://bun.com/reference/node/child_process/CommonSpawnOptions)

  + [argv0](https://bun.com/reference/node/child_process/CommonSpawnOptions/argv0)?: string
  + [cwd](https://bun.com/reference/node/child_process/CommonSpawnOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [env](https://bun.com/reference/node/child_process/CommonSpawnOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/CommonSpawnOptions/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/CommonSpawnOptions/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [serialization](https://bun.com/reference/node/child_process/CommonSpawnOptions/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [shell](https://bun.com/reference/node/child_process/CommonSpawnOptions/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/CommonSpawnOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [stdio](https://bun.com/reference/node/child_process/CommonSpawnOptions/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/CommonSpawnOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/CommonSpawnOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/CommonSpawnOptions/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/CommonSpawnOptions/windowsVerbatimArguments)?: boolean
* ### interface [Control](https://bun.com/reference/node/child_process/Control)

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/child_process/Control/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/child_process/Control/addListener)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [emit](https://bun.com/reference/node/child_process/Control/emit)<K>(

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
  + [eventNames](https://bun.com/reference/node/child_process/Control/eventNames)(): string | symbol[];

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
  + [getMaxListeners](https://bun.com/reference/node/child_process/Control/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/child_process/Control/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/child_process/Control/listeners)<K>(

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
  + [off](https://bun.com/reference/node/child_process/Control/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/child_process/Control/on)<K>(

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
  + [once](https://bun.com/reference/node/child_process/Control/once)<K>(

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
  + [prependListener](https://bun.com/reference/node/child_process/Control/prependListener)<K>(

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
  + [prependOnceListener](https://bun.com/reference/node/child_process/Control/prependOnceListener)<K>(

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
  + [rawListeners](https://bun.com/reference/node/child_process/Control/rawListeners)<K>(

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
  + [ref](https://bun.com/reference/node/child_process/Control/ref)(): void;
  + [removeAllListeners](https://bun.com/reference/node/child_process/Control/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/child_process/Control/removeListener)<K>(

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
  + [setMaxListeners](https://bun.com/reference/node/child_process/Control/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [unref](https://bun.com/reference/node/child_process/Control/unref)(): void;
* ### interface [ExecException](https://bun.com/reference/node/child_process/ExecException)

  + [cause](https://bun.com/reference/node/child_process/ExecException/cause)?: unknown

    The cause of the error.
  + [cmd](https://bun.com/reference/node/child_process/ExecException/cmd)?: string
  + [code](https://bun.com/reference/node/child_process/ExecException/code)?: number
  + [killed](https://bun.com/reference/node/child_process/ExecException/killed)?: boolean
  + [message](https://bun.com/reference/node/child_process/ExecException/message): string
  + [name](https://bun.com/reference/node/child_process/ExecException/name): string
  + [signal](https://bun.com/reference/node/child_process/ExecException/signal)?: Signals
  + [stack](https://bun.com/reference/node/child_process/ExecException/stack)?: string
  + [stderr](https://bun.com/reference/node/child_process/ExecException/stderr)?: string
  + [stdout](https://bun.com/reference/node/child_process/ExecException/stdout)?: string
* ### interface [ExecFileOptions](https://bun.com/reference/node/child_process/ExecFileOptions)

  + [cwd](https://bun.com/reference/node/child_process/ExecFileOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecFileOptions/encoding)?: null | string
  + [env](https://bun.com/reference/node/child_process/ExecFileOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecFileOptions/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/ExecFileOptions/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecFileOptions/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecFileOptions/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/ExecFileOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [timeout](https://bun.com/reference/node/child_process/ExecFileOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecFileOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecFileOptions/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/ExecFileOptions/windowsVerbatimArguments)?: boolean
* ### interface [ExecFileOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/encoding): null | 'buffer'
  + [env](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [timeout](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/ExecFileOptionsWithBufferEncoding/windowsVerbatimArguments)?: boolean
* ### interface [ExecFileOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/encoding)?: BufferEncoding
  + [env](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [timeout](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/ExecFileOptionsWithStringEncoding/windowsVerbatimArguments)?: boolean
* ### interface [ExecFileSyncOptions](https://bun.com/reference/node/child_process/ExecFileSyncOptions)

  + [cwd](https://bun.com/reference/node/child_process/ExecFileSyncOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecFileSyncOptions/encoding)?: null | BufferEncoding | 'buffer'
  + [env](https://bun.com/reference/node/child_process/ExecFileSyncOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecFileSyncOptions/gid)?: number
  + [input](https://bun.com/reference/node/child_process/ExecFileSyncOptions/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/ExecFileSyncOptions/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecFileSyncOptions/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecFileSyncOptions/shell)?: string | boolean
  + [stdio](https://bun.com/reference/node/child_process/ExecFileSyncOptions/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit, or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/ExecFileSyncOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecFileSyncOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecFileSyncOptions/windowsHide)?: boolean
* ### interface [ExecFileSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/encoding)?: null | 'buffer'
  + [env](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/gid)?: number
  + [input](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/shell)?: string | boolean
  + [stdio](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit, or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithBufferEncoding/windowsHide)?: boolean
* ### interface [ExecFileSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/encoding): BufferEncoding
  + [env](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/gid)?: number
  + [input](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/shell)?: string | boolean
  + [stdio](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit, or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecFileSyncOptionsWithStringEncoding/windowsHide)?: boolean
* ### interface [ExecOptions](https://bun.com/reference/node/child_process/ExecOptions)

  + [cwd](https://bun.com/reference/node/child_process/ExecOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecOptions/encoding)?: null | string
  + [env](https://bun.com/reference/node/child_process/ExecOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecOptions/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/ExecOptions/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecOptions/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecOptions/shell)?: string
  + [signal](https://bun.com/reference/node/child_process/ExecOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [timeout](https://bun.com/reference/node/child_process/ExecOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecOptions/windowsHide)?: boolean
* ### interface [ExecOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/encoding): null | 'buffer'
  + [env](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/shell)?: string
  + [signal](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [timeout](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecOptionsWithBufferEncoding/windowsHide)?: boolean
* ### interface [ExecOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/encoding)?: BufferEncoding
  + [env](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/shell)?: string
  + [signal](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
  + [timeout](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecOptionsWithStringEncoding/windowsHide)?: boolean
* ### interface [ExecSyncOptions](https://bun.com/reference/node/child_process/ExecSyncOptions)

  + [cwd](https://bun.com/reference/node/child_process/ExecSyncOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecSyncOptions/encoding)?: null | BufferEncoding | 'buffer'
  + [env](https://bun.com/reference/node/child_process/ExecSyncOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecSyncOptions/gid)?: number
  + [input](https://bun.com/reference/node/child_process/ExecSyncOptions/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/ExecSyncOptions/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecSyncOptions/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecSyncOptions/shell)?: string
  + [stdio](https://bun.com/reference/node/child_process/ExecSyncOptions/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit, or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/ExecSyncOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecSyncOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecSyncOptions/windowsHide)?: boolean
* ### interface [ExecSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/encoding)?: null | 'buffer'
  + [env](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/gid)?: number
  + [input](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/shell)?: string
  + [stdio](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit, or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecSyncOptionsWithBufferEncoding/windowsHide)?: boolean
* ### interface [ExecSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding)

  + [cwd](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/encoding): BufferEncoding
  + [env](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/gid)?: number
  + [input](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/killSignal)?: number | Signals
  + [maxBuffer](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/maxBuffer)?: number
  + [shell](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/shell)?: string
  + [stdio](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit, or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/ExecSyncOptionsWithStringEncoding/windowsHide)?: boolean
* ### interface [ForkOptions](https://bun.com/reference/node/child_process/ForkOptions)

  + [cwd](https://bun.com/reference/node/child_process/ForkOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [detached](https://bun.com/reference/node/child_process/ForkOptions/detached)?: boolean
  + [env](https://bun.com/reference/node/child_process/ForkOptions/env)?: ProcessEnv
  + [execArgv](https://bun.com/reference/node/child_process/ForkOptions/execArgv)?: string[]
  + [execPath](https://bun.com/reference/node/child_process/ForkOptions/execPath)?: string
  + [gid](https://bun.com/reference/node/child_process/ForkOptions/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/ForkOptions/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [serialization](https://bun.com/reference/node/child_process/ForkOptions/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [signal](https://bun.com/reference/node/child_process/ForkOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [silent](https://bun.com/reference/node/child_process/ForkOptions/silent)?: boolean
  + [stdio](https://bun.com/reference/node/child_process/ForkOptions/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/ForkOptions/timeout)?: number

    In milliseconds the maximum amount of time the process is allowed to run.
  + [uid](https://bun.com/reference/node/child_process/ForkOptions/uid)?: number
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/ForkOptions/windowsVerbatimArguments)?: boolean
* ### interface [MessageOptions](https://bun.com/reference/node/child_process/MessageOptions)

  + [keepOpen](https://bun.com/reference/node/child_process/MessageOptions/keepOpen)?: boolean
* ### interface [MessagingOptions](https://bun.com/reference/node/child_process/MessagingOptions)

  + [killSignal](https://bun.com/reference/node/child_process/MessagingOptions/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [serialization](https://bun.com/reference/node/child_process/MessagingOptions/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [signal](https://bun.com/reference/node/child_process/MessagingOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [timeout](https://bun.com/reference/node/child_process/MessagingOptions/timeout)?: number

    In milliseconds the maximum amount of time the process is allowed to run.
* ### interface [ProcessEnvOptions](https://bun.com/reference/node/child_process/ProcessEnvOptions)

  + [cwd](https://bun.com/reference/node/child_process/ProcessEnvOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [env](https://bun.com/reference/node/child_process/ProcessEnvOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/ProcessEnvOptions/gid)?: number
  + [uid](https://bun.com/reference/node/child_process/ProcessEnvOptions/uid)?: number
* ### interface [PromiseWithChild](https://bun.com/reference/node/child_process/PromiseWithChild)<T>

  + readonly [[Symbol.toStringTag]](https://bun.com/reference/node/child_process/PromiseWithChild/[toStringTag]): string
  + [child](https://bun.com/reference/node/child_process/PromiseWithChild/child): [ChildProcess](https://bun.com/reference/node/child_process/ChildProcess)
  + [catch](https://bun.com/reference/node/child_process/PromiseWithChild/catch)<TResult = never>(

    onrejected?: null | (reason: any) => TResult | PromiseLike<TResult>

    ): Promise<T | TResult>;

    Attaches a callback for only the rejection of the Promise.

    @param onrejected

    The callback to execute when the Promise is rejected.

    @returns

    A Promise for the completion of the callback.
  + [finally](https://bun.com/reference/node/child_process/PromiseWithChild/finally)(

    onfinally?: null | () => void

    ): Promise<T>;

    Attaches a callback that is invoked when the Promise is settled (fulfilled or rejected). The resolved value cannot be modified from the callback.

    @param onfinally

    The callback to execute when the Promise is settled (fulfilled or rejected).

    @returns

    A Promise for the completion of the callback.
  + [then](https://bun.com/reference/node/child_process/PromiseWithChild/then)<TResult1 = T, TResult2 = never>(

    onfulfilled?: null | (value: T) => TResult1 | PromiseLike<TResult1>,

    onrejected?: null | (reason: any) => TResult2 | PromiseLike<TResult2>

    ): Promise<TResult1 | TResult2>;

    Attaches callbacks for the resolution and/or rejection of the Promise.

    @param onfulfilled

    The callback to execute when the Promise is resolved.

    @param onrejected

    The callback to execute when the Promise is rejected.

    @returns

    A Promise for the completion of which ever callback is executed.
* ### interface [SpawnOptions](https://bun.com/reference/node/child_process/SpawnOptions)

  + [argv0](https://bun.com/reference/node/child_process/SpawnOptions/argv0)?: string
  + [cwd](https://bun.com/reference/node/child_process/SpawnOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [detached](https://bun.com/reference/node/child_process/SpawnOptions/detached)?: boolean
  + [env](https://bun.com/reference/node/child_process/SpawnOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/SpawnOptions/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/SpawnOptions/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [serialization](https://bun.com/reference/node/child_process/SpawnOptions/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [shell](https://bun.com/reference/node/child_process/SpawnOptions/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/SpawnOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [stdio](https://bun.com/reference/node/child_process/SpawnOptions/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/SpawnOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/SpawnOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/SpawnOptions/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/SpawnOptions/windowsVerbatimArguments)?: boolean
* ### interface [SpawnOptionsWithoutStdio](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio)

  + [argv0](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/argv0)?: string
  + [cwd](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [detached](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/detached)?: boolean
  + [env](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [serialization](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [shell](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [stdio](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/stdio)?: [StdioPipeNamed](https://bun.com/reference/node/child_process/StdioPipeNamed) | [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)[]

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/SpawnOptionsWithoutStdio/windowsVerbatimArguments)?: boolean
* ### interface [SpawnOptionsWithStdioTuple](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple)<Stdin extends [StdioNull](https://bun.com/reference/node/child_process/StdioNull) | [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), Stdout extends [StdioNull](https://bun.com/reference/node/child_process/StdioNull) | [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe), Stderr extends [StdioNull](https://bun.com/reference/node/child_process/StdioNull) | [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe)>

  + [argv0](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/argv0)?: string
  + [cwd](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [detached](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/detached)?: boolean
  + [env](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/gid)?: number
  + [killSignal](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [serialization](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [shell](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [stdio](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/stdio): [Stdin, Stdout, Stderr]

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/SpawnOptionsWithStdioTuple/windowsVerbatimArguments)?: boolean
* ### interface [SpawnSyncOptions](https://bun.com/reference/node/child_process/SpawnSyncOptions)

  + [argv0](https://bun.com/reference/node/child_process/SpawnSyncOptions/argv0)?: string
  + [cwd](https://bun.com/reference/node/child_process/SpawnSyncOptions/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/SpawnSyncOptions/encoding)?: null | BufferEncoding | 'buffer'
  + [env](https://bun.com/reference/node/child_process/SpawnSyncOptions/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/SpawnSyncOptions/gid)?: number
  + [input](https://bun.com/reference/node/child_process/SpawnSyncOptions/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/SpawnSyncOptions/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [maxBuffer](https://bun.com/reference/node/child_process/SpawnSyncOptions/maxBuffer)?: number
  + [serialization](https://bun.com/reference/node/child_process/SpawnSyncOptions/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [shell](https://bun.com/reference/node/child_process/SpawnSyncOptions/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/SpawnSyncOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [stdio](https://bun.com/reference/node/child_process/SpawnSyncOptions/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/SpawnSyncOptions/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/SpawnSyncOptions/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/SpawnSyncOptions/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/SpawnSyncOptions/windowsVerbatimArguments)?: boolean
* ### interface [SpawnSyncOptionsWithBufferEncoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding)

  + [argv0](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/argv0)?: string
  + [cwd](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/encoding)?: null | 'buffer'
  + [env](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/gid)?: number
  + [input](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [maxBuffer](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/maxBuffer)?: number
  + [serialization](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [shell](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [stdio](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithBufferEncoding/windowsVerbatimArguments)?: boolean
* ### interface [SpawnSyncOptionsWithStringEncoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding)

  + [argv0](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/argv0)?: string
  + [cwd](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/cwd)?: string | [URL](https://bun.com/reference/node/url/URL)
  + [encoding](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/encoding): BufferEncoding
  + [env](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/env)?: ProcessEnv
  + [gid](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/gid)?: number
  + [input](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/input)?: string | ArrayBufferView<ArrayBufferLike>
  + [killSignal](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/killSignal)?: number | Signals

    The signal value to be used when the spawned process will be killed by the abort signal.
  + [maxBuffer](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/maxBuffer)?: number
  + [serialization](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/serialization)?: [SerializationType](https://bun.com/reference/node/child_process/SerializationType)

    Specify the kind of serialization used for sending messages between processes.
  + [shell](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/shell)?: string | boolean
  + [signal](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [stdio](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/stdio)?: [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions)

    Can be set to 'pipe', 'inherit', 'overlapped', or 'ignore', or an array of these strings. If passed as an array, the first element is used for `stdin`, the second for `stdout`, and the third for `stderr`. A fourth element can be used to specify the `stdio` behavior beyond the standard streams. See ChildProcess.stdio for more information.
  + [timeout](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/timeout)?: number
  + [uid](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/uid)?: number
  + [windowsHide](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/windowsHide)?: boolean
  + [windowsVerbatimArguments](https://bun.com/reference/node/child_process/SpawnSyncOptionsWithStringEncoding/windowsVerbatimArguments)?: boolean
* ### interface [SpawnSyncReturns](https://bun.com/reference/node/child_process/SpawnSyncReturns)<T>

  + [error](https://bun.com/reference/node/child_process/SpawnSyncReturns/error)?: [Error](https://bun.com/reference/globals/Error)
  + [output](https://bun.com/reference/node/child_process/SpawnSyncReturns/output): null | T[]
  + [pid](https://bun.com/reference/node/child_process/SpawnSyncReturns/pid): number
  + [signal](https://bun.com/reference/node/child_process/SpawnSyncReturns/signal): null | Signals
  + [status](https://bun.com/reference/node/child_process/SpawnSyncReturns/status): null | number
  + [stderr](https://bun.com/reference/node/child_process/SpawnSyncReturns/stderr): T
  + [stdout](https://bun.com/reference/node/child_process/SpawnSyncReturns/stdout): T
* type [ExecFileException](https://bun.com/reference/node/child_process/ExecFileException) = Omit<[ExecException](https://bun.com/reference/node/child_process/ExecException), 'code'> & Omit<NodeJS.ErrnoException, 'code'> & { code: string | number | null }
* type [IOType](https://bun.com/reference/node/child_process/IOType) = 'overlapped' | 'pipe' | 'ignore' | 'inherit'
* type [SendHandle](https://bun.com/reference/node/child_process/SendHandle) = [net.Socket](https://bun.com/reference/node/net/Socket) | [net.Server](https://bun.com/reference/node/net/Server) | [dgram.Socket](https://bun.com/reference/node/dgram/Socket) | undefined
* type [Serializable](https://bun.com/reference/node/child_process/Serializable) = string | object | number | boolean | bigint
* type [SerializationType](https://bun.com/reference/node/child_process/SerializationType) = 'json' | 'advanced'
* type [StdioNull](https://bun.com/reference/node/child_process/StdioNull) = 'inherit' | 'ignore' | [Stream](https://bun.com/reference/node/stream/default)
* type [StdioOptions](https://bun.com/reference/node/child_process/StdioOptions) = [IOType](https://bun.com/reference/node/child_process/IOType) | [IOType](https://bun.com/reference/node/child_process/IOType) | 'ipc' | [Stream](https://bun.com/reference/node/stream/default) | number | null | undefined[]
* type [StdioPipe](https://bun.com/reference/node/child_process/StdioPipe) = undefined | null | [StdioPipeNamed](https://bun.com/reference/node/child_process/StdioPipeNamed)
* type [StdioPipeNamed](https://bun.com/reference/node/child_process/StdioPipeNamed) = 'pipe' | 'overlapped'