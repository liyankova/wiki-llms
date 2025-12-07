---
url: https://bun.com/reference/node/events
title: Node.js events module | API Reference | Bun
source_domain: bun.com
---

# Node.js events module | API Reference | Bun

Node.js module

# [events](https://bun.com/reference/node/events)

The `'node:events'` module provides the `EventEmitter` class, which is the foundation for handling event-driven programming in Node.js. Objects inheriting from EventEmitter can emit named events and have listeners subscribe to those events.

It supports adding and removing listeners, once-only listeners, event forwarding, and wildcard events, serving as the backbone for core modules like `http.Server` and many application frameworks.

Works in Bun

Fully implemented. 100% of Node.js's test suite passes. EventEmitterAsyncResource uses AsyncResource underneath.

* ### [export default namespace events](https://bun.com/reference/node/events/default)

  + ### class [EventEmitterAsyncResource](https://bun.com/reference/node/events/default/EventEmitterAsyncResource)

    Integrates `EventEmitter` with `AsyncResource` for `EventEmitter`s that require manual async tracking. Specifically, all events emitted by instances of `events.EventEmitterAsyncResource` will run within its `async context`.

    ```
    import { EventEmitterAsyncResource, EventEmitter } from 'node:events';
    import { notStrictEqual, strictEqual } from 'node:assert';
    import { executionAsyncId, triggerAsyncId } from 'node:async_hooks';

    // Async tracking tooling will identify this as 'Q'.
    const ee1 = new EventEmitterAsyncResource({ name: 'Q' });

    // 'foo' listeners will run in the EventEmitters async context.
    ee1.on('foo', () => {
      strictEqual(executionAsyncId(), ee1.asyncId);
      strictEqual(triggerAsyncId(), ee1.triggerAsyncId);
    });

    const ee2 = new EventEmitter();

    // 'foo' listeners on ordinary EventEmitters that do not track async
    // context, however, run in the same async context as the emit().
    ee2.on('foo', () => {
      notStrictEqual(executionAsyncId(), ee2.asyncId);
      notStrictEqual(triggerAsyncId(), ee2.triggerAsyncId);
    });

    Promise.resolve().then(() => {
      ee1.emit('foo');
      ee2.emit('foo');
    });
    ```

    The `EventEmitterAsyncResource` class has the same methods and takes the same options as `EventEmitter` and `AsyncResource` themselves.

    - readonly [asyncId](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/asyncId): number

      The unique `asyncId` assigned to the resource.
    - readonly [asyncResource](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/asyncResource): [EventEmitterReferencingAsyncResource](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource)

      The returned `AsyncResource` object has an additional `eventEmitter` property that provides a reference to this `EventEmitterAsyncResource`.
    - readonly [triggerAsyncId](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/triggerAsyncId): number

      The same triggerAsyncId that is passed to the AsyncResource constructor.
    - static [captureRejections](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/captureRejections): boolean

      Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

      Change the default `captureRejections` option on all new `EventEmitter` objects.
    - readonly static [captureRejectionSymbol](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

      Value: `Symbol.for('nodejs.rejection')`

      See how to write a custom `rejection handler`.
    - static [defaultMaxListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/defaultMaxListeners): number

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
    - readonly static [errorMonitor](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

      This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

      Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
    - [[events.captureRejectionSymbol]](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/[captureRejectionSymbol])<K>(

      error: [Error](https://bun.com/reference/globals/Error),

      event: string | symbol,

      ...args: AnyRest

      ): void;
    - [addListener](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/addListener)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.on(eventName, listener)`.
    - [emit](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/emit)<K>(

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
    - [emitDestroy](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/emitDestroy)(): void;

      Call all `destroy` hooks. This should only ever be called once. An error will be thrown if it is called more than once. This **must** be manually called. If the resource is left to be collected by the GC then the `destroy` hooks will never be called.
    - [eventNames](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/eventNames)(): string | symbol[];

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
    - [getMaxListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/getMaxListeners)(): number;

      Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
    - [listenerCount](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/listenerCount)<K>(

      eventName: string | symbol,

      listener?: Function

      ): number;

      Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

      @param eventName

      The name of the event being listened for

      @param listener

      The event handler function
    - [listeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/listeners)<K>(

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
    - [off](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/off)<K>(

      eventName: string | symbol,

      listener: (...args: any[]) => void

      ): this;

      Alias for `emitter.removeListener()`.
    - [on](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/on)<K>(

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
    - [once](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/once)<K>(

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
    - [prependListener](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/prependListener)<K>(

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
    - [prependOnceListener](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/prependOnceListener)<K>(

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
    - [rawListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/rawListeners)<K>(

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
    - [removeAllListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/removeAllListeners)(

      eventName?: string | symbol

      ): this;

      Removes all listeners, or those of the specified `eventName`.

      It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - [removeListener](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/removeListener)<K>(

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
    - [setMaxListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/setMaxListeners)(

      n: number

      ): this;

      By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

      Returns a reference to the `EventEmitter`, so that calls can be chained.
    - static [addAbortListener](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/addAbortListener)(

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
    - static [getEventListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/getEventListeners)(

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
    - static [getMaxListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/getMaxListeners)(

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
    - static [on](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/on)(

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

      static [on](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/on)(

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
    - static [once](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/once)(

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

      static [once](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/once)(

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
    - static [setMaxListeners](https://bun.com/reference/node/events/default/EventEmitterAsyncResource/setMaxListeners)(

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
  + ### interface [Abortable](https://bun.com/reference/node/events/default/Abortable)

    - [signal](https://bun.com/reference/node/events/default/Abortable/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

      When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + ### interface [EventEmitterAsyncResourceOptions](https://bun.com/reference/node/events/default/EventEmitterAsyncResourceOptions)

    - [captureRejections](https://bun.com/reference/node/events/default/EventEmitterAsyncResourceOptions/captureRejections)?: boolean

      Enables automatic capturing of promise rejection.
    - [name](https://bun.com/reference/node/events/default/EventEmitterAsyncResourceOptions/name)?: string

      The type of async event, this is required when instantiating `EventEmitterAsyncResource` directly rather than as a child class.
    - [requireManualDestroy](https://bun.com/reference/node/events/default/EventEmitterAsyncResourceOptions/requireManualDestroy)?: boolean

      Disables automatic `emitDestroy` when the object is garbage collected. This usually does not need to be set (even if `emitDestroy` is called manually), unless the resource's `asyncId` is retrieved and the sensitive API's `emitDestroy` is called with it.
    - [triggerAsyncId](https://bun.com/reference/node/events/default/EventEmitterAsyncResourceOptions/triggerAsyncId)?: number

      The ID of the execution context that created this async event.
  + ### interface [EventEmitterReferencingAsyncResource](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource)

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

    - readonly [eventEmitter](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource/eventEmitter): [EventEmitterAsyncResource](https://bun.com/reference/node/events/default/EventEmitterAsyncResource)
    - [asyncId](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource/asyncId)(): number;

      @returns

      The unique `asyncId` assigned to the resource.
    - [bind](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource/bind)<Func extends (...args: any[]) => any>(

      fn: Func

      ): Func;

      Binds the given function to execute to this `AsyncResource`'s scope.

      @param fn

      The function to bind to the current `AsyncResource`.
    - [emitDestroy](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource/emitDestroy)(): this;

      Call all `destroy` hooks. This should only ever be called once. An error will be thrown if it is called more than once. This **must** be manually called. If the resource is left to be collected by the GC then the `destroy` hooks will never be called.

      @returns

      A reference to `asyncResource`.
    - [runInAsyncScope](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource/runInAsyncScope)<This, Result>(

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
    - [triggerAsyncId](https://bun.com/reference/node/events/default/EventEmitterReferencingAsyncResource/triggerAsyncId)(): number;

      @returns

      The same `triggerAsyncId` that is passed to the `AsyncResource` constructor.
  + ### interface [NodeEventTarget](https://bun.com/reference/node/events/default/NodeEventTarget)

    The `NodeEventTarget` is a Node.js-specific extension to `EventTarget` that emulates a subset of the `EventEmitter` API.

    - [addEventListener](https://bun.com/reference/node/events/default/NodeEventTarget/addEventListener)(

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

      [addEventListener](https://bun.com/reference/node/events/default/NodeEventTarget/addEventListener)(

      type: string,

      listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

      options?: boolean | [AddEventListenerOptions](https://bun.com/reference/globals/AddEventListenerOptions)

      ): void;

      Adds a new handler for the `type` event. Any given `listener` is added only once per `type` and per `capture` option value.

      If the `once` option is true, the `listener` is removed after the next time a `type` event is dispatched.

      The `capture` option is not used by Node.js in any functional way other than tracking registered event listeners per the `EventTarget` specification. Specifically, the `capture` option is used as part of the key when registering a `listener`. Any individual `listener` may be added once with `capture = false`, and once with `capture = true`.
    - [addListener](https://bun.com/reference/node/events/default/NodeEventTarget/addListener)(

      type: string,

      listener: (arg: any) => void

      ): this;

      Node.js-specific extension to the `EventTarget` class that emulates the equivalent `EventEmitter` API. The only difference between `addListener()` and `addEventListener()` is that `addListener()` will return a reference to the `EventTarget`.
    - [dispatchEvent](https://bun.com/reference/node/events/default/NodeEventTarget/dispatchEvent)(

      event: [Event](https://bun.com/reference/globals/Event)

      ): boolean;

      Dispatches a synthetic event event to target and returns true if either event's cancelable attribute value is false or its preventDefault() method was not invoked, and false otherwise.
    - [emit](https://bun.com/reference/node/events/default/NodeEventTarget/emit)(

      type: string,

      arg: any

      ): boolean;

      Node.js-specific extension to the `EventTarget` class that dispatches the `arg` to the list of handlers for `type`.

      @returns

      `true` if event listeners registered for the `type` exist, otherwise `false`.
    - [eventNames](https://bun.com/reference/node/events/default/NodeEventTarget/eventNames)(): string[];

      Node.js-specific extension to the `EventTarget` class that returns an array of event `type` names for which event listeners are registered.
    - [getMaxListeners](https://bun.com/reference/node/events/default/NodeEventTarget/getMaxListeners)(): number;

      Node.js-specific extension to the `EventTarget` class that returns the number of max event listeners.
    - [listenerCount](https://bun.com/reference/node/events/default/NodeEventTarget/listenerCount)(

      type: string

      ): number;

      Node.js-specific extension to the `EventTarget` class that returns the number of event listeners registered for the `type`.
    - [off](https://bun.com/reference/node/events/default/NodeEventTarget/off)(

      type: string,

      listener: (arg: any) => void,

      options?: EventListenerOptions

      ): this;

      Node.js-specific alias for `eventTarget.removeEventListener()`.
    - [on](https://bun.com/reference/node/events/default/NodeEventTarget/on)(

      type: string,

      listener: (arg: any) => void

      ): this;

      Node.js-specific alias for `eventTarget.addEventListener()`.
    - [once](https://bun.com/reference/node/events/default/NodeEventTarget/once)(

      type: string,

      listener: (arg: any) => void

      ): this;

      Node.js-specific extension to the `EventTarget` class that adds a `once` listener for the given event `type`. This is equivalent to calling `on` with the `once` option set to `true`.
    - [removeAllListeners](https://bun.com/reference/node/events/default/NodeEventTarget/removeAllListeners)(

      type?: string

      ): this;

      Node.js-specific extension to the `EventTarget` class. If `type` is specified, removes all registered listeners for `type`, otherwise removes all registered listeners.
    - [removeEventListener](https://bun.com/reference/node/events/default/NodeEventTarget/removeEventListener)(

      type: string,

      callback: null | EventListenerOrEventListenerObject,

      options?: boolean | EventListenerOptions

      ): void;

      Removes the event listener in target's event listener list with the same type, callback, and options.

      [MDN Reference](https://developer.mozilla.org/docs/Web/API/EventTarget/removeEventListener)

      [removeEventListener](https://bun.com/reference/node/events/default/NodeEventTarget/removeEventListener)(

      type: string,

      listener: [EventListener](https://bun.com/reference/globals/EventListener) | [EventListenerObject](https://bun.com/reference/globals/EventListenerObject),

      options?: boolean | [EventListenerOptions](https://bun.com/reference/bun/EventListenerOptions)

      ): void;

      Removes the event listener in target's event listener list with the same type, callback, and options.
    - [removeListener](https://bun.com/reference/node/events/default/NodeEventTarget/removeListener)(

      type: string,

      listener: (arg: any) => void,

      options?: EventListenerOptions

      ): this;

      Node.js-specific extension to the `EventTarget` class that removes the `listener` for the given `type`. The only difference between `removeListener()` and `removeEventListener()` is that `removeListener()` will return a reference to the `EventTarget`.
    - [setMaxListeners](https://bun.com/reference/node/events/default/NodeEventTarget/setMaxListeners)(

      n: number

      ): void;

      Node.js-specific extension to the `EventTarget` class that sets the number of max event listeners as `n`.
* ### class [default](https://bun.com/reference/node/events/default)<T extends EventMap<T> = DefaultEventMap>

  The `EventEmitter` class is defined and exposed by the `node:events` module:

  ```
  import { EventEmitter } from 'node:events';
  ```

  All `EventEmitter`s emit the event `'newListener'` when new listeners are added and `'removeListener'` when existing listeners are removed.

  It supports the following option:

  + static [captureRejections](https://bun.com/reference/node/events/default/captureRejections): boolean

    Value: [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type)

    Change the default `captureRejections` option on all new `EventEmitter` objects.
  + readonly static [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol): typeof [captureRejectionSymbol](https://bun.com/reference/node/events/default/captureRejectionSymbol)

    Value: `Symbol.for('nodejs.rejection')`

    See how to write a custom `rejection handler`.
  + static [defaultMaxListeners](https://bun.com/reference/node/events/default/defaultMaxListeners): number

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
  + readonly static [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor): typeof [errorMonitor](https://bun.com/reference/node/events/default/errorMonitor)

    This symbol shall be used to install a listener for only monitoring `'error'` events. Listeners installed using this symbol are called before the regular `'error'` listeners are called.

    Installing a listener using this symbol does not change the behavior once an `'error'` event is emitted. Therefore, the process will still crash if no regular `'error'` listener is installed.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/events/default/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: Key<K, T>,

    ...args: Args<K, T>

    ): void;
  + [addListener](https://bun.com/reference/node/events/default/addListener)<K>(

    eventName: Key<K, T>,

    listener: Listener<K, T>

    ): this;

    Alias for `emitter.on(eventName, listener)`.
  + [emit](https://bun.com/reference/node/events/default/emit)<K>(

    eventName: Key<K, T>,

    ...args: Args<K, T>

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
  + [eventNames](https://bun.com/reference/node/events/default/eventNames)(): string | symbol & Key2<unknown, T>[];

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
  + [getMaxListeners](https://bun.com/reference/node/events/default/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [listenerCount](https://bun.com/reference/node/events/default/listenerCount)<K>(

    eventName: Key<K, T>,

    listener?: Listener<K, T, Function>

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/events/default/listeners)<K>(

    eventName: Key<K, T>

    ): Listener<K, T, Function>[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [off](https://bun.com/reference/node/events/default/off)<K>(

    eventName: Key<K, T>,

    listener: Listener<K, T>

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/events/default/on)<K>(

    eventName: Key<K, T>,

    listener: Listener<K, T>

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
  + [once](https://bun.com/reference/node/events/default/once)<K>(

    eventName: Key<K, T>,

    listener: Listener<K, T>

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
  + [prependListener](https://bun.com/reference/node/events/default/prependListener)<K>(

    eventName: Key<K, T>,

    listener: Listener<K, T>

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
  + [prependOnceListener](https://bun.com/reference/node/events/default/prependOnceListener)<K>(

    eventName: Key<K, T>,

    listener: Listener<K, T>

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
  + [rawListeners](https://bun.com/reference/node/events/default/rawListeners)<K>(

    eventName: Key<K, T>

    ): Listener<K, T, Function>[];

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
  + [removeAllListeners](https://bun.com/reference/node/events/default/removeAllListeners)(

    eventName?: Key<unknown, T>

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/events/default/removeListener)<K>(

    eventName: Key<K, T>,

    listener: Listener<K, T>

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
  + [setMaxListeners](https://bun.com/reference/node/events/default/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + static [addAbortListener](https://bun.com/reference/node/events/default/addAbortListener)(

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
  + static [getEventListeners](https://bun.com/reference/node/events/default/getEventListeners)(

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
  + static [getMaxListeners](https://bun.com/reference/node/events/default/getMaxListeners)(

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
  + static [on](https://bun.com/reference/node/events/default/on)(

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

    static [on](https://bun.com/reference/node/events/default/on)(

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
  + static [once](https://bun.com/reference/node/events/default/once)(

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

    static [once](https://bun.com/reference/node/events/default/once)(

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
  + static [setMaxListeners](https://bun.com/reference/node/events/default/setMaxListeners)(

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