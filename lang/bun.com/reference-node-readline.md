---
url: https://bun.com/reference/node/readline
title: Node.js readline module | API Reference | Bun
source_domain: bun.com
---

# Node.js readline module | API Reference | Bun

Node.js module

# [readline](https://bun.com/reference/node/readline)

The `'node:readline'` module provides an interface for reading data from a Readable stream (such as process.stdin) one line at a time. It includes the `readline.Interface` class with `question`, `on('line')`, and `close` events.

Use cases include building command-line tools, interactive prompts, and REPL-style applications.

Works in Bun

Fully implemented.

* ### class [Interface](https://bun.com/reference/node/readline/Interface)

  Instances of the `readline.Interface` class are constructed using the `readline.createInterface()` method. Every instance is associated with a single `input` [Readable](https://nodejs.org/docs/latest-v24.x/api/stream.html#readable-streams) stream and a single `output` [Writable](https://nodejs.org/docs/latest-v24.x/api/stream.html#writable-streams) stream. The `output` stream is used to print prompts for user input that arrives on, and is read from, the `input` stream.

  + readonly [cursor](https://bun.com/reference/node/readline/Interface/cursor): number

    The cursor position relative to `rl.line`.

    This will track where the current cursor lands in the input string, when reading input from a TTY stream. The position of cursor determines the portion of the input string that will be modified as input is processed, as well as the column where the terminal caret will be rendered.
  + readonly [line](https://bun.com/reference/node/readline/Interface/line): string

    The current input data being processed by node.

    This can be used when collecting input from a TTY stream to retrieve the current value that has been processed thus far, prior to the `line` event being emitted. Once the `line` event has been emitted, this property will be an empty string.

    Be aware that modifying the value during the instance runtime may have unintended consequences if `rl.cursor` is not also controlled.

    **If not using a TTY stream for input, use the `'line'` event.**

    One possible use case would be as follows:

    ```
    const values = ['lorem ipsum', 'dolor sit amet'];
    const rl = readline.createInterface(process.stdin);
    const showResults = debounce(() => {
      console.log(
        '\n',
        values.filter((val) => val.startsWith(rl.line)).join(' '),
      );
    }, 300);
    process.stdin.on('keypress', (c, k) => {
      showResults();
    });
    ```
  + readonly [terminal](https://bun.com/reference/node/readline/Interface/terminal): boolean
  + static [captureRejections](https://bun.com/reference/node/readline/Interface/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/readline/Interface/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/readline/Interface/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/readline/Interface/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/readline/Interface/[asyncIterator])(): AsyncIterator<string>;
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/readline/Interface/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [[Symbol.dispose]](https://bun.com/reference/node/readline/Interface/[dispose])(): void;

    Alias for `rl.close()`.
  + [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: string,

    listener: (...args: any[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'line',

    listener: (input: string) => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'SIGCONT',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'SIGINT',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'SIGTSTP',

    listener: () => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history

    [addListener](https://bun.com/reference/node/readline/Interface/addListener)(

    event: 'history',

    listener: (history: string[]) => void

    ): this;

    events.EventEmitter

    1. close
    2. line
    3. pause
    4. resume
    5. SIGCONT
    6. SIGINT
    7. SIGTSTP
    8. history
  + [close](https://bun.com/reference/node/readline/Interface/close)(): void;

    The `rl.close()` method closes the `Interface` instance and relinquishes control over the `input` and `output` streams. When called, the `'close'` event will be emitted.

    Calling `rl.close()` does not immediately stop other events (including `'line'`) from being emitted by the `Interface` instance.
  + [emit](https://bun.com/reference/node/readline/Interface/emit)(

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

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'close'

    ): boolean;

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'line',

    input: string

    ): boolean;

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'SIGCONT'

    ): boolean;

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'SIGINT'

    ): boolean;

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'SIGTSTP'

    ): boolean;

    [emit](https://bun.com/reference/node/readline/Interface/emit)(

    event: 'history',

    history: string[]

    ): boolean;
  + [eventNames](https://bun.com/reference/node/readline/Interface/eventNames)(): string | symbol[];

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
  + [getCursorPos](https://bun.com/reference/node/readline/Interface/getCursorPos)(): [CursorPos](https://bun.com/reference/node/readline/CursorPos);

    Returns the real position of the cursor in relation to the input prompt + string. Long input (wrapping) strings, as well as multiple line prompts are included in the calculations.
  + [getMaxListeners](https://bun.com/reference/node/readline/Interface/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [getPrompt](https://bun.com/reference/node/readline/Interface/getPrompt)(): string;

    The `rl.getPrompt()` method returns the current prompt used by `rl.prompt()`.

    @returns

    the current prompt string
  + [listenerCount](https://bun.com/reference/node/readline/Interface/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/readline/Interface/listeners)<K>(

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
  + [off](https://bun.com/reference/node/readline/Interface/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/readline/Interface/on)(

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

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'close',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'line',

    listener: (input: string) => void

    ): this;

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'SIGCONT',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'SIGINT',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'SIGTSTP',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/readline/Interface/on)(

    event: 'history',

    listener: (history: string[]) => void

    ): this;
  + [once](https://bun.com/reference/node/readline/Interface/once)(

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

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'close',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'line',

    listener: (input: string) => void

    ): this;

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'SIGCONT',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'SIGINT',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'SIGTSTP',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/readline/Interface/once)(

    event: 'history',

    listener: (history: string[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/readline/Interface/pause)(): this;

    The `rl.pause()` method pauses the `input` stream, allowing it to be resumed later if necessary.

    Calling `rl.pause()` does not immediately pause other events (including `'line'`) from being emitted by the `Interface` instance.
  + [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

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

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'line',

    listener: (input: string) => void

    ): this;

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'SIGCONT',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'SIGINT',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'SIGTSTP',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/readline/Interface/prependListener)(

    event: 'history',

    listener: (history: string[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

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

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'line',

    listener: (input: string) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'SIGCONT',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'SIGINT',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'SIGTSTP',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/readline/Interface/prependOnceListener)(

    event: 'history',

    listener: (history: string[]) => void

    ): this;
  + [prompt](https://bun.com/reference/node/readline/Interface/prompt)(

    preserveCursor?: boolean

    ): void;

    The `rl.prompt()` method writes the `Interface` instances configured`prompt` to a new line in `output` in order to provide a user with a new location at which to provide input.

    When called, `rl.prompt()` will resume the `input` stream if it has been paused.

    If the `Interface` was created with `output` set to `null` or `undefined` the prompt is not written.

    @param preserveCursor

    If `true`, prevents the cursor placement from being reset to `0`.
  + [question](https://bun.com/reference/node/readline/Interface/question)(

    query: string,

    callback: (answer: string) => void

    ): void;

    The `rl.question()` method displays the `query` by writing it to the `output`, waits for user input to be provided on `input`, then invokes the `callback` function passing the provided input as the first argument.

    When called, `rl.question()` will resume the `input` stream if it has been paused.

    If the `Interface` was created with `output` set to `null` or `undefined` the `query` is not written.

    The `callback` function passed to `rl.question()` does not follow the typical pattern of accepting an `Error` object or `null` as the first argument. The `callback` is called with the provided answer as the only argument.

    An error will be thrown if calling `rl.question()` after `rl.close()`.

    Example usage:

    ```
    rl.question('What is your favorite food? ', (answer) => {
      console.log(`Oh, so your favorite food is ${answer}`);
    });
    ```

    Using an `AbortController` to cancel a question.

    ```
    const ac = new AbortController();
    const signal = ac.signal;

    rl.question('What is your favorite food? ', { signal }, (answer) => {
      console.log(`Oh, so your favorite food is ${answer}`);
    });

    signal.addEventListener('abort', () => {
      console.log('The food question timed out');
    }, { once: true });

    setTimeout(() => ac.abort(), 10000);
    ```

    @param query

    A statement or query to write to `output`, prepended to the prompt.

    @param callback

    A callback function that is invoked with the user's input in response to the `query`.

    [question](https://bun.com/reference/node/readline/Interface/question)(

    query: string,

    options: [Abortable](https://bun.com/reference/node/events/default/Abortable),

    callback: (answer: string) => void

    ): void;

    The `rl.question()` method displays the `query` by writing it to the `output`, waits for user input to be provided on `input`, then invokes the `callback` function passing the provided input as the first argument.

    When called, `rl.question()` will resume the `input` stream if it has been paused.

    If the `Interface` was created with `output` set to `null` or `undefined` the `query` is not written.

    The `callback` function passed to `rl.question()` does not follow the typical pattern of accepting an `Error` object or `null` as the first argument. The `callback` is called with the provided answer as the only argument.

    An error will be thrown if calling `rl.question()` after `rl.close()`.

    Example usage:

    ```
    rl.question('What is your favorite food? ', (answer) => {
      console.log(`Oh, so your favorite food is ${answer}`);
    });
    ```

    Using an `AbortController` to cancel a question.

    ```
    const ac = new AbortController();
    const signal = ac.signal;

    rl.question('What is your favorite food? ', { signal }, (answer) => {
      console.log(`Oh, so your favorite food is ${answer}`);
    });

    signal.addEventListener('abort', () => {
      console.log('The food question timed out');
    }, { once: true });

    setTimeout(() => ac.abort(), 10000);
    ```

    @param query

    A statement or query to write to `output`, prepended to the prompt.

    @param callback

    A callback function that is invoked with the user's input in response to the `query`.
  + [rawListeners](https://bun.com/reference/node/readline/Interface/rawListeners)<K>(

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
  + [removeAllListeners](https://bun.com/reference/node/readline/Interface/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/readline/Interface/removeListener)<K>(

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
  + [resume](https://bun.com/reference/node/readline/Interface/resume)(): this;

    The `rl.resume()` method resumes the `input` stream if it has been paused.
  + [setMaxListeners](https://bun.com/reference/node/readline/Interface/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [setPrompt](https://bun.com/reference/node/readline/Interface/setPrompt)(

    prompt: string

    ): void;

    The `rl.setPrompt()` method sets the prompt that will be written to `output` whenever `rl.prompt()` is called.
  + [write](https://bun.com/reference/node/readline/Interface/write)(

    data: string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>,

    key?: [Key](https://bun.com/reference/node/readline/Key)

    ): void;

    The `rl.write()` method will write either `data` or a key sequence identified by `key` to the `output`. The `key` argument is supported only if `output` is a `TTY` text terminal. See `TTY keybindings` for a list of key combinations.

    If `key` is specified, `data` is ignored.

    When called, `rl.write()` will resume the `input` stream if it has been paused.

    If the `Interface` was created with `output` set to `null` or `undefined` the `data` and `key` are not written.

    ```
    rl.write('Delete this!');
    // Simulate Ctrl+U to delete the line written previously
    rl.write(null, { ctrl: true, name: 'u' });
    ```

    The `rl.write()` method will write the data to the `readline` `Interface`'s `input` *as if it were provided by the user*.

    [write](https://bun.com/reference/node/readline/Interface/write)(

    data: undefined | null | string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>,

    key: [Key](https://bun.com/reference/node/readline/Key)

    ): void;

    The `rl.write()` method will write either `data` or a key sequence identified by `key` to the `output`. The `key` argument is supported only if `output` is a `TTY` text terminal. See `TTY keybindings` for a list of key combinations.

    If `key` is specified, `data` is ignored.

    When called, `rl.write()` will resume the `input` stream if it has been paused.

    If the `Interface` was created with `output` set to `null` or `undefined` the `data` and `key` are not written.

    ```
    rl.write('Delete this!');
    // Simulate Ctrl+U to delete the line written previously
    rl.write(null, { ctrl: true, name: 'u' });
    ```

    The `rl.write()` method will write the data to the `readline` `Interface`'s `input` *as if it were provided by the user*.
  + static [addAbortListener](https://bun.com/reference/node/readline/Interface/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/readline/Interface/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/readline/Interface/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/readline/Interface/on)(

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

    static [on](https://bun.com/reference/node/readline/Interface/on)(

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
  + static [once](https://bun.com/reference/node/readline/Interface/once)(

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

    static [once](https://bun.com/reference/node/readline/Interface/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/readline/Interface/setMaxListeners)(

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
* function [clearLine](https://bun.com/reference/node/readline/clearLine)(

  stream: WritableStream,

  dir: [Direction](https://bun.com/reference/node/readline/Direction),

  callback?: () => void

  ): boolean;

  The `readline.clearLine()` method clears current line of given [TTY](https://nodejs.org/docs/latest-v24.x/api/tty.html) stream in a specified direction identified by `dir`.

  @param callback

  Invoked once the operation completes.

  @returns

  `false` if `stream` wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* function [clearScreenDown](https://bun.com/reference/node/readline/clearScreenDown)(

  stream: WritableStream,

  callback?: () => void

  ): boolean;

  The `readline.clearScreenDown()` method clears the given [TTY](https://nodejs.org/docs/latest-v24.x/api/tty.html) stream from the current position of the cursor down.

  @param callback

  Invoked once the operation completes.

  @returns

  `false` if `stream` wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* function [createInterface](https://bun.com/reference/node/readline/createInterface)(

  input: ReadableStream,

  output?: WritableStream,

  completer?: [Completer](https://bun.com/reference/node/readline/Completer) | [AsyncCompleter](https://bun.com/reference/node/readline/AsyncCompleter),

  terminal?: boolean

  ): [Interface](https://bun.com/reference/node/readline/Interface);

  The `readline.createInterface()` method creates a new `readline.Interface` instance.

  ```
  import readline from 'node:readline';
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });
  ```

  Once the `readline.Interface` instance is created, the most common case is to listen for the `'line'` event:

  ```
  rl.on('line', (line) => {
    console.log(`Received: ${line}`);
  });
  ```

  If `terminal` is `true` for this instance then the `output` stream will get the best compatibility if it defines an `output.columns` property and emits a `'resize'` event on the `output` if or when the columns ever change (`process.stdout` does this automatically when it is a TTY).

  When creating a `readline.Interface` using `stdin` as input, the program will not terminate until it receives an [EOF character](https://en.wikipedia.org/wiki/End-of-file#EOF_character). To exit without waiting for user input, call `process.stdin.unref()`.

  function [createInterface](https://bun.com/reference/node/readline/createInterface)(

  options: [ReadLineOptions](https://bun.com/reference/node/readline/ReadLineOptions)

  ): [Interface](https://bun.com/reference/node/readline/Interface);

  The `readline.createInterface()` method creates a new `readline.Interface` instance.

  ```
  import readline from 'node:readline';
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
  });
  ```

  Once the `readline.Interface` instance is created, the most common case is to listen for the `'line'` event:

  ```
  rl.on('line', (line) => {
    console.log(`Received: ${line}`);
  });
  ```

  If `terminal` is `true` for this instance then the `output` stream will get the best compatibility if it defines an `output.columns` property and emits a `'resize'` event on the `output` if or when the columns ever change (`process.stdout` does this automatically when it is a TTY).

  When creating a `readline.Interface` using `stdin` as input, the program will not terminate until it receives an [EOF character](https://en.wikipedia.org/wiki/End-of-file#EOF_character). To exit without waiting for user input, call `process.stdin.unref()`.
* function [cursorTo](https://bun.com/reference/node/readline/cursorTo)(

  stream: WritableStream,

  x: number,

  y?: number,

  callback?: () => void

  ): boolean;

  The `readline.cursorTo()` method moves cursor to the specified position in a given [TTY](https://nodejs.org/docs/latest-v24.x/api/tty.html) `stream`.

  @param callback

  Invoked once the operation completes.

  @returns

  `false` if `stream` wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* function [emitKeypressEvents](https://bun.com/reference/node/readline/emitKeypressEvents)(

  stream: ReadableStream,

  readlineInterface?: [Interface](https://bun.com/reference/node/readline/Interface)

  ): void;

  The `readline.emitKeypressEvents()` method causes the given `Readable` stream to begin emitting `'keypress'` events corresponding to received input.

  Optionally, `interface` specifies a `readline.Interface` instance for which autocompletion is disabled when copy-pasted input is detected.

  If the `stream` is a `TTY`, then it must be in raw mode.

  This is automatically called by any readline instance on its `input` if the `input` is a terminal. Closing the `readline` instance does not stop the `input` from emitting `'keypress'` events.

  ```
  readline.emitKeypressEvents(process.stdin);
  if (process.stdin.isTTY)
    process.stdin.setRawMode(true);
  ```

  ## [Example: Tiny CLI](https://bun.com/reference/node/readline#example-tiny-cli)

  The following example illustrates the use of `readline.Interface` class to implement a small command-line interface:

  ```
  import readline from 'node:readline';
  const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
    prompt: 'OHAI> ',
  });

  rl.prompt();

  rl.on('line', (line) => {
    switch (line.trim()) {
      case 'hello':
        console.log('world!');
        break;
      default:
        console.log(`Say what? I might have heard '${line.trim()}'`);
        break;
    }
    rl.prompt();
  }).on('close', () => {
    console.log('Have a great day!');
    process.exit(0);
  });
  ```

  ## [Example: Read file stream line-by-Line](https://bun.com/reference/node/readline#example-read-file-stream-line-by-line)

  A common use case for `readline` is to consume an input file one line at a time. The easiest way to do so is leveraging the `fs.ReadStream` API as well as a `for await...of` loop:

  ```
  import fs from 'node:fs';
  import readline from 'node:readline';

  async function processLineByLine() {
    const fileStream = fs.createReadStream('input.txt');

    const rl = readline.createInterface({
      input: fileStream,
      crlfDelay: Infinity,
    });
    // Note: we use the crlfDelay option to recognize all instances of CR LF
    // ('\r\n') in input.txt as a single line break.

    for await (const line of rl) {
      // Each line in input.txt will be successively available here as `line`.
      console.log(`Line from file: ${line}`);
    }
  }

  processLineByLine();
  ```

  Alternatively, one could use the `'line'` event:

  ```
  import fs from 'node:fs';
  import readline from 'node:readline';

  const rl = readline.createInterface({
    input: fs.createReadStream('sample.txt'),
    crlfDelay: Infinity,
  });

  rl.on('line', (line) => {
    console.log(`Line from file: ${line}`);
  });
  ```

  Currently, `for await...of` loop can be a bit slower. If `async` / `await` flow and speed are both essential, a mixed approach can be applied:

  ```
  import { once } from 'node:events';
  import { createReadStream } from 'node:fs';
  import { createInterface } from 'node:readline';

  (async function processLineByLine() {
    try {
      const rl = createInterface({
        input: createReadStream('big-file.txt'),
        crlfDelay: Infinity,
      });

      rl.on('line', (line) => {
        // Process the line.
      });

      await once(rl, 'close');

      console.log('File processed.');
    } catch (err) {
      console.error(err);
    }
  })();
  ```
* function [moveCursor](https://bun.com/reference/node/readline/moveCursor)(

  stream: WritableStream,

  dx: number,

  dy: number,

  callback?: () => void

  ): boolean;

  The `readline.moveCursor()` method moves the cursor *relative* to its current position in a given [TTY](https://nodejs.org/docs/latest-v24.x/api/tty.html) `stream`.

  @param callback

  Invoked once the operation completes.

  @returns

  `false` if `stream` wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

## Type definitions

* ### interface [CursorPos](https://bun.com/reference/node/readline/CursorPos)

  + [cols](https://bun.com/reference/node/readline/CursorPos/cols): number
  + [rows](https://bun.com/reference/node/readline/CursorPos/rows): number
* ### interface [Key](https://bun.com/reference/node/readline/Key)

  + [ctrl](https://bun.com/reference/node/readline/Key/ctrl)?: boolean
  + [meta](https://bun.com/reference/node/readline/Key/meta)?: boolean
  + [name](https://bun.com/reference/node/readline/Key/name)?: string
  + [sequence](https://bun.com/reference/node/readline/Key/sequence)?: string
  + [shift](https://bun.com/reference/node/readline/Key/shift)?: boolean
* ### interface [ReadLineOptions](https://bun.com/reference/node/readline/ReadLineOptions)

  + [completer](https://bun.com/reference/node/readline/ReadLineOptions/completer)?: [Completer](https://bun.com/reference/node/readline/Completer) | [AsyncCompleter](https://bun.com/reference/node/readline/AsyncCompleter)

    An optional function used for Tab autocompletion.
  + [crlfDelay](https://bun.com/reference/node/readline/ReadLineOptions/crlfDelay)?: number

    If the delay between `\r` and

    ```

    ```

    exceeds `crlfDelay` milliseconds, both `\r` and

    ```

    ```

    will be treated as separate end-of-line input. `crlfDelay` will be coerced to a number no less than `100`. It can be set to `Infinity`, in which case `\r` followed by

    ```

    ```

    will always be considered a single newline (which may be reasonable for [reading files](https://nodejs.org/docs/latest-v24.x/api/readline.html#example-read-file-stream-line-by-line) with

    ```
    \r
    ```

    line delimiter).
  + [escapeCodeTimeout](https://bun.com/reference/node/readline/ReadLineOptions/escapeCodeTimeout)?: number

    The duration `readline` will wait for a character (when reading an ambiguous key sequence in milliseconds one that can both form a complete key sequence using the input read so far and can take additional input to complete a longer key sequence).
  + [history](https://bun.com/reference/node/readline/ReadLineOptions/history)?: string[]

    Initial list of history lines. This option makes sense only if `terminal` is set to `true` by the user or by an internal `output` check, otherwise the history caching mechanism is not initialized at all.
  + [historySize](https://bun.com/reference/node/readline/ReadLineOptions/historySize)?: number

    Maximum number of history lines retained. To disable the history set this value to `0`. This option makes sense only if `terminal` is set to `true` by the user or by an internal `output` check, otherwise the history caching mechanism is not initialized at all.
  + [input](https://bun.com/reference/node/readline/ReadLineOptions/input): ReadableStream

    The [`Readable`](https://nodejs.org/docs/latest-v24.x/api/stream.html#readable-streams) stream to listen to
  + [output](https://bun.com/reference/node/readline/ReadLineOptions/output)?: WritableStream

    The [`Writable`](https://nodejs.org/docs/latest-v24.x/api/stream.html#writable-streams) stream to write readline data to.
  + [prompt](https://bun.com/reference/node/readline/ReadLineOptions/prompt)?: string

    The prompt string to use.
  + [removeHistoryDuplicates](https://bun.com/reference/node/readline/ReadLineOptions/removeHistoryDuplicates)?: boolean

    If `true`, when a new input line added to the history list duplicates an older one, this removes the older line from the list.
  + [signal](https://bun.com/reference/node/readline/ReadLineOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    Allows closing the interface using an AbortSignal. Aborting the signal will internally call `close` on the interface.
  + [tabSize](https://bun.com/reference/node/readline/ReadLineOptions/tabSize)?: number

    The number of spaces a tab is equal to (minimum 1).
  + [terminal](https://bun.com/reference/node/readline/ReadLineOptions/terminal)?: boolean

    `true` if the `input` and `output` streams should be treated like a TTY, and have ANSI/VT100 escape codes written to it. Default: checking `isTTY` on the `output` stream upon instantiation.
* type [AsyncCompleter](https://bun.com/reference/node/readline/AsyncCompleter) = (line: string, callback: (err?: null | [Error](https://bun.com/reference/globals/Error), result?: [CompleterResult](https://bun.com/reference/node/readline/CompleterResult)) => void) => void
* type [Completer](https://bun.com/reference/node/readline/Completer) = (line: string) => [CompleterResult](https://bun.com/reference/node/readline/CompleterResult)
* type [CompleterResult](https://bun.com/reference/node/readline/CompleterResult) = [string[], string]
* type [Direction](https://bun.com/reference/node/readline/Direction) = -1 | 0 | 1
* type [ReadLine](https://bun.com/reference/node/readline/ReadLine) = [Interface](https://bun.com/reference/node/readline/Interface)