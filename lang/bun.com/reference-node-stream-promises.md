---
url: https://bun.com/reference/node/stream/promises
title: Node.js stream/promises module | API Reference | Bun
source_domain: bun.com
---

# Node.js stream/promises module | API Reference | Bun

Node.js module

# [stream/promises](https://bun.com/reference/node/stream/promises)

The `'node:stream/promises'` submodule provides Promise-based stream utility functions such as `pipeline` and `finished`, enabling async/await syntax for stream completion and pipeline composition.

Use it to coordinate multiple streams and handle errors cleanly in async code.

* function [finished](https://bun.com/reference/node/stream/promises/finished)(

  stream: ReadWriteStream | ReadableStream | WritableStream,

  options?: [FinishedOptions](https://bun.com/reference/node/stream/promises/FinishedOptions)

  ): Promise<void>;
* function [pipeline](https://bun.com/reference/node/stream/promises/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

  source: A,

  destination: B,

  options?: [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)

  ): [PipelinePromise](https://bun.com/reference/node/stream/default/PipelinePromise)<B>;

  function [pipeline](https://bun.com/reference/node/stream/promises/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

  source: A,

  transform1: T1,

  destination: B,

  options?: [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)

  ): [PipelinePromise](https://bun.com/reference/node/stream/default/PipelinePromise)<B>;

  function [pipeline](https://bun.com/reference/node/stream/promises/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

  source: A,

  transform1: T1,

  transform2: T2,

  destination: B,

  options?: [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)

  ): [PipelinePromise](https://bun.com/reference/node/stream/default/PipelinePromise)<B>;

  function [pipeline](https://bun.com/reference/node/stream/promises/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, T3 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T2, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

  source: A,

  transform1: T1,

  transform2: T2,

  transform3: T3,

  destination: B,

  options?: [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)

  ): [PipelinePromise](https://bun.com/reference/node/stream/default/PipelinePromise)<B>;

  function [pipeline](https://bun.com/reference/node/stream/promises/pipeline)<A extends [PipelineSource](https://bun.com/reference/node/stream/default/PipelineSource)<any>, T1 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<A, any>, T2 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T1, any>, T3 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T2, any>, T4 extends [PipelineTransform](https://bun.com/reference/node/stream/default/PipelineTransform)<T3, any>, B extends WritableStream | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<string | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>, any> | [PipelineDestinationIterableFunction](https://bun.com/reference/node/stream/default/PipelineDestinationIterableFunction)<any> | [PipelineDestinationPromiseFunction](https://bun.com/reference/node/stream/default/PipelineDestinationPromiseFunction)<any, any>>(

  source: A,

  transform1: T1,

  transform2: T2,

  transform3: T3,

  transform4: T4,

  destination: B,

  options?: [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)

  ): [PipelinePromise](https://bun.com/reference/node/stream/default/PipelinePromise)<B>;

  function [pipeline](https://bun.com/reference/node/stream/promises/pipeline)(

  streams: readonly ReadWriteStream | ReadableStream | WritableStream[],

  options?: [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)

  ): Promise<void>;

  function [pipeline](https://bun.com/reference/node/stream/promises/pipeline)(

  stream1: ReadableStream,

  stream2: ReadWriteStream | WritableStream,

  ...streams: ReadWriteStream | WritableStream | [PipelineOptions](https://bun.com/reference/node/stream/default/PipelineOptions)[]

  ): Promise<void>;

## Type definitions

* ### interface [FinishedOptions](https://bun.com/reference/node/stream/promises/FinishedOptions)

  + [cleanup](https://bun.com/reference/node/stream/promises/FinishedOptions/cleanup)?: boolean

    If true, removes the listeners registered by this function before the promise is fulfilled.
  + [error](https://bun.com/reference/node/stream/promises/FinishedOptions/error)?: boolean
  + [readable](https://bun.com/reference/node/stream/promises/FinishedOptions/readable)?: boolean
  + [signal](https://bun.com/reference/node/stream/promises/FinishedOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)

    When provided the corresponding `AbortController` can be used to cancel an asynchronous action.
  + [writable](https://bun.com/reference/node/stream/promises/FinishedOptions/writable)?: boolean