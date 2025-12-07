---
url: https://bun.com/reference/node/timers/promises
title: Node.js timers/promises module | API Reference | Bun
source_domain: bun.com
---

# Node.js timers/promises module | API Reference | Bun

Node.js module

# [timers/promises](https://bun.com/reference/node/timers/promises)

The `'node:timers/promises'` submodule provides Promise-based timer functions such as `setTimeout` and `setImmediate`, enabling async/await syntax for delayed execution.

It simplifies scheduling and timing of asynchronous code in modern JavaScript.

* const [scheduler](https://bun.com/reference/node/timers/promises/scheduler): [Scheduler](https://bun.com/reference/node/timers/promises/Scheduler)
* function [setImmediate](https://bun.com/reference/node/timers/promises/setImmediate)<T = void>(

  value?: T,

  options?: [TimerOptions](https://bun.com/reference/node/timers/TimerOptions)

  ): Promise<T>;

  ```
  import {
    setImmediate,
  } from 'node:timers/promises';

  const res = await setImmediate('result');

  console.log(res);  // Prints 'result'
  ```

  @param value

  A value with which the promise is fulfilled.
* function [setInterval](https://bun.com/reference/node/timers/promises/setInterval)<T = void>(

  delay?: number,

  value?: T,

  options?: [TimerOptions](https://bun.com/reference/node/timers/TimerOptions)

  ): AsyncIterator<T>;

  Returns an async iterator that generates values in an interval of `delay` ms. If `ref` is `true`, you need to call `next()` of async iterator explicitly or implicitly to keep the event loop alive.

  ```
  import {
    setInterval,
  } from 'node:timers/promises';

  const interval = 100;
  for await (const startTime of setInterval(interval, Date.now())) {
    const now = Date.now();
    console.log(now);
    if ((now - startTime) > 1000)
      break;
  }
  console.log(Date.now());
  ```

  @param delay

  The number of milliseconds to wait between iterations. **Default:** `1`.

  @param value

  A value with which the iterator returns.
* function [setTimeout](https://bun.com/reference/node/timers/promises/setTimeout)<T = void>(

  delay?: number,

  value?: T,

  options?: [TimerOptions](https://bun.com/reference/node/timers/TimerOptions)

  ): Promise<T>;

  ```
  import {
    setTimeout,
  } from 'node:timers/promises';

  const res = await setTimeout(100, 'result');

  console.log(res);  // Prints 'result'
  ```

  @param delay

  The number of milliseconds to wait before fulfilling the promise. **Default:** `1`.

  @param value

  A value with which the promise is fulfilled.

## Type definitions

* ### interface [Scheduler](https://bun.com/reference/node/timers/promises/Scheduler)

  + [wait](https://bun.com/reference/node/timers/promises/Scheduler/wait)(

    delay: number,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): Promise<void>;

    An experimental API defined by the [Scheduling APIs](https://github.com/WICG/scheduling-apis) draft specification being developed as a standard Web Platform API.

    Calling `timersPromises.scheduler.wait(delay, options)` is roughly equivalent to calling `timersPromises.setTimeout(delay, undefined, options)` except that the `ref` option is not supported.

    ```
    import { scheduler } from 'node:timers/promises';

    await scheduler.wait(1000); // Wait one second before continuing
    ```

    @param delay

    The number of milliseconds to wait before resolving the promise.
  + [yield](https://bun.com/reference/node/timers/promises/Scheduler/yield)(): Promise<void>;

    An experimental API defined by the [Scheduling APIs](https://github.com/WICG/scheduling-apis) draft specification being developed as a standard Web Platform API.

    Calling `timersPromises.scheduler.yield()` is equivalent to calling `timersPromises.setImmediate()` with no arguments.