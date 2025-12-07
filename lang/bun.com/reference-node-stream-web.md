---
url: https://bun.com/reference/node/stream/web
title: Node.js stream/web module | API Reference | Bun
source_domain: bun.com
---

# Node.js stream/web module | API Reference | Bun

Node.js module

# [stream/web](https://bun.com/reference/node/stream/web)

The `'node:stream/web'` submodule implements WHATWG Streams API interfaces (`ReadableStream`, `WritableStream`) in Node.js, aligning with browser stream standards.

This allows interoperation between web-standard and Node-native streams in modern applications.

* ### class [CompressionStream](https://bun.com/reference/node/stream/web/CompressionStream)

  + readonly [readable](https://bun.com/reference/node/stream/web/CompressionStream/readable): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)
  + readonly [writable](https://bun.com/reference/node/stream/web/CompressionStream/writable): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)
* ### class [DecompressionStream](https://bun.com/reference/node/stream/web/DecompressionStream)

  + readonly [readable](https://bun.com/reference/node/stream/web/DecompressionStream/readable): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)
  + readonly [writable](https://bun.com/reference/node/stream/web/DecompressionStream/writable): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)
* const [ByteLengthQueuingStrategy](https://bun.com/reference/node/stream/web/ByteLengthQueuingStrategy): new (init: [QueuingStrategyInit](https://bun.com/reference/node/stream/web/QueuingStrategyInit)) => [ByteLengthQueuingStrategy](https://bun.com/reference/node/stream/web/ByteLengthQueuingStrategy)
* const [CountQueuingStrategy](https://bun.com/reference/node/stream/web/CountQueuingStrategy): new (init: [QueuingStrategyInit](https://bun.com/reference/node/stream/web/QueuingStrategyInit)) => [CountQueuingStrategy](https://bun.com/reference/node/stream/web/CountQueuingStrategy)
* const [ReadableByteStreamController](https://bun.com/reference/node/stream/web/ReadableByteStreamController): new () => [ReadableByteStreamController](https://bun.com/reference/node/stream/web/ReadableByteStreamController)
* const [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream): {new (underlyingSource: [UnderlyingByteSource](https://bun.com/reference/node/stream/web/UnderlyingByteSource), strategy?: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>) => [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>; new (underlyingSource?: [UnderlyingSource](https://bun.com/reference/node/stream/web/UnderlyingSource)<R>, strategy?: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<R>) => [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<R>}
* const [ReadableStreamBYOBReader](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader): new (stream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)) => [ReadableStreamBYOBReader](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader)
* const [ReadableStreamBYOBRequest](https://bun.com/reference/node/stream/web/ReadableStreamBYOBRequest): new () => [ReadableStreamBYOBRequest](https://bun.com/reference/node/stream/web/ReadableStreamBYOBRequest)
* const [ReadableStreamDefaultController](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController): new () => [ReadableStreamDefaultController](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController)
* const [ReadableStreamDefaultReader](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader): new (stream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<R>) => [ReadableStreamDefaultReader](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader)<R>
* const [TextDecoderStream](https://bun.com/reference/node/stream/web/TextDecoderStream): new (encoding?: string, options?: [TextDecoderOptions](https://bun.com/reference/node/stream/web/TextDecoderOptions)) => [TextDecoderStream](https://bun.com/reference/node/stream/web/TextDecoderStream)
* const [TextEncoderStream](https://bun.com/reference/node/stream/web/TextEncoderStream): new () => [TextEncoderStream](https://bun.com/reference/node/stream/web/TextEncoderStream)
* const [TransformStream](https://bun.com/reference/node/stream/web/TransformStream): new (transformer?: [Transformer](https://bun.com/reference/node/stream/web/Transformer)<I, O>, writableStrategy?: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<I>, readableStrategy?: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<O>) => [TransformStream](https://bun.com/reference/node/stream/web/TransformStream)<I, O>
* const [TransformStreamDefaultController](https://bun.com/reference/node/stream/web/TransformStreamDefaultController): new () => [TransformStreamDefaultController](https://bun.com/reference/node/stream/web/TransformStreamDefaultController)
* const [WritableStream](https://bun.com/reference/node/stream/web/WritableStream): new (underlyingSink?: [UnderlyingSink](https://bun.com/reference/node/stream/web/UnderlyingSink)<W>, strategy?: [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<W>) => [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<W>
* const [WritableStreamDefaultController](https://bun.com/reference/node/stream/web/WritableStreamDefaultController): new () => [WritableStreamDefaultController](https://bun.com/reference/node/stream/web/WritableStreamDefaultController)
* const [WritableStreamDefaultWriter](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter): new (stream: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<W>) => [WritableStreamDefaultWriter](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter)<W>

## Type definitions

* ### interface [ByteLengthQueuingStrategy](https://bun.com/reference/node/stream/web/ByteLengthQueuingStrategy)

  This Streams API interface provides a built-in byte length queuing strategy that can be used when constructing streams.

  + readonly [highWaterMark](https://bun.com/reference/node/stream/web/ByteLengthQueuingStrategy/highWaterMark): number
  + readonly [size](https://bun.com/reference/node/stream/web/ByteLengthQueuingStrategy/size): [QueuingStrategySize](https://bun.com/reference/node/stream/web/QueuingStrategySize)<ArrayBufferView<ArrayBufferLike>>
* ### interface [CountQueuingStrategy](https://bun.com/reference/node/stream/web/CountQueuingStrategy)

  This Streams API interface provides a built-in byte length queuing strategy that can be used when constructing streams.

  + readonly [highWaterMark](https://bun.com/reference/node/stream/web/CountQueuingStrategy/highWaterMark): number
  + readonly [size](https://bun.com/reference/node/stream/web/CountQueuingStrategy/size): [QueuingStrategySize](https://bun.com/reference/node/stream/web/QueuingStrategySize)
* ### interface [QueuingStrategy](https://bun.com/reference/node/stream/web/QueuingStrategy)<T = any>

  + [highWaterMark](https://bun.com/reference/node/stream/web/QueuingStrategy/highWaterMark)?: number
  + [size](https://bun.com/reference/node/stream/web/QueuingStrategy/size)?: [QueuingStrategySize](https://bun.com/reference/node/stream/web/QueuingStrategySize)<T>
* ### interface [QueuingStrategyInit](https://bun.com/reference/node/stream/web/QueuingStrategyInit)

  + [highWaterMark](https://bun.com/reference/node/stream/web/QueuingStrategyInit/highWaterMark): number

    Creates a new ByteLengthQueuingStrategy with the provided high water mark.

    Note that the provided high water mark will not be validated ahead of time. Instead, if it is negative, NaN, or not a number, the resulting ByteLengthQueuingStrategy will cause the corresponding stream constructor to throw.
* ### interface [QueuingStrategySize](https://bun.com/reference/node/stream/web/QueuingStrategySize)<T = any>
* ### interface [ReadableByteStreamController](https://bun.com/reference/node/stream/web/ReadableByteStreamController)

  + readonly [byobRequest](https://bun.com/reference/node/stream/web/ReadableByteStreamController/byobRequest): undefined
  + readonly [desiredSize](https://bun.com/reference/node/stream/web/ReadableByteStreamController/desiredSize): null | number
  + [close](https://bun.com/reference/node/stream/web/ReadableByteStreamController/close)(): void;
  + [enqueue](https://bun.com/reference/node/stream/web/ReadableByteStreamController/enqueue)(

    chunk: ArrayBufferView

    ): void;
  + [error](https://bun.com/reference/node/stream/web/ReadableByteStreamController/error)(

    error?: any

    ): void;
* ### interface [ReadableByteStreamControllerCallback](https://bun.com/reference/node/stream/web/ReadableByteStreamControllerCallback)
* ### interface [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<R = any>

  This Streams API interface represents a readable stream of byte data.

  + readonly [locked](https://bun.com/reference/node/stream/web/ReadableStream/locked): boolean
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/stream/web/ReadableStream/[asyncIterator])(): [ReadableStreamAsyncIterator](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator)<R>;
  + [blob](https://bun.com/reference/node/stream/web/ReadableStream/blob)(): Promise<[Blob](https://bun.com/reference/globals/Blob)>;

    Consume as a Blob
  + [bytes](https://bun.com/reference/node/stream/web/ReadableStream/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Consume as a Uint8Array, backed by an ArrayBuffer
  + [cancel](https://bun.com/reference/node/stream/web/ReadableStream/cancel)(

    reason?: any

    ): Promise<void>;
  + [getReader](https://bun.com/reference/node/stream/web/ReadableStream/getReader)(

    options: { mode: 'byob' }

    ): [ReadableStreamBYOBReader](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader);

    [getReader](https://bun.com/reference/node/stream/web/ReadableStream/getReader)(): [ReadableStreamDefaultReader](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader)<R>;

    [getReader](https://bun.com/reference/node/stream/web/ReadableStream/getReader)(

    options?: [ReadableStreamGetReaderOptions](https://bun.com/reference/node/stream/web/ReadableStreamGetReaderOptions)

    ): [ReadableStreamReader](https://bun.com/reference/node/stream/web/ReadableStreamReader)<R>;
  + [json](https://bun.com/reference/node/stream/web/ReadableStream/json)(): Promise<any>;

    Consume as JSON
  + [pipeThrough](https://bun.com/reference/node/stream/web/ReadableStream/pipeThrough)<T>(

    transform: [ReadableWritablePair](https://bun.com/reference/node/stream/web/ReadableWritablePair)<T, R>,

    options?: [StreamPipeOptions](https://bun.com/reference/node/stream/web/StreamPipeOptions)

    ): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<T>;
  + [pipeTo](https://bun.com/reference/node/stream/web/ReadableStream/pipeTo)(

    destination: [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<R>,

    options?: [StreamPipeOptions](https://bun.com/reference/node/stream/web/StreamPipeOptions)

    ): Promise<void>;
  + [tee](https://bun.com/reference/node/stream/web/ReadableStream/tee)(): [[ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<R>, [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<R>];
  + [text](https://bun.com/reference/node/stream/web/ReadableStream/text)(): Promise<string>;

    Consume as text
  + [values](https://bun.com/reference/node/stream/web/ReadableStream/values)(

    options?: { preventCancel: boolean }

    ): [ReadableStreamAsyncIterator](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator)<R>;
* ### interface [ReadableStreamAsyncIterator](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator)<T>

  + [[Symbol.asyncDispose]](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator/[asyncDispose])(): PromiseLike<void>;
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator/[asyncIterator])(): [ReadableStreamAsyncIterator](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator)<T>;
  + [next](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator/next)(

    ...\_\_namedParameters: [] | [unknown]

    ): Promise<IteratorResult<T, undefined>>;
  + [return](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator/return)(

    value?: PromiseLike<undefined>

    ): Promise<IteratorResult<T, undefined>>;
  + [throw](https://bun.com/reference/node/stream/web/ReadableStreamAsyncIterator/throw)(

    e?: any

    ): Promise<IteratorResult<T, undefined>>;
* ### interface [ReadableStreamBYOBReader](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader)

  + readonly [closed](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader/closed): Promise<void>
  + [cancel](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader/cancel)(

    reason?: any

    ): Promise<void>;
  + [read](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader/read)<T extends ArrayBufferView<ArrayBufferLike>>(

    view: T,

    options?: { min: number }

    ): Promise<[ReadableStreamReadResult](https://bun.com/reference/node/stream/web/ReadableStreamReadResult)<T>>;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader/read)
  + [releaseLock](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader/releaseLock)(): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBReader/releaseLock)
* ### interface [ReadableStreamBYOBRequest](https://bun.com/reference/node/stream/web/ReadableStreamBYOBRequest)

  [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest)

  + readonly [view](https://bun.com/reference/node/stream/web/ReadableStreamBYOBRequest/view): null | ArrayBufferView<ArrayBufferLike>

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest/view)
  + [respond](https://bun.com/reference/node/stream/web/ReadableStreamBYOBRequest/respond)(

    bytesWritten: number

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest/respond)
  + [respondWithNewView](https://bun.com/reference/node/stream/web/ReadableStreamBYOBRequest/respondWithNewView)(

    view: ArrayBufferView

    ): void;

    [MDN Reference](https://developer.mozilla.org/docs/Web/API/ReadableStreamBYOBRequest/respondWithNewView)
* ### interface [ReadableStreamDefaultController](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController)<R = any>

  + readonly [desiredSize](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController/desiredSize): null | number
  + [close](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController/close)(): void;
  + [enqueue](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController/enqueue)(

    chunk?: R

    ): void;
  + [error](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController/error)(

    e?: any

    ): void;
* ### interface [ReadableStreamDefaultReader](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader)<R = any>

  + readonly [closed](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader/closed): Promise<void>
  + [cancel](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader/cancel)(

    reason?: any

    ): Promise<void>;
  + [read](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader/read)(): Promise<[ReadableStreamReadResult](https://bun.com/reference/node/stream/web/ReadableStreamReadResult)<R>>;
  + [releaseLock](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader/releaseLock)(): void;
* ### interface [ReadableStreamErrorCallback](https://bun.com/reference/node/stream/web/ReadableStreamErrorCallback)
* ### interface [ReadableStreamGenericReader](https://bun.com/reference/node/stream/web/ReadableStreamGenericReader)

  + readonly [closed](https://bun.com/reference/node/stream/web/ReadableStreamGenericReader/closed): Promise<void>
  + [cancel](https://bun.com/reference/node/stream/web/ReadableStreamGenericReader/cancel)(

    reason?: any

    ): Promise<void>;
* ### interface [ReadableStreamGetReaderOptions](https://bun.com/reference/node/stream/web/ReadableStreamGetReaderOptions)

  + [mode](https://bun.com/reference/node/stream/web/ReadableStreamGetReaderOptions/mode)?: 'byob'

    Creates a ReadableStreamBYOBReader and locks the stream to the new reader.

    This call behaves the same way as the no-argument variant, except that it only works on readable byte streams, i.e. streams which were constructed specifically with the ability to handle "bring your own buffer" reading. The returned BYOB reader provides the ability to directly read individual chunks from the stream via its read() method, into developer-supplied buffers, allowing more precise control over allocation.
* ### interface [ReadableStreamReadDoneResult](https://bun.com/reference/node/stream/web/ReadableStreamReadDoneResult)<T>

  + [done](https://bun.com/reference/node/stream/web/ReadableStreamReadDoneResult/done): true
  + [value](https://bun.com/reference/node/stream/web/ReadableStreamReadDoneResult/value)?: T
* ### interface [ReadableStreamReadValueResult](https://bun.com/reference/node/stream/web/ReadableStreamReadValueResult)<T>

  + [done](https://bun.com/reference/node/stream/web/ReadableStreamReadValueResult/done): false
  + [value](https://bun.com/reference/node/stream/web/ReadableStreamReadValueResult/value): T
* ### interface [ReadableWritablePair](https://bun.com/reference/node/stream/web/ReadableWritablePair)<R = any, W = any>

  + [readable](https://bun.com/reference/node/stream/web/ReadableWritablePair/readable): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<R>
  + [writable](https://bun.com/reference/node/stream/web/ReadableWritablePair/writable): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<W>

    Provides a convenient, chainable way of piping this readable stream through a transform stream (or any other { writable, readable } pair). It simply pipes the stream into the writable side of the supplied pair, and returns the readable side for further use.

    Piping a stream will lock it for the duration of the pipe, preventing any other consumer from acquiring a reader.
* ### interface [StreamPipeOptions](https://bun.com/reference/node/stream/web/StreamPipeOptions)

  + [preventAbort](https://bun.com/reference/node/stream/web/StreamPipeOptions/preventAbort)?: boolean
  + [preventCancel](https://bun.com/reference/node/stream/web/StreamPipeOptions/preventCancel)?: boolean
  + [preventClose](https://bun.com/reference/node/stream/web/StreamPipeOptions/preventClose)?: boolean

    Pipes this readable stream to a given writable stream destination. The way in which the piping process behaves under various error conditions can be customized with a number of passed options. It returns a promise that fulfills when the piping process completes successfully, or rejects if any errors were encountered.

    Piping a stream will lock it for the duration of the pipe, preventing any other consumer from acquiring a reader.

    Errors and closures of the source and destination streams propagate as follows:

    An error in this source readable stream will abort destination, unless preventAbort is truthy. The returned promise will be rejected with the source's error, or with any error that occurs during aborting the destination.

    An error in destination will cancel this source readable stream, unless preventCancel is truthy. The returned promise will be rejected with the destination's error, or with any error that occurs during canceling the source.

    When this source readable stream closes, destination will be closed, unless preventClose is truthy. The returned promise will be fulfilled once this process completes, unless an error is encountered while closing the destination, in which case it will be rejected with that error.

    If destination starts out closed or closing, this source readable stream will be canceled, unless preventCancel is true. The returned promise will be rejected with an error indicating piping to a closed stream failed, or with any error that occurs during canceling the source.

    The signal option can be set to an AbortSignal to allow aborting an ongoing pipe operation via the corresponding AbortController. In this case, this source readable stream will be canceled, and destination aborted, unless the respective options preventCancel or preventAbort are set.
  + [signal](https://bun.com/reference/node/stream/web/StreamPipeOptions/signal)?: [AbortSignal](https://bun.com/reference/globals/AbortSignal)
* ### interface [TextDecoderOptions](https://bun.com/reference/node/stream/web/TextDecoderOptions)

  + [fatal](https://bun.com/reference/node/stream/web/TextDecoderOptions/fatal)?: boolean
  + [ignoreBOM](https://bun.com/reference/node/stream/web/TextDecoderOptions/ignoreBOM)?: boolean
* ### interface [TextDecoderStream](https://bun.com/reference/node/stream/web/TextDecoderStream)

  + readonly [[Symbol.toStringTag]](https://bun.com/reference/node/stream/web/TextDecoderStream/[toStringTag]): string
  + readonly [encoding](https://bun.com/reference/node/stream/web/TextDecoderStream/encoding): string

    Returns encoding's name, lower cased.
  + readonly [fatal](https://bun.com/reference/node/stream/web/TextDecoderStream/fatal): boolean

    Returns `true` if error mode is "fatal", and `false` otherwise.
  + readonly [ignoreBOM](https://bun.com/reference/node/stream/web/TextDecoderStream/ignoreBOM): boolean

    Returns `true` if ignore BOM flag is set, and `false` otherwise.
  + readonly [readable](https://bun.com/reference/node/stream/web/TextDecoderStream/readable): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<string>
  + readonly [writable](https://bun.com/reference/node/stream/web/TextDecoderStream/writable): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<[BufferSource](https://bun.com/reference/node/stream/web/BufferSource)>
* ### interface [TextEncoderStream](https://bun.com/reference/node/stream/web/TextEncoderStream)

  + readonly [[Symbol.toStringTag]](https://bun.com/reference/node/stream/web/TextEncoderStream/[toStringTag]): string
  + readonly [encoding](https://bun.com/reference/node/stream/web/TextEncoderStream/encoding): 'utf-8'

    Returns "utf-8".
  + readonly [readable](https://bun.com/reference/node/stream/web/TextEncoderStream/readable): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>
  + readonly [writable](https://bun.com/reference/node/stream/web/TextEncoderStream/writable): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<string>
* ### interface [Transformer](https://bun.com/reference/node/stream/web/Transformer)<I = any, O = any>

  + [cancel](https://bun.com/reference/node/stream/web/Transformer/cancel)?: [TransformerCancelCallback](https://bun.com/reference/node/stream/web/TransformerCancelCallback)
  + [flush](https://bun.com/reference/node/stream/web/Transformer/flush)?: [TransformerFlushCallback](https://bun.com/reference/node/stream/web/TransformerFlushCallback)<O>
  + [readableType](https://bun.com/reference/node/stream/web/Transformer/readableType)?: undefined
  + [start](https://bun.com/reference/node/stream/web/Transformer/start)?: [TransformerStartCallback](https://bun.com/reference/node/stream/web/TransformerStartCallback)<O>
  + [transform](https://bun.com/reference/node/stream/web/Transformer/transform)?: [TransformerTransformCallback](https://bun.com/reference/node/stream/web/TransformerTransformCallback)<I, O>
  + [writableType](https://bun.com/reference/node/stream/web/Transformer/writableType)?: undefined
* ### interface [TransformerCancelCallback](https://bun.com/reference/node/stream/web/TransformerCancelCallback)
* ### interface [TransformerFlushCallback](https://bun.com/reference/node/stream/web/TransformerFlushCallback)<O>
* ### interface [TransformerStartCallback](https://bun.com/reference/node/stream/web/TransformerStartCallback)<O>
* ### interface [TransformerTransformCallback](https://bun.com/reference/node/stream/web/TransformerTransformCallback)<I, O>
* ### interface [TransformStream](https://bun.com/reference/node/stream/web/TransformStream)<I = any, O = any>

  + readonly [readable](https://bun.com/reference/node/stream/web/TransformStream/readable): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<O>
  + readonly [writable](https://bun.com/reference/node/stream/web/TransformStream/writable): [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<I>
* ### interface [TransformStreamDefaultController](https://bun.com/reference/node/stream/web/TransformStreamDefaultController)<O = any>

  + readonly [desiredSize](https://bun.com/reference/node/stream/web/TransformStreamDefaultController/desiredSize): null | number
  + [enqueue](https://bun.com/reference/node/stream/web/TransformStreamDefaultController/enqueue)(

    chunk?: O

    ): void;
  + [error](https://bun.com/reference/node/stream/web/TransformStreamDefaultController/error)(

    reason?: any

    ): void;
  + [terminate](https://bun.com/reference/node/stream/web/TransformStreamDefaultController/terminate)(): void;
* ### interface [UnderlyingByteSource](https://bun.com/reference/node/stream/web/UnderlyingByteSource)

  + [autoAllocateChunkSize](https://bun.com/reference/node/stream/web/UnderlyingByteSource/autoAllocateChunkSize)?: number
  + [cancel](https://bun.com/reference/node/stream/web/UnderlyingByteSource/cancel)?: [ReadableStreamErrorCallback](https://bun.com/reference/node/stream/web/ReadableStreamErrorCallback)
  + [pull](https://bun.com/reference/node/stream/web/UnderlyingByteSource/pull)?: [ReadableByteStreamControllerCallback](https://bun.com/reference/node/stream/web/ReadableByteStreamControllerCallback)
  + [start](https://bun.com/reference/node/stream/web/UnderlyingByteSource/start)?: [ReadableByteStreamControllerCallback](https://bun.com/reference/node/stream/web/ReadableByteStreamControllerCallback)
  + [type](https://bun.com/reference/node/stream/web/UnderlyingByteSource/type): 'bytes'
* ### interface [UnderlyingSink](https://bun.com/reference/node/stream/web/UnderlyingSink)<W = any>

  + [abort](https://bun.com/reference/node/stream/web/UnderlyingSink/abort)?: [UnderlyingSinkAbortCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkAbortCallback)
  + [close](https://bun.com/reference/node/stream/web/UnderlyingSink/close)?: [UnderlyingSinkCloseCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkCloseCallback)
  + [start](https://bun.com/reference/node/stream/web/UnderlyingSink/start)?: [UnderlyingSinkStartCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkStartCallback)
  + [type](https://bun.com/reference/node/stream/web/UnderlyingSink/type)?: undefined
  + [write](https://bun.com/reference/node/stream/web/UnderlyingSink/write)?: [UnderlyingSinkWriteCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkWriteCallback)<W>
* ### interface [UnderlyingSinkAbortCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkAbortCallback)
* ### interface [UnderlyingSinkCloseCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkCloseCallback)
* ### interface [UnderlyingSinkStartCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkStartCallback)
* ### interface [UnderlyingSinkWriteCallback](https://bun.com/reference/node/stream/web/UnderlyingSinkWriteCallback)<W>
* ### interface [UnderlyingSource](https://bun.com/reference/node/stream/web/UnderlyingSource)<R = any>

  + [cancel](https://bun.com/reference/node/stream/web/UnderlyingSource/cancel)?: [UnderlyingSourceCancelCallback](https://bun.com/reference/node/stream/web/UnderlyingSourceCancelCallback)
  + [pull](https://bun.com/reference/node/stream/web/UnderlyingSource/pull)?: [UnderlyingSourcePullCallback](https://bun.com/reference/node/stream/web/UnderlyingSourcePullCallback)<R>
  + [start](https://bun.com/reference/node/stream/web/UnderlyingSource/start)?: [UnderlyingSourceStartCallback](https://bun.com/reference/node/stream/web/UnderlyingSourceStartCallback)<R>
  + [type](https://bun.com/reference/node/stream/web/UnderlyingSource/type)?: undefined
* ### interface [UnderlyingSourceCancelCallback](https://bun.com/reference/node/stream/web/UnderlyingSourceCancelCallback)
* ### interface [UnderlyingSourcePullCallback](https://bun.com/reference/node/stream/web/UnderlyingSourcePullCallback)<R>
* ### interface [UnderlyingSourceStartCallback](https://bun.com/reference/node/stream/web/UnderlyingSourceStartCallback)<R>
* ### interface [WritableStream](https://bun.com/reference/node/stream/web/WritableStream)<W = any>

  This Streams API interface provides a standard abstraction for writing streaming data to a destination, known as a sink. This object comes with built-in back pressure and queuing.

  + readonly [locked](https://bun.com/reference/node/stream/web/WritableStream/locked): boolean
  + [abort](https://bun.com/reference/node/stream/web/WritableStream/abort)(

    reason?: any

    ): Promise<void>;
  + [close](https://bun.com/reference/node/stream/web/WritableStream/close)(): Promise<void>;
  + [getWriter](https://bun.com/reference/node/stream/web/WritableStream/getWriter)(): [WritableStreamDefaultWriter](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter)<W>;
* ### interface [WritableStreamDefaultController](https://bun.com/reference/node/stream/web/WritableStreamDefaultController)

  This Streams API interface represents a controller allowing control of a WritableStream's state. When constructing a WritableStream, the underlying sink is given a corresponding WritableStreamDefaultController instance to manipulate.

  + [error](https://bun.com/reference/node/stream/web/WritableStreamDefaultController/error)(

    e?: any

    ): void;
* ### interface [WritableStreamDefaultWriter](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter)<W = any>

  This Streams API interface is the object returned by WritableStream.getWriter() and once created locks the < writer to the WritableStream ensuring that no other streams can write to the underlying sink.

  + readonly [closed](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter/closed): Promise<void>
  + readonly [desiredSize](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter/desiredSize): null | number
  + readonly [ready](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter/ready): Promise<void>
  + [abort](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter/abort)(

    reason?: any

    ): Promise<void>;
  + [close](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter/close)(): Promise<void>;
  + [releaseLock](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter/releaseLock)(): void;
  + [write](https://bun.com/reference/node/stream/web/WritableStreamDefaultWriter/write)(

    chunk?: W

    ): Promise<void>;
* type [BufferSource](https://bun.com/reference/node/stream/web/BufferSource) = ArrayBufferView | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)
* type [CompressionFormat](https://bun.com/reference/node/stream/web/CompressionFormat) = 'brotli' | 'deflate' | 'deflate-raw' | 'gzip'
* type [ReadableStreamController](https://bun.com/reference/node/stream/web/ReadableStreamController)<T> = [ReadableStreamDefaultController](https://bun.com/reference/node/stream/web/ReadableStreamDefaultController)<T>
* type [ReadableStreamReader](https://bun.com/reference/node/stream/web/ReadableStreamReader)<T> = [ReadableStreamDefaultReader](https://bun.com/reference/node/stream/web/ReadableStreamDefaultReader)<T> | [ReadableStreamBYOBReader](https://bun.com/reference/node/stream/web/ReadableStreamBYOBReader)
* type [ReadableStreamReaderMode](https://bun.com/reference/node/stream/web/ReadableStreamReaderMode) = 'byob'
* type [ReadableStreamReadResult](https://bun.com/reference/node/stream/web/ReadableStreamReadResult)<T> = [ReadableStreamReadValueResult](https://bun.com/reference/node/stream/web/ReadableStreamReadValueResult)<T> | [ReadableStreamReadDoneResult](https://bun.com/reference/node/stream/web/ReadableStreamReadDoneResult)<T>