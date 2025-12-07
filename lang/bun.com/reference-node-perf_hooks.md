---
url: https://bun.com/reference/node/perf_hooks
title: Node.js perf_hooks module | API Reference | Bun
source_domain: bun.com
---

# Node.js perf_hooks module | API Reference | Bun

Node.js module

# [perf\_hooks](https://bun.com/reference/node/perf_hooks)

The `'node:perf_hooks'` module provides performance measurement APIs based on the User Timing specification. It includes `performance.now()`, `performance.mark`, `performance.measure`, and PerformanceObserver.

Use it to benchmark code execution, measure memory usage, and observe performance entries for timely optimization.

Works in Bun

Missing event loop delay monitoring. It's recommended to use the `performance` global instead of `perf\_hooks.performance`.

* ### namespace [constants](https://bun.com/reference/node/perf_hooks/constants)

  + const [NODE\_PERFORMANCE\_GC\_FLAGS\_ALL\_AVAILABLE\_GARBAGE](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_FLAGS_ALL_AVAILABLE_GARBAGE): number
  + const [NODE\_PERFORMANCE\_GC\_FLAGS\_ALL\_EXTERNAL\_MEMORY](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_FLAGS_ALL_EXTERNAL_MEMORY): number
  + const [NODE\_PERFORMANCE\_GC\_FLAGS\_CONSTRUCT\_RETAINED](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_FLAGS_CONSTRUCT_RETAINED): number
  + const [NODE\_PERFORMANCE\_GC\_FLAGS\_FORCED](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_FLAGS_FORCED): number
  + const [NODE\_PERFORMANCE\_GC\_FLAGS\_NO](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_FLAGS_NO): number
  + const [NODE\_PERFORMANCE\_GC\_FLAGS\_SCHEDULE\_IDLE](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_FLAGS_SCHEDULE_IDLE): number
  + const [NODE\_PERFORMANCE\_GC\_FLAGS\_SYNCHRONOUS\_PHANTOM\_PROCESSING](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_FLAGS_SYNCHRONOUS_PHANTOM_PROCESSING): number
  + const [NODE\_PERFORMANCE\_GC\_INCREMENTAL](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_INCREMENTAL): number
  + const [NODE\_PERFORMANCE\_GC\_MAJOR](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_MAJOR): number
  + const [NODE\_PERFORMANCE\_GC\_MINOR](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_MINOR): number
  + const [NODE\_PERFORMANCE\_GC\_WEAKCB](https://bun.com/reference/node/perf_hooks/constants/NODE_PERFORMANCE_GC_WEAKCB): number
* ### class [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)

  The constructor of this class is not exposed to users directly.

  + readonly [duration](https://bun.com/reference/node/perf_hooks/PerformanceEntry/duration): number

    The total number of milliseconds elapsed for this entry. This value will not be meaningful for all Performance Entry types.
  + readonly [entryType](https://bun.com/reference/node/perf_hooks/PerformanceEntry/entryType): [EntryType](https://bun.com/reference/node/perf_hooks/EntryType)

    The type of the performance entry. It may be one of:

    - `'node'` (Node.js only)
    - `'mark'` (available on the Web)
    - `'measure'` (available on the Web)
    - `'gc'` (Node.js only)
    - `'function'` (Node.js only)
    - `'http2'` (Node.js only)
    - `'http'` (Node.js only)
  + readonly [name](https://bun.com/reference/node/perf_hooks/PerformanceEntry/name): string

    The name of the performance entry.
  + readonly [startTime](https://bun.com/reference/node/perf_hooks/PerformanceEntry/startTime): number

    The high resolution millisecond timestamp marking the starting time of the Performance Entry.
  + [toJSON](https://bun.com/reference/node/perf_hooks/PerformanceEntry/toJSON)(): any;
* ### class [PerformanceMark](https://bun.com/reference/node/perf_hooks/PerformanceMark)

  Exposes marks created via the `Performance.mark()` method.

  + readonly [detail](https://bun.com/reference/node/perf_hooks/PerformanceMark/detail): any
  + readonly [duration](https://bun.com/reference/node/perf_hooks/PerformanceMark/duration): 0

    The total number of milliseconds elapsed for this entry. This value will not be meaningful for all Performance Entry types.
  + readonly [entryType](https://bun.com/reference/node/perf_hooks/PerformanceMark/entryType): 'mark'

    The type of the performance entry. It may be one of:

    - `'node'` (Node.js only)
    - `'mark'` (available on the Web)
    - `'measure'` (available on the Web)
    - `'gc'` (Node.js only)
    - `'function'` (Node.js only)
    - `'http2'` (Node.js only)
    - `'http'` (Node.js only)
  + readonly [name](https://bun.com/reference/node/perf_hooks/PerformanceMark/name): string

    The name of the performance entry.
  + readonly [startTime](https://bun.com/reference/node/perf_hooks/PerformanceMark/startTime): number

    The high resolution millisecond timestamp marking the starting time of the Performance Entry.
  + [toJSON](https://bun.com/reference/node/perf_hooks/PerformanceMark/toJSON)(): any;
* ### class [PerformanceMeasure](https://bun.com/reference/node/perf_hooks/PerformanceMeasure)

  Exposes measures created via the `Performance.measure()` method.

  The constructor of this class is not exposed to users directly.

  + readonly [detail](https://bun.com/reference/node/perf_hooks/PerformanceMeasure/detail): any
  + readonly [duration](https://bun.com/reference/node/perf_hooks/PerformanceMeasure/duration): number

    The total number of milliseconds elapsed for this entry. This value will not be meaningful for all Performance Entry types.
  + readonly [entryType](https://bun.com/reference/node/perf_hooks/PerformanceMeasure/entryType): 'measure'

    The type of the performance entry. It may be one of:

    - `'node'` (Node.js only)
    - `'mark'` (available on the Web)
    - `'measure'` (available on the Web)
    - `'gc'` (Node.js only)
    - `'function'` (Node.js only)
    - `'http2'` (Node.js only)
    - `'http'` (Node.js only)
  + readonly [name](https://bun.com/reference/node/perf_hooks/PerformanceMeasure/name): string

    The name of the performance entry.
  + readonly [startTime](https://bun.com/reference/node/perf_hooks/PerformanceMeasure/startTime): number

    The high resolution millisecond timestamp marking the starting time of the Performance Entry.
  + [toJSON](https://bun.com/reference/node/perf_hooks/PerformanceMeasure/toJSON)(): any;
* ### class [PerformanceNodeTiming](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming)

  *This property is an extension by Node.js. It is not available in Web browsers.*

  Provides timing details for Node.js itself. The constructor of this class is not exposed to users.

  + readonly [bootstrapComplete](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/bootstrapComplete): number

    The high resolution millisecond timestamp at which the Node.js process completed bootstrapping. If bootstrapping has not yet finished, the property has the value of -1.
  + readonly [duration](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/duration): number

    The total number of milliseconds elapsed for this entry. This value will not be meaningful for all Performance Entry types.
  + readonly [entryType](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/entryType): 'node'

    The type of the performance entry. It may be one of:

    - `'node'` (Node.js only)
    - `'mark'` (available on the Web)
    - `'measure'` (available on the Web)
    - `'gc'` (Node.js only)
    - `'function'` (Node.js only)
    - `'http2'` (Node.js only)
    - `'http'` (Node.js only)
  + readonly [environment](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/environment): number

    The high resolution millisecond timestamp at which the Node.js environment was initialized.
  + readonly [idleTime](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/idleTime): number

    The high resolution millisecond timestamp of the amount of time the event loop has been idle within the event loop's event provider (e.g. `epoll_wait`). This does not take CPU usage into consideration. If the event loop has not yet started (e.g., in the first tick of the main script), the property has the value of 0.
  + readonly [loopExit](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/loopExit): number

    The high resolution millisecond timestamp at which the Node.js event loop exited. If the event loop has not yet exited, the property has the value of -1. It can only have a value of not -1 in a handler of the `'exit'` event.
  + readonly [loopStart](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/loopStart): number

    The high resolution millisecond timestamp at which the Node.js event loop started. If the event loop has not yet started (e.g., in the first tick of the main script), the property has the value of -1.
  + readonly [name](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/name): string

    The name of the performance entry.
  + readonly [nodeStart](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/nodeStart): number

    The high resolution millisecond timestamp at which the Node.js process was initialized.
  + readonly [startTime](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/startTime): number

    The high resolution millisecond timestamp marking the starting time of the Performance Entry.
  + readonly [uvMetricsInfo](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/uvMetricsInfo): [UVMetrics](https://bun.com/reference/node/perf_hooks/UVMetrics)

    This is a wrapper to the `uv_metrics_info` function. It returns the current set of event loop metrics.

    It is recommended to use this property inside a function whose execution was scheduled using `setImmediate` to avoid collecting metrics before finishing all operations scheduled during the current loop iteration.
  + readonly [v8Start](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/v8Start): number

    The high resolution millisecond timestamp at which the V8 platform was initialized.
  + [toJSON](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming/toJSON)(): any;
* ### class [PerformanceObserver](https://bun.com/reference/node/perf_hooks/PerformanceObserver)

  + [asyncId](https://bun.com/reference/node/perf_hooks/PerformanceObserver/asyncId)(): number;

    @returns

    The unique `asyncId` assigned to the resource.
  + [bind](https://bun.com/reference/node/perf_hooks/PerformanceObserver/bind)<Func extends (...args: any[]) => any>(

    fn: Func

    ): Func;

    Binds the given function to execute to this `AsyncResource`'s scope.

    @param fn

    The function to bind to the current `AsyncResource`.
  + [disconnect](https://bun.com/reference/node/perf_hooks/PerformanceObserver/disconnect)(): void;

    Disconnects the `PerformanceObserver` instance from all notifications.
  + [emitDestroy](https://bun.com/reference/node/perf_hooks/PerformanceObserver/emitDestroy)(): this;

    Call all `destroy` hooks. This should only ever be called once. An error will be thrown if it is called more than once. This **must** be manually called. If the resource is left to be collected by the GC then the `destroy` hooks will never be called.

    @returns

    A reference to `asyncResource`.
  + [observe](https://bun.com/reference/node/perf_hooks/PerformanceObserver/observe)(

    options: { buffered: boolean; entryTypes: readonly [EntryType](https://bun.com/reference/node/perf_hooks/EntryType)[] } | { buffered: boolean; type: [EntryType](https://bun.com/reference/node/perf_hooks/EntryType) }

    ): void;

    Subscribes the `PerformanceObserver` instance to notifications of new `PerformanceEntry` instances identified either by `options.entryTypes` or `options.type`:

    ```
    import {
      performance,
      PerformanceObserver,
    } from 'node:perf_hooks';

    const obs = new PerformanceObserver((list, observer) => {
      // Called once asynchronously. `list` contains three items.
    });
    obs.observe({ type: 'mark' });

    for (let n = 0; n < 3; n++)
      performance.mark(`test${n}`);
    ```
  + [runInAsyncScope](https://bun.com/reference/node/perf_hooks/PerformanceObserver/runInAsyncScope)<This, Result>(

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
  + [takeRecords](https://bun.com/reference/node/perf_hooks/PerformanceObserver/takeRecords)(): [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)[];

    @returns

    Current list of entries stored in the performance observer, emptying it out.
  + [triggerAsyncId](https://bun.com/reference/node/perf_hooks/PerformanceObserver/triggerAsyncId)(): number;

    @returns

    The same `triggerAsyncId` that is passed to the `AsyncResource` constructor.
  + static [bind](https://bun.com/reference/node/perf_hooks/PerformanceObserver/bind)<Func extends (this: ThisArg, ...args: any[]) => any, ThisArg>(

    fn: Func,

    type?: string,

    thisArg?: ThisArg

    ): Func;

    Binds the given function to the current execution context.

    @param fn

    The function to bind to the current execution context.

    @param type

    An optional name to associate with the underlying `AsyncResource`.
* ### class [PerformanceObserverEntryList](https://bun.com/reference/node/perf_hooks/PerformanceObserverEntryList)

  + [getEntries](https://bun.com/reference/node/perf_hooks/PerformanceObserverEntryList/getEntries)(): [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)[];

    Returns a list of `PerformanceEntry` objects in chronological order with respect to `performanceEntry.startTime`.

    ```
    import {
      performance,
      PerformanceObserver,
    } from 'node:perf_hooks';

    const obs = new PerformanceObserver((perfObserverList, observer) => {
      console.log(perfObserverList.getEntries());

       * [
       *   PerformanceEntry {
       *     name: 'test',
       *     entryType: 'mark',
       *     startTime: 81.465639,
       *     duration: 0,
       *     detail: null
       *   },
       *   PerformanceEntry {
       *     name: 'meow',
       *     entryType: 'mark',
       *     startTime: 81.860064,
       *     duration: 0,
       *     detail: null
       *   }
       * ]

      performance.clearMarks();
      performance.clearMeasures();
      observer.disconnect();
    });
    obs.observe({ type: 'mark' });

    performance.mark('test');
    performance.mark('meow');
    ```
  + [getEntriesByName](https://bun.com/reference/node/perf_hooks/PerformanceObserverEntryList/getEntriesByName)(

    name: string,

    type?: [EntryType](https://bun.com/reference/node/perf_hooks/EntryType)

    ): [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)[];

    Returns a list of `PerformanceEntry` objects in chronological order with respect to `performanceEntry.startTime` whose `performanceEntry.name` is equal to `name`, and optionally, whose `performanceEntry.entryType` is equal to`type`.

    ```
    import {
      performance,
      PerformanceObserver,
    } from 'node:perf_hooks';

    const obs = new PerformanceObserver((perfObserverList, observer) => {
      console.log(perfObserverList.getEntriesByName('meow'));

       * [
       *   PerformanceEntry {
       *     name: 'meow',
       *     entryType: 'mark',
       *     startTime: 98.545991,
       *     duration: 0,
       *     detail: null
       *   }
       * ]

      console.log(perfObserverList.getEntriesByName('nope')); // []

      console.log(perfObserverList.getEntriesByName('test', 'mark'));

       * [
       *   PerformanceEntry {
       *     name: 'test',
       *     entryType: 'mark',
       *     startTime: 63.518931,
       *     duration: 0,
       *     detail: null
       *   }
       * ]

      console.log(perfObserverList.getEntriesByName('test', 'measure')); // []

      performance.clearMarks();
      performance.clearMeasures();
      observer.disconnect();
    });
    obs.observe({ entryTypes: ['mark', 'measure'] });

    performance.mark('test');
    performance.mark('meow');
    ```
  + [getEntriesByType](https://bun.com/reference/node/perf_hooks/PerformanceObserverEntryList/getEntriesByType)(

    type: [EntryType](https://bun.com/reference/node/perf_hooks/EntryType)

    ): [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)[];

    Returns a list of `PerformanceEntry` objects in chronological order with respect to `performanceEntry.startTime` whose `performanceEntry.entryType` is equal to `type`.

    ```
    import {
      performance,
      PerformanceObserver,
    } from 'node:perf_hooks';

    const obs = new PerformanceObserver((perfObserverList, observer) => {
      console.log(perfObserverList.getEntriesByType('mark'));

       * [
       *   PerformanceEntry {
       *     name: 'test',
       *     entryType: 'mark',
       *     startTime: 55.897834,
       *     duration: 0,
       *     detail: null
       *   },
       *   PerformanceEntry {
       *     name: 'meow',
       *     entryType: 'mark',
       *     startTime: 56.350146,
       *     duration: 0,
       *     detail: null
       *   }
       * ]

      performance.clearMarks();
      performance.clearMeasures();
      observer.disconnect();
    });
    obs.observe({ type: 'mark' });

    performance.mark('test');
    performance.mark('meow');
    ```
* ### class [PerformanceResourceTiming](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming)

  Provides detailed network timing data regarding the loading of an application's resources.

  The constructor of this class is not exposed to users directly.

  + readonly [connectEnd](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/connectEnd): number

    The high resolution millisecond timestamp representing the time immediately after Node.js finishes establishing the connection to the server to retrieve the resource.
  + readonly [connectStart](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/connectStart): number

    The high resolution millisecond timestamp representing the time immediately before Node.js starts to establish the connection to the server to retrieve the resource.
  + readonly [decodedBodySize](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/decodedBodySize): number

    A number representing the size (in octets) received from the fetch (HTTP or cache), of the message body, after removing any applied content-codings.
  + readonly [domainLookupEnd](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/domainLookupEnd): number

    The high resolution millisecond timestamp representing the time immediately after the Node.js finished the domain name lookup for the resource.
  + readonly [domainLookupStart](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/domainLookupStart): number

    The high resolution millisecond timestamp immediately before the Node.js starts the domain name lookup for the resource.
  + readonly [duration](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/duration): number

    The total number of milliseconds elapsed for this entry. This value will not be meaningful for all Performance Entry types.
  + readonly [encodedBodySize](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/encodedBodySize): number

    A number representing the size (in octets) received from the fetch (HTTP or cache), of the payload body, before removing any applied content-codings.
  + readonly [entryType](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/entryType): 'resource'

    The type of the performance entry. It may be one of:

    - `'node'` (Node.js only)
    - `'mark'` (available on the Web)
    - `'measure'` (available on the Web)
    - `'gc'` (Node.js only)
    - `'function'` (Node.js only)
    - `'http2'` (Node.js only)
    - `'http'` (Node.js only)
  + readonly [fetchStart](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/fetchStart): number

    The high resolution millisecond timestamp immediately before the Node.js starts to fetch the resource.
  + readonly [name](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/name): string

    The name of the performance entry.
  + readonly [redirectEnd](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/redirectEnd): number

    The high resolution millisecond timestamp that will be created immediately after receiving the last byte of the response of the last redirect.
  + readonly [redirectStart](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/redirectStart): number

    The high resolution millisecond timestamp that represents the start time of the fetch which initiates the redirect.
  + readonly [requestStart](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/requestStart): number

    The high resolution millisecond timestamp representing the time immediately before Node.js receives the first byte of the response from the server.
  + readonly [responseEnd](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/responseEnd): number

    The high resolution millisecond timestamp representing the time immediately after Node.js receives the last byte of the resource or immediately before the transport connection is closed, whichever comes first.
  + readonly [secureConnectionStart](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/secureConnectionStart): number

    The high resolution millisecond timestamp representing the time immediately before Node.js starts the handshake process to secure the current connection.
  + readonly [startTime](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/startTime): number

    The high resolution millisecond timestamp marking the starting time of the Performance Entry.
  + readonly [transferSize](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/transferSize): number

    A number representing the size (in octets) of the fetched resource. The size includes the response header fields plus the response payload body.
  + readonly [workerStart](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/workerStart): number

    The high resolution millisecond timestamp at immediately before dispatching the `fetch` request. If the resource is not intercepted by a worker the property will always return 0.
  + [toJSON](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming/toJSON)(): any;

    Returns a `object` that is the JSON representation of the `PerformanceResourceTiming` object
* const [performance](https://bun.com/reference/node/perf_hooks/performance): [Performance](https://bun.com/reference/node/perf_hooks/Performance)
* function [createHistogram](https://bun.com/reference/node/perf_hooks/createHistogram)(

  options?: [CreateHistogramOptions](https://bun.com/reference/node/perf_hooks/CreateHistogramOptions)

  ): [RecordableHistogram](https://bun.com/reference/node/perf_hooks/RecordableHistogram);

  Returns a `RecordableHistogram`.
* function [monitorEventLoopDelay](https://bun.com/reference/node/perf_hooks/monitorEventLoopDelay)(

  options?: [EventLoopMonitorOptions](https://bun.com/reference/node/perf_hooks/EventLoopMonitorOptions)

  ): [IntervalHistogram](https://bun.com/reference/node/perf_hooks/IntervalHistogram);

  *This property is an extension by Node.js. It is not available in Web browsers.*

  Creates an `IntervalHistogram` object that samples and reports the event loop delay over time. The delays will be reported in nanoseconds.

  Using a timer to detect approximate event loop delay works because the execution of timers is tied specifically to the lifecycle of the libuv event loop. That is, a delay in the loop will cause a delay in the execution of the timer, and those delays are specifically what this API is intended to detect.

  ```
  import { monitorEventLoopDelay } from 'node:perf_hooks';
  const h = monitorEventLoopDelay({ resolution: 20 });
  h.enable();
  // Do something.
  h.disable();
  console.log(h.min);
  console.log(h.max);
  console.log(h.mean);
  console.log(h.stddev);
  console.log(h.percentiles);
  console.log(h.percentile(50));
  console.log(h.percentile(99));
  ```

## Type definitions

* ### interface [CreateHistogramOptions](https://bun.com/reference/node/perf_hooks/CreateHistogramOptions)

  + [figures](https://bun.com/reference/node/perf_hooks/CreateHistogramOptions/figures)?: number

    The number of accuracy digits. Must be a number between 1 and 5.
  + [highest](https://bun.com/reference/node/perf_hooks/CreateHistogramOptions/highest)?: number | bigint

    The maximum recordable value. Must be an integer value greater than min.
  + [lowest](https://bun.com/reference/node/perf_hooks/CreateHistogramOptions/lowest)?: number | bigint

    The minimum recordable value. Must be an integer value greater than 0.
* ### interface [EventLoopMonitorOptions](https://bun.com/reference/node/perf_hooks/EventLoopMonitorOptions)

  + [resolution](https://bun.com/reference/node/perf_hooks/EventLoopMonitorOptions/resolution)?: number

    The sampling rate in milliseconds. Must be greater than zero.
* ### interface [EventLoopUtilization](https://bun.com/reference/node/perf_hooks/EventLoopUtilization)

  + [active](https://bun.com/reference/node/perf_hooks/EventLoopUtilization/active): number
  + [idle](https://bun.com/reference/node/perf_hooks/EventLoopUtilization/idle): number
  + [utilization](https://bun.com/reference/node/perf_hooks/EventLoopUtilization/utilization): number
* ### interface [Histogram](https://bun.com/reference/node/perf_hooks/Histogram)

  + readonly [count](https://bun.com/reference/node/perf_hooks/Histogram/count): number

    The number of samples recorded by the histogram.
  + readonly [countBigInt](https://bun.com/reference/node/perf_hooks/Histogram/countBigInt): bigint

    The number of samples recorded by the histogram. v17.4.0, v16.14.0
  + readonly [exceeds](https://bun.com/reference/node/perf_hooks/Histogram/exceeds): number

    The number of times the event loop delay exceeded the maximum 1 hour event loop delay threshold.
  + readonly [exceedsBigInt](https://bun.com/reference/node/perf_hooks/Histogram/exceedsBigInt): bigint

    The number of times the event loop delay exceeded the maximum 1 hour event loop delay threshold.
  + readonly [max](https://bun.com/reference/node/perf_hooks/Histogram/max): number

    The maximum recorded event loop delay.
  + readonly [maxBigInt](https://bun.com/reference/node/perf_hooks/Histogram/maxBigInt): number

    The maximum recorded event loop delay. v17.4.0, v16.14.0
  + readonly [mean](https://bun.com/reference/node/perf_hooks/Histogram/mean): number

    The mean of the recorded event loop delays.
  + readonly [min](https://bun.com/reference/node/perf_hooks/Histogram/min): number

    The minimum recorded event loop delay.
  + readonly [minBigInt](https://bun.com/reference/node/perf_hooks/Histogram/minBigInt): bigint

    The minimum recorded event loop delay. v17.4.0, v16.14.0
  + readonly [percentiles](https://bun.com/reference/node/perf_hooks/Histogram/percentiles): Map<number, number>

    Returns a `Map` object detailing the accumulated percentile distribution.
  + readonly [percentilesBigInt](https://bun.com/reference/node/perf_hooks/Histogram/percentilesBigInt): Map<bigint, bigint>

    Returns a `Map` object detailing the accumulated percentile distribution.
  + readonly [stddev](https://bun.com/reference/node/perf_hooks/Histogram/stddev): number

    The standard deviation of the recorded event loop delays.
  + [percentile](https://bun.com/reference/node/perf_hooks/Histogram/percentile)(

    percentile: number

    ): number;

    Returns the value at the given percentile.

    @param percentile

    A percentile value in the range (0, 100].
  + [percentileBigInt](https://bun.com/reference/node/perf_hooks/Histogram/percentileBigInt)(

    percentile: number

    ): bigint;

    Returns the value at the given percentile.

    @param percentile

    A percentile value in the range (0, 100].
  + [reset](https://bun.com/reference/node/perf_hooks/Histogram/reset)(): void;

    Resets the collected histogram data.
* ### interface [IntervalHistogram](https://bun.com/reference/node/perf_hooks/IntervalHistogram)

  + readonly [count](https://bun.com/reference/node/perf_hooks/IntervalHistogram/count): number

    The number of samples recorded by the histogram.
  + readonly [countBigInt](https://bun.com/reference/node/perf_hooks/IntervalHistogram/countBigInt): bigint

    The number of samples recorded by the histogram. v17.4.0, v16.14.0
  + readonly [exceeds](https://bun.com/reference/node/perf_hooks/IntervalHistogram/exceeds): number

    The number of times the event loop delay exceeded the maximum 1 hour event loop delay threshold.
  + readonly [exceedsBigInt](https://bun.com/reference/node/perf_hooks/IntervalHistogram/exceedsBigInt): bigint

    The number of times the event loop delay exceeded the maximum 1 hour event loop delay threshold.
  + readonly [max](https://bun.com/reference/node/perf_hooks/IntervalHistogram/max): number

    The maximum recorded event loop delay.
  + readonly [maxBigInt](https://bun.com/reference/node/perf_hooks/IntervalHistogram/maxBigInt): number

    The maximum recorded event loop delay. v17.4.0, v16.14.0
  + readonly [mean](https://bun.com/reference/node/perf_hooks/IntervalHistogram/mean): number

    The mean of the recorded event loop delays.
  + readonly [min](https://bun.com/reference/node/perf_hooks/IntervalHistogram/min): number

    The minimum recorded event loop delay.
  + readonly [minBigInt](https://bun.com/reference/node/perf_hooks/IntervalHistogram/minBigInt): bigint

    The minimum recorded event loop delay. v17.4.0, v16.14.0
  + readonly [percentiles](https://bun.com/reference/node/perf_hooks/IntervalHistogram/percentiles): Map<number, number>

    Returns a `Map` object detailing the accumulated percentile distribution.
  + readonly [percentilesBigInt](https://bun.com/reference/node/perf_hooks/IntervalHistogram/percentilesBigInt): Map<bigint, bigint>

    Returns a `Map` object detailing the accumulated percentile distribution.
  + readonly [stddev](https://bun.com/reference/node/perf_hooks/IntervalHistogram/stddev): number

    The standard deviation of the recorded event loop delays.
  + [[Symbol.dispose]](https://bun.com/reference/node/perf_hooks/IntervalHistogram/[dispose])(): void;

    Disables the update interval timer when the histogram is disposed.

    ```
    const { monitorEventLoopDelay } = require('node:perf_hooks');
    {
      using hist = monitorEventLoopDelay({ resolution: 20 });
      hist.enable();
      // The histogram will be disabled when the block is exited.
    }
    ```
  + [disable](https://bun.com/reference/node/perf_hooks/IntervalHistogram/disable)(): boolean;

    Disables the update interval timer. Returns `true` if the timer was stopped, `false` if it was already stopped.
  + [enable](https://bun.com/reference/node/perf_hooks/IntervalHistogram/enable)(): boolean;

    Enables the update interval timer. Returns `true` if the timer was started, `false` if it was already started.
  + [percentile](https://bun.com/reference/node/perf_hooks/IntervalHistogram/percentile)(

    percentile: number

    ): number;

    Returns the value at the given percentile.

    @param percentile

    A percentile value in the range (0, 100].
  + [percentileBigInt](https://bun.com/reference/node/perf_hooks/IntervalHistogram/percentileBigInt)(

    percentile: number

    ): bigint;

    Returns the value at the given percentile.

    @param percentile

    A percentile value in the range (0, 100].
  + [reset](https://bun.com/reference/node/perf_hooks/IntervalHistogram/reset)(): void;

    Resets the collected histogram data.
* ### interface [MarkOptions](https://bun.com/reference/node/perf_hooks/MarkOptions)

  + [detail](https://bun.com/reference/node/perf_hooks/MarkOptions/detail)?: unknown

    Additional optional detail to include with the mark.
  + [startTime](https://bun.com/reference/node/perf_hooks/MarkOptions/startTime)?: number

    An optional timestamp to be used as the mark time.
* ### interface [MeasureOptions](https://bun.com/reference/node/perf_hooks/MeasureOptions)

  + [detail](https://bun.com/reference/node/perf_hooks/MeasureOptions/detail)?: unknown

    Additional optional detail to include with the mark.
  + [duration](https://bun.com/reference/node/perf_hooks/MeasureOptions/duration)?: number

    Duration between start and end times.
  + [end](https://bun.com/reference/node/perf_hooks/MeasureOptions/end)?: string | number

    Timestamp to be used as the end time, or a string identifying a previously recorded mark.
  + [start](https://bun.com/reference/node/perf_hooks/MeasureOptions/start)?: string | number

    Timestamp to be used as the start time, or a string identifying a previously recorded mark.
* ### interface [NodeGCPerformanceDetail](https://bun.com/reference/node/perf_hooks/NodeGCPerformanceDetail)

  + readonly [flags](https://bun.com/reference/node/perf_hooks/NodeGCPerformanceDetail/flags): number

    When `performanceEntry.entryType` is equal to 'gc', the `performance.flags` property contains additional information about garbage collection operation. See perf\_hooks.constants for valid values.
  + readonly [kind](https://bun.com/reference/node/perf_hooks/NodeGCPerformanceDetail/kind): number

    When `performanceEntry.entryType` is equal to 'gc', the `performance.kind` property identifies the type of garbage collection operation that occurred. See perf\_hooks.constants for valid values.
* ### interface [Performance](https://bun.com/reference/node/perf_hooks/Performance)

  + [eventLoopUtilization](https://bun.com/reference/node/perf_hooks/Performance/eventLoopUtilization): [EventLoopUtilityFunction](https://bun.com/reference/node/perf_hooks/EventLoopUtilityFunction)

    eventLoopUtilization is similar to CPU utilization except that it is calculated using high precision wall-clock time. It represents the percentage of time the event loop has spent outside the event loop's event provider (e.g. epoll\_wait). No other CPU idle time is taken into consideration.
  + readonly [nodeTiming](https://bun.com/reference/node/perf_hooks/Performance/nodeTiming): [PerformanceNodeTiming](https://bun.com/reference/node/perf_hooks/PerformanceNodeTiming)

    *This property is an extension by Node.js. It is not available in Web browsers.*

    An instance of the `PerformanceNodeTiming` class that provides performance metrics for specific Node.js operational milestones.
  + readonly [timeOrigin](https://bun.com/reference/node/perf_hooks/Performance/timeOrigin): number

    The [`timeOrigin`](https://w3c.github.io/hr-time/#dom-performance-timeorigin) specifies the high resolution millisecond timestamp at which the current `node` process began, measured in Unix time.
  + [clearMarks](https://bun.com/reference/node/perf_hooks/Performance/clearMarks)(

    name?: string

    ): void;

    If `name` is not provided, removes all `PerformanceMark` objects from the Performance Timeline. If `name` is provided, removes only the named mark.
  + [clearMeasures](https://bun.com/reference/node/perf_hooks/Performance/clearMeasures)(

    name?: string

    ): void;

    If `name` is not provided, removes all `PerformanceMeasure` objects from the Performance Timeline. If `name` is provided, removes only the named measure.
  + [clearResourceTimings](https://bun.com/reference/node/perf_hooks/Performance/clearResourceTimings)(

    name?: string

    ): void;

    If `name` is not provided, removes all `PerformanceResourceTiming` objects from the Resource Timeline. If `name` is provided, removes only the named resource.
  + [getEntries](https://bun.com/reference/node/perf_hooks/Performance/getEntries)(): [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)[];

    Returns a list of `PerformanceEntry` objects in chronological order with respect to `performanceEntry.startTime`. If you are only interested in performance entries of certain types or that have certain names, see `performance.getEntriesByType()` and `performance.getEntriesByName()`.
  + [getEntriesByName](https://bun.com/reference/node/perf_hooks/Performance/getEntriesByName)(

    name: string,

    type?: [EntryType](https://bun.com/reference/node/perf_hooks/EntryType)

    ): [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)[];

    Returns a list of `PerformanceEntry` objects in chronological order with respect to `performanceEntry.startTime` whose `performanceEntry.name` is equal to `name`, and optionally, whose `performanceEntry.entryType` is equal to `type`.
  + [getEntriesByType](https://bun.com/reference/node/perf_hooks/Performance/getEntriesByType)(

    type: [EntryType](https://bun.com/reference/node/perf_hooks/EntryType)

    ): [PerformanceEntry](https://bun.com/reference/node/perf_hooks/PerformanceEntry)[];

    Returns a list of `PerformanceEntry` objects in chronological order with respect to `performanceEntry.startTime` whose `performanceEntry.entryType` is equal to `type`.
  + [mark](https://bun.com/reference/node/perf_hooks/Performance/mark)(

    name: string,

    options?: [MarkOptions](https://bun.com/reference/node/perf_hooks/MarkOptions)

    ): [PerformanceMark](https://bun.com/reference/node/perf_hooks/PerformanceMark);

    Creates a new `PerformanceMark` entry in the Performance Timeline. A `PerformanceMark` is a subclass of `PerformanceEntry` whose `performanceEntry.entryType` is always `'mark'`, and whose `performanceEntry.duration` is always `0`. Performance marks are used to mark specific significant moments in the Performance Timeline.

    The created `PerformanceMark` entry is put in the global Performance Timeline and can be queried with `performance.getEntries`, `performance.getEntriesByName`, and `performance.getEntriesByType`. When the observation is performed, the entries should be cleared from the global Performance Timeline manually with `performance.clearMarks`.
  + [markResourceTiming](https://bun.com/reference/node/perf_hooks/Performance/markResourceTiming)(

    timingInfo: object,

    requestedUrl: string,

    initiatorType: string,

    global: object,

    cacheMode: '' | 'local',

    bodyInfo: object,

    responseStatus: number,

    deliveryType?: string

    ): [PerformanceResourceTiming](https://bun.com/reference/node/perf_hooks/PerformanceResourceTiming);

    Creates a new `PerformanceResourceTiming` entry in the Resource Timeline. A `PerformanceResourceTiming` is a subclass of `PerformanceEntry` whose `performanceEntry.entryType` is always `'resource'`. Performance resources are used to mark moments in the Resource Timeline.

    @param timingInfo

    [Fetch Timing Info](https://fetch.spec.whatwg.org/#fetch-timing-info)

    @param requestedUrl

    The resource url

    @param initiatorType

    The initiator name, e.g: 'fetch'

    @param cacheMode

    The cache mode must be an empty string ('') or 'local'

    @param bodyInfo

    [Fetch Response Body Info](https://fetch.spec.whatwg.org/#response-body-info)

    @param responseStatus

    The response's status code

    @param deliveryType

    The delivery type. Default: ''.
  + [measure](https://bun.com/reference/node/perf_hooks/Performance/measure)(

    name: string,

    startMark?: string,

    endMark?: string

    ): [PerformanceMeasure](https://bun.com/reference/node/perf_hooks/PerformanceMeasure);

    Creates a new PerformanceMeasure entry in the Performance Timeline. A PerformanceMeasure is a subclass of PerformanceEntry whose performanceEntry.entryType is always 'measure', and whose performanceEntry.duration measures the number of milliseconds elapsed since startMark and endMark.

    The startMark argument may identify any existing PerformanceMark in the the Performance Timeline, or may identify any of the timestamp properties provided by the PerformanceNodeTiming class. If the named startMark does not exist, then startMark is set to timeOrigin by default.

    The endMark argument must identify any existing PerformanceMark in the the Performance Timeline or any of the timestamp properties provided by the PerformanceNodeTiming class. If the named endMark does not exist, an error will be thrown.

    @returns

    The PerformanceMeasure entry that was created

    [measure](https://bun.com/reference/node/perf_hooks/Performance/measure)(

    name: string,

    options: [MeasureOptions](https://bun.com/reference/node/perf_hooks/MeasureOptions)

    ): [PerformanceMeasure](https://bun.com/reference/node/perf_hooks/PerformanceMeasure);
  + [now](https://bun.com/reference/node/perf_hooks/Performance/now)(): number;

    Returns the current high resolution millisecond timestamp, where 0 represents the start of the current `node` process.
  + [setResourceTimingBufferSize](https://bun.com/reference/node/perf_hooks/Performance/setResourceTimingBufferSize)(

    maxSize: number

    ): void;

    Sets the global performance resource timing buffer size to the specified number of "resource" type performance entry objects.

    By default the max buffer size is set to 250.
  + [timerify](https://bun.com/reference/node/perf_hooks/Performance/timerify)<T extends (...params: any[]) => any>(

    fn: T,

    options?: [TimerifyOptions](https://bun.com/reference/node/perf_hooks/TimerifyOptions)

    ): T;

    *This property is an extension by Node.js. It is not available in Web browsers.*

    Wraps a function within a new function that measures the running time of the wrapped function. A `PerformanceObserver` must be subscribed to the `'function'` event type in order for the timing details to be accessed.

    ```
    import {
      performance,
      PerformanceObserver,
    } from 'node:perf_hooks';

    function someFunction() {
      console.log('hello world');
    }

    const wrapped = performance.timerify(someFunction);

    const obs = new PerformanceObserver((list) => {
      console.log(list.getEntries()[0].duration);

      performance.clearMarks();
      performance.clearMeasures();
      obs.disconnect();
    });
    obs.observe({ entryTypes: ['function'] });

    // A performance timeline entry will be created
    wrapped();
    ```

    If the wrapped function returns a promise, a finally handler will be attached to the promise and the duration will be reported once the finally handler is invoked.
  + [toJSON](https://bun.com/reference/node/perf_hooks/Performance/toJSON)(): any;

    An object which is JSON representation of the performance object. It is similar to [`window.performance.toJSON`](https://developer.mozilla.org/en-US/docs/Web/API/Performance/toJSON) in browsers.
* ### interface [RecordableHistogram](https://bun.com/reference/node/perf_hooks/RecordableHistogram)

  + readonly [count](https://bun.com/reference/node/perf_hooks/RecordableHistogram/count): number

    The number of samples recorded by the histogram.
  + readonly [countBigInt](https://bun.com/reference/node/perf_hooks/RecordableHistogram/countBigInt): bigint

    The number of samples recorded by the histogram. v17.4.0, v16.14.0
  + readonly [exceeds](https://bun.com/reference/node/perf_hooks/RecordableHistogram/exceeds): number

    The number of times the event loop delay exceeded the maximum 1 hour event loop delay threshold.
  + readonly [exceedsBigInt](https://bun.com/reference/node/perf_hooks/RecordableHistogram/exceedsBigInt): bigint

    The number of times the event loop delay exceeded the maximum 1 hour event loop delay threshold.
  + readonly [max](https://bun.com/reference/node/perf_hooks/RecordableHistogram/max): number

    The maximum recorded event loop delay.
  + readonly [maxBigInt](https://bun.com/reference/node/perf_hooks/RecordableHistogram/maxBigInt): number

    The maximum recorded event loop delay. v17.4.0, v16.14.0
  + readonly [mean](https://bun.com/reference/node/perf_hooks/RecordableHistogram/mean): number

    The mean of the recorded event loop delays.
  + readonly [min](https://bun.com/reference/node/perf_hooks/RecordableHistogram/min): number

    The minimum recorded event loop delay.
  + readonly [minBigInt](https://bun.com/reference/node/perf_hooks/RecordableHistogram/minBigInt): bigint

    The minimum recorded event loop delay. v17.4.0, v16.14.0
  + readonly [percentiles](https://bun.com/reference/node/perf_hooks/RecordableHistogram/percentiles): Map<number, number>

    Returns a `Map` object detailing the accumulated percentile distribution.
  + readonly [percentilesBigInt](https://bun.com/reference/node/perf_hooks/RecordableHistogram/percentilesBigInt): Map<bigint, bigint>

    Returns a `Map` object detailing the accumulated percentile distribution.
  + readonly [stddev](https://bun.com/reference/node/perf_hooks/RecordableHistogram/stddev): number

    The standard deviation of the recorded event loop delays.
  + [add](https://bun.com/reference/node/perf_hooks/RecordableHistogram/add)(

    other: [RecordableHistogram](https://bun.com/reference/node/perf_hooks/RecordableHistogram)

    ): void;

    Adds the values from `other` to this histogram.
  + [percentile](https://bun.com/reference/node/perf_hooks/RecordableHistogram/percentile)(

    percentile: number

    ): number;

    Returns the value at the given percentile.

    @param percentile

    A percentile value in the range (0, 100].
  + [percentileBigInt](https://bun.com/reference/node/perf_hooks/RecordableHistogram/percentileBigInt)(

    percentile: number

    ): bigint;

    Returns the value at the given percentile.

    @param percentile

    A percentile value in the range (0, 100].
  + [record](https://bun.com/reference/node/perf_hooks/RecordableHistogram/record)(

    val: number | bigint

    ): void;

    @param val

    The amount to record in the histogram.
  + [recordDelta](https://bun.com/reference/node/perf_hooks/RecordableHistogram/recordDelta)(): void;

    Calculates the amount of time (in nanoseconds) that has passed since the previous call to `recordDelta()` and records that amount in the histogram.
  + [reset](https://bun.com/reference/node/perf_hooks/RecordableHistogram/reset)(): void;

    Resets the collected histogram data.
* ### interface [TimerifyOptions](https://bun.com/reference/node/perf_hooks/TimerifyOptions)

  + [histogram](https://bun.com/reference/node/perf_hooks/TimerifyOptions/histogram)?: [RecordableHistogram](https://bun.com/reference/node/perf_hooks/RecordableHistogram)

    A histogram object created using `perf_hooks.createHistogram()` that will record runtime durations in nanoseconds.
* ### interface [UVMetrics](https://bun.com/reference/node/perf_hooks/UVMetrics)

  + readonly [events](https://bun.com/reference/node/perf_hooks/UVMetrics/events): number

    Number of events that have been processed by the event handler.
  + readonly [eventsWaiting](https://bun.com/reference/node/perf_hooks/UVMetrics/eventsWaiting): number

    Number of events that were waiting to be processed when the event provider was called.
  + readonly [loopCount](https://bun.com/reference/node/perf_hooks/UVMetrics/loopCount): number

    Number of event loop iterations.
* type [EntryType](https://bun.com/reference/node/perf_hooks/EntryType) = 'dns' | 'function' | 'gc' | 'http2' | 'http' | 'mark' | 'measure' | 'net' | 'node' | 'resource'
* type [EventLoopUtilityFunction](https://bun.com/reference/node/perf_hooks/EventLoopUtilityFunction) = (utilization1?: [EventLoopUtilization](https://bun.com/reference/node/perf_hooks/EventLoopUtilization), utilization2?: [EventLoopUtilization](https://bun.com/reference/node/perf_hooks/EventLoopUtilization)) => [EventLoopUtilization](https://bun.com/reference/node/perf_hooks/EventLoopUtilization)
* type [PerformanceObserverCallback](https://bun.com/reference/node/perf_hooks/PerformanceObserverCallback) = (list: [PerformanceObserverEntryList](https://bun.com/reference/node/perf_hooks/PerformanceObserverEntryList), observer: [PerformanceObserver](https://bun.com/reference/node/perf_hooks/PerformanceObserver)) => void