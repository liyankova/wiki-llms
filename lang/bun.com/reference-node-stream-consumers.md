---
url: https://bun.com/reference/node/stream/consumers
title: Node.js stream/consumers module | API Reference | Bun
source_domain: bun.com
---

# Node.js stream/consumers module | API Reference | Bun

Node.js module

# [stream/consumers](https://bun.com/reference/node/stream/consumers)

The `'node:stream/consumers'` submodule offers helper functions that consume Readable streams into other forms, such as `blob`, `arrayBuffer`, `text`, or `json`.

It simplifies common stream-to-data conversions without manual event handling.

* function [arrayBuffer](https://bun.com/reference/node/stream/consumers/arrayBuffer)(

  stream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<any> | ReadableStream | AsyncIterable<any, any, any>

  ): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

  @returns

  Fulfills with an `ArrayBuffer` containing the full contents of the stream.
* function [blob](https://bun.com/reference/node/stream/consumers/blob)(

  stream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<any> | ReadableStream | AsyncIterable<any, any, any>

  ): Promise<[Blob](https://bun.com/reference/node/buffer/Blob)>;

  @returns

  Fulfills with a `Blob` containing the full contents of the stream.
* function [buffer](https://bun.com/reference/node/stream/consumers/buffer)(

  stream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<any> | ReadableStream | AsyncIterable<any, any, any>

  ): Promise<NonSharedBuffer>;

  @returns

  Fulfills with a `Buffer` containing the full contents of the stream.
* function [json](https://bun.com/reference/node/stream/consumers/json)(

  stream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<any> | ReadableStream | AsyncIterable<any, any, any>

  ): Promise<unknown>;

  @returns

  Fulfills with the contents of the stream parsed as a UTF-8 encoded string that is then passed through `JSON.parse()`.
* function [text](https://bun.com/reference/node/stream/consumers/text)(

  stream: [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream)<any> | ReadableStream | AsyncIterable<any, any, any>

  ): Promise<string>;

  @returns

  Fulfills with the contents of the stream parsed as a UTF-8 encoded string.