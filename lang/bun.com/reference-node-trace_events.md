---
url: https://bun.com/reference/node/trace_events
title: Node.js trace_events module | API Reference | Bun
source_domain: bun.com
---

# Node.js trace_events module | API Reference | Bun

Node.js module

# [trace\_events](https://bun.com/reference/node/trace_events)

The `'node:trace_events'` module enables programmatic control of Node.js's built-in tracing system. You can enable or disable tracing categories that log V8, Node core, or user-defined events to a trace file.

Traces can be analyzed with Chrome DevTools or other profiling tools to diagnose performance bottlenecks.

Not implemented in Bun

Not implemented. Profiling and tracing capabilities might be available through other means (e.g., `bun --profile`, `bun:jsc`).

* function [createTracing](https://bun.com/reference/node/trace_events/createTracing)(

  options: [CreateTracingOptions](https://bun.com/reference/node/trace_events/CreateTracingOptions)

  ): [Tracing](https://bun.com/reference/node/trace_events/Tracing);

  Creates and returns a `Tracing` object for the given set of `categories`.

  ```
  import trace_events from 'node:trace_events';
  const categories = ['node.perf', 'node.async_hooks'];
  const tracing = trace_events.createTracing({ categories });
  tracing.enable();
  // do stuff
  tracing.disable();
  ```
* function [getEnabledCategories](https://bun.com/reference/node/trace_events/getEnabledCategories)(): undefined | string;

  Returns a comma-separated list of all currently-enabled trace event categories. The current set of enabled trace event categories is determined by the *union* of all currently-enabled `Tracing` objects and any categories enabled using the `--trace-event-categories` flag.

  Given the file `test.js` below, the command `node --trace-event-categories node.perf test.js` will print `'node.async_hooks,node.perf'` to the console.

  ```
  import trace_events from 'node:trace_events';
  const t1 = trace_events.createTracing({ categories: ['node.async_hooks'] });
  const t2 = trace_events.createTracing({ categories: ['node.perf'] });
  const t3 = trace_events.createTracing({ categories: ['v8'] });

  t1.enable();
  t2.enable();

  console.log(trace_events.getEnabledCategories());
  ```

## Type definitions

* ### interface [CreateTracingOptions](https://bun.com/reference/node/trace_events/CreateTracingOptions)

  + [categories](https://bun.com/reference/node/trace_events/CreateTracingOptions/categories): string[]

    An array of trace category names. Values included in the array are coerced to a string when possible. An error will be thrown if the value cannot be coerced.
* ### interface [Tracing](https://bun.com/reference/node/trace_events/Tracing)

  The `Tracing` object is used to enable or disable tracing for sets of categories. Instances are created using the `trace_events.createTracing()` method.

  When created, the `Tracing` object is disabled. Calling the `tracing.enable()` method adds the categories to the set of enabled trace event categories. Calling `tracing.disable()` will remove the categories from the set of enabled trace event categories.

  + readonly [categories](https://bun.com/reference/node/trace_events/Tracing/categories): string

    A comma-separated list of the trace event categories covered by this `Tracing` object.
  + readonly [enabled](https://bun.com/reference/node/trace_events/Tracing/enabled): boolean

    `true` only if the `Tracing` object has been enabled.
  + [disable](https://bun.com/reference/node/trace_events/Tracing/disable)(): void;

    Disables this `Tracing` object.

    Only trace event categories *not* covered by other enabled `Tracing` objects and *not* specified by the `--trace-event-categories` flag will be disabled.

    ```
    import trace_events from 'node:trace_events';
    const t1 = trace_events.createTracing({ categories: ['node', 'v8'] });
    const t2 = trace_events.createTracing({ categories: ['node.perf', 'node'] });
    t1.enable();
    t2.enable();

    // Prints 'node,node.perf,v8'
    console.log(trace_events.getEnabledCategories());

    t2.disable(); // Will only disable emission of the 'node.perf' category

    // Prints 'node,v8'
    console.log(trace_events.getEnabledCategories());
    ```
  + [enable](https://bun.com/reference/node/trace_events/Tracing/enable)(): void;

    Enables this `Tracing` object for the set of categories covered by the `Tracing` object.